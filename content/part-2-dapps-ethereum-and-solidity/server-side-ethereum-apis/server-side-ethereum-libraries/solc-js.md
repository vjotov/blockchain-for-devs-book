# Solidity Compiler

Solc-js (Solidity Compiler js) is a JavaScript binding for the solidity compiler. 

It can be installed with node package manager. 

      npm install -g solc

We can compile contract using command **solcjs** and as a parameters we will use what we would like to be generated. For example if we use file **SimpleStorage.sol**:
```cs
contract SimpleStorage {
	uint private storedData;
	function set(uint x) public {
	    storedData = x;
	}

	function get() view public returns (uint){
	    return storedData;
	}
}
```


     solcjs SimpleStorage.sol --bin --abi 

This command will generate **two files**: the **ABI definition** and the **bytecode**.
![](/assets/server-side-ethereum-libraries-solc-js-01.png) SimpleStorage.sol
![](/assets/server-side-ethereum-libraries-solc-js-02.png) SimpleStorage_sol_SimpleStorage.abi
![](/assets/server-side-ethereum-libraries-solc-js-03.png) SimpleStorage_sol_SimpleStorage.bin



You can install it as a dev dependency so in the **package.json** it will be only used in the development enviroment. 

```npm install --save-dev solc```


The contract can be compilated in **JavaScript**. We have to define the variable and get the contract code as a string literal. 

`const solc = require('solc');`

```cs
**let** contractStr = `contract SimpleStorage {
   uint private storedData;
   function set(uint x) public { storedData = x;}
   function get() view public returns (uint) {
      return storedData; }
}`;
let output = solc.compile(contractStr);
```

Here we don`t use single quote but **back tilt**. This is becouse of ECMAScript 6 so if you use only single quote it get only the first line of code. In another way we can just read the code from file.

*TODO: Now let`s do the exercise: Playing with Smart Contracts using Ethers.js*

*TODO: Demo Video: try the compilation.*
*TODO: Compile Contract Result*


<div class="video-player">
  Watch the video: <a target="_blank" href="https://youtu.be/_p7EJ2m6iu8">https://youtu.be/_p7EJ2m6iu8</a>.
</div>
<script src="/assets/js/video.js"></script>





# Server-Side Ethereum Libraries
# Web3.js
Web3.js is a library that interacts with the ethereum nodes. 
It can be installed with node package manager. 

      npm install -g web3



## Installing Web3 in Windows

For Windows we need to install first **Windows build tools** for Node.js from 
[https://www.npmjs.com/package/windows-build-tools](https://www.npmjs.com/package/windows-build-tools)

It can be installed with npm. Run as administrator:

      npm install --global --production windows-build-tools



Then, configure the VC++ target.

       set VCTargetsPath=C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\v140



  Finally, install the "web3" package

    npm install -g web3

## Using Web3 API
We can create an instance of web3 using HTTP provider with commands:

       let Web3 = require('web3');
       
       
 This is how we can define the provider.  

      let Web3 = require('web3');

      
      let web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
or
      let web3 = new Web3("http://localhost:8545");



If we provide the provider only with the URL it defaults to HTTP provider. If the user wants, for example, WebSocket provider he needs to declare it in the constructor of the web3 object instance.

In web3 we have a large variety of methods. The web3-eth package allows you to interact with an Ethereum blockchain and Ethereum smart contracts.
This are examples of some basic methods. 
We can get the coinbase address to which mining rewards will go. 

      web3.eth.getCoinbase().then(console.log)  
Here we will get balance for the given address.

     let balance = web3.eth.getBalance("0x407d73d8a49eeb85d32cf465507dd71d507100c1");

List all accounts.

    let accounts = web3.eth.accounts;
    
With web3.eth we can create contract object. We need to paste the ABI. 

    let MyContract = new web3.eth.Contract(abiArray);

And then we can deploy the contract. For this we must create a **transaction** from our account and again we need to paste the bytecode here.

    let contract = MyContract.new({data: '0x12345...', from: myAccount, gas: 4700000});

To invoke functions from existing smart contract, we need to create again contract object (instance of the contract). 
    const contractAddress = '0x987ae6c8837e88dff419ac01a9a41c693ddeda33';
    
   For this purpose we will need the contract address and the ABI definition.

    const contractABI = [{"constant":false,"inputs":[{"name":"hash","type":"string"}],"name":"add","outputs":[{"name":"dateAdded","type":"uint256"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"hash","type":"string"}],"name":"verify","outputs":[{"name":"dateAdded","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"}];



    let contract = new web3.eth.Contract(contractABI, contractAddress);
 
 Then we can invoke functions from the smart contract.
     
     contract.verify(documentHash).call().then(console.log);
 
      
    
   


     
                 

   
  
## Infura API

**Infura** provides a **gateway** to the Ethereum blockchain. Infura is a **third-party web provider**. With it we can signup and get a free JSON RPC endpoint to the Ethereum Mainnet, Ropsten, Kovan, Rinkeby and other networks. 
Instead of running a local Ethereum node, we can just use Infura.io. 
To connect to Infura API we must set the provider. Just use the appropriate URL (in the example we are connecting to the Ropsten network). If we want another network, for example Rinkeby we should type it's name here. The next number (8HIzwWmxZbPPDZmBnth4) is the token that Infura provides us so they can controll the proces. 

    let web3 = new Web3();
    web3.setProvider(new web3.providers.HttpProvider('https://ropsten.infura.io/8HIzwWmxZbPPDZmBnth4'));
   Then we can interact with the blockchain.
    
    web3.eth.getBalance("0x7cB57B5A97eAbe94205C07890BE4c1aD31E486A8").toString();

The Infura's API is free in some way, but you cannot just flood the Infura API with a lot of requests because they will either ban you or they will just charge you. So, for **testing purposes** Infura is very good option. But if you`re going to be using and interacting with the blockchain a lot it will be better to run on your own client and interact with it.


Let`s do the Exercise: Smart Contracts Web3 and Infura
 



## Ethers.js

**Ethers.js** is a Feature-Complete library for Ethereum applications in JavaScript. It is a web3 alternative. Web3 is developed with ethereum developers, where the Ethers.js is developed from the community. It is very easy to use and more intuitive. 
It can be installed with node package manager.

    npm install --save-dev ethers

sdf

    let ethers = require('ethers');


In ethers.js the things are devided into **modules** and each of them take care of something. For example: 
**ethers.Wallet** take care of holding the **keys**, **signing transactions** and everything connected with the wallet features. 
**ethers.providers** manages the **connection to the etherium network**, checking the states and sending the transaction after it is signed by the wallet module. 

Get a provider to an Ethereum blockchain (e.g. Ropsten)

    let ethers = require('ethers');
    let provider = ethers.providers.getDefaultProvider('ropsten');


With this code we can **wait for transaction** to be mined and then just specify in the promise what we would like to be done.

     provider.waitForTransaction(transactionHash).then(transaction => console.log(transaction));


With next code we can **create a wallet** instance for a particular chain. For this purpose we must specify the **provider**.

    let wallet = new ethers.Wallet(privateKey, provider);

When we want to **get the balance** of the wallet it's not like in web3 where we need to pass our address and etc. In **ethers.js** we just type **wallet.getBalance()** because here we have an **instance** of our wallet. 

    wallet.getBalance().then(console.log);
    
To deploy a contract 

    let walle;



With next 

    let walle;



With next

    let walle;



With next  .

    let walle;



With next  .

    let walle;

 




