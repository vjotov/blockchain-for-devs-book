# Truffle Install and Configure

<div class="video-player">
  Watch the video: <a target="_blank" href="https://www.youtube.com/watch?v=9Jf6y6oM1pE">https://www.youtube.com/watch?v=9Jf6y6oM1pE</a>.
</div>
<script src="/assets/js/video.js"></script>


Truffle is built with JavaScript and we can install it with the **npm** package manager:

```
$ npm install -g truffle
```
After that we will have the `truffle` command available in our terminal. To initialize new Truffle project we use the `truffle init` command:
```
$ mkdir myProject
$ cd myProject
$ truffle init
```
Output:
```
Downloading...
Unpacking...
Setting up...
Unbox successfull. Sweet!

Commands:
   Compile:        truffle compile
   Migrate:        truffle migrate
   Test contracts: truffle test
```

Truffle generated for us a basic project with contracts, migrations and tests. The project structure that we now have is: 
```
contracts
migrations
test
truffle.js
truffle-config.js
```
## Configure networks
We have 2 files for our configuration: `truffle.js` and `truffle-config.js`. Both files can be used for configuration. If you are using Windows, when you use `truffle` command you will receive a script error, because Windows tries to run the file. You can use **PowerShell** or delete the `truffle.js` file and use only `truffle-config.js`. In the examples in this chapter we will use **PowerShell** instead of **cmd**.

In the `truffle.js` file we must specify the network, this network will be used for migrating and deploying contracts. If you are developing and you want to test your contracts, use **Ganache**, because the transactions will be executed immediately and you will save time.

```js
module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*" // Match any network id
    }
  }
};
```
Now you can run `truffle migrate` and you will migrate your contracts, currently you have one that comes with Truffle. If everything is OK you will receive `Network up to date`, otherwise you will receive `Error: No network specified. Cannot determine current network.`

You can specify more than one network, which is very helpful because it lets you also deploy to **Mainnet** or other networks.

```js
networks: {
  development: {
    host: "127.0.0.1",
    port: 8545,
    network_id: "*" // match any network
  },
  live: {
    host: "178.25.19.88", // Random IP for example purposes (do not use)
    port: 80,
    network_id: 1,        // Ethereum public network
    // optional config values:
    // gas
    // gasPrice
    // from - default address to use for any transaction Truffle makes during migrations
    // provider - web3 provider instance Truffle should use to talk to the Ethereum network.
    //          - function that returns a web3 provider instance (see below.)
    //          - if specified, host and port are ignored.
  }
}
```
Now we have two networks, we can specify a **gas limit** and a **gas price** and Truffle will use it when making transactions.

When you finish with the development, you can migrate your contracts directly to the Mainnet:
```
$ truffle migrate --network live
``` 
After this command your contracts will be deployed to the Mainnet.

**Disclaimer: The examples are made with Truffle v4.1.14 if you use different version it is possible some difference with the syntax.**






