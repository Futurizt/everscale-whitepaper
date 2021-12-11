# Context



In 2018 Dr. Nikolai Durov released a series of papers in which he described a Virtual Machine, network and consensus protocols, which were dubbed TON.  In late 2019 a prototype of C++ network node implementation was released by Dr. Durov and his team. Starting from 2018, TON Labs, using just documents available at that date, started to work on a parallel and completely independent implementation of the protocol in Rust programming language. In the first half of 2020 the full node implementation in Rust was released followed by  the validator node release in late 2020.

In computer system terms we view Dr. Durov’s design as a distributed virtual microprocessor or network operating system kernel, thus it is called Ever Kernel or EK version 1.0 or similar, throughout that paper. While the design laid a very solid foundation, to answer the requirements of a truly decentralized, distributed, secure, sustainable, scalable, low latency world computer, it had to be developed further. When TON Labs created Ever Operating System and community has launched the Everscale network, the design and real usage requirements of the network demanded not only additional functionality and modules on top of the Kernel, but quite significant changes in the underlying architecture itself, which is often the case in any computing system design evolution (let’s call it Ever OS Kernel).

The Ever Kernel provides a system with the following components: virtual processing engine (Virtual Machine),  network protocol stack responsible for addressing, virtual messaging buses connecting Virtual Machines (DHT, ADNL, Overlay, Broadcast and RLDP protocols), and a consensus layer that synchronizes and validates the execution of smart contract code on Virtual Machines of different physical computers over the network (Catchain, BFT).&#x20;

To that stack of EK protocols we have made several additions that will be discussed in some details later in this section:&#x20;

REMP (Reliable External Messaging Protocol)\
MBPP (MasterChain Block Propagation Protocol)\
SMFT (Soft Majority Fault Tolerance)\
MSRP (Masterchain Slashing and Recovery Protocol)\
DDVS (Distributed Dynamic Validator Set)

Many enhancements and optimizations are constantly made to the existing EK protocols , but they are largely falling outside of the scope of this document. It is important to mention though, that some of these changes are incompatible with the first version of Ever Kernel. We will concentrate in this paper just on the significant changes we made, leaving the smaller patches and changes out. We will discuss the code handling, bootstrapping and upgradability issues in a separate chapter.
