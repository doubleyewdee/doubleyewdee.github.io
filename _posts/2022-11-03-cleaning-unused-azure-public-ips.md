---
layout: post
title: "cleaning up unused Public IPs in Azure"
date: 2022-11-03 18:30:00 -0700
tags: work
---

# the code

```powershell
$locks = az lock list -o json | convertfrom-json

function remove-lock([string]$resource) {
    $lock = $locks | where-object { $_.id.StartsWith($resource, [System.StringComparison]::OrdinalIgnoreCase) }
    if ($lock) {
        write-host "deleting lock $($lock.id)"
        az lock delete --ids $lock.id
        start-sleep 30
    }
}

$delete_ips = az network public-ip list -o json | convertfrom-json | where-object { $_.ipConfiguration -eq $null }
foreach ($ip in $delete_ips) {
    remove-lock $ip.id
    write-host "deleting unused public IP $($ip.id)"
}
```

# the why/how:

We've had an R&D sub on my team for, I don't know, like 5 or 6 years? It has accumulated a lot of crap. One of those crap variants is public IPs. These cost money and are a limited resource. Sometimes we're not even using them anymore! So I wrote a script to clean them up. It's not perfect, but we are gonna run it in prod too because YOLO.

Anyway, it turns out it's super easy to figure out if a public IP is attached to anything in Azure! If the ipConfiguration property is null, then it's not attached to anything. So we can just filter on that. Then we can just nuke 'em.

We also locked (some of) our IPs, and I'll tell you right now, fucking do not use Azure resource locks ever. They're super unreliable to delete. Just don't waste your time. More trouble than they're worth. This started as a one-liner that wasn't even powershell-specific, but I had to add the lock removal stuff. Again, don't use Azure resource locks, they're just gonna be painful later.

This should've been a gist, but I need to upgrade jekyll to get the module, and I'm too fucking lazy. rip.

## the one liner (if you wisely avoided locks)
```sh
az network public-ip list | jq '.[] | select(.ipConfiguration == null) | .id' | xargs az resource delete --ids
```