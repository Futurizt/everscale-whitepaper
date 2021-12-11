# Pipes

In Unix Pipe (or Pipeline) are some processes chained together, so that the output text of such a process (stdout) is passed directly as input (stdin) to the next one. The concept has two reincarnations in Ever OS.&#x20;

Smart contracts that pass messages between each other, a design sometimes called “composability”, are actually a pipeline. Everscale composability is built in because of its asynchronous nature, mandatory delivery of messages in a particular order and the nature of all addresses having a smart contract code associated with them.&#x20;

But there are also pipelines in DeBots, so users can create DeBots as a single scenario that could be activated and finished possibly without any user interaction. We call this type of DeBot scenarios — Pipes.

Using Pipes, third-party applications can call DeBots as services in a non-interactive mode (or in semi-interactive mode) and receive responses as a result.

This allows users to compact the DeBot interaction into a single action (like tapping on a button or double clicking). Now applications can draw a custom UI, collect inputs from the user and then run DeBot's certain scenario: read blockchain data, send on-chain transactions and so on - and receive answers.

DeBot Browser can run as a standalone instance without UI components. Browser should isolate DeBot communication with the user and automatically insert necessary inputs for DeBots using the DeBot Pipe. DeBot Pipe defines which function to call to start DeBot (by default, it is the start function without arguments) and what values should be passed to DeBot on each interface call or approve request.
