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
 


