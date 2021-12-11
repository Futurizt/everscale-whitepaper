# Improved Finality



In practice, the collated block that has been broadcast and that is correct can be considered final because the collator and the validator of the thread will have too much to lose. And since the block broadcast to all full nodes in the network, any party that would run a full node and collect a block from collator while himself an honest participant could himself validate that block and consider it final, simply because the fact that their full node has received the block proves that the block indeed has been broadcast.&#x20;

It will be a little harder for a light client to verify that the full node owner did not collude with a collator, it should either wait for a masterblock or collect some number of verifiers ACKs.
