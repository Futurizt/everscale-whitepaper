# File System

In Ever Kernel the address of a smart contract is calculated by hashing its code and initial data. The full address, consisting of a 32-bit WorkChain\_id, and the 256-bit internal address or account identifier account\_id inside the chosen WorkChain. In operating system terms it provides address space management functionality.

In the context of the Ever Operating System though, The Merkle tree of Ever Kernel 1.0 provides just part of the necessary functionality to build a fully distributed file system. Therefore we are adding two additional search trees in which nodes would represent contract code hash and contract data and leafs would be contract addresses. We are optimising for fast lookup for contracts with similar data or code hash from within the Node and adding subsequent instructions to ESVM to allow this lookup from within smart contracts. Additionally, we add code versioning within these trees thus allowing following the evolution of a smart contract code after setCode operations.

This functionality will be particularly useful in the Distributed Programming Paradigm (see below).
