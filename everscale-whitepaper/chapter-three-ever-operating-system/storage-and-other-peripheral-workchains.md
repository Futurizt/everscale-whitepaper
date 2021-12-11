# Storage and other Peripheral Workchains



Apart from dynamic memory, which is supported in the form of hashmaps and key-value databases, which Everscale as a whole in fact is, there should be a Permanent Storage for large amounts of raw data. This storage should be accessible by an external user as well as by smart contracts running on EK. It should support common file-system data operations (such as read and write) as well as metadata operations (such as create file and lookup).

There are many known problem of distributed storage architectures: as per CAP Theorem, we either store the data on every node of our consensus therefore ensuring availability and partition tolerance (the system continues to operate despite an arbitrary number of messages being dropped (or delayed) or we start to optimise for consistency (every read receives the most recent write or an error) thus trying to reduce the number of nodes holding the stored data, reducing therefore partition tolerance and availability as with smaller amount of nodes there is much larger chance for them being off line or corrupted.

Economically the cost to store a file on a hard drive is constantly decreasing. The most cost validators pay today is for the internet traffic. Therefore it is the partitioning tolerance that costs the most. The more validators relocate the data — the more it costs.

Ultimately the cheapest way to store a file would be to contract a particular validator and store it on their hard drive once. Of course this will be at the same time the least secure option.

The problem is, when we talk about decentralized storage we are not just talking about some consensus over a stored data ensuring censorship resistance and safety. We also need to be sure the data is actually being transmitted to its consumer whenever requested.

A protocol is needed to ensure that the data is stored continuously for an agreed upon period of time, that this data is protected from attacks on its integrity, that it is private, that it is censorship resistance, that it is verifiably retrievable and that the incentives of network participants aligned with their goals of storing and retrieving the data.

Let's imagine a Workchain where shards are not rotating (or rotating very slowly to avoid collusion of validators using a limited number of storage devices), i.e. having the same set of validators more or less. This Workchain would be optimised for storage. Let's call it a "DriveChain" (will discuss other types of storage such as "IceChain" for cold storage later).

DriveChain will execute a Everscale Virtual Machine with some additional set of instructions related to storage. Such instructions will be: Write Init, Write Receipt, Read and Delete.

The Nodes which would like to join DriveChain as Validators will state their capabilities in terms of disk space they would contribute to the network. The D'Elector contract of the DriveChain will "mount" the Validator into a particular shard (in which case the shard would be more appropriate to call "a Drive" or \`\`DeDrive). If a validator has fallen out of sync, it must signal this to the DriveChain D'Elector contract. If more than 10% of the validators are out of sync, the D'Elector should start adding validators to the DeDrive.

In order to make sure that the validators are committing the disk space, files consisting of pseudo random bits would be written into the disk space to fill all the committed space. Once the real file arrives for a particular account to be stored, the file would be created which will replace random files.

As usual the DeDrive validators will produce blocks periodically. The blocks would be added to the global DriveChain state exactly like they are in any other Workchain following the multithreaded approach. Therefore the blockchain data associated with DriveChain will be the same across all the DeDrive Validators, only the Storage data, which is located on DeDrive Validators hard drives, will be sharded.

The File is written into the validator's hard drives by chunks of some length defined in the DriveChain config. Validators will construct an Extended Merkle Grid of all the chunks of a File with SHA-2 hashes of the chunks for the DeDrive Storage and update the root hash in the DeDrive index smart contract (think of it as a directory index).

In each DeDrive block the collator will reveal a File chunk corresponding to a sequence number of a chunk calculated from a pseudo random  hash (RND) of the DeDrive Root, hash of the last masterchain block and a sequence number of a collated block (Rnd mod X, where X is the number of validators in the DeDrive). The validators will validate on their own data (running a checksum verification on the file beforehand) that such a hash of a chunk corresponds to the hash of their chunk and sign the block. This information, including the chunk itself will be written into a MasterChain block. They will Reject the block if data is not corresponding.

Every masterchain block, a random set of Verifiers on all Everscale Workchain will perform a sampling by requesting a chunk corresponding to the data committed to different DriveChain blocks written into the Masterchain block corresponding to a sequence number of a chunk calculated from a signed by that validators private key hash of a masterchain block (RND mod X, where X is the number of validators in the DeDrive)

If the data does not exist or does not match, the validator will be asked to provide additional proofs of different data chunks by a global set of Verifiers.

The sampling will be initiated by the same set of Verifiers used in a SMFT Consensus Protocol. Several Verifiers from each Workchain are chosen to perform the sampling. If the chunk is not available or is corrupted and the validator is not in the D'Elector list of "out of sync" validators, the Verifiers will produce a Blame and if the total amount of Blames reaching 3 additional verification will be initiated by the selected Validators Committee. The blame must include the wrong block provided by the validator as well as all other blocks received by the slasher from the DeDrive. All Verifiers will request the corrupted or unavailable chunk as well as an additional chunk corresponding to the last hash of the MasterChain block and the verifier pubkey.

The 66% of votes of the Validators Committee will decide on the data availability. If the DeDrive validator has failed to produce chunks for less than 10% of requested chunks it will be slashed by 50% of his stake, if more than 10% is detected the 100% of the validator's stake will be slashed.

The slashing amount will go to the Verifiers who detected the slashing conditions in case the Validators Committee acknowledges the failure. If the Validators Committee rejects the failure those Verifiers will lose their stake.

Remember that all validators within the DeDrive will store all the data associated with Accounts of that DeDrive. The only difference with a regular thread would be that instead of storing everything in a database, calling storage instructions of the ESVM will result in a file being written or read from the disk on that Validator machine.

The file that is written into DriveChain has exactly one File index smart contract. When a File is stored on a Validator machine's hard drive, the name of the resulting file will exactly match the File index Address.

In order to give a file a human-readable name, the DriveChain DeNS contract should be used which will point into a File index smart contract.

When a consumer wants to write data it will need to deploy a File index smart contract on the DriveChain. On deploy the smart contract will call the "Write" instruction with the hash of the file the user wants to commit. In return, ESVM (Collator) sends a FileConnector. The User obtains the Connector from the smart contract once deployed and sends a file. The Collator receives the file, and invokes the smart contract with Write Receipt instruction.
