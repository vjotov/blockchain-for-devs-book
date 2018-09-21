# Compiling Contracts
In this chapter, we will write and compile contracts. In our folder structure we can find the `contracts` folder, this is the folder where we can put our code. In that same folder we will also find the `Migrations.sol` contract, which is responsible for tracking the migrations - do not delete it!

Now we will create our first contract, `SimpleStorage.sol`
```js
pragma solidity ^0.4.24;

contract SimpleStorage {
    uint private storedData;
    
    function set(uint x) public {
        storedData = x;
    }
    
    function get() view public returns(uint) {
        return storedData;
    }
}
```

Now we have a contract and we can compile it. The `compile` command will generate everything needed for the deployment in the `build` directory.
```
$ truffle compile
```
Output
```
Compiling .\contracts\SimpleStorage.sol...
Writing artifacts to .\build\contracts
```
In the `build` folder you can find `build/contracts/{contract_name}.json`, this file contains the Application Binary Interface (ABI) and the bytecode of the contract.

### Truffle console
Sometimes it is nice interact with your contracts directly in the terminal. Truffle has two different consoles: 
- **Truffle console**: Basic interactive console that can connect to any Ethereum client. It is useful when you want to import your own wallet, when you are almost ready to deploy your app to the network. 
- **Truffle develop**: For long-term development, does not specify **mnemonic** and accounts. It comes with a local network and you do not need Ganache or other third party software, you have a local blockchain in the terminal.

```
$ truffle console
truffle(development)>
```
Now we are running an interactive console that is connected to the network from our **config** file, so it can be Ganache, Testnet, Mainnet... We have `web3` inside and we can use everything from the **web3** library:
```
truffle(development)> web3.eth.blockNumber
3
```
We asked for the number of the last block. We can deploy and interact with contracts, we will learn more about this in the "Server-Side APIs" chapter. 
```
truffle(development)> web3.eth.getBalance('0xf5b5546761331ba399788c1661708fe693ed61c1').toNumber()
100000000000000000000
```

When you run the **develop** console you will see this output
```
$ truffle develop
Truffle Develop started at http://127.0.0.1:9545/
Accounts:
(0) 0x627306090abab3a6e1400e9345bc60c78a8bef57
(1) 0xf17f52151ebef6c7334fad080c5704d77216b732
(2) 0xc5fdf4076b8f3a5357c5e395ab970b5b54098fef
(3) 0x821aea9a577a9b44299b9c15c88cf3087f3b5544
(4) 0x0d1d4e623d10f9fba5db95830f7d3839406c6af2
(5) 0x2932b7a2355d6fecc4b5c0b6bd44cc31df247a2e
(6) 0x2191ef87e392377ec08e7c08eb105ef5448eced5
(7) 0x0f4f2ac550a1b4e2280d04c21cea7ebd822934b5
(8) 0x6330a553fc93768f612722bb8c2ec78ac90b3bbc
(9) 0x5aeda56215b167893e80b4fe645ba6d5bab767de

Private Keys:
(0) c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3
(1) ae6ae8e5ccbfb04590405997ee2d52d2b330726137b875053c36d94e974d162f
(2) 0dbbe8e4ae425a6d2687f1a7e3ba17bc98c673636790f1b8ad91193c05875ef1
(3) c88b703fb08cbea894b6aeff5a544fb92e78a18e19814cd85da83b71f772aa6c
(4) 388c684f0ba1ef5017716adb5d21a053ea8e90277d0868337519f97bede61418
(5) 659cbb0e2411a44db63778987b1e22153c086a95eb6b18bdf89de078917abc63
(6) 82d052c865f5763aad42add438569276c00d3d88a2d062d36b2bae914d58b8c8
(7) aa3680d5d48a8283413f7a108367c7299ca73f553735860a87b08f39395618b7
(8) 0f62d96d6675f32685bbdb8ac13cda7c23436f63efbb9d07700d8669ff12b7c4
(9) 8d5366123cb560bb606379f90a0bfd4769eecc0557f1b362dcae9012b548b1e5

Mnemonic: candy maple cake sugar pudding cream honey rich smooth crumble sweet treat

⚠️  Important ⚠️  : This mnemonic was created for you by Truffle. It is not secure.
Ensure you do not use it on production blockchains, or else you risk losing funds.
```

So now we have a local Ethereum network which can be used for deploying contracts.
```
truffle(develop)> web3.eth.blockNumber
0
``` 
```
truffle(develop)> web3.eth.getBalance('0x627306090abab3a6e1400e9345bc60c78a8bef57').toNumber()
```

### Play with a contract
We have our `SimpleStorage` contract in the contracts folder and we can play with it with the **truffle console**. The example will work with both versions of the console.
```
truffle(develop)> compile
Compiling .\contracts\Migrations.sol...
Compiling .\contracts\SimpleStorage.sol...
Compiling .\contracts\Token.sol...
Writing artifacts to .\build\contracts
``` 
We compiled the contracts, we use just `compile` instead `truffle compile`, because we are already inside a Truffle console.
```
truffle(develop)> migrate
Using network 'develop'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0x2a988465265ed718f4946de85435208f0d0d8d23097b4891886e0c0663867ba6
  Migrations: 0x9fbda871d559710256a2502a2517b794b482db40
Saving successful migration to network...
  ... 0xd25ff9b6c664ef81d7120ca521d702a0dfec8dc7098262c8bf2bd0613e4b735d
Saving artifacts...
Running migration: 2_deploy_storage.js
  Deploying SimpleStorage...
  ... 0xb6217d7b0c303c3f07dbc443adc59f0cecd73757f44428c1c4631c8efa01c4e4
  SimpleStorage: 0x30753e4a8aad7f8597332e813735def5dd395028
Saving successful migration to network...
  ... 0x46524c6377615bf3314cb2579ccde803dda14c5d3872ade1def68777bd6d1f2c
  ... 0x4cd0ce05a9fd49c10a6eece13acaecb6779236969f53cad26e6ec869ac10122d
Saving artifacts...
```

Now the contracts are deployed we can play with them directly in the terminal:
```
var contract = SimpleStorage.at('0x30753e4a8aad7f8597332e813735def5dd395028')
```
It is a JavaScript terminal and we can use it to call methods and do anything that we can do in JS:
```
truffle(develop) > contract.set(10)
{ tx: '0x5d55c1c602355b843f35b8daea01b819db217faf32ef5592a6c338ceb88cdfbf',
  receipt:
   { transactionHash: '0x5d55c1c602355b843f35b8daea01b819db217faf32ef5592a6c338ceb88cdfbf',
     transactionIndex: 0,
     blockHash: '0xf22c652cafef7d1ea75ac682f49e83d9de99f76a0dc7ef8843fd2e7d79a9bca1',
     blockNumber: 16,
     gasUsed: 26669,
     cumulativeGasUsed: 26669,
     contractAddress: null,
     logs: [],
     status: '0x01',
     logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000' },
  logs: [] }
```
When we want to call the `get` method:
```
truffle(develop)> contract.get()
BigNumber { s: 1, e: 1, c: [ 10 ] }
```

This is how you can test faster with `truffle console`.


