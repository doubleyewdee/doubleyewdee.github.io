---
layout: post
title:  "fleeting thoughts"
date:   2021-01-13 19:00:00 -0800
tags: work kubernetes
---

For the last several months I've been thinking about how my team approaches desired state config (or goal state automation) for our Kubernetes clusters. I've been looking at what's available in the OSS world and what I expect to come from Microsoft's internal CI/CD platforms for first party workloads and trying to form a coherent view between them and figure out what we're going to do. In my case "us" is the control plane for Azure Machine Learning. We are available in [about two dozen regions](https://azure.microsoft.com/en-us/global-infrastructure/services/?products=machine-learning-service) spanning [multiple Azure clouds](https://docs.microsoft.com/en-us/cli/azure/manage-clouds-azure-cli)

Our arrangement involves a small number of clusters for each region sitting behind a traffic manager in each region. So just in the public cloud we've got lots of clusters to wrangle. We want them all to look identical (cattle, not pets) and go through a lot of trouble to make that happen even within just one region, let alone across a whole cloud. We've cooked up a bespoke system to manager this now, but it's expensive to maintain, expensive to add features to, and is itself a 'pet' (or snowflake) bit of software.

## Considerations

Above all we must honor our commitment to [safe deployment practices](https://azure.microsoft.com/en-us/blog/advancing-safe-deployment-practices/) or SDP. We've got a solid CI/CD system that orchestrates this on our behalf, and whatever solution we settle on needs to integrate with that tooling.

We're also pretty committed to multi-cluster even within a single region. It gives us a tremendous amount of flexibility, and if I could I'd probably have *more* clusters per region over the use of nodepools or similar for horizontal scaling. It's so incredibly nice to look at a cluster, say "boy that's horked and I just don't know why," and be able to just yank it from the traffic manager and dissect it or remake it whenever we want.

Finally, we must also consider each Azure Cloud as its own isolated unit, with its own unique and *self-contained* stamp. I cannot reliably run an orchestrator for our clusters in `cloud A` from `cloud B` because they must fundamentally be designed to require *no physical network connectivity* between each other. This imposes surprising challenges for models like GitOps!

## The contenders

After doing periodic research and thinking I've binned my prospective choices as:

1. Wait for someone else internally to do this for us.
2. Build something for our specific scenario / team to replace what we have.
3. 'Buy' something (really find a good OSS component) that meets our needs.

### Waiting for internal tooling

This is the easiest choice in terms of active effort. Other than explaining to our sad internal customers that they'll need to wait for *that other team* I don't have to do anything. Unfortunately this option is marred by two realities: our existing solution is already creaky and hard to maintain and I don't expect deep Kubernetes multi-cluster orchestration within even the next year because of other competing interests. In any case I'd rather blaze a trail here, if possible.

### Building something

On paper the problem, peeled down to our exact requirements *right now* might actually be tractable to just rewrite or whatever in a few months in a nicer fashion. Unfortunately that leaves us in nearly the same position in terms of maintaining this new pet we've constructed and, at best, open sourcing it and hoping for the best as our requirements grow beyond what we have today. Seems like a huge bummer to do this if we can ...

### Buy something

'Buying' in this case means adopting an existing open source solution (of which there are ... some) to the realities of our situation and it's very appealing. If somebody did 90% of the work for us already we'd be foolish not to consider glomming on to that. The biggest downsides are dealing with that last 10%, with wiring it up to work with our requirements, and with having to potentially wait for desirable features to ship in a stable state.

Worse yet, we could end up being left behind by a fundamental change in the external project which will render it unsuitable! That would dump us back into the position of having a pet we must care and feed for, with the additional drawback of potentially having no experienced handlers for that pet. I think these kinds of events are not common, but when they happen they can be pretty disastrous for an organization because it's basically instantaneous rot/tech debt broadsiding you.

## What I think I want to do

I've been looking at [fleet](https://github.com/rancher/fleet) and [flux](https://github.com/fluxcd/flux) pretty closely. Both are heavily focused on GitOps style declarative state. Point them at a Git repo and they make your cluster(s) look like what's in the branch you ask them to track. This is actually more than what we need because of the aforementioned internal CI/CD system which is, alas, not GitOps backed at this time. Meaning that we have to integrate changing $some_git_repo with it and then shipping that repo, somehow, to the clusters in whatever cloud+region needs to be updated. It's not a tremendous hurdle certainly, but it's also not super intuitive.

Flux came recommended from the land of AKS as an interesting option, but it doesn't appear to solve our multi-cluster problem or plan to do so.

Fleet is quite new, but looks to be built with the express purpose of managing multiple clusters. I'm actually pretty excited about it and tentatively want to use it. It looks like it could support either managing a small slice of clusters (one region's worth) or even be adapted to handle multiple regions within a cloud. 

I still need to think through the mechanics of having and modifying some git repository that both our CI/CD system and fleet can work with at the same time, but that feels like something we'll have to do no matter what. It even has some upsides in terms of being inspectable and providing an audit trail, which would be nice.

