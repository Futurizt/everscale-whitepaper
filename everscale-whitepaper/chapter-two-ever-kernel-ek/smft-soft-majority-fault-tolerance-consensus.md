# SMFT (Soft Majority Fault Tolerance) Consensus



EK has a BFT-based consensus protocol. It has 4 phases (approve, vote, pre-commit and commit) in order to ensure the consensus is reached. Basic assumptions of BFT consensus is that at least ⅔ of all network validators are honest. It means that a collusion of more than ⅓ of validators can result in a network halt. If more than ⅔ of validators are colluded then network corruption can occur.

When a validator detects a non-valid block, it broadcasts a Reject message.&#x20;

One of the problems of any BFT consensus-based network, is that in order to reach a consensus, it has to pass all the protocol phases, which results in network delays because of the number of messages the nodes need to exchange. In the case of Catchain it is n\*log(n) messages where n is the number of nodes in the network.

Thus, any BFT based consensus, while assuming that a communication could be malicious at any given time, is also assuming some large percentage of its participants is honest.&#x20;

First of all, the assumption that the majority of participants in a social construct are honest, does not necessarily mean that they are right. A lot of times it is a minority that is both honest and correct. The more complicated the subject of a decision to be made is, the more chances there will be  groups with different opinions. Therefore, the network Validators consensus should remain in a very simple and limited capacity, and mostly related to technical aspects of network operations. Validators' own stakes should be subject to slashing by non-validators' stakes ( for more on that see DePools).

Second, why is this assumption made at all? What exactly stimulates the majority of network nodes to be honest in the first place? There must be some motivation of network participants to behave one way or another. This motivation lies outside of any particular protocol and relates to the economics of that protocol.

In the Proof-of-Stake network the validator's motivation to approve correct blocks is secured by their fear of losing their stake if they do not. There is no sound ground to believe that a particular percentage of validators should be honest, and why, apart from game theory arguments.&#x20;

“Note that there have been some recent attempts to develop consensus algorithms based on traditional Byzantine fault tolerance theory; however, all such approaches are based on an M-of-N security model, and the concept of “Byzantine fault tolerance” by itself still leaves open the question of which set the N should be sampled from. In most cases, the set used is stakeholders, so we will treat such neo-BFT paradigms as simply being clever subcategories of “proof of stake”.”

Therefore, the whole point of viewing BFT consensus having, say, ⅔ of honest nodes as theoretically secure is misleading at best. And game theory arguments are weak, because they can not prove anything outside of a closed system and to view a blockchain as a closed game system is naive.

Let us assume that there are two coins and a market for them with derivatives and margin trading (of course there are many such markets in existence). It is quite easy to prove that holding a large stake in one network and being able to short another may provide a better incentive which will destroy the security motivation of the latter network validators. Large stake holder may short the other network token using his long position as collateral with margin and pay say half of the premium to any validators who will prove to destroy the second network value. It will be enough to have ⅓ of the stakes of the second network to stop it completely and destroy its token value. Having a large number of network participants helps only in the sense of communication and coordination hurdle such attacks could carry, but as recent examples of coordinate stock market pumps shows — this is by far not a security guarantee.

The problem multiplies when the network is partitioned. If there is a subset of validators which could corrupt a thread, it will, by proxy, reflect on the security of the whole network.

As a general rule if a simple majority of token holders wants the network to continue — nobody should be able to prevent that. It is not currently so in any proof-of-stake networks.

In a BFT consensus algorithm, network participants agree upon a block. In the case of a single chain of blocks (no sharding, no threading) this block agreement is final, unless a fisherman detects a problem in it and blames validators for dishonesty. Remember that fishermen are not a part of the consensus. In fact we can say that fisherman is a representative of all other network participants who are not part of the validator consensus, but who want to secure the network.&#x20;

A fisherman is someone who is motivated to secure the network by a potential reward. Fishermen do not need to be a token holder. Of course fishermen can not guarantee anything because there is no guarantee that fishermen will do anything. There are many more problems with fishermen we discuss in "Practical Byzantine Dynamic Slashing (PBDS)". For the purpose of this discussion what is interesting is that the security of the network relies on a party which does not participate in its "consensus".&#x20;

The notion of Time is critical. It is safe to assume that a block approved and included in the chain even by a single node 10 years ago would most probably be correct, or not, but if nobody cares why is it important? Therefore, the block validity is a function not only of a number of consensus participants but of time. There is simply a threshold function of time/consensus participants that other network participants are ready to accept as an agreement on block finality.

This is similar to Bitcoin transaction subjective finality, where a participant will wait for some number of blocks to be mined on top of the block in question for it to ensure its validity (since each mined block increases the hash power spent, it may be prohibitively expensive to reverse the transactions after a certain number of blocks (usually 6)).&#x20;

What is the problem with such an approach? The finality time. We need to wait 6 Bitcoin blocks (about an hour) or 32 Solana slots (about 13 sec.) for a transaction to be probabilistically secured.

The BFT finality is faster since it takes about \~5 sec. to agree on a block by ⅔ of 100 nodes. But is 100 nodes enough to be considered a decentralized network and is even 5 sec. acceptable?

Theoretically we would like to have a consensus protocol that can produce blocks as fast as 500 ms. and have a sub-second finality, with the security guarantees provided by a large set of nodes, say north of 10,000 assuming just ½+1 are honest. Is that even possible?

Remember that practically speaking  most of the time most of the validators are honest. Indeed it is hard to imagine a network which would constantly pay fishermen success fees. Such a network would halt after several blocks. Occasionally there are bad actors which believe they would defy the protocol and try to corrupt it. But all current protocols all of the time are optimised for the event that is extremely rare.

Let's make a protocol that would come to a consensus using the Soft Majority Voting mechanism with some modifications. Remember that in soft majority voting the consensus is reached after some small number of positive Votes, say 20%, while no single negative vote is received. If at least one negative vote is received, the consensus threshold is increased until the point where the majority threshold is set (51% for simple majority).&#x20;

Of course this will lead to the following problems:

1. If a collator collides with just 20% of the nodes, it will not transmit blocks to other validators of the set, quickly approve the block and send it to masterchain without even a single node being able to send a Reject.
2. The same malicious set can create a message from thin air and write it into that rogue block. The message will be viewed as valid by another shard that will execute it within another smart contract of that shard.
3. Because Everscale is very fast, all those operations will happen in a few seconds time frame (masterblock validation \~4 sec, shard block creation \~3 sec) and that time won’t be enough to stop the attack.
4. In a paradigm of distributed programming, when the smart contract is an object which interacts with other objects asynchronously the chain of interactions between those objects could be very long. Since it is impossible to predict what messages smart contracts will emit before executing them it will be very hard to correct any corruption in a block in the middle of such a transaction chain.&#x20;
5. Once executed, such a transaction could allow attackers to exit with large sums of money using decentralized exchanges and bridges with other networks which could render all the staking security guarantees useless.
6. In which event the fishermen will be too late for the party. The fork of a blockchain (whether in a form of vertical block or just fork) will recover a very insignificant portion of the attacker's reward. The blockchain will suffer catastrophic perception damage. \


Let’s emphasize that the idea that we could correct such an action retrospectively is false. Forks, vertical blocks or any other such mechanism won’t be able to mitigate such a catastrophic event. Therefore the whole security assumption relying on fishermen is wrong. &#x20;

Let also emphasize that guaranteeing a security of a native token in a shard does not provide enough security guarantees as it should also guarantee the smart contract execution correctness on that shard, facing catastrophic consequences if not.\


Let us present a Soft Majority Fault Tolerance protocol (or SMFT for short):



Will leave the Catchain BFT protocol intact as of the leadership selection and consensus phazes. The Thread validators will validate the block as they are now, just with the BFT threshold lowered to say 51% signatures, which will be used for preventing natural forking and  slashing in case of an attack.

In addition, let's have a protocol that samples some random nodes out of the WorkChain Validator set and requires them to validate every block (let’s call them “Verifiers”). The randomness must be calculated after the block candidate has been propagated. The protocol must be non-interactive, succinct and low latency.

Let us concentrate on the block collation phaze, before the consensus, because in order for malicious validators to validate the malicious block it should be collated in the first place. If we prove that the malicious collation will be impractical, it won’t matter how many potentially malicious validators the thread has.

Instead of broadcasting the block that has been already validated, we will ask collator to broadcast the block candidate to all nodes in the WorkChain. If a collator won’t do this, the block header won’t be included into Masterchain and the Collator will be slashed for data withholding.&#x20;

Before we describe how blocks are verified let’s prove that the block has indeed been broadcast. Without such proof the malicious set of actors could siphon the block only to themselves, “mining” the necessary outcome.

Let some validators be defined as Broadcast Protectors  (BPs for short).

When receiving a new block broadcast from the collator, the validators calculate a set of BPs from a hash of the block and list of validators. Say, taking the Workchain Validator Set divided by some number. &#x20;

Validators will send a Block Receipt — a block hash signed by a BLS signature to all BPs. When a BP collects 51% of Receipts it will broadcast a multiplied Receipts and a numbered list of validators it got receipts from. The Validators that are not sending Block Receipts over some period of time or within a particular delay must be slashed.

The MC will verify the broadcast proof message by decrypting the block hash using multiplication of  pubkeys of validators which provided receipts and comparing it with the a collator’s block hash. Passing the check for 51% of validators will finalize the block if no NACK messages have been received so far. Assuming there are 200 neighbors and that there are less than 50% of malicious validators, getting 50%+1 receipt guarantees that there is 2-200 probability for broadcast not to happen.

