# Mining Rewards

Miners get rewarded for helping secure the network in two ways:

-  **Block subsidy**
- **Transaction fees**

The block subsidy is a special transaction (called **"coinbase[^1]** transaction") that miners get to add **once per block**, with a pre-determined output amount. This is the only transaction that is allowed to not reference any inputs - it essentially creates new coins. In Bitcoin the subsidy started out at **50 BTC**, and is halved every **210,000 blocks**; at the time of writing this book, it's 12.5 BTC. It will go down to zero in the **year 2140**.

The transaction fees are determined by the users, and miners pick what transactions they'll include in a block based on how much they will **profit**. This means there is essentially a "fee market", where users and miners agree on a price based on market principles. Usually miners are looking at **"Satoshis[^2] per byte"**, because there's a limit to how big blocks can be, so accepting a large transaction might mean not having room for several smaller ones.

The end result is that if you want your transaction to be processed faster (or even *at all*), you have to offer an appropriate fee. Most wallets have "fee calculators" that will determine how much to pay automatically, based on whether you want "quick" or "regular" processing.

# Mining Difficulty

In order to keep the block time relatively constant (e.g. 10 minutes in Bitcoin), even when the total hash rate of the miners in the network fluctuates, the requirements for which block hashes are considered **"acceptable"** can change dynamically. In Bitcoin, every 2016 blocks the timestamps of the blocks are evaluated, and if they're less than 10 minutes apart (on average), the difficulty will **increase**; the hashes will be required to have a **smaller numeric** value than what was required before. Conversely, if they are more than 10 minutes apart, the difficulty will be **decreased** - the "limit" will be moved up, so that more possible hashes are acceptable. Here's a graph of Bitcoin's mining difficulty over time:

![](/content/part-1-blockchain-networks-concepts/mining-and-mining-pools/difficulty.png)

Something interesting to note is that there's a correlation between Bitcoin's price and mining difficulty; as Bitcoin increases in value, more miners are attracted to it, thus increasing its **security** (a network with more hash rate is harder to attack).

[^1]: Not related to the coinbase.com exchange of the same name.
[^2]: A Satoshi is the smallest unit of Bitcoin, kind of like cents for US dollars.