# WorkChains



WorkChains in Ever Kernel v1.0 are not supported apart from the basic (0) workchain while they are fully supported in the Ever OS Kernel. Many rules and messaging protocols to support direct interaction between Workchains were added.

One should remember that all Validators of a WorkChain store all the data of that WorkChain exchanging all the blocks produced within such a Workchain and making it a Shard in a strict database design definition.

WorkChains could be viewed as distributed processor cores or even as distributed peripheral functionality. They can have different functionality, but they share the same block and consensus structures. Some WorkChains will simply scale the number of accounts out of the practical limitation of a single WorkChain to process data related to a certain number of addresses (let’s call them “processing WorkChains”). Others will support additional functionality, such as DriveChain for persistent storage, or IceChain for long term archives as will be explained in some details later, and so on (let’s call them “peripheral WorkChains”).

Processing WorkChains are created dynamically at the time of the elections if the total  capacity of all current processing WorkChains are utilized by about  90%, and some other parameters are met. When added, the Processing WorkChain starts operating once validators from a dynamic validator set are allocated to this workchain and synchronized. The address space of such a WorkChain is a division of the address space of the latest available Processing WorkChain, similar to the thread address split/merge mechanism.

Peripheral WorkChains are added by the decision of the Network Governance.&#x20;

The validator set with the same capabilities is assigned to a new WorkChain during the elections (or, more precisely, during the D’Elector contract execution, see below).

Other types of WorkChains could be theoretically imagined, but the rules of a  block commitment into MasterChain should be followed. Theoretically, one can also imagine  that another blockchain could be added to Ever OS as a workchain if validators of that blockchain decide to convert the block into a necessary structure and post capabilities required for such a blockchain. In effect, it will turn such a WorkChain into a decentralized bridge to that other network. For instance, to add Ethereum 2.0 network as Everscale WorkChain, the stated capabilities should include a certain Ethereum client for EVM and ETH 2.0 protocol processing, the ability to wrap Ethereum blocks into Everscale block structure and proof that such Validator is also a validator in Ethereum. Those WorkChain validators will of course deposit their stakes into the D'Elector contracts and produce the same Everscale consensus guarantees for the Ethereum network while completely disregarding that network's own security assumptions, making it in a way even more secure (as both would run in parallel).

There are many ways to submit such transactions on the Ethereum side. For example this workchain validators could form some Layer 2 solution for Ethereum, designs of which are discussed in the Ethereum community at length and are not in the scope of this paper.&#x20;

Gas would be paid for transactions within such WorkChain in Everscale native currency, while EVM transactions would be paid in Ether. Yet, nothing may stop these WorkChain validators from supporting transactions within their WorkChain, which will, for example, execute a conversion of Ethereum native currency to Everscale native currency, or vice versa, provide proof of blocks, transactions etc. The number of validators and their stakes will therefore guarantee that WorkChain is correct.

Another difference between Processing and Peripheral Workchains is their address space. The peripheral WorkChains may have special address prefixes while Processing Workchains share the same address space.

One of the hardest problems in the multi-sharded approach has been inter-shard communications. If our system is heterogeneous, then we can assume it may not need any specific guarantees with respect to the messages that one such shard sends to another. Yet, it almost certainly creates quite an awful user and developer experience. That would be like adding a horizontal layered approach to the vertical layered approach discussed above. The more layers in which a developer application resides , the more difficult it is to use.

Of course, it is immensely more difficult to design a homogeneous system. In a truly homogeneous system we want to abstract interaction of different system components between each other and the user. So for a smart contract in one thread of a particular WorkChain, it won’t make any difference sending messages to another smart contract, no matter which thread or WorkChain it resides in.&#x20;

There are two situations when a contract is sending a message to another contract: (i) when the contract knows the exact address of such contract and (ii) when it does not, in which case it will calculate the address (see “Distributed Programming”).

When a contract sends a message to a Peripheral Workchain, it must know the destination address and a prefix of such a WorkChain, which is as logical as sending a document from an editing program to a printer for instance.

When a contract emits an internal message to another address, and if this address is in another WorkChain, the internal message will be converted into REMP message and sent externally (see REMP below). Such messages are sent to the corresponding WorkChain’s thread validators and placed in a "message queue catchain" (MQC), which is part of the REMP protocol. But in addition to regular external messages, if the external message originated in another WorkChain, it has a special status of “internal-external” message (IEM), to which a proof of such a message being part of the particular WorkChain block is added. Such messages are then added to the destination’s WorkChain thread block just as any internal message of that WorkChain would be.
