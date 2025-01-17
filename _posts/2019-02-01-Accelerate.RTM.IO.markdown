---
layout: post
title:  "Accelerated Reverse Time Migration with optimized IO"
date:   2019-07-05 01:12:32 +0200
categories: RTM updates
---

Advanced computing technologies are extending the performance limits of computing power by increasing the number of microprocessor processing cores, clock rate, and word size; thereby, making advanced seismic imaging and migration techniques, such as Reverse-Time-Migration (RTM) economically feasible. The RTM seismic imaging approach is widely used for migrating areas of complex structures. The standard implementation of keeping a snapshot for every time step is the easiest though most IO traffic intensive implementation. Handling snapshots in memory has clear limitations due to large footprint requirements, extra data movement and extra communication between domains that frequently generated load unbalance.

Our optimized approach, however, works on reducing space used for storing the propagated data by compressing seismic data and hence reducing IO time. The data compressor is based on the newly developed ZFP lossy compression algorithm. ZFP achieves negligible data loss due to it offering highly spatial data correlation. This allows us to reduce propagated data IO traffic at any time instant and its corresponding memory footprint. It does, however, add the extra processing time of compression and decompression. Here, we review 2 implementations in addition to the compression capable version, one using the standard approach, and the second doing an extra propagation, using random velocity boundaries and reducing IO.

Doing the 3 propagations without keeping snapshots is beneficial for kernel optimization. We benchmarked our optimized RTM with IO compression and compared its performance to the standard, random boundaries-based and compression-based optimized RTM on Intel's latest architectures (such as Broadwell and Skylake with/out 3DNAND P4500/P4600 storage for memory snapshots); we notice significant speedup of the random boundaries-based RTM and compression-based RTM of factors of 6.3x and 2.4, respectively, compared to the conventional RTMs.


