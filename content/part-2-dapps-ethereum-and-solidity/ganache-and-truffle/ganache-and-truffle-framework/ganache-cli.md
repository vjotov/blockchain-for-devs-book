# Ganache CLI

Ganache-cli is a node module that you can use if you prefer command-line interface. Ganache-cli is written in JavaScript and distributed as a Node package via **npm**
```
$ npm install -g ganache-cli
```
After successful installation you will have ganache-cli command in your terminal.
```
$ ganache-cli <options>
```
You have a lot of options you can specify before running your ganache-cli. If you type just **ganache-cli** command it will load the default options. You will receive 10 Ethereum addresses, each one will have 100 ethers. You can use this accounts for deploying contracts and send transactions.

```
Available Accounts
==================
(0) 0x32d41bd79892d39625f0dca281f95b1b3489717b (~100 ETH)
(1) 0xd9571b488f8084342e4652a67696ac2d0ca15c46 (~100 ETH)
(2) 0xe0917d5c7238e50689c15ff9b152039fcbe64fd6 (~100 ETH)
(3) 0x8abb2759133c76a7b88d779c054df15871024253 (~100 ETH)
(4) 0xbf264c2d35e4a749b090159d987841f67a8d442b (~100 ETH)
(5) 0xa2011c3e6596cee21c3f82a867e0d1ed530c83b7 (~100 ETH)
(6) 0x4047ed13d73bfd95129faa3688f8245148a0cc0a (~100 ETH)
(7) 0x5910d6c5525f85b21a973967861d6796450e22d4 (~100 ETH)
(8) 0xc7a4a51e736886bc5af0e43a7847ff80a151257f (~100 ETH)
(9) 0xa64f754b8bb3c147954c74f14006341d54104498 (~100 ETH)
```

**Disclaimer: Do not use these accounts on production**

You have the corresponding private keys for them.

```
Private Keys
==================
(0) 0x81cf39b44e3b6ab3c010f2bcea007fdd62aba041b582e842676d47cbb9df17a8
(1) 0x3210bf1b77cd1b829c5c91e6ab9f159897ebd1ff7a9c7704daf942df233bea03
(2) 0xded837e55b13725cd6b471c1c6afcafcba2ad3a0efe50edd5419ac84d46c28a7
(3) 0x10aa63ce66e87e5b078d1316c7f1b55d20d7e207a14d26088a8c4952dab60af8
(4) 0x8d18f9bbc1126903efa4b7474c9cb244a0fee7b74c5c5fc445922fe2b53b7eac
(5) 0xdd10df490397470c9c2f4a7d4e73a1aa3aca912d16728cc717c190a9b48c5821
(6) 0xf875248b879904cbc389932389b3bafd8df86e4f38ab50457abe8539f56d5c9b
(7) 0x8d3d7609b2e44066384d1f1a2a387f1e8b53be05ab0ae9abe616db0cd8edecea
(8) 0x732c9e891a7122af605c4517ca481051105a80e6a414b3c2ace8badf2a39512c
(9) 0x72f21d53a484930d5246a4952b33d5ee6a18dedce80655a7e73c27d1812db67a
```

These accounts are generated from deterministic wallet and you have the mnemonic phrase for unlocking this wallet.

```
HD Wallet
==================
Mnemonic:      pink bonus spoil quality hen crisp pull crime elite debate panther reason
Base HD Path:  m/44'/60'/0'/0/{account_index}
```

Additional information that you will have is the Gas Price, Gas Limit and the URL of the RPC (Remote procedure call)

```
Gas Price
==================
20000000000

Gas Limit
==================
6721975

Listening on 127.0.0.1:8545
```

These settings can be changed from the options parameters.

### Options
You have several settings that you can specify when running a **ganache-cli**.

- **-a** or **--accounts**: Specify the number of the accounts to generate at startup. Default is 10 
- **-e** or **--defaultBalanceEther**: Amount of ether to assign each test account. Default is 100 ethers.
- **-b** or **--blockTime**: Specify the blockTime in seconds for automatic mining. If you do not specify this flag, ganache will instantly mine a new block for every transaction. Using the –blockTime flag is discouraged unless you have tests which require a specific mining interval.
- **-d** or **--determenistic**: Generate determenistic address based on pre-defined mnemonic phrase
- **-m** or **--mnemonic**: Use bip39 mnemonic phrase for generating a PRNG seed, which is in turn used for hierarchical deterministic (HD) account generation.
- **-p** or **--port**: Port number to listen on. Default is 8545.
- **-h** or **--host** or --hostname: Hostname to listen on. Defaults to 127.0.0.1 (defaults to 0.0.0.0 for Docker instances of ganache-cli)
- **-g** or **--gasPrice**: The price of gas in wei. Default is 20000000000
- **-l** or **--gasLimit**: The block gas limit. Default is 0x6691b7

The full list of available flags can be find here https://github.com/trufflesuite/ganache-cli

**Disclaimer: The examples are made with Ganache-cli v6.1.6 (ganache-core: 2.1.5) if you use different version it is possible some difference in the syntax.**







