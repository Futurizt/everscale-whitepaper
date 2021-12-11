# Distributed programming



Usually in a blockchain the address is associated with some cryptographic key which means that in order to create a new address one needs to generate a new key pair and calculate the address from its public key. Everscale Address is calculated from initial data and a contract code. Every address in the active (called “initialised”) state has a deployed smart contract code. This code can be the original code from which the address was originally calculated or a different code in which case it means the “setcode” instruction has been used to update the code. If the initial contract code does not have a setcode function in it, the Everscale address will unambiguously correspond to the code. Non-active (called “uninitialised”) addresses can only receive tokens if sent as a message with a special (unbounce) flag. They can not perform any operations.&#x20;

This unique feature of Everscale has several implications. For example a user key can have an infinite number of addresses which depend on the initial data and code of a contract deployed on it. The ability to calculate addresses from the data and the code of the smart contract and then updating these without changing the address, makes the whole Everscale blockchain — an advanced key-value store. The difference with a simple key-value store for example, would be that the address (which is a value in this case) depends on two keys (contract initial data and its code). Each of the keys could be viewed as a separate hash array in terms of the database. That allows the creation of subsets of arrays which would have one unique key. &#x20;

A code associated with a Ever OS address can be verified by another address and therefore be trusted. History of address code mutations including initial data and code that was produced by a known source (cryptographic key or another address) is provided as well (as described in “File system” section).

This web of trust allows a completely new way to program a blockchain application. Now we can fully trust the behaviour of a particular address and therefore assume the immutability of its input and outputs. We can distribute almost any business logic across global ledger entries without a need for any nested data structures. The ERC-20 type of contract becomes obsolete and generally a bad practice. To program a hashmap inside a contract would mean to program a database within a key-value database cell. Sometimes those hashmaps are practical, but only to store some temporary, small structures. Think of it as an application dynamic memory. What one would put in a program memory you may store in a hashmap within a contract, if one would normally use a database to store an object — use the whole Everscale blockchain as a key-value database. If one wants to store large files, it is better to use a DriveChain which acts like a distributed Hard Disk.

Good question to ask when writing a program on Everscale: would this data structure be better placed in a local memory or in a database? If the answer is the former — use a hashmap, later — create an address.

Let's think of a Everscale as a key-value store, where what has been used in address calculation is a key and the address itself is a value. Then if we can find an address by calculating over some keys, we can then retrieve and execute what is within that address.

Great example of this is the Everscale TIP-2 Certificate. Usually to create a record of something on a blockchain one would make a ledger smart contract that would consist of name and an address. Of course as with any other such contract the heavier the use of that service the more complicated such a smart contract becomes, in the end one would need to start thinking about sharding it somehow. And that is not trivial at all, or may be entirely impossible.

In Everscale there is an elegant solution using a distributed programming paradigm:

For example, that is how a decentralized and distributed certificate system is implemented in Everscale. As described in more details below, such a system is used in providing many services which require a certified provable key-value store. For example, a Decentralized Name Service (DeNS) is used as a basic filename and directory structure in the Ever OS filesystem. Other uses include a Proof of Ownership / Prove of Purchase certificate and many others.

Current solutions (for example a Everscale DNS) are either large smart contracts which maintain a full list of records, or a tree-like solution which shards the list based on some parameters. Neither of these solutions are satisfactory due to a lack of scalability, high costs of maintenance, long search time, single point of failure and so on.

Let’s take a look at TIP-2 implementation. Root is a smart contract that contains a Code of Certificate smart contract without data. Root has methods for Certificate Issuance, Certificate Code Retrieval, Root PubKey retrieval and Version history. Each Certificate can become a Root, therefore a Root smart contract and its Certificate smart contract are the same. The Code contains an address of its Root, therefore making it immutable.

When a User wishes to register a certificate, it calls a Certificate Issuance method in Root, sending a Certificate Data (for example an alphanumeric string of a certificate body).

Root takes its Public Key and a Code of Certificate smart contract, inserts a Certificate Data sent by a User, calculates the address of the Certificate and checks if the address already has a Certificate or any other Code deployed by sending a bounced true message calling the “getData” method.

If a contract exists it means that a Certificate with the same Certificate Data already exists. The contract can then return registration information to the Root which will return it to a User. If a contract does not exist the message will bounce to the Root smart contract which would mean the Certificate can be registered.

If a Certificate does not exist, the Root will Issue the Certificate by deploying the Certificate Contract with its Data. On deploy the Certificate will check that it has been deployed from the root address by comparing the address of a Root inside with the deployer address. If there is no match the deploy will fail.

Of course additional business logic steps could be included between the last two steps, such as monetization or other mechanics as shown below in one of the examples.
