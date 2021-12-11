# Resolving

To resolve the Name, any User can now call the Get method “Resolve” of a Root locally to obtain an Address. Root will use the Certificate Code, Root PubKey, insert a name the User wishes to resolve into the Certificate Code and calculate the address.&#x20;

A user application can cache the Certificate Code smart contract and Root PubKey once, after which resolving any name is achieved locally with a simple address calculation, with no need for network connection at all, therefore making it the fastest certification system in the world.

Knowing a Certificate Code hash enables retrieving all smart contracts having the same hash by simply querying the blockchain state. Decoding contract data will produce a full list of names under a specific Root. It would be quite easy to produce a table with all the certificate records.

The Certificate itself contains variable types of addresses of target smart contracts to which the Certificate owner wishes the name to point. A user should choose which type of address they wish to use.
