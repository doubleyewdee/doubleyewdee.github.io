---
layout: post
title:  "combined engineering @ microsoft"
date:   2014-07-23 00:00:00 -0800
tags: work
---

(I am writing for myself, for fun. I like to say controversial things. I **do not write for my employer**. My employer would perhaps rather I did not write. If my employer asks that I do not write or that I remove something I will do that because they have been great to me. **I might be an asshole**.)

Let me preface this by saying I don't have anything against software testing. Software testing is fine. It's more than fine. It's pretty importasnt to do. My understanding as a kind of younger-ish person is that Microsoft even did a lot to pioneer the world of software testing. Cool. I also started writing this before the massive layoff hammer at Microsoft came down. I've edited it a bit in light of what is happening now.

## Functional organizations
The notion of the functional organization inside Microsoft revolved (***it is dead now and past tense is appropriate***) around three distinct engineering disciplines doing distinct things, arguably in silos from each other. Whether the siloing was intended or not the reality is that this is what happened.

The first silo to do a thing was the program management silo. They would (in concert with the other two silos) come up with a specification for the thing to be done.

The second silo to do a thing was the developer silo. They would implement the specification that the program management silo provided.

The last silo was the testing silo. They would ensure the thing that was specified was the thing the developers implemented. If it was not the thing there would be bugs filed and hopefully discussions had and all of that.

There are some terrific strengths in this structure. It is rigorous. It is clear. It is generally quite thorough. It's fairly easy to understand, separate, and delegate responsibilities.

Unfortunately there are some really terrific weaknesses in this structure.  It is the epitome of 'waterfall' design. While the PMs are specifying the developers have very little to do. While the developers are developing the testers have very little to do. The theory of waterfall is, as I understand it, that you fix these seeming inefficiences by ensuring that the PMs have new things to specify when they hand the current things to the devs, the devs have new things to dev when they hand current things to the testers, and the testers have new things to test when they're done with testing the previous thing as a result of this. And so there's always a continuous circle of specs to code to tests.

Theory sounds great but in practice this is bullshit. I've never heard from anyone in traditional waterfall orgs **in any company** that they were kept suitably busy! They weren't. They aren't. Waterfall is not suitable for the world of rapid release or continuous integration. In any software project there are simply times when all the hot things are happening and times when they aren't. The ideal is to break that into smaller chunks to keep folks busy as much as you can. Being bored for an hour is fine. Being bored for a week means your job sucks.

## Okay, can we make this easier?

The obvious answer is to break down walls. It happens to be that the easiest wall to split is the wall between development and testing of software.

Why? Simple: both disciplines, as a bottom line, write code. Good program managers can write code and do write code, but the way they are measured isn't (typically) as much or at all about the code they wrote as it is about the products they made sure shipped on time, on budget, and generally correctly.

Notionally developers write the code that does a thing and testers write the code that proves the developers thing. This is where I'm going to, in some folks' minds, just go off the rails and be a self-centered fuck and, really, this is how I feel about this subject and I don't think my mind will change on this topic. The bottom line is that only one group's code is the thing you use: the developers. The code that testers write does not (in general) ever land on a disk, disc, thumb drive, cartridge, or download server. The end user doesn't run their code. The end user almost certainly doesn't even know there was a LOT of extra code involved in the thing they use which they'll never interact with in any way.

You, the person paying for the product with your money or your privacy, only care about the product you got. You don't care how you got it, as long as it works right. The code that the testers wrote is therefore simply not as **visibly valuable** to you. It doesn't matter whether they did a bang-up job or found a showstopper bug to you. You won't glamorize them in horrid Hollywood movies about hackers. You. Do. Not. Care. About. Testers.

Perception of the masses is reality. A reality that seeps into organizations. The best coders are developers. The acceptable coders are testers at good companies or developers at mediocre companies. The worst coders ... are just the pits.

## So we don't need testers?

Bluntly: in general, for most software, no.

We need high quality tests for software. We need people to care about verifying functionality, security, safety, etc. But at the end of the day we need those principles and not a bifurcated group to uphold them. **Every developer** needs to care about these things. If you don't then you're a bad developer and you should feel bad. If the word verifiability doesn't mean something to you, and you write software, please do me a favor and exit my profession right now.

