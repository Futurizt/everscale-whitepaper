# Multithreading

> "A thread is a unit of execution on concurrent programming. Multithreading is a technique which allows a CPU to execute many tasks of one process at the same time. These threads can execute individually while sharing their resources."



Multithreading in the Ever OS Kernel allows for parallel execution of smart contracts by subgroups of the validator set that share the same data. It allows for fast validator rotation, execution parallelism and other features not covered in the Ever Kernel 1.0.

Multithreading parallel execution enables each shard in a EK to scale to execution capacity levels only constrained by node network connections and interfaces.&#x20;

Validators within a WorkChain are all divided into rotating groups, each of such groups serving only a subset of smart contracts, something we call "threads", dividing accounts’ address space by their number. Number of threads is a configuration parameter of such WorkChain, which can be adjusted depending on a network load to exchange all of the blocks of all of the threads. With a global increase of network throughput, the number of threads could increase.

Our WorkChain has a practical limit of about 256 threads currently, because of network load to exchange all blocks of all threads. With a global increase of network throughput, the number of threads could increase.

Since all threads share the same data, it is incorrect to call them “shardchains”; the term “thread” should be used instead. Also because of that same reason, there is no need for hypercube routing of the messages between threads as they only add unnecessary delays and produce many more messages.
