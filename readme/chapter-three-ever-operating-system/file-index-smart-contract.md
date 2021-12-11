# File index smart contract



Below is an example of how to upload a file into a DriveChain.

Let's take a hash of the file and add a contract code to calculate the address. Deploy a File index smart contract with the size and a hash of the file and call its constructor (with the ESVM command WriteInit). The contract generates a special action, WriteInit, which stores the FileConnector. FileConnector contains the collator's ADNL address, expiration time and owner PubKey (to check connection initiator). Once a File index is deployed, the user can send a file to the ADNL address indicated by the FileConnector within an expiration time provided, signed by a PubKey of the File index.

DriveChain ESVM instructions could be called from a smart contract by internal messages. The message is sent to the contract in the DriveChain. It will pay for the execution of a storage operation instruction which includes the storage fees for that file.

Pubkey is necessary to validate the upload client to get rid of spammers who can use the upload credentials. To initiate an upload, the owner should send a message signed with his private key. Collator checks the signature with the pubkey and starts uploading.

To share the data, the owner would need to give corresponding permissions by changing the File index accordingly. In operating systems the file usually has permissions applying to that user. When a user logs into an operating system it checks the permissions this user has on that file. In the case of Ever OS such permissions would be added to the File Index in the form of an address or a PubKey or a DeCert certificate. The Validators won’t transmit the file to an unauthorized party and if they do the Relayer would stop such transmission and slash the shard validator. Of course the validator could just give direct access to that file to some third party, but in that case this would be equivalent to stealing a physical storage device from somebody. Apart from the encryption there is no way to defend against such an attack.&#x20;

#### How the rest of the DeDrive validators get the file

A collator creates a special CreateFile transaction in the file smart contract and attaches the hash of the uploaded file. The contract will count 66% of all validator transactions to validate the file states as available and issue a WriteReceipt transaction. Now everyone knows the file is available. The rest of the validators must download a file in order not to be slashed when verified.\


#### How to Read the File

The Read Instruction will return the hash of the offset the user requested. From this offset the calculation can be made using all validators PubKeys to determine which validators should relay the file to the user. The user will run the same calculation using a validator public key to determine where to connect to get the file. It will open simultaneous connections to all Relayers and send them a signed message with a request for the file. The Relayers will connect with the DeDrive Validators, and send them the user-signed message to receive the file. The Validators will check that the Relayers are chosen relayers, that the message is signed by a user which has permission to read the file and transmit the data.

In order to read the data a user will post some Bond into a smart contract. The user gets the Bond back if it sends the proof that the file has been transmitted to him minus the Read cost. A Relayer will receive 66% of the read reward (the rest goes to the DeDrive Validator) if the data has been transmitted, which the Relayer can easily verify by taking a hash of a chunk which has been relayed and checking if it belongs to the Merkle tree of a storage since the file root hash is stored in its index. If the Data isn't available the Relayer will send a Blame. If there are 66% of blames for that data received the DeDrive Validators will be slashed for not transmitting. If the user gets the file, it sends the proof that would release its bond.

The Relayers reward for a Blame is much less than its reward for successful transmission, but they only get it if the user has sent a proof of the file transmit. Now it seems there is nobody in the system who is incentified not to store, transmit or lie about the data.

One of the first consumers of the DriveChain would be other Workchains which would archive an old state. The D'Elector smart contract will once in a while create a request to store some passed state archives and randomly choose validators who will commit its archives to the DriveChain. The validators who do not successfully upload files will be penalised. The storage costs of the Archives will be paid out from the Validator Giver account. The cost will be offset by reading fees for the archives.&#x20;

The consumer could store any data in the encrypted format. No validator would have the ability to decrypt the data and read it. Relayers will get chunks of data to transmit to the consumer making it de-facto a torrent-like network. There could be a garlic-like protocol implemented on top of Relayers easily as their addresses are ADNL addresses.

In order to give permission to modify or read the file, such permission should be written into the DeFile index smart contract.
