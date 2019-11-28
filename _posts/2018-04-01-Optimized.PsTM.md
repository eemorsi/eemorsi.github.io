---
layout: post
title:  "Highly scalable flexi-trace-based pre-stack time migration"
date:   2019-07-05 01:12:32 +0200
categories: RTM updates
---
Pre-stack Time Migration (PsTM) has been widely adopted as a flexible seismic migration method. PsTM is computationally intensive even with the high performance clusters; some 3D seismic data may take days or weeks to migrate the final image. The most intensive PsTM’ modules are travel-time calculations and diffraction summations; both of which exhibit trade off between travel-time computations and other resources.

The algorithm's compute time is largely governed by the computation and storage of travel-times and its feeding mechanism to the migration process. Traditionally; the straight ray-based assumption is used in estimating travel-times. Efficient parallelization is a challenge due to the high demand of computation resources e.g. memory, storage and I/O.

The parallelization strategy highly depends on the feeding of the diffraction stacking process and advances in current computing technologies e.g. number of core, memory,etc. The new approach exhibits flexibility in migrating large datasets optimizing available memory per computing with the minimal IO requirement and inter-node communications. 

We based our parallelization method on three main steps; 1) optimized travel-time computation based on lateral velocity with retain/replace methodology to minimize travel-time generation overheads without the need to interpolate during runtime. Retain/Replace policy helps in maximizing the use of the computed travel-times; minimizing re-computations to major extents. 2) Utilize available memory nodes at runtime by migrating shot gathers using flexi-trace iterations; taking into consideration aperture constraints. 3) Minimize inter-node communications at the final migrated image.

We benchmark our method using the BP model and compared performance of both standard and optimized approaches on Intel's latest architectures (such as Broadwell, Skylake and Knights Landing);.
