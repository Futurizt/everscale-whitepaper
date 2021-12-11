# Distributed Dynamic Validator Set (DDVS)



In order to implement MSRP protocol the Election process of the Everscale network must be organised in the following way:

The Election mechanism should be replaced by a DDVS, which is a constantly running Election consensus mechanism with no epochs or elections. Elections in general are bad by design. Apart from putting stress on the network by creating unnecessary heavy iterations over a single ledger. It also makes it difficult to implement dynamic slashing mechanisms and despite the fact that it has been implemented already, we believe a distributed smart contracts implementation of the validator set is essential. Additionally, such a dynamic validator set is needed to allow MSRP.

This works as follows: anyone wishing to become a Validator will deploy a DePool Root Contract at any Workchain they want except for the Masterchain. The contract will have several methods, such as, “accept stake”, "stake lock", "slash" etc.

DePools are a liquid stacking protocol invented in Everscale; it preceded any liquid stacking solutions that later appeared on other networks. Most capital in Everscale is currently staked through DePools. But the first version of the contract had some limitations by design. Let’s talk about the new DePool design and about the new Elector contract design.

The DePool Root Contract is a Root for DePool Wallet contract. Any user can ask a DePool Root to deploy them to a DePool Wallet. Once deployed, this user will be able to deposit their funds into this contract. DePool Wallet can accept the user's funds and then users can choose to Stake their funds with any DePool Root Contract deployed by a specific validator. The user coin never leaves the DePool Wallet, as it will only send a message to the DePool Root Contract that the user has chosen with a confirmation to the stake; if DePool Root accepts the stake it will respond with "Lock" instruction. The Lock period is a discrete constant for each DePool contract. It also includes the set unlock period for each stake to leave the network. &#x20;

Now we have a lot of tokens locked in user DePool Wallets and some DePool Root Contracts which accepted some of the DePool Wallet stake requests and locked their tokens. We need some distributed mechanism to change the Validator Set in the network configs.

Let’s have a copy of the Distributed Elector & Config Contract (D’Elector & Config) sitting in every chain the network has. In fact, let D'Elector & Config be required to start any Everscale chain (whether Masterchain or Workchain). In order to become a validator or add/withdraw stake, the DePool Root Contract will send a corresponding message to the D’Elector & Config contract requesting the change. D’Elector will receive such a message, verify that DePool Root is an authentic contract (see Distributed Programming for more details on how that's done), execute config parameter change and send a corresponding message with the new config to all other D’Elector & Config contracts on the network.&#x20;

Other contracts will vote for a proposed change with the stakes they register. If the proposed change receives more than 50% support, the nodes will execute the configuration change.
