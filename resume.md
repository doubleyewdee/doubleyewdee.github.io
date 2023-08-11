---
layout: page
title: Resume
permalink: /resume/
---

## Contact Information
- Name: Chip Locke
- Phone: +1 (206) 388-7789
- Email: [wd@teleri.net](mailto:wd@teleri.net)
- [LinkedIn](https://www.linkedin.com/in/doubleyewdee)

## Professional Experience

### Microsoft Corporation (2005 - Present)

#### Principal Software Engineer, Azure Machine Learning (June 2020 - Present)

- Architect for control plane infrastructure team, guiding a team of more than ten engineers.
- Supported regional expansion from ~10 to over 30 regions to satisfy customer demand.
- Guided development of multi-cloud solutions to enable low-effort CI/CD across public, sovereign (national), and air-gapped clouds.
- Implemented fully private/encrypted networking solution for customers using Azure's Private Link / Endpoint mechanics.
- Leading transition to IPv6+IPv4 support for all Azure ML services.
- Designed solution for high-availability, multi-cluster Kubernetes backend, including dynamic nodepool scaling, atomic rollout+rollback, etc.

#### Senior Software Engineer, Azure Machine Learning (June 2018 - June 2020)

- Helped launch the general availability of Azure ML "v2" in late 2018, including addressing compliance, disaster recovery, etc.
- Designed and implemented CI/CD system for a 200+ engineer team to reliably ship updates to control plane microservices.
- Guided efforts in porting Bing-internal experimentation / training services from .NET Framework (Windows-specific) to .NET Core + Docker container microservices.

#### Senior Software Engineer, Bing Engineering Fundamentals (July 2015 - June 2018)

- Migrated all Bing source code from proprietary (Perforce-fork) source control to Azure DevOps Git.
- Helped build and maintain packaging solutions (versioning, distribution) for C++ libraries shared across many repositories.

#### Senior Software Engineer, Bing Application Platform (August 2011 - July 2015)

- Designed, implemented, and shipped an internal metrics platform (similar to Prometheus) for Bing's internal services, handling over 15,000 baremetal machines, each emitting over 1,000,000 metrics per minute.
- Migrated Bing's core query distribution and aggregation system from C++ to C# with no regression in performance (latency or throughput).
- Designed and implemented a discovery mechanism for the ~100 distinct microservices, including dynamic graph building for dependencies, as well as optimistic caching.
- Improved realtime query-serving network performance and reliability by implementing a custom load balancing and fault detecting mechanism for microservices hosted across >30,000 baremetal machines per region, across several regions.

#### Software Engineer I+II, Bing (June 2007 - August 2011)

- Designed and implemented a service to provide dynamic timezone conversion utilizing user location data, and reactive to timezone database updates shipped as part of the core Windows infrastructure.
- Implemented a system for realtime validation of "instant answer" services by reversing per-service grammars to ensure user results were returned as expected whenever data sets were updated.

#### Systems Engineer, Bing (May 2005 - June 2007)

- Hands-on build out of Bing's second-ever (and largest) datacenter, including scripted provisioning of Top-of-rack routers using serial connections and Python scripts.
- Implemented a system to ship a large (100s of TB) dataset cross-country over a weekend in preference of physically shipping HDDs.

### Network Engineer, Akamai Technologies (September 2004 - May 2005)

### Systems Administrator + Developer, Lunarpages, Inc. (August 2003 - August 2004)

### Systems Administrator, Verio Webhosting (July 2000 - October 2001)

### Systems Administrator, United Online (February 2000 - July 2000)

### Intern Systems & Network Engineer, Sears Roebuck, & Co. (May 1999 - August 1999)

## Technical Skills

- Deep familiarty with Windows, Linux, and BSD-based operating systems.
- Current primary languages are Go, C#, Python
- Significant experience with highly available, latency-sensitive distributed applications across multiple languages
- Familiar with many other languages, including C, C++, Bourne (again) shell (bash), PowerShell, Ruby, etc
- Experienced with Kubernetes, Docker, and containerization in general
- Deep networking knowledge across many layers of protocols (IP + TCP/UDP, HTTP (1/2/3), BGP, Ethernet, etc)
- Extensive experience with many revision control systems, particularly Git, Perforce, and Subversion, with knowledge of Mercurial and CVS
- Experience developing kernel drivers for FreeBSD and Windows