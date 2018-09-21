# Decentralized Trading Platforms

In this chapter, we'll look at some of the more popular decentralized exchanges. The decentralized exchanges do not rely on a third party service to hold the customer's funds. Instead, trades occur directly between users through an automated process.  Decentralized cryptocurrency exchanges require users to register for an account before they can trade.

Some of this exchanges use proxy tokens that represent a certain fiat or crypto currency. Others use assets that are like shares in a company. Another way to achieve decentralisation is using of a decentralized multi-signature escrow system.

Using decentralized cryptocurrency exchanges brings a lot of benefits. Many decentralized cryptocurrency exchanges are hosted on decentralized servers or existing solely in the cloud. This make decentralized exchanges much harder to hack than traditionally hosted exchanges. Decentralization gives more security to user data and funds. Decentralized cryptocurrency exchanges are much harder to regulate or even shut down by the government. This reduces political risk.

Decentralized exchanges require the registration of a trading account. But unlike traditional exchanges, they require much less information, allowing users to maintain a much more privacy.

When people use centralized exchanges, they lost control over private keys and have only records in exchange database. Decentralized exchanges on the other hand leave ownership of cryptocurrency in the hands of their users and simply act as a place for peer-to-peer trading.

Decentralized exchanges are less used than traditional ones, which is reflected in weaker liquidity. Generally, they are more complex to use and create difficulties for new users. The weak regulation of this type of exchanges is both an advantage and a disadvantage. Very often it is not known who is behind these exchanges and who controls them.

![](/assets/DecentralizedTradingPlatforms.png)

## Stellar

![](/assets/Stellar.png)

Stellar is open-source, distributed payments infrastructure. The Stellar network \(Horizon API and Stellar Core\) is a distributed blockchain based ledger and database that facilitates cross-asset transfers of value, including payments. The native cryptocurrency of Stellar is called Lumens \(XLM\). Stellar has a small testnet open to developers.

Stellar-core is the backbone of the Stellar network. It maintains a local copy of the ledger, communicating and staying in sync with other instances of stellar-core on the network. Optionally, stellar-core can store historical records of the ledger and participate in consensus.

Stellar-core is a replicated state machine that maintains a local copy of a cryptographic ledger and processes transactions against it, in consensus with a set of peers. It implements the Stellar Consensus Protocol, a federated consensus protocol. It is written in C++11 and runs on Linux, OSX and Windows. Learn more by reading the overview document.

Horizon is the client-facing API server for the Stellar ecosystem. It acts as the interface between Stellar Core and applications that want to access the Stellar network. Horizon allows you to submit transactions to the network, check the status of accounts, and subscribe to event streams. For more details, see an overview of the Stellar network.

You can interact directly with Horizon via cURL or a web browser. Stellar.org also provides a JavaScript SDK for clients to use to interact with Horizon.

Stellar can be used to build sophisticated smart contracts.

Stellar smart contracts is much different from Ethereum smart contracts. They are not Turing complete. They are implemented as an agreement between multiple parties and enforced by transactions. A single transaction on the Stellar network costs only ~$0.0000002.

### Stellar Operations

Transactions in Stallar are made up of a list of operations. Each operation is an individual command that mutates the ledger. For example: Create Account has Result: CreateAccountResult.

![](/assets/StellarOperations.png)

### Lumen \(XLM\)

![](/assets/LumenXML.png)

Native asset of the Stellar network is called Lumen \(XLM\). In 2014 the Stellar network launched with 100 billion stellars, the original name of the network’s native asset. In 2015, with the launch of the upgraded network, the name of the native asset changed from stellar to lumen to distinguish it from: first, the Stellar network itself and second, Stellar.org, the nonprofit organization that contributes to development of the network. Lumens are essential to the Stellar network—they contribute to the ability to move money around the world and to conduct transactions between different currencies. Lumen, serves two purposes:

* Lumens play a small anti-spam role. Lumens are needed for transaction fees and minimum balances on accounts on the Stellar network in order to prevent people from overwhelming the network and to aid in prioritization. Each transaction has a minor fee—0.00001 lumens—associated with it. This fee prevents users with malicious intentions from flooding the network \(otherwise known as a DoS attack\). Lumens serve as a security measure that mitigates DoS attacks that attempt to generate large numbers of transactions or consume large amounts of space in the ledger. Similarly, the Stellar network requires all accounts to hold a minimum balance of 0.5 lumens. This requirement incentivizes users to declutter the ledger by eliminating abandoned accounts, thereby that ensuring that all accounts are likely to have economic utility on the network.

* Lumens may facilitate multi-currency transactions. Lumens sometimes facilitate trades between pairs of currencies between which there is not a large direct market, acting as a bridge. This function is possible when there is a liquid market between the lumen and each currency involved.

Lumen supply is determined by fixed, protocol-level rules. Every year, there is a 1% inflation rate. New lumens cannot be generated arbitrarily by anyone.

Interesting fact is that Stellar Lumens \(XLM\) and Ripple \(XRP\) are both founded by Jed McCaleb.

### Stellar Decentralized Exchange \(SDEX\)

Stellar Decentralized Exchange \(SDEX\) is a Stellar\`s project. At the end of 2017 Stellar recruited a team to build a front-end for Stellar’s SDEX. SDEX will enable on-chain, protocol-level trades for any Stellar token. SDEX is the Stellar network per se. 

### StellarTerm

![](/assets/StellarTerm.png)

StellarTerm is different from the SDEX. It is a client or an application that is built on top of SDEX and uses SDEX backend \(the network\) to exchange assets. StellarTerm is an open source client for the Stellar network, developed by Iris Li, a former employee of the Stellar Development Foundation. The project is independent of the Stellar Development Foundation. 



