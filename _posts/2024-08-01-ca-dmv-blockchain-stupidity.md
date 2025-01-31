---
layout: post
title: "the California DMV isn't actually using 'the blockchain'"
date: 2024-09-18 23:00:00 -0700
tags: blockchain musing
---

# the California DMV isn't actually using 'the blockchain'

Most of this post is just copied from [two](https://www.reddit.com/r/technology/comments/1ehly72/comment/lg1foql/) [comments](https://www.reddit.com/r/technology/comments/1ehly72/comment/lg3l1ko/) I slapped together today on Reddit in response to an [r/technology post](https://www.reddit.com/r/technology/comments/1ehly72/california_dmv_puts_42_million_car_titles_on/) trumpeting California's DMV placing 42 million vehicle titles on "the blockchain" to "fight fraud."

TL;DR: title fraud can be most effectively fought using centrally-managed digital databases which avoid the commoditization of high quality tools to produce fraudulent paper documents. Blockchains aren't adding anything, and the article is essentially a stealth press release by VC-backed providers trying to prove out any conceivable use for this overengineered and socially corrosive technology to claw back anything they can since the era of free money is over.

## Parent posts

I should say I did the usual bullshit of replying near the top of the thread, on the top-rated post, because who doesn't want to ride someone else's wake?

[Top reply](https://www.reddit.com/r/technology/comments/1ehly72/comment/lg0aqat/):
> Hey look, an actual use for blockchain instead of the constant pedaling for decentralized scam banking that inevitably leads to being regulated.
[Top reply to that](https://www.reddit.com/r/technology/comments/1ehly72/comment/lg0s5i4/):
> Why blockchain, though? A simple database would have worked just fine in this instance.

Why blockchain, indeed. I'll take a swing at this, I thought! Feelin' sassy.

## My initial reply

As you note, a traditional transactional database probably makes more sense here. I'd go further and say it is almost always (>99% of the time) superior to blockchains unless you need something *exceptionally* specific. In this case, though, it's quite likely that the blockchain aspect is doing the least interesting work, and so is mostly an implementation detail vs. being truly novel or important, except insofar as some VCs cajoled some California government employees to cut their investment vehicle a sweet deal.

The linked article makes mention of users having to download "wallets" to manage their titles, but I'd be surprised if the reality was not that this app/"wallet"-based scenario looked absolutely nothing like the typical 'DeFi' wallet solution. Users, after all, cannot lose the title to their vehicle because their phone ended up in a Cybertruck which Autopiloted itself off Highway 1. More than likely the user installs the app, authenticates, and then is provided a "wallet" that is a centrally-managed key which can be retrieved by a human being and is not irreversibly losable.

Either that or selling a car in California is about to become *real* bad, *real* fast.

Also, what people think of as 'blockchains' in the DeFi/cryptocurrency sense are a very specific subvariant, called 'public, permissionless' blockchains. These are your Bitcoins (powered by proof-of-~~waste~~work) or Ethereums (proof-of-stake). The key here is the 'permissionless', meaning they allow for open participation from any member node of the network who meets the requirements (for PoW, that's "show up and hash good" and for PoS that's "already own some tokens to prove you're not some poor schlub").

This blockchain, via Avalanche, is powered by proof-of-stake, but critically the stakeholders **are not the general public**, nor would they ever be. The "stake" in the operating nodes is entirely owned and operated by either Avalanche or the State of California. You can't go run a "California Title Chain" node for GavinNewsomBux or whatever. More than likely the real, on-the-ground implementation involves some small set of hand-rolled nodes running somewhere on EC2 or GCP with human-provisioned "stake." At best maybe they have a leasing system and containerized the work and threw it in Kubernetes somewhere.

So, basically, it's a distributed (in terms of being in multiple compute nodes) ledger database being used as a backing store for transactional data (title transfers). It's extremely likely that most or all of the meaningful database information (e.g. metadata about humans such as name/SSN/state ID/etc) remains in what I'll just bluntly call a "real" database, and this whole ledger exists purely to express directional/ownership transactions like (ownerID, titleID) -> (ownerID', titleID), which are infrequently reversed and can be acceptably reversed by a human reversing that pairing on this blockchain. The cryptographic assurances add very little or nothing.

Super overengineered, but hey, how else are you gonna employ all those CS grads?

## Oh no, critique!

At this point, feeling smug about that banger Tesla/Cybertruck diss, I departed to live a fulfilling evening. Which meant going to Costco. At some point I got [a reply to that comment](https://www.reddit.com/r/technology/comments/1ehly72/comment/lg3d1wu/):
> What do you mean the cryptographic assurances add very little? Those assurances are the only thing that makes it effective against fraud. They mean nothing in terms of anonymity, ironically they let you prove that you are what you say you are. 

I was burnt out from Costco, and decided that instead of doing something useful, I'd take a deep dive into what the hell is going on here. This is the actual bit I felt like preserving in the fossilized amber of this unread blog I'll link on Bluesky for twelve poeple to read and enjoy:

The app and users' "wallets" are centrally managed and controlled by a single entity. Check out [the California DMV site](https://qr.dmv.ca.gov/portal/ca-dmv-wallet/mdl-faqs/) that discusses their 'mDL' offering for a sneak peek. The controlling entity is the DMV, they are the sole arbiter of access control in this system. You can gain access to an mDL only through a digital scan of your existing physical ID. While that is likely to change in the future, probably in conjunction with services like ID.me, the reality is that the identification/identity database is centrally managed by the State of California. Absolutely none of that is backed by a blockchain in any form. It's just the usual cryptography and centrally managed data stores with industry-standard oversight and safety guarantees.

The titie digitalization program's benefits, as touted, seem to largely be around the typical benefits of digitalization over paper records. The digitalization trend of formerly paper-backed records is well over half a century old and does not appear to benefit from the "every write is signed" ledger-style database trappings of blockchains in any meaningful way (as evinced by the glacial uptake and routine rollback of this stuff in both private and public sectors) and the [repeated](https://www.zdnet.com/finance/blockchain/microsoft-is-shutting-down-its-azure-blockchain-service/) [failures](https://www.infoq.com/news/2024/07/aws-kill-qldb/) of this technology to win on the merits with large solution providers who do not have any VC dollars to try and recoup, and thus are deciding the customers simply are not there in a way that makes running these things profitable. To me, that speaks volumes.

The Reuters article linked actually notes that the blockchain touting is coming from the MSPs who built this stuff, as the article now points out in a corrected first paragraph:
> the agency's technology partners exclusively told Reuters on Tuesday.

So, what's happened here is that the CA DMV has digitized their existing collection of title data and stored it on a centrally-managed and centrally-controlled database. For reasons that are likely to be related more to brokered deals than technological merits, their MSP decided to use a blockchain as the backing store for this data. However, the cryptographic "merits" here added purely by the blockchain are largely not valuable since the database is centrally owned and managed by an entity which can reasonably trust itself to run its own nodes. Notably, you can use [Avalanche's own site](https://subnets.avax.network/subnets) to confirm that no title data is on the public portion of its blockchain. There is no 'CA DMV' subnet or anything like it, you cannot find these title assets stored in public *because they are not and never will be*. The whole thing is using some private implementation (which their developer documentation can show you how to run). Meaning that in the face of, say, a rogue actor who has compromised the DMV, they can simply modify the ledger by writing in to it from one of the trusted nodes within the network. This is textbook Oracle Problem stuff. Just like a real, big kid database, a rogue actor from outside the DB can input invalid data. The fact that this input is ensconced in cryptographically hashed and validated blocks makes it no more, nor less, invalid. It just burnt more electricity to do than an `INSERT` in a SQL database because someone really wanted to score a point for their VC-backed startup(s).

You can also just use an [append-only ledger](https://learn.microsoft.com/en-us/sql/relational-databases/security/ledger/ledger-overview?view=sql-server-ver16) from your database provider if you want that particular behavior.

I really want to reiterate, because this is crucial, the blockchain being used here is both *private* and *permissioned*. It is not the kind of "blockchain" that is implied with the colloquial use of the word, which is *always* "public, permissionless blockchain". What they have is just an append-only ledger using a technology largely designed and engineered to solve a problem (trust of nodes hosting the ledger) that *does not need to be solved in this case*. Also, notably, they're not using this for actual *identity*. Which should give you pause.

Supplemental reading:
- [The technological case against Bitocin and blockchain](https://lukeplant.me.uk/blog/posts/the-technological-case-against-bitcoin-and-blockchain/) hosts a bevy of links to well-written critiques from luminaries in the fields of both cryptography and general computing.
- [EE380 Talk](https://blog.dshr.org/2022/02/ee380-talk.html) goes through the issues with permissionless blockchains nicely. It also makes the case that (these are my words) permissioned blockchains are essentially just merkle trees (think along the lines of git repositories) wrapped up in the rough equivalent of Zookeeper to enable running on multiple trusted nodes.

So much to say: this whole title database could have been a private GitHub repository. Christ, I'm so sick of this shit.