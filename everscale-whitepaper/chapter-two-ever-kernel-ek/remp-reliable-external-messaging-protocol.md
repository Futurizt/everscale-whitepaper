# REMP — Reliable External Messaging Protocol



REMP’s objectives are to guarantee delivery of external messages to a smart contract in one WorkChain from any network participant in a particular order and only once. It is hard to overstate the importance of achieving these objectives.

In EK 1.0 design a full node transmits messages via overlay groups to the validators which then try to apply these messages to a block without any guarantee of delivery. It has five main flaws: the message is delivered slowly, the delivery is not guaranteed, unnecessary traffic is created, the order of messages in the block is arbitrary and messages could be replayed.

The acceptable time of message execution should be measured in milliseconds. If a high frequency of messages are sent the replay is a real issue. Done on the contract level, it complicates code, costs fees and is generally unreliable.

REMP is a protocol that guarantees real-time reliable delivery and execution of messages with built-in replay protection.

Definition: A Network Participant (NP) is any node that has all communication protocols and software needed to access and parse block data, resolve ADNL address of all current and future validators in a shardset, send a p2p message to a Collator and receive an Accept (AR) or Error Receipt (ER) from it.

Message transmission to thread validators: Network Participant should broadcast external message to the current and next validator set of a thread depending on destination contract address.

In order to do so NP should:

1. Calculate an ADNL address for all current and next thread validators (from the latest masterblock available to the NP and max parameter).
2. Send a unicast message to REMP participants, which are calculated as current and future thread validators.
3. Validators should immediately write the corresponding status of that message into “Message Queue Catchain" (MQC) with a timestamp as a 64-bit time\_t integers.
4. Only the collator will send a signed Confirmation to the NP, once it has successfully collated the block. Collators will write the confirmation to the MCQ as well. If there are more than one collator all of them will send such a message. If the block timestamp collated by a Collator is later than the confirmation, the message must be inside that block. If the message has not been included into the Block by the collator which signed the message, the NP can send such message with validator signature into a special smart contract which will slash all validators of a particular thread.
5. Validators will slash the Collator if: it did not include all messages it confirmed (soft slashing), it has included the same message twice (hard slashing)
6. If the block was not collated and another collator has produced it the order of the messages should be as following: all internal messages that were received by the time of the unsuccessful block collation, all external messages received by the time of the block collation, all new internal messages, all new external messages.

The order of the messages within a block time slot is not very important; what is important is reliability of message collation in case they were received, the order of messages between internal and external of the current and next block.

The next set of validators will naturally create a new MQC which will include Next validators of the current thread. Same thing will happen with Split/Merge. Once the new MQC is created the Validators should look at the last masterchain block before the set changed, look at the last shard block that has been written there and compare the untreated external messages in their MQC.

They will move untreated messages in the old MQC into the new MQC once they become validators of that thread.

If a thread is split, both queues should split as well. If it merges with another thread, queues should merge as well.

If the same message arrives more than once it should be discarded by both validator sets on arrival and not inserted into any queue, thus ensuring replay protection. Collator can not collate two external messages which are the same.

Collators should try to apply all external messages to a thread block immediately. At least 30% of the block should be allocated to external messages. There could be more included if the block has empty space or less if there are not enough external messages in the queue.

There are some exceptions to the REMP messages guarantee, for example the ‘now’ ESVM instruction. Since it's dealing with the current real time, the execution of such an instruction could not be guaranteed over some time period, therefore if a REMP message contains such instruction execution the REMP will not be guaranteed (such message sender will have to wait for block finality in the thread and potentially even masterchain. &#x20;

#### DDOS protection

If an NP is sending too many messages that are not accepted, the shard validators will ban such NP for a particular period of time (cooling), they should not try to execute messages from said NP for a period of a ban, yet they should write a message about their decision to ban NP into MQC together with time duration of the ban. They should notify NP about the ban by sending a special Error message to the first 100 messages received from such NP. The Error messages should include the Ban code and time of its expiration.
