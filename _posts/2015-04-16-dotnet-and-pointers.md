---
layout: post
title:  "unsafe code in .NET"
date:   2015-04-16 00:00:00 -0800
categories: dotnet
---

## Using 'unsafe' code in .NET
One of the fun things that .NET lets you do as a core feature is execute so-called 'unsafe' code. This is code that is, effectively, equivalent to unmanaged code (C/C++/etc). The code is called 'unsafe' because it bypasses all the features the CLR provides to ensure consistency and stability of the core application. Most specifically it allows you to directly access memory in the same way you would through an unmanaged language. I'm going to talk here about C#, but the facilities that enable unsafe code are a core function of the CLR and could theoretically be used in any language running on .NET, if the language syntax supports it.

For the remainder of this post I'm going to assume basic familiarity with core .NET concepts such as the difference between reference and value types. If this sounds weird to you then this post may be difficult to understand in places.

You can, of course, use features like platform invoke (P/Invoke) to run unmanaged code within your application but this method has a few drawbacks:
1. There is a cost to call through P/Invoke. The platform performs various transformations of data and has to do a fair amount to ensure that garbage collections remain safe. While this is also true for embedded unsafe code the cost is a bit lower. For some types marshalling of data is entirely unavoidable and depending on the data this can be very expensive.
2. You need to bundle up the unsafe code outside your own core code. This is a minor issue.
3. You need to write that code in some other language than the one you're working with (let's go with C# since it has very robust 'unsafe' code support).

## Why you don't want to use unsafe code

As usual the arguments boil down to danger. Direct access to application memory introduces a lot of ways to shoot yourself in the foot. Specifically you're opening up opportunities for instantaneous and effectively unmanageable process crashes, [heisenbugs](http://en.wikipedia.org/wiki/Heisenbug), and a lot of nightmarish debugging.

If you never felt comfortable with C or C++ or other 'native' or 'unmanaged' languages you'll hit the same discomfort with 'unsafe' in .NET. The debugging experience moves from fairly glorious to the 'oh god where is this memory even' that is a big wall for a lot of users, crashes resulting from bugs have the same (un)predictability they do in native languages, etc.

In addition it's critical to call out that these methods expose you to all the security dangers inherent with anything that can read and write to memory directly. Input sanitation becomes extremely critical, and buffer overflows mean anyone who finds a way to get your application to overwrite memory has a shot at exploiting the holes in all the usual and scary ways.

Additionally there are contexts in which you simply **cannot** use unsafe code. In particular in things like Silverlight applications, and some other contexts, assemblies marked as 'unsafe' will simply not be run, generally for extremely good reasons. .NET provides other facilities for determining whether or not 'unsafe' code is allowed and these are enabled in a variety of places.

## Why you do want to use unsafe code

The simplest reason to use unsafe code is because you need the performance of effectively raw memory access. For many applications these considerations will never come up, and there will never be a reason to use unsafe code. For example the canonical desktop applications and even many server applications will never find a need to do this as their performance will be sufficient for common use. There has been a great deal written about .NET performance relative to unmanaged code, and the landscape is continuously changing. If I were less lazy I'd go find some of my faborite articles, but here we are and I'm not going to do that. For many users .NET without unsafe code is just peachy and there's no reason to wander into the dangerous swamps ahead.

However there are going to be times in your software where you find that squeezing a 10%+ performance boost out of a core piece of code is worth the difficulties of using unsafe code. In particular for applications which do intensive processing of data this can be enormously beneficial if you structure your application correctly. When you run code on dozens, hundreds, or thousands of machines the savings in time and power from a 10%+ boost add up to serious money saved.

Interestingly, after measuring on two different pieces of hardware I got two very different results. I'm looking into that further but for the purpose of the above paragraph I'm discussing the **floor** for performance boosts. In tests on server-class hardware I actually got around **50%** improvement, which are the results I'll share below. The 10% number comes from an i5 Surface Pro 3 which is rather farther from what you'll see in environments like a datacenter.

## How to use unsafe code

