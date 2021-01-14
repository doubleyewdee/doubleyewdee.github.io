---
layout: post
title:  "the dichotomy of devops"
date:   2014-08-13 00:00:00 -0800
tags: musing
---

**Operations**: Keey your systems and processes running smoothly and minimize disruption.
**Development**: Create new features, and change the status quo (... *disrupt* ...). Iterate. Reimagine. Release.

So let's combine those two? How could anything go wrong?!

Things may or may not go sideways, depending on how you structure your arrangement. For example if you ask the folks doing your operations to automate more of their work while focusing on quality and scalability you may be very happy. If you ask the folks doing feature work for you to also be responsible for 24x7 operational maintenance of their product you may not be quite as happy. My experience has been, broadly, that people are more interested in the latter.

## This is the last time I'll use 'devops'

It is only a mild exaggeration to say I want to throttle people who say devops. Of course the list of things I **want** to do but, almost certainly, will never do is a mile long. That said I do believe the term 'devops' is almost 100% bullshit in the software industry. It is a term used to sell reduction-in-force and combination of people. It is a way to both make one group of people feel better about what they're doing and make another group feel more responsible than they might have been trained to feel.

## 'That thing' for the uninitiated.

The concept of "developer" + "operations" *(I made a promise and I'm sticking to it)* isn't new. The buzzword bingo term for it is also, at this point, no longer new. But it's hung around like many buzzword bingo bullshit terms and it is routinely used incorrectly to convey a sense of duality that doesn't actually exist in the mind of the person who is tasked with being ... that person. Be a developer! Be an operations person! You're doing two jobs and we're paying you for one!

... that last bit tends to be omitted but let's be fucking real, please. This is one of the big value propositions of devops. More work done by less expensive fleshy people.

## Traditional operations

My experience in traditional operations was really enlightening. The people who have done well in this field have, in my experience, been either:
1. Ex-military.
2. Former managers at critical utility services (think telecoms, electricity, etc).

Now let's think about this. In both these professions a fuck-up can and often does mean that **somebody is going to get hurt or die**. These folks have serious responsibilities and take those responsibilities very seriously, as well they should. Mistakes cost, and the cost is often not justifiable when your sole justification is "trying to get shit done quickly."

The interesting thing is that it tends to pay better to move farther away from government roles, at least in the US, so some of these operational and process experts look around and say, "hey, maybe I can go rake in some bucks doing what I'm good at over here." They absolutely can. Moreover, their expertise sounds appealing. Their rigor, attention to detail, and discipline will almost certainly come across as appealing to somebody hiring them. These people are buttoned up, straight-laced, no-goddamn-nonsense folks. Who wouldn't want to have somebody like that helping them run the show?

## Let's hack some Gibsons

I've been *(humblebrag)* writing software in some form since a very young age. I can't pinpoint exactly when I started **really** writing software, as opposed to manually entering examples of BASIC and then tweaking them to learn, but it had to be somewhere around 11 or 12 when I, um, borrowed my uncle's Turbo C book with associated set of diskettes.

*(Borland's Turbo C was legit. I mean crazy legit. Just want to say. It remains with me as a truly formative experience in computing.)*

I've talked to some people who are developers too so I'm going to take the liberty of speaking for a class of folks *(probably a mistake)* and say that what motivates developers is creation. Creation is anathema to control. It is actually entropy at work. It's taking some form of previously concentrated order and rearranging it to be something new and different.

Most important to the dogma of the dev is that, hey, we know we're gonna break some shit. *Nobody ever made an omelette without breaking a few eggs*, right? So obviously bugs will happen. Chaos will happen. Change will happen. Problems will be created and, to be blunt, the job of the developer is to create new problems **and** new solutions. Ideally with a ratio that favors solutions but, hey, depends on the developer and the structures around them.

What developers don't do, routinely, is worry about the repercussions of their changes. In particular when they're going to have second, third, or increasingly N-distant level impact. It's not part of the culture. If it builds it runs. If it unit tests it *really* runs. If the script against the modestly validated build executes and you can pretend that was a real end-to-end test then, omfg, it's gold goddamn master bits.

## So let's combine some stuff!

Well, er, you ***can*** do that. I hope what I've said illustrates why maybe this is harder than it sounds.

It's not that the two disciplines cannot meld together or shouldn't. But you should understand what you're getting in to. In particular you should understand that a hardcore person from either discipline may struggle to understand why "that other guy's" view is meaningful. Different things matter to different people. 

My personal experience boils down to:
1. I am not actually algorithmically smart and so I tend to learn a lot from others about how to improve the ideas I have.
2. I am very motivated by other people being happy (or unhappy) with the thing I made.

In particular I am, like many (most?) humans, motivated to make other humans happy. Even indirectly. This probably means I lean a little bit closer to the "operations" side of the spectrum. After all, nobody is ever happy when the product they tried to use doesn't work! So I focus more closely on that particular aspect and eschew what I would classify as "algorithmic beauty" in favor of a thing that works. That isn't to say I don't have a love for beautiful and simple algorithms and code, I truly do, but if I had to pick a side then functiionality would be where I land. I'm just into making people happy in the way I feel I can do the best.

That said, when you set aside personal opinions, I still believe you land in a tough situation in terms of how to position this work. There are some pretty common constraints that a lot of businesses face here:
1. Operations are, well, opex. They are costing your business right now to do what you have. They are not future (capex) expenditures. Even worse, they might have a fixed ratio of expenditure against your expansion *(oh god nooooo)*.
2. Operations folks spend a shitload of time saying "no." They are actually trained and incentivized to say "no" when they believe a request is dangerous, frivolous, or both. Nobody likes to be told "no" but, from experience, I can say it's sometimes really fun to **say**.
3. Hackers really fucking hate being told "no."
4. Hackers are notoriously harder to wrangle that the more straight-laced operational folks.
5. Operations folks are perceived as "anti-future" because they are motivated by keeping what works now and improving the current situation. They are not "green field/blue skies/etc" people.

## Hold on why are we trying to combine these folks?

Because there's immense value in both mindsets. In truth running a high quality service means you need both types of personalities. The weird devops dichotomy is actually indicative of this desire. Operational excellence, rigor, and innovation. Roll them into one! This can work, right?

It can and it can't. The truth is that smart organizations realize who cares about what and split them out. The people who care deeply about uptime and operational excellence tend to coalesce in the part of the world where high availability is paramount. The folks who care about the worlds of data science and algorithmic excellence end up in those places. Meeting in the middle is hard because of the competing values.

How distinctively these things are split is different by organization. Some organizations maintain explicit operations teams with an expectation that their teams are also good developers with an ability to create software to autokmate the mundane and audit/understand/improve the software they support. Other organizations simply ask the authors of various software to support that software as part of their job. Still others find a place somewhere between these two, perhaps by tasking only a subset of individuals with operational work, etc.

Again, the real motivator here is to have less humans involved in running systems. This isn't an entirely cynical or money-driven play, either. Less humans tends to mean less human error, lower transition costs, more predictability, all kinds of good news for organizations trying to build and plan for the future.

## Finding the right balance is hard

The reality is that you probably don't want the developers who make the product to be alone on the front lines of their product. It's a pretty ugly mix for those folks. It tends to be draining and a bit demoralizing to support what you wrote in front of others and, when trying to resolve an end-user facing situation, have to both think fast and also eat the heaping helping of humble pie that is "you fucked up, boy."

On top of that heavy-duty support has a real human toll. It can mean that you were wide awake at 4am dealing with something while being expected to be bright-eyed and bushy-tailed at the 10am meeting on the same day. This is not a sustainable lifestyle for any but the most masochistic of folks. Trying to get people to live in two worlds at once is destructive.

Even worse when participating in this kind of world, you are probably "too deep in the shit" to see the systemic operability issues at this point. You have become so immersed in the cycle of code/release/support that you tend to lose sight of the bigger issues hurting you in any of those three stages. This is going to make your life unpleasant and your work suffer. In turn this will make your organization and your product suffer along with you.

Ideally you do find a place for other humans to offer their perspective here. While it is true that too many cooks spoil a meal, it is also true that you'll have a hard time preparing a banquet with only one person in the kitchen. Finding that balance is critical to create a terrific and supportable product. The folks you bring in to help you nail operability and operations need to have the right combination of flexibility vs. rigor, but critically they also need to be a little detached so they can offer you a different perspective on your product.

So effectively it becomes critical to both demand technical excellence from everybody involved in your product while still ensuring that some disciplines have a reasonable split between them. Ideally you have people who could, in a pinch, trade jobs with anybody else but, when not in a pinch, are given the freedom to work in the places where they are strongest.

Asking somebody to be two people at once is a recipe for sadness.

