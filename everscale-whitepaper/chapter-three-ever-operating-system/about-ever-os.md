# About Ever OS



Ever Operating System is an intermediary between a user and a blockchain — a distributed verifiable computing engine.

A modern blockchain like Everscale is not just an immutable ledger. Bitcoin and other earlier blockchains were mostly ledgers, yet even Bitcoin supports a non-Turing complete script that provides some transaction execution instructions.&#x20;

Most blockchains after Ethereum are, in large part, distributed computing engines that execute and verify Turing-complete programs called smart contracts. In simpler words they are a special breed of network processors working in orchestration (called "consensus") to perform common operations and in that way verify the correctness of their execution.

In Everscale this paradigm is taken to the extreme. The immutable ledger is quite a small part of Everscale. Of course it is an immutable ledger and a chain of blocks — that is how the data is written and transmitted from one network processor to another — yet there are at least two aspects which make Everscale uniquely more so a computing engine than a simple ledger.

Almost everything in Everscale is smart contracts. Every account in Everscale must be associated with a smart contract code (or initialized) in order for a user to be able to perform any operation with it. Smart contracts are Everscale Assembly programs executed in the Everscale Virtual machine much like any assembly code is executed by hardware or by a virtual processor in a regular computer.

Between a regular computer and a user (which may be a developer who would like to write programs for that computer or a regular user who would like to execute and interact with these programs) there is something called an operating system.

That is how GNU defines an operating system:

Linux is an operating system: a series of programs that let you interact with your computer and run other programs.

An operating system consists of various fundamental programs which are needed by your computer so that it can communicate and receive instructions from users; read and write data to hard disks, tapes, and printers; control the use of memory; and run other software.

It is quite obvious why computers need an operating system. Before operating systems existed, interaction with computers looked horribly unpleasant to the end user. Something resembling today’s interaction between a user and a blockchain.

Any way you look at it, blockchain is quite a good candidate to be called a decentralized computer. At least some of the blockchains are. Everscale most definitely is.

And just as with any computer, a blockchain needs an intermediate layer (or layers) that manages its resources and provides services to the programs the user runs or interacts with. Of course blockchain, in terms of architecture, cannot perhaps be compared directly 1:1 with a regular PC. But in logical terms, whenever we think about a software stack needed to enable interaction with a user — to call it an operating system is quite compelling.

Let's run some arguments. For reasons of practicality we will not talk only about the Everscale blockchain, but most of the arguments could be applied to some other modern blockchains as well.

A classical operating system is expected to provide: Memory Management, Processor Managing, Device Managing, File handling, Security Handling and so on. In this chapter we will discuss how all that is implemented on the blockchain for the first time.