Again I'll focus on C# here. There are a few steps to cover before you can get to that juicy pointer goodness. The biggest thing is telling the C# compiler that you're going to make an unsafe assembly, as it must tag the assembly metadata so others know what you're up to.

Here's what happens when you try to use unsafe code without warning the compiler:

    > csc /o+ /out:benchmark.exe benchmark.cs
    Microsoft (R) Visual C# Compiler version 4.6.0042.0
    for Microsoft (R) .NET Framework 4.5
    Copyright (C) Microsoft Corporation. All rights reserved.
    
    Benchmark.cs(6,32): error CS0227: Unsafe code may only appear if compiling with /unsafe


Whoops! Throw `/unsafe` on the command line and you'll be good to go. For more complex projects the easiest thing to do is modify the .csproj file to let the compiler know you've got unsafe code coming. There's a GUI way to do this but I usually just hand-edit the file and add `<AllowUnsafeCode>true</AllowUnsafeCode>` to the global `<Properties>` section. Using the GUI checkbox does the same thing.

Now that you **can** use unsafe code in your application you still need to let the compiler know which things are, in fact, unsafe. This is done through the `unsafe` keyword. This keyword may be used either at the class or method level. Depending on your scenario it may be better to tag one or the other. A class that predominantly does buffer processing in most or all methods can be marked unsafe. Alternately if you have just one method that is unsafe it may be more suitable to mark that method, particularly for shared libraries which may be used in a variety of contexts.

