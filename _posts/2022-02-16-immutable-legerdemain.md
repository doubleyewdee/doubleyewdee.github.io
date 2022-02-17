---
layout: post
title: "immutable legerdemain"
date: 2022-02-16 11:30:00 -0800
tags: blockchain musing
---

I've spent an unhealthy amount of time [tweeting](https://twitter.com/doubleyewdee/status/1493357937405743106) [mean](https://twitter.com/doubleyewdee/status/1489792844395008003) [things](https://twitter.com/doubleyewdee/status/1489066710736859138) [about](https://twitter.com/doubleyewdee/status/1488736235975626753) [crypto](https://twitter.com/doubleyewdee/status/1485762177738760195) but I haven't taken the time to write down my own criticisms in a longer form. I am, as the kids say, "big mad" about crypto and the blockchain craze. In my defense, I've been a skeptic for a very long time, so I'm not just hopping on the bandwagon of [truly](https://threadreaderapp.com/thread/1445795667826208770.html) [exceptional](https://www.youtube.com/watch?v=YQ_xWvX1n9g&t=16s) [deconstructions](https://blog.dshr.org/2022/02/ee380-talk.html) of the burgeoning crypto industry and all its inherent problems. I am neither as bright nor as eloquent as any of the folks I've linked to who have truly insightful criticisms of crypto, but being less qualified has never stopped anyone from opining on the internet, damnit.

I'm going to spend this post focusing on one tenet of blockchains, specifically the immutable nature of the ledger. This is heralded as a core value of blockchains, as a significant addition of value, and as a feature that is absolutely critical for the very *future functioning of a new utopian society built on the chain*. It's also absolutely insane, it's one of the technology's single biggest faults, and it's *expensive as hell already*.

## a whirlwind tour of immutability through the ages (and how we got around it!)

In the annals of history we have seen myriad ways of producing, storing, and reproducing information. Technological advances in this fine art have contributed immensely to the proliferation of our species. And along the way I would argue that every improvement has tried to make that information *more* mutable, *more* able to be adjusted with *less* effort. Off the top of my head:

1. Stone or wood carvings. Tedious to produce, transport, and absolutely dreadful to modify.
2. Hand-written or drawn works on paper. Still tedious to produce, but much more portable. Multiple pieces of parchment can now be individually replaced or modified without having to reproduce the entire work.
3. Material presses (e.g. plates) creating reproducible works. Still tedious to produce at first, but affording the benefits of individual replaceable components in a compound work, and substantially faster reproduction of those works.
4. Movable type / the printing press. Much easier to correct mistakes in any one page and reprint that page, further accelerating the rate at which information can be disseminated and mistakes corrected.
5. Typewriters! Movable type in the convenience of your own home or office. Mistakes still cost you a page, but you can easily retype the page and pass it along. We got filing cabinets somewhere along the line too, to make these burgeoning reams of information easier to dig out later.
6. Somewhere in here we get white-out and similar. Plus typewriters integrating similar offerings.
7. Digital typewriters / word processors. No more white-out, no more redoing an entire page, just you and your trusty backspace/delete key.
8. Terrible blogs that anyone can publish, generally for free, on the internet. Sorry about that.

Along with the move to digital storage we see a move to embrace more and more mutability of information. Data is now extremely malleable and, even better, you can give your data to another person, and *they can modify it easily*! This has been a massive win for society. Having mechanisms to both produce and iterate on information at an ever more rapid rate has, in turn, accelerated the advancement of science and technology tremendously[^2].

### a boring anecdote about my trip through school

My kindergarten through 12th grade years spanned, roughly, 1987 to 2000 (ugh). Not only did I get to deeply enjoy the 90s, but I got to participate in a rapid evolution of how the education system viewed "written output" of students.

In elementary school (K-5) we were taught cursive, and from about third grade on, anything we wrote needed to be hand-written in cursive. White-out was frowned upon, and if you made a sufficient number of mistakes in a single page, you'd simply have to rewrite that entire page. I guess the thought process here was that, somehow, this would train you to just not make mistakes as often because the pain of doing so was substantial. In practice, what this did to myself and many other students, was make us wish to write the least possible amount so that we could stop being punished for imperfection.

By middle school (6-8) I had managed to convince my teachers that we'd all be a lot happier if I typed and printed my papers[^1]. One teacher was rather insistent about cursive being important, but when I handed her a typed paper printed in a cursive font, she relented (thanks to my mom for the assist there, certainly).

Finally, in high school (9-12) teachers *preferred* papers typed. Students began being encouraged to use the computer lab, typing classes were offered, etc. Handing in a mistake-riddled paper was at least as bad as it ever was, but the process of producing a paper no longer required you to laboriously write and re-write it until it was reasonably perfect.

I'm bringing this up because, in 2022, virtually nobody is teaching kids cursive. Handwritten papers are unheard of. We've all moved on, ceding information creation to the best-suited technology, the venerable word processor. We've embraced more reproducible and mutable data transmission yet again!

## immutability in computer systems

I've led off by noting that mutability is actually pretty good for people, and I stand by that. Making mistakes easier to correct is, generally, a nice thing. However, there are obviously cases where mutability is quite bad, and undesirable. I do not want some rando to show up and "fix" my horrible blog on my behalf, for example. More critically, I want some guarantees that the database in which my bank keeps records of all my monies is inviolable.

Computers have provided many mechanisms to make certain data immutable, and to make data resistant to inadvertent modification or tampering, and these are important. From the lowly "read only" tab on a floppy disk, to filesystem permissions, to checksumming of data to ensure its integrity, making sure data isn't modified *when it should not be* is terrifically important and we've spent a lot of time on that class of problems. However, in all of these cases, affordances are made for times when mistakes need to be corrected, or data actually needs to be altered. Floppy tabs could be flicked, permissions can be changed, checksums can be updated, and so on. A modification has some fixed cost to undo, but the cost is not so exorbitant that mistakes are effectively uncorrectable.

Modern, well-run databases operate using both transactions and extensive backups. This makes it possible to both restore data in the event of a failure and, critically, to repair the system and undo bad transactions (roll back). It's a core value of a reputable data store that incorrect or malicious modification can be undone *with relative ease*.

Modern databases and other data stores also afford granular modification of sections of the data. If you need to correct the balance of two accounts you can simply modify those two accounts without a wildly expensive change that touches *literally else everything in the database*.

## a shitty data store

This brings us to the blockchain. A system that has made it exceptionally difficult to "Control+Z" a bad transaction, to somehow undo a mistake. Because the ledger is immutable, the chain tries to make it nigh-impossible to wind back the clock and repair a mistake, or undo a malevolent action. A disagreement about this is quite literally how we got both Ethereum and Ethereum classic. Amusingly, the more valuable non-classic variant is the one which "broke the rules" to undo a fraudulent transaction. However, the general ethos is that when a mistake occurs, or when theft occurs, that's just bad luck for you and the chain can't be fixed to correct for it. If someone stole your ape then you're shit outta luck, bud.

This is no way to run a railroad for a system that expressly wishes to be a currency. In modern currencies mistakes are correctable, fraudulent transactions are trivially reversible, and that produces a more trustworthy system. Even hundreds of years ago it was possible to pull down a ledger, go through it, find a problem, and then correct it. A single human could do this effectively! In blockchain-land the intentional, built-in difficulty of undoing something means that mistakes are effectively irreversible.

To be clear, this isn't a problem with blockchains themselves, but rather with the philosophy of public, permissionless[^3] blockchains. If you cannot convince the stakeholders to collectively reverse a transaction, then you're boned. Full stop. And the stakeholders (the miners, or the literal stakeholders in Proof-of-Stake systems) have no incentive to help you. They keep getting coins whether they give you back the ape somebody stole or not, and litigating accidental or fraudulent transactions and undoing them is *hard*. Not to mention, they have explicit financial stake in *not helping you*. Every undone transaction at the behest of an Ethereum miner is a lost gas fee they could've charged somebody else to squeeze yet another NFT sale into the next block.

Bitcoin has had over a decade to build consensus among a majority of its stakeholders to provide any meaningful mechanism for transaction reversal and, to date, has not done so. Ethereum literally split itself in half because people couldn't come to an agreement about fixing an *obviously malicious action*, and after the fact neither side of it learned a single lesson from this either. There is no reason to believe this is going to get better. Because the proprietors of these chains have no incentive to help you, they simply won't. Fraudulent transactions are rampant, mistakes are uncorrectable, and the response from the community is the crypto-enthusiast version of gamers telling you to [git gud, scrub](https://knowyourmeme.com/memes/git-gud). It was all your fault, and you're a moron for not doing [whatever magic handwaving woo would've prevented the theft or error]. Go buy a hardware wallet, you absolute cretin.

### a permissioned blockchain is also still a lousy data store

For most of what blockchains are billed as being great for the use of blockchains *in general* is likely a loss of efficiency. There might be legitimate, valuable uses for blockchains, but they seem to be few and far between, and financial transactions almost certainly aren't one of them. Because this information needs to be modifiable, the "write once" nature of a chain is pure overhead.

Blockchain futurists have said that a wonderful world of decentralization and "community ownership" will be here any day now because of this unbeatable technology. The reality so far has instead been a hotbed of speculation, theft, and massive waste generation. I have yet to see a single use of blockchains that did not revolve around financial speculation.

There are cases where [Merkle tree](https://en.wikipedia.org/wiki/Merkle_tree) stores are actually terrific. Git is one of them, but Git is also a significantly more mutable system, without many of the drawbacks of blockchain ledgers. You can literally change the head of a branch to point to a new (or old!) hash whenever you need to fix something. You can tell the server or 'origin' store of the repository that this is the new state of the world. It is not computationally cost prohibitive to do so. Git, instead, is a pleasant mix of "decentralized" (the entire tree[^4] is available locally) and "centralized" (typically a single server is the authoritative origin store). This design is why Git is wildly popular and basically swallowed the entire version control ecosystem in less time than Bitcoin has existed.

Bitcoin, notably, has not swallowed even a significant fraction of financial transactions. But hey, any day now, right?

### endnotes
[^1]: It's fair to argue that, hey, maybe accelerating the advancement of science and technology isn't so great, but I wouldn't be able to hear you from your log cabin in the mountains if you did so
[^2]: this is where my handwriting really started going to crap
[^3]: see [this DSHR post I already linked](https://blog.dshr.org/2022/02/ee380-talk.html) for a great breakdown of permissioned vs. permissionless
[^4]: you can ['shallow clone'](https://www.git-scm.com/docs/git-clone#Documentation/git-clone.txt---depthltdepthgt) git repositories and do sparse checkouts of the tree, of course