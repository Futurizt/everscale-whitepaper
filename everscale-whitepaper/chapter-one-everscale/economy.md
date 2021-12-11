# Economy



Our target is to create an economy for the operating system whose main distinguishing asset is its malleability.&#x20;

As some of you may know Nasim Taleb did not invent antifragile. It was  Andrei Tarkovsky’s invention, as he put it in “Stalker”: "Weakness is a great thing, and strength is nothing. When a man is just born, he is weak and flexible. When he dies, he is hard and insensitive. When a tree is growing, it's tender and pliant. But when it's dry and hard, it dies. Hardness and strength are death's companions. Pliancy and weakness are expressions of the freshness of being. Because what has hardened will never win.”  We believe “malleability” is a good term to replace “antifragile”.

If the Governance token is a unit of account of certain rights within a particular decentralized project then the economic system becomes malleable. Of course, if the Governance token loses its value all the time, less people will be inclined to hold such a  token. Therefore, the token itself should be a store of value, which contradicts its other use - as money.&#x20;

The reasons for that are discussed in “EVER and NEVER Binary system” paper:

“According to the current economic teachings, money has three main characteristics: medium of exchange, unit of account, and store of value. This definition may have been correct 100 years ago. Today it is nothing but a lie.”

“In fact it would probably be correct to say that the money in the modern economy must gradually lose its value in order to be an attractive medium of exchange. Quite simply when a person holds on to something that loses its value over time, it will most likely try to exchange it with something more valuable. Such a person would not hesitate going to a shop and buying not only things they dearly need, such as pizza, but also things they do not need so much, such as entertainment, or things they don’t need at all, such as a new phone.”

From a pure practical perspective, therefore, if EVERis a value capturing token, another native token should be created as an integral part of Everscale that would be used for money transactions and that would lose value while EVER would gain. As mentioned above such a token is NEVER. Some part of the EVER supply should be used as a NEVERstability fund as proposed in the “EVER and NEVER Binary system” paper and as will be described below.

Since  EVER token is not money, it should not be used for network usage fee payments, or such fees will constantly diminish. In order to achieve that, the dynamic gas price should be introduced, but unlike in other blockchains, it should not be set forward by network validators. In general, letting validators decide on transaction inclusion, order and price, has been one of the worst ideas of our time.

Yet, the price for gas should not be too low, or better, should not be arbitrarily low, by reason of spam prevention. Imagine: if the network fees are too low and the network has an upward capacity limit, it is quite simple to calculate how much money one would need to pay to buy out 100% of such network capacity for X amount of time in the form of shilling (or penny) attack. If the price is very low, the network will constantly be out of gas.

Thus, let’s have a dynamic network price function derived from the number of transactions as a percentage of current perceived network capacity and some starting gas price which could be calculated from a perceived cost of running a validator node necessary to run Ever OS, multiplied by the number of such validators necessary to run current Ever Kernel configuration. As will be discussed later, Everscale is almost infinitely scalable, which makes things easier in terms of gas payments, but still in order for it to scale more validators need to join, therefore gas prices should reflect the growing need to attract new validators. The transaction price should start from almost zero and once it reaches the capacity of a Processing WorkChain (see WorkChains) the total price should accommodate the launch of a new WorkChain with a minimum set of Validators. Moreover the premium of the gas price increase should not be paid to current validators, but should be returned to the Validator Giver in order to accommodate the start of a new workchain.\


Let X-axis be the workchain capacity fullness, let Y-axis be the gas price.&#x20;

Let the initial price “a” be very close to 0.

Let's choose a simple power function so that the area under the graph is equal to 1.

Let f(x) = a + b \* x^n

Then the integral of this function from 0 to 1 is equal to a + b / (n + 1) = 1&#x20;

Neglecting the small value of "a" can put b = n + 1

Then f(x) = a+x^n\*(n+1)

\


&#x20;

![](https://lh4.googleusercontent.com/q75gIaLA3pmV3\_jyTwkNyJTvuUiOEUgkRAGdETq5zQaJsx7wIbCUAxexoblKzODB3UooRug9Aq8jZr00xvoJvcN-DzmQIWT-wrfGmtHKRlY7J-7Q4l04mG3OrwaFfJnpK0ZhRk9R)

\


The higher the degree, the more “sharp” the function. At point 1, the function takes on the value (a + b) \~ b

Another aspect that needs to be discussed is a payment for empty blocks. After all, without such payments invented by Bitcoin, there would be no cryptocurrency. In the light of this, we believe there should be no emission of new EVER.

All EVER s were organized at launch into three accounts we call “Givers”:  Validator, Developer and Governance Givers. The tokens from these Givers are distributed through the MTD mechanism by the community.&#x20;

The Validator Giver should pay for every block validators produce (1T for shardblock and 1.7T for Masterblock, changeable only by the community decision if necessary). The total supply of tokens should be kept to around 2 bln EVERs. No new tokens should ever be issued. When Validator Giver runs out of tokens, presumably there will be no empty blocks.

Following the malleability principle, the economic system of Everscale should accommodate for other forms of token distribution or public funding as the community would see fit from time to time. The new givers would be formed, funds would go to support experiments in funding models. It is our firm belief that the guiding principle to all these experiments, though, should be that no funds are distributed to a project without an entrepreneur behind it having vested interest in it and risk associated with it.

\###

While trustless gold can decentralize central banks and trustless applications can decentralize finance, only a trustless operating system can decentralize the economy and get rid of monopoly altogether.

By monopoly we mean control over any market by a single entity. In economic theory the monopoly is always referred to in a negative connotation because it destroys the open market competition, which, in turn, affects the price and motivation system behind free market economy thus greatly diminishing progress. In most modern economies monopolies are prohibited by law. Yet, the fight against them is spotty and ineffective as almost everything governments usually do precisely because any government is a monopoly by itself. Sometimes they execute monopoly power over just a few aspects such as the use of force, and sometimes they monopolize almost everything. Therefore let's assume there is no difference between government monopoly and enterprise monopoly, as they all are equally bad. Bottom line is, there is no effective mechanism to fight against monopoly in a modern society.

Cryptocurrency can solve that problem. First of all, it is almost impossible to purchase another project in a decentralized world because of a potential fork. The power of decentralized applications runs in the immutability of its system software, yet at the same time in the free and open nature of its source code. Governance tokens, unlike shares in a company, give very little control over the project software, management or operations. Such decisions as projects merge can be done in a friendly manner by simply transferring the talent from one team to another, but nobody in this case would prevent a project from being picked up by another team, continued by its community or simply forked. That changes an economic reality completely, rendering all asset holders protection agencies unnecessary in the future when blockchain technology and cryptocurrency will dominantly empower the world economy.&#x20;

Technically, though, in order to achieve that future, a design should propose a truly decentralized, distributed, secure, sustainable, scalable, low latency world computer, together with an operating system.

This paper discusses the design of such a system from three perspectives:  technical, governance and economic. Because of the sheer volume of the topics to cover, it should be viewed as a framework of ideas and design blueprints to be further discussed in separate documents, some of which are already available (links to them will be provided throughout the paper), and some are still under development.