Here's a very basic example of a chunk of unsafe code to sum the values of an array:
    public static unsafe long SumArray(long[] values)
    {
        var sum # 0L;
        fixed (long* v # values)
        {
            long* end # v + values.Length;
            while (v < end)
            {
                sum +# *v;
            }
        }
    }

I've thrown another new keyword in here: `fixed`. I'll discuss that more momentarily. There are a couple of other noteworthy things going on here that I want to call out first:
1. Note that I calculate the address of the end of the array by doing `long* end # v + values.Length`. Just like in C and C++ this handles correctly determining the pointer value **relative to the size of the underlying type**. If I was using a byte/sbyte pointer I'd be working with single byte increments, for long I'm working with `sizeof(long)` or eight byte increments.
2. Just like in C and C++ the value of an address in memory is retrieved using the 'value-pointed-to' prefix operator (`sum +# *v`). If you've spent time in these languages this should all look extremely familiar. After all it is C***#***.

The code above is meant to be instructive. It shouldn't be used as it has some fun issues like integer overflow that certainly are **not** going to be handled.

Now, let's go back to what's happening when you use the `fixed` syntax above. Fixed is some C# syntactic sugar which actually does more under the hood than its unassuming name would imply. Specifically what is really happening is that you are acquiring a garbage collector (GC) handle to the underlying object, in this case the `values` array passed to the method. You can do the same thing manually using the [GCHandle.Alloc method](https://msdn.microsoft.com/en-us/library/vstudio/83y4ak54(v#vs.100).aspx) method to acquire a handle from the GC to allow you to manipulate underlying data. In this case you are getting a 'pinned' handle. There are several types of handles you can acquire from the GC for various kinds of operations. Feel free to ask me for a more detailed explanation and I'll be happy to elaborate, although there are lots of other great resources online for this.

In general don't do direct handle allocation, though. Using `fixed` is a lot like `using` for the IDisposable type or `lock` for Monitor objects. It does more under the hood to help keep your code generally safe including unilaterally releasing the handle in the event of an exception within the block (you can think of this as the same behavior done by both `using` and `lock` statements). There are a tiny handful of cases where you actually need to manually allocate a pinned GCHandle but I'm going to aggressively ignore them for the sake of brevity.

Pinning tells the .NET garbage collector that it **must not** move the memory which underlies an object for the duration of the pinning. This is what allows you to accomplish direct memory access in the language. Without telling the collector that it may not move data it is entirely possible that a pre-emptive collection would move memory halfway through an operation against it, resulting in some pretty awful shenanigans.

Now for something pretty important: pinning can be extremely bad if you abuse it. The .NET garbage collector relies heavily on the ability to 'move' objects in memory for efficient performance. If you keep an object pinned for a long period of time you may experience some unpleasant side effects, in particular memory growth as new segments must be allocated to fit in newly allocated data since previous segments cannot be compacted. At its worst this can lead to extreme slowdown of the application, which is of course the last thing you want!

Interestingly, for the Microsoft CLR, pinning so-called 'large' objects for longer periods is substantially less detrimental. This is because the large object heap is only compacted on-demand, allowing greater control of application behavior assuming you take the time to fine tune. This ends up working out well for the user, as you will typically need many more cycles to work on a large segment of memory vs. a smaller one. However, for smaller memory segments if you desire the best possible performance avoid allocation of new reference type objects as this naturally creates pressure on the garbage collector which can result in collections that do not run optimally, given one or more chunks of unmovable data.

## Benchmarking Performance
Everybody loves synthetic benchmarks, so I went ahead and put one together to demonstrate the success of the unsafe approach. [The code is available on GitHub](https://github.com/doubleyewdee/dotnet-fixed-benchmark). I've used the venerable 'bubblesort' algorithm because it's pleasantly extremely slow even for small N of data. I create an array to be sorted, either with inverted values (guaranteeing N^2 runtime) or random values (providing the potential for not-worst-case) and then use four different mechanisms to sort the array.
1. Inline safe sort: a single method which sorts the entire array.
2. Nested safe sort: a method which calls an inner method for each element to place the element.
3. Inline unsafe sort: Just like #1 but with all array access performed via pointers.
3. Nested unsafe sort: Just like #2 but with all array access performed via pointers.



As the results above indicate there is not a large performance delta between inline and nested. Interestingly for safe code the nested method comes out very slightly ahead (about 0.5%, reliably in my experience). For unsafe code the results are effectively a wash. It is quite probable the JIT compiler inlines the nested code, but it may emit slightly different code in the safe methods. I'll look into this in the future.

For those curious, here is the information about the system these results come from. I've redacted some data specific to the Microsoft corporate network. Yes that's a not-public-right-now Windows 10 build! Please look forward to future builds!
    > systeminfo
    
    OS Name:                   Microsoft Windows 10 Enterprise Technical Preview
    OS Version:                10.0.10061 N/A Build 10061
    OS Manufacturer:           Microsoft Corporation
    OS Configuration:          Member Workstation
    OS Build Type:             Multiprocessor Free
    Registered Owner:          Microsoft Corp.
    Registered Organization:   Microsoft IT
    Original Install Date:     4/14/2015, 3:53:07 AM
    System Boot Time:          4/14/2015, 3:47:40 AM
    System Manufacturer:       Dell Inc.
    System Model:              Precision WorkStation T5500
    System Type:               x64-based PC
    Processor(s):              2 Processor(s) Installed.
                               [01]: Intel64 Family 6 Model 44 Stepping 2 GenuineIntel ~2395 Mhz
                               [02]: Intel64 Family 6 Model 44 Stepping 2 GenuineIntel ~2395 Mhz
    BIOS Version:              Dell Inc. A12, 12/29/2011
    Windows Directory:         C:\WINDOWS
    System Directory:          C:\WINDOWS\system32
    Boot Device:               \Device\HarddiskVolume1
    System Locale:             en-us;English (United States)
    Input Locale:              en-us;English (United States)
    Time Zone:                 (UTC-08:00) Pacific Time (US & Canada)
    Total Physical Memory:     24,574 MB
    Available Physical Memory: 13,819 MB
    Virtual Memory: Max Size:  28,542 MB
    Virtual Memory: Available: 13,316 MB
    Virtual Memory: In Use:    15,226 MB
    Page File Location(s):     C:\pagefile.sys
    Hotfix(s):                 N/A
    Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.

The CPUs are likely to be the most interesting part of this. If you don't speak Intel CPU branding they are both Intel Xeon E5645 parts clocked at 2.4ghz. The memory is 6 4GB DIMMs clocked at 1333mhz. There was copious available memory for the benchmarking task (which caps out in the tens of MB of memory range).
