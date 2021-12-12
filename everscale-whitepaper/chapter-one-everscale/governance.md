# Governance

Everscale governance is very simple — anyone can upload a proposal for which the community votes with their tokens using the Soft Majority Voting (SMV) mechanism.&#x20;

Soft majority voting is a transparent voting process with advance announcement and clear  deadline. If members don’t have an opinion and/or are reluctant to vote, it is assumed that they are neutral. Instead of making an attempt to force everyone to vote for every decision, SMV essentially allows decisions by those who care.&#x20;

The metric for passing a decision is the difference between % of Yes minus % of No. For example, if 10% of voters said Yes and none said No, then it is assumed the decision is sufficiently supported and there are no objections. At the same time, if all members voted, then a simple majority rule applies: 50%+1 vote for passing a decision. When we connect those two dots on a graph with % of Yes and % of No axes, we get a “soft” simple majority threshold line.&#x20;

For important decisions like amendment of constitutional community documents, we can draw a “soft” super-majority threshold line (see Diagram below). Soft majority voting mechanism is programmed on Everscale via SMV Smart Contract.

![](https://lh3.googleusercontent.com/-j0JOFjtbcxvo1-GLWUUqwAhfxke9Q5Dcr8b8qlD9xHloM3j8PyBedD6OhEyE8t1lUAQFejI3sUBxn7u5ObsAuHtlyR2FvBnqdxsbVWzJP\_pesYEos9cImqC7WSXB11m1XTXMJGp)

In his work “Moving beyond coin voting governance” Vitalik Buterin identifies vote buying as a major threat to the decentralized on-chain coin voting governance model. It describes at length a possibility of an attack on a governance system by an automated smart contract that auctions voting rights in exchange for some tokens. The SMV protocol is a unique voting mechanism proposed by Pavel Prigolovko, optimized for low participation. It is not a simple token holders voting solution. In fact, by addressing a low participation problem it also has other implications. Remember that in SMV each negative vote increases the decision passing threshold. Therefore the attacker will run into ever increasing cost of vote buying because the honest participants' negative votes have more voting power. In an important decision the attacker may need to buy 75% or more of all tokens for the decision to pass. In effect this is a form of quadratic voting already.

As mentioned above, it is quite a simple system; yet taken in conjunction with the Meritocratic Token Distribution, it becomes a very powerful tool for solving many governance problems.