Now that we proved 51% of validators got the block, let's choose a set of verifiers.&#x20;

In order to do this let’s choose a random number and a secret that only the verifier knows. Let’s then calculate if the validator is a verifier based on those two numbers which would be random and could not be calculated by an outsider.

When receiving the block candidate broadcast, the WorkChain validators will calculate Ω from a thread ID, block candidate sequence number and hash of a masterchain block signed by a verifier private key. Calculate Hv = hash (Ω). Let N be a number of validators in WorkChain, R is a predefined parameter in a workchain’s config. Then T is a multithreading factor equal to \[N/R]. If a remainder of Hv/T division = 0 then the Validator is a Verifier for a thread block.

If the Validator is a Verifier it will verify the block immediately and send the result (ACK or NACK) to all Masterchain Validators and to a certain number of validators in all other Workchains together with the hash of the block candidate and the proof of correct Verifier selection.&#x20;

If a Verifier will not submit either Nack or Ack it should be slashed. In order to accommodate that we could imagine a protocol that would reveal the true verifiers after the block has been finalized. Several such schemes could be imagined where the Verifier will have to calculate its participation from some key that must be revealed in another context. Since all ACKS and NACKS are included in the masterchain block it is available publicly.  The Broadcast protection receipt can include a validator signature that would reveal the key from which the Verifier has been calculated. &#x20;

Now Masterchain validators will need to wait for a thread block signed by 51% of that thread consensus and broadcast proof from at least one of Broadcast Protectors. If no NACK has been received for a certain period of time (which in reality is the broadcast proof creation time), the block header will be included into the Masterchain. If at least 1 NACK message has been received, the Masterchain will issue a special verification procedure.       &#x20;

Since in every round the probability of any particular validator to become a verifier is 1/T, the probabilities for each verifier are discrete.

Malicious validators (M) attack could only be successful if the majority of thread validators are dishonest, none of the honest validators are chosen as Verifier and their message delivery fails. Disregarding the network failure rate the probability of this event was compared with failure of Bitcoin “6 block finality”.

Let’s compare this with a probability of similar attack on Bitcoin for C =4, R = 15, N = 900

![](https://lh5.googleusercontent.com/zMfreijDN0xkphMHqVeWXbSTMw-UovMHTC88dLd4skofNoeF7imfkViYlVaK8TQftCLEFdSFvB5dSXM0ZVXZ6D0kEEW6a6pi8xcgvyC5-XRj\_Hum3JmJF1fBQqj4O-7QfkkHEu2\_)

We have proved that by having a mechanism of block verification by a random validator set from a global set we can decrease the threshold of the consensus validation in the thread (effectively to zero), reducing the amount of time necessary for block finality while simultaneously greatly improving the thread security. Applying the correct economics to that model we have also proved that it will be completely impractical to corrupt any block data.

We can also prove that by reducing the BFT assumptions in the thread we mitigate most attacks on that consensus. In BFT consensus if the thread validators could not come to the consensus regarding the block, i.e. more than ⅓ of its validators are malicious, they could be easily slashed and excluded from the thread validator set by masterchain validators based on the verifiers' attestations of the collate candidate. Moreover we could extend the use of that mechanism to the Masterchain blocks as well and therefore ensure that even the masterchain could not be attacked by a ⅓ of malicious validators. In fact, the only thing BFT is good at is fast coordination of an execution, providing necessary redundancy.

By proving that only one node could be enough to Reject a malicious block to stop the attack we demonstrate great improvement in security assumptions of proof-of-stake networks making it a more secure network than a proof-of-work.

Question remains, could we make it even more radical and provide a zero probability network security guarantee? What if we add a full node capability of producing Nack messages as in Dynamic Fisherman with one critical difference. In fisherman the proof of a block corruption is supplied post factum, rendering the whole idea practically useless, as we discussed above. Adding the ability of a full node to deliver a Nack message within the block producing delay changes everything. Now we only need to prevent DDOS attacks on both the full node itself or by a full node. In order to do this we can imagine a simple commit reveal scheme with a deposit bond. The full node which wishes to check blocks for validity (lets call it a Watchdog) will create a contract in the Masterchain using some private key and post a bond there. Once a malicious block candidate is detected, such Watchdog will send a Nack message and a bond contract address, signed with the private key of a bond contract holder. Now if proved wrong Masterchain validators would know who to slash and nobody would not know who are the holders of the bond contracts before the Nack is actually received.

Such a mechanism would not be incentified and the fisherman-type incentives are useless because there would be no corrupted blocks detected ever, since the attack will have practically 0 chance of succeeding, as we demonstrated in this chapter. Yet since there are many parties which hold a lot of tokens,  altruistic behaviour is expected in this case as it will guarantee the security of their tokens to be virtually 100%.
