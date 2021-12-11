# Reverse resolution via Index smart contract

A lot of times even the advanced key-value store won’t be enough. For example a user deploys some multisig wallet with several custodians public keys. Now how could that user keep track of all such multisig contracts she deployed? And even more interestingly, how the custodians she has added could keep track of all multisigs they are custodians in.

Let’s deploy an index for each of the multisig owners. Initial data will have an owner account address for which the index is created (which will be used as a pointer to a contract we are looking for) and the code will be an index certificate code plus the custodian public key.&#x20;

Now we only need to know the certificate code (which is public information) to add a public key to collect pointers to all target smart contracts.
