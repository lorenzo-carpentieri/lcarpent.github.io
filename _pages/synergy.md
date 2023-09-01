---
title: "UNISA HPC - SYnergy"
layout: textlay
excerpt: "UNISA HPC: SYnergy"
sitemap: false
permalink: /synergy/
---

# SYnergy
SYnergy is a software layer for general-purpose, cross-stack, energy-efficient computing on large-scale HPC clusters.
It takes advantage of the frequency-scaling capabilities of modern hardware, especially GPUs, and exposes them to the user through a high-level, easy-to-use interface. 

## Overview
SYnergy is built around three basic components: a SYCL-based API, a compilation framework integrated with a set of target models, and a SLURM plugin.
The figure below illustrates the relationships between these components.

![SYnergy approach]({{ site.url }}{{ site.baseurl }}/images/projpic/SYnergy_approach.png){: style="width: 800px; display: block; margin: 20px auto"}

A SYnergy application is either a SYCL or SYCL+MPI application that uses the SYnergy API.
SYnergy's interface is basically a wrapper of the `sycl::queue`, providing additional features to allow frequency scaling and energy/power measurements at the kernel level.
In particular, each kernel is annotated with a specific energy target.

At compile time, the SYCL compilation toolchain is extended with an additional feature extraction pass that statically extracts a feature vector from each kernel, which is later fed into a target machine learning model that computes the target frequency.
Model inference depends on the energy target provided by the user, and the predicted frequency configuration is made available to the SYCL library at runtime.

After compilation, a SYnergy application is already energy-aware and instrumented with the frequency settings specified by the per-kernel user annotation. 
In the case of an MPI+SYCL application, to enable the frequency scaling and measurement capabilities on a cluster, a SLURM job scheduler plugin extends the job execution policy with a specific prologue and epilogue, enabling energy-efficient computing on all devices in the job. 

### SYnergy Programming Interface

The SYnergy energy-aware SYCL API is one of the building blocks upon which the SYnergy infrastructure is built.
The API, inspired by the SYCL extension [Celerity](https://celerity.github.io), provides a common interface that allows energy profiling and frequency scaling on devices from different vendors, without requiring developers to work with vendor-specific libraries.
The API is released as a header-only library that can be integrated into an existing C++ building environment. The API currently supports NVIDIA, AMD and Intel GPUs.

**More details about the dependencies and usage of SYnergy are available on its [Github repository](https://github.com/unisa-hpc/SYnergy).**
