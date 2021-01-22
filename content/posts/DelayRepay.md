---
title: "DelayRepay"
date: 2021-01-20T21:12:07Z
draft: true
---
We presented _DelayRepay: Delayed Execution for Kernel Fusion in Python_ at the Dynamic Languages Symposium 2020. DLS was supposed to be in Chicago, but alas.

The long and short of the paper is that if we trace calls on a NumPy array and
delay the execution until needed, we can fuse these calls together when we
execute them on a GPU, resulting in improved performance.

I'll include the abstract:

> Python is a popular, dynamic language for data science and scientific computing.
> To ensure efficiency, significant numerical libraries are implemented in static native languages. 
> However, performance suffers when switching between native and non-native code, especially if data has to be converted between native arrays and Python data structures.
> As GPU accelerators are increasingly used, this problem becomes particularly acute.
> Data and control has to be repeatedly transferred between the accelerator and the host.
>
> In this paper, we present DelayRepay, a delayed execution framework for numeric Python programs.
> It avoids excessive switching and data transfer by using lazy evaluation and kernel fusion. 
> Using DelayRepay, operations on NumPy arrays are executed lazily, allowing multiple calls to accelerator kernels to be fused together dynamically.
> DelayRepay is available as a drop-in replacement for existing Python libraries.
> This approach enables significant performance improvement over the state-of-the-art and is invisible to the application programmer.
> We show that our approach provides a maximum 377x speedup over NumPy - a
> 409% increase over the state of the art.

This work was focused on GPUs - we didn't check if this approach helped with
vanilla NumPy on CPU. I suspect that a very naïve implementation might see a
benefit from warm caches, but probably not much. I have thought of a few tricks
that might help, we'll see.

DelayRepay is free and open source, and is available on
[sourcehut](https://git.sr.ht/~magnusmorton/delayrepay). The paper is available
here:
[https://doi.org/10.1145/3426422.3426980](https://doi.org/10.1145/3426422.3426980),
along with a video presentation.