Thus was combined engineering born, in my estimation. The push was already on for the original developer to test his stuff instead of throwing shit over the wall at testers. Unit testing and the growth of [test driven development](http://en.wikipedia.org/wiki/Test-driven_development) show this broader movement. You, developer guy, need to have written tests before anyone else uses your shit. Again, if you don't think you should test your software before foisting it on others you're a bad developer and you should feel bad.

Ah, but what does testing mean? Herein lies the other downfall of many.  It does not mean manually repeating steps to make sure something works. It does not mean multi-step documents telling your peers "how to run tests on this." Continuous integration and rapid iteration mean **writing software to test your software**. If the way you test that the thing you wrote is to start an app and click some buttons or type some commands then you have royally fucked up. That's called QA, and it's a totally different thing, and it **is not what test is considered to be**.

Oh, and QA is insanely important. QA is a job where people try to use software like normal humans. QA is where you didn't read the code but you tried to get some real-world task done with the product and you tell people how that went for you. User experience is quality that must be assured as a distinct and important thing. Automated testing (or pseudo-automated testing) is not QA.

So the bad news is that, because testers cannot be viewed as being as valuable as developers, they are generally not required to be as good at writing software as their peers. This means that, assuming they automated testing, their automation is quite probably haphazard and half-assed compared to what a high quality developer can produce. In my personal experience that automation has been at least as much liability as it has been an asset.

Yes. Really. I'm a bad guy. I'm mean and I'm being nasty. I'm saying something that's just not friendly or nice. However, this is reality. The reality is that the things valued from testers are almost anathema to the things valued from developers. The notion is that testers employ rigor, they treat a specification as an inflexible requirement and hold developers accountable. Developers are flexible, they solve problems and they make compromises and they find a way to get shit done. There are people who blur these lines but the reality is that this is the bifurcation.

In the right industry and with the right environment **this is what testers should do and why they can be great**. To be super clear I do **not** want the folks making avionics software to treat software as a malleable and continuously flexible thing that they can fix on the fly (***sorrynotsorry***) after the fact. My safety and yours demands rigor and not some cowboy coder treating his bugs as a thing he can just fix tomorrow if he goofed and did not find them. PS: I'm a cowboy coder and I would never get near software where my idiot mistakes could endanger lives.

But, oops, 95%+ of the software you actually use every day **does not demand this kind of rigor or quality**. Bugs suck and they're annoying and, given widespread adoption of buggy software, they can hurt humanity (***insert joke about XP still having users here***). Still, at the end of the day, most of what you use, when it is buggy, is merely inconvenient and not dangerous or meaningfully expensive.

## So we mostly don't need testers?

Well. Yes.

## What about program managers?

Ask me later.

## So a lot of testers lost their jobs ...

This is what I'm hearing. To you all, I am truly sorry. I don't want people to lose their livelihood or be out of work. Maybe you saw this bad news coming and maybe you did not. In any event I hope you land on your feet and I wish the best for you.

If you want my advice, if you're not furious, then...

## Bing did this way less severely and I watched it happen.

Let me start with my observation about what happened in Bing. It is, after all, the source of "combined engineering" at Microsoft. So what happened?

It was announced that the test and dev organizations would merge. All test folks would become developers. This pretty immediately caused a variety of reactions, among them:

* "But I'm comfortable in my role."
* "But my job isn't to test software."
* "But my job isn't to write software."
* "But I can't do the job I wasn't doing before."
* and more bullshit.

Here's what happened. Here's what I (personally and ***not speaking for anyone but me***) believe was **meant** to happen. The people best suited to this new world thrived. The people who were adaptable adapted to the new world. Less talented people either saw the writing on the wall and left or didn't see the writing on the wall and lost their jobs.

Basically, harshly, adapt or die. I'm sure I'll be on the wrong end of this sentence later in my life too. It's not a nice sentence and I understand that.

Make no mistake, combining 1.5 or 1.75 jobs means less jobs for folks. This is, plainly, visible. And developing and testing software are, at least to Microsoft now, the same job. Whether you see this as evolution or trying to squeeze blood from a stone, the reality is that those things that were separate are now simply not.

The first question a smart observer will ask is: "so you got rid of all these testing specialists. Didn't your quality suffer?" No. No it did not.  And on top of that our agility (as measured in velocity to ship changes) improved. Our collaboration improved. Life, overall, got better for the organization. I believe we are faster, leaner, and better for it.

Why? There's just less stuff in the way. Leaner organizations execute faster. This is why startups are so fucking fast. There just aren't a lot of people so squabbles are easier. Not that startups are the best, but just as they are not the best for good software nor are huge monolithic organizations. A happy medium must be found and maintained and nurtured.

## This new change, though, isn't it harsh?

I don't know how to answer that. When Bing did it, for the company, it was legitimately an experiment. The result was not known. I believe now that after doing it for a very large group as a gradual rollout the expectations have been set. I think they are the right expectations.

Also, there is a harsh reality out there in the world: competition is fierce, rampant, and generally not forgiving. Moving slowly, experimenting gradually with giant organizations, and so on? That's not a luxury you can take in the modern world. You need to move fast and think faster. As the world of computation has grown the competition has grown. As competition grows complacency necessarily has less space. Microsoft is not a complacent company. It is a company of competitors and fighters and people who want to succeed and do a great job.


