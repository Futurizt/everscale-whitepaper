# Smart Contract Languages



Ever Kernel v1.0 uses the Everscale Virtual Machine for smart contract execution. The reason to use such a virtual machine mostly relates to the compactness of its code and supposedly easier security model. For Ever OS design considerations it was very clear though that in order for such a platform to be adopted by many developers the high level and familiar programming languages should be adopted to write programs for ESVM.

The special nature of blockchain immutable programs that may hold very large monetary value dictates special attention to its security. There are largely two ways to look at a solution to that problem. One would imply creating new Domain Specific Languages (DSL) to limit the ability of a programmer to make mistakes. We always believed this way leads to the oblivion of such a platform. Therefore Ever OS middleware includes compilers for Solidity and C/C++ languages (using the LLVM framework). In a special note let’s mention the Ever LLVM compiler team work on advancing the comprehensive stackification logic within LLVM community.

The security model for writing such programs using general purpose programming languages is described in the next section, yet there is one tiny note of hypocrisy and one larger problem of efficiency in this logical construction.

The thing is Solidity and even C/C++ we are using to write for ESVM are not exactly general purpose programming languages. Even a proficient C++ programmer can not simply write a Ever OS program in C++ without first understanding quite a lot of limitations that ESVM (or any other such Virtual Machine for that matter) execution imposes on a language.

For example, the inability to write code like this:

`int *arr = new int[10];`

Or the notion of memory which is completely different etc, could probably illustrate the point. Of course one would claim that a distributed processor architecture probably requires a special model of program execution. After all, the use cases for such programs are very different from use cases of a local computer or a network server. Yet is it really so? Can we have a fast compact code execution which would be really easy to develop?

Michael Franz has developed several interesting concepts that are worth researching in terms of its potential applicability to Ever OS. There is a prototype developed in TON Labs for translating Solidity into Slim Binary. On average, a code of several Kilobytes is translated to just a few hundred bytes even without index compression and similar optimizations. Such a code could be executed in a separate isolated environment as part of the ESVM instruction set or as a non-ESVM code.
