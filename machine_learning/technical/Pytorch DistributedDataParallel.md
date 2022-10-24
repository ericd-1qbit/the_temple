Multi GPU
> The module is replicated on each machine and each device. During the forward pass, each worker (GPU) processes the data and computes its own gradient locally. During the backwards pass, gradients from each node are averaged. Finally, each worker performs a parameter update and sends to all the other nodes the computed parameter update.

Good practices
Any methods that download data should be isolated to the master process. Any methods that perform file I/O should be isolated to the master process.

https://pytorch.org/docs/stable/notes/ddp.html