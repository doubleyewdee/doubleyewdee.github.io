---
layout: post
title:  "open microsoft"
date:   2015-02-05 00:00:00 -0800
categories: work
---

(Standard disclaimer: I write for me, not Microsoft, despite working there)

I've worked at Microsoft for approximately nine years and nine months. My growing years in computers were a wild mix of OS/2, Windows 9x, Linux, and FreeBSD. By the time I was about 15 I was fully immersed and entrenched in the Unix side of things. I pretty much wrecked the family computer (*still waiting for the year of Linux on the desktop*). After I left home I worked almost exclusively in Unix-land. I contributed to a variety of open source projects (FreeBSD, all sorts of IRC projects, some PHP stuff, and so on) and launched some of my own to boot.

I've always been a huge fan of open source software. I'm not per se ideological about it in that whole "information wants to be free" ESR ranty way. It's cool if you are, I'm just not. For me the joy in OSS comes purely from sharing in an artistic community. If you don't think that code is akin to artwork, think again. Much like any other craft (carpentry, architecture, etc) there is a level of artistry in our creations. And a huge amount of that artistry and investment is literally in the code a developer writes. The finished products are of course their own works, but sharing in a community of coders is one of the most compelling parts of the work I do. It's why I get up in the morning and come to work, it's why I'll spend a lot of time talking to you about hard vs. soft tabs, how to format, why Python's whitespace-as-blocks is actually great (*it is, shut up, I don't want to hear it*), and other boring shit.

So it's probably a little strange that I ever ended up at Microsoft. Our former CEO famously said at one time that ["Linux is a cancer"](http://www.theregister.co.uk/2001/06/02/ballmer_linux_is_a_cancer/). Obviously a bombastic and divisive comment from perhaps the most colorful character I've ever seen run a major company. I knew about that, I knew about the generally closed off nature of Microsoft, too. However, a lot of things ended up drawing me here regardless. Working with brilliant engineers and the opportunity to really learn deeply about a world of computing were at the top of the list, along with the need to get off the east coast. So I took the job in 2005 and haven't looked back since.

Still, I had always been a little bit sad that, while I could share code with my immediate peers, my ability to use and contribute to OSS felt severely curtailed. In particular it was, historically, fairly difficult to make use of external software and even harder to contribute back on company time. There were a lot of legal hoops to jump through and a lot of side-eye from people around you for not *doing it the Microsoft way*. That the Microsoft way routinely boiled down to NIH did not seem to bother people. You just did not go digging around on github or the historical equivalents for a helpful library that did the thing you wanted. If you were lucky you found it in your team's repository (because you sure couldn't go look at other teams' stuff!) but that was the best you could do before just having to code it all up yourself.

Obviously in a rapidly moving world of software this kind of approach becomes really hard to maintain. When your competitors can make use of the wide world of freely available and high quality software, and you have to write everything yourself from scratch, you're not going to move as fast. Or you're going to need a lot more humans just to keep up. It's a huge competitive disadvantage. It's also a cultural disadvantage. If you grew up learning about OSS and making use of others' code to advance your purposes only to lose the ability to do so at work you'll probably end up fairly disappointed.

## The Brave New World

![OPEN SOURCE ALL THE THINGS!](http://cdn.meme.am/instances/500x/58465614.jpg)
But in the last six months or so that has all changed. Drastically. I've watched slow cultural shifts inside the company, but the dramatic nature of this change has been, frankly, **astounding**. The company is moving, across the board, in a rapid direction back towards the greater software community. This is happening in three critical ways that are already paying huge dividends for the company:
1. We're working a lot harder to integrate with the rest of the software world than we ever have before. You can see this in the excellent work by the Azure team, the CLR/.NET team, and others.
2. We're much more proactive about trying to use existing OSS vs. writing our own. The business sense of this is pretty clear, especially for extremely well-supported products with big communities. This benefits by both ensuring we do not duplicate effort and by affording us the opportunity to use widely-known software which new team members may already be familiar with.
3. We're releasing lots of our own code to the world! This is the most exciting bit to me because we're already seeing great community involvement in what we're releasing, and I firmly believe the floodgates are only just opening.

## What We're Getting

At the highest level what we're getting is the massive advantages of participating with hundreds of thousands of software developers across the globe to build a better world. I realize that is a pretty sentimental sounding statement, but I firmly believe it. By participating with our friends and peers around the world we all get to make technology better together.

We get to benefit from the hard work of our compatriots in the world, and we get to share back with them our own hard work. We get the opportunity to earn mutual respect.

We get to share some of our own work with the world, and hopefully make life easier for developers and users of our products. We get to demonstrate techniques that may not be immediately obvious, or may not be easily discovered through books or MSDN or so on. We get to experience the pride of sharing our art with the world at large, instead of hiding it inside a code repository that will never be seen by more than a handful of people.

You can imagine that right now there are a lot of very excited people here.

## What's Not Coming

I'm very skeptical about some things ever getting released as open source. The reasons for this should be obvious. We at Bing would no more release our proprietary ranking algorithms than would Google. They're secret sauce and competitive advantage. There is negative value in exposing that to the world. I similarly do not see the Office code or large chunks of Windows ever getting released, simply because doing so is arguably more harmful than beneficial.

In general if you look at something and think *why would they ever release that code* then I wouldn't expect to see it released. There are a lot of reasons not to release code, but the top ones are:
1. The code offers a strong competitive advantage to the company. External examples are: pretty much all of Google's server-side stuff, anything in Android play, core parts of Facebook's social engine, and so on.
2. The code isn't very good and/or is temporal.
3. The team is not in a position to take back community contributions. Examples of this may be applications that are developed by small feature teams, particularly when the majority of the team then moves on to other projects and can only devote minimal maintenance time to the existing project.

## What's Coming And What We Give Back

(I want to reiterate that I'm not making commitments **for** Microsoft to do anything specific here. I'm observing what I see going on inside and making some general statements, unless otherwise noted.)

We've already had some amazing releases. You can see the majority of what we've already released [on our company GitHub page](https://github.com/microsoft/) and [the .NET team's GitHub page](https://github.com/dotnet). Projects like CoreCLR and Bond are truly impressive releases that I've seen a lot of hours put into.

Tomorrow I get to do my first release, too! I'll publicize that [on Twitter](https://twitter.com/doubleyewdee). I'm not actually the author of this particular code (I have made only a handful of changes) but it marks the initial release of what I plan to be a cascade of software. It's a core foundational element that we use for memory management in .NET applications here at Bing to greatly improve the performance of long-lived applications.

I've got more in the works. As an infrastructure guy I've spent the last few years here working on logging and analytics software for Bing, where we have some fairly large scales of data to work with. I'm going through the processes of getting signoff from legal and management, but given the new attitudes on display I am extremely confident that these releases will happen over the next couple of months.

These are the kinds of projects it makes a lot of sense for us to release. They do not really offer us a competitive advantage or leverage to sell more products. They **do** help us run a world-class internet service at scale, though, and we have other customers who might be interested in taking advantage of these ready-made libraries and tools for their own projects. That's the sort of stuff we're looking at releasing, or when we find a similar existing bit of code, integrating with or adopting.

![HYPE TRAIN COMING THROUGH](http://cdn.head-fi.org/9/9e/9eeaf04f_HypeTrain.jpeg)

