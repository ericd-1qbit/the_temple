# JAX
Acronym stood for: Just After eXecution. But that's outdated, now JAX is just JAX.

## Core Ingredients
- Automatic Differentiation of python and numpy code based on:
https://github.com/hips/autograd
- 




JAX even lets you just-in-time compile your own Python functions into XLA-optimized kernels using a one-function API
Compilation and automatic differentiation can be composed arbitrarily, so you can express sophisticated algorithms and get maximal performance without having to leave Python.

## Glossary
| Term | Explanation                |
| ---- | -------------------------- |
| jit  | just-in-time               |
| XLA  | accelerator linear algebra |
|      |                            |




**How does Just-In-Time (JIT) compilation actually work?**  

> I would call the “conventional approach” to program compilation the process of building the program (creating an executable) before the execution. This is done by translating a high level language (let’s say a C++ file) into machine instructions (object code/assembler language). A linker is involved to make the connection between high-level and machine instructions.  
> During the evolution of computing languages, a different approach arose at one point: the usage of interpreters. Instead of translating high-level instructions to machine code, they are translated to “pseudo-code”. The interpreter runs your program by translating the pseudo-code into instructions on the OS/hardware-platform you are running on, making the program more portable.  
> Just-In-Time compilation is a feature sitting in-between these two approaches: the program is still translated into pseudo-code but instead of each method getting re-interpreted every time they are invoked, the methods are translated into machine instructions on the machine they are run on. You basically get a mixture of on-the-fly interpretation and compilation into “fixed” machine code. Note that there’s a trade-off between JIT compilation time and runtime improvements. For (most?) ML applications, the runtime improvements far outweigh the compilation overhead.  
> Specifically for JAX, there’s a neat write-up in the docs: [https://jax.readthedocs.io/en/latest/jax-101/02-jitting.html](https://jax.readthedocs.io/en/latest/jax-101/02-jitting.html)  
> JAX code is translated into the pseudo-code language jaxpr. A good practical advice is in there too:  
> “[...] Therefore, it usually only saves time if the compiled function is complex and you will run it numerous times. Fortunately, this is common in machine learning, where we tend to compile a large, complicated model, then run it for millions of iterations.  
> Generally, you want to jit the largest possible chunk of your computation; ideally, the entire update step. This gives the compiler maximum freedom to optimise.[…]”

**What’s the advantage of JAX’ using the forward pass through gradient functions over backpropagation?**  

> According to my current understanding, both “reverse mode” (used by backpropagation algorithms) and “forward mode” autodiff are similar and valid approaches. The flax docs have a concise section:  
> [https://flax.readthedocs.io/en/latest/guides/jax_for_the_impatient.html?highlight=autodiff#gradients-and-autodiff](https://flax.readthedocs.io/en/latest/guides/jax_for_the_impatient.html?highlight=autodiff#gradients-and-autodiff)  
> [...]  
> Even though, theoretically, a VJP (Vector-Jacobian product - reverse autodiff) and a JVP (Jacobian-Vector product - forward-mode autodiff) are similar—they compute a product of a Jacobian and a vector—they differ by the computational complexity of the operation. In short, when you have a large number of parameters (hence a wide matrix), a JVP is less efficient computationally than a VJP, and, conversely, a JVP is more efficient when the Jacobian matrix is a tall matrix.  
> [...]

**Why is auto-vectorisation a thing in JAX? Hasn’t it been around for long?**  

> Vectorisation (eg. working with arrays) has of course been around for long. The feature JAX offers is to automatically apply functions written for a single vector/array to a batch of vectors/arrays. This is a cool feature - you can find more details here: [https://jax.readthedocs.io/en/latest/jax-101/03-vectorization.html](https://jax.readthedocs.io/en/latest/jax-101/03-vectorization.html)

**What’s the advantage of the PRNG setup in JAX?**  

> This question related to the possibility to pass a random seed around in classic stateful PRNG like in numpy. The advantage of the explicity way PRNG are handled in JAX is that the handling of the “entropy” is thread/process/device-safe by design - the user gets “forced” to properly take care of the handling of PRN. Passing a seed in a stateful PRNG might still lead to scenarios with hidden effects.  
> More info here: [https://jax.readthedocs.io/en/latest/notebooks/Common_Gotchas_in_JAX.html#random-numbers](https://jax.readthedocs.io/en/latest/notebooks/Common_Gotchas_in_JAX.html#random-numbers)