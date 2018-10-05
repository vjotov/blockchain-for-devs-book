# Solidity Compiler

Solc-js (Solidity Compiler js) is a JavaScript binding for the solidity compiler. It is a JavaScript library that can help us to compile solidity code.  

It can be installed with node package manager. 

      npm install -g solc

To deploy and interact with a smart contract we need a **ABI definition** and **bycode**. We can get them by compile contract using command **solcjs** and as a parameters we will use what we would like to be generated. For example if we use solidity file **SimpleStorage.sol** the command will be:
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

This command will generate **two files**: the **ABI definition** and the **bytecode**. We can require this files in our prokects and use it.
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
Web3.js is a library that interacts with the ethereum nodes. There are two versions.  For server side there is version 1.0, it is very heavy for the browser. When you use MetaMask you use Web3 JavaScript app API 0.20 it can be changed.

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

**Ethers.js** is a Feature-Complete library for Ethereum applications in JavaScript. It is a web3 alternative. Web3 is developed with ethereum developers, where the Ethers.js is developed from the community. It is very easy to use and very intuitive. Ethers.js has a very good documentation:  [https://docs.ethers.io/ethers.js/html/](https://docs.ethers.io/ethers.js/html/). 
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
    
To **deploy a contract** with **ethers.js** we must include **0x** in the begining of the bytecode (let bytecode = "**0x**6060060c57fe5b60405161012d3803…") but the solidity compiler don't put this automaticaly so if we just copy the bytecode it won't be deployed. 
To **deploy a transaction** we use **ethers.Contract.getDeployTransaction(bytecode, abi)**. This construct our raw transaction. Then we use the wallet module to send transaction **wallet.sendTransaction(deployTransaction)**. The code here is much cleaner and much readable then web3 library. 



    let bytecode = "0x6060060c57fe5b60405161012d3803…";
    let abi = [{"constant":false,"inputs"…];
    let deployTransaction = ethers.Contract.getDeployTransaction(bytecode, abi);
    wallet.sendTransaction(deployTransaction);



TODO: Live demo: Interact with Contracts
To deploy a transaction.

    let walle;



With next

    let walle;



With next  .

    let walle;



With next  .

    let walle;

## Nethereum
**Nethereum** is a .NET integration library for Ethereum. It simplifying the access and smart contract interaction with Ethereum nodes.
We can get the Nethereum libraryes via NuGetPackages. In Nethereum we have a differente modules. For example:

Nethereum.Contracts is a module that interacts with the smart contracts. 

    Nethereum.Contracts

For the web we have another NuGet package Nethereum.Web3.

    Nethereum.Web3


We can **create account** from **private key**. We just **create new Account object** with passing the **private ke**y in the **constructor**.

    var account = new Account("0x688…");
 

We can create an instance of **web3** using **HTTP provider**. 

    var web3 = new Web3(account, provider);

To **create an instance** of an **existing contract** we need **abi definition** and **contract's address**.

    var abi = "[{\"constant\":false,…]";
    var contractAddress = "0x356E7677971C952bAe7...";
    var contract = web3.Eth.GetContract(abi, contractAddress);


If we want to send transaction. We need to **get the function** from the contract and then use it. 

    var setFunction = contract.GetFunction("set");
    setFunction.SendTransactionAsync(account.Address, gas, gasPrice, value);



To read from the contract we must initialize the **get function**. Then make asynchronous method and again we should specify the **contract method return type** (in our case **int**) because this is a statically typed language.

    var getFunction = contract.GetFunction("get");
    var value = getFunction.CallAsync<int>().Result;
    Console.WriteLine("Storage value data: " + value)


If we want to **get transaction hash** and **don't wait for it to be mined**. We just have to send asynchronous transaction and use **.ConfigureAwait** method set to **false**. 

    var txHash = setFunction.SendTransactionAsync(…)
    .ConfigureAwait(false).GetAwaiter().GetResult();


If we use this line of code we need to add some other point to check if this transaction has been approved or not. In some cases this would be very useful. *We can just provide the transaction hash for the user to check himselves is his transaction is has passed or not. So if we only need to provide with transaction hash just don't wait for the transaction to be mined, because the user will be just waiting for his transaction hash so he can manually check his transaction himselves in the block explorer. If we want to be sure that the transaction is mined we must just make a synchronous call and wait transaction to be mined. This can be done with Drizzle. Drizzle listen the blockchain for us. *

##Web3j
**Web3j** is **Java** and **Android** library for integration with **Ethereum**. It creates contract **wrappers** from native Java code. 

We have Web3j **command line tools** to generate wrapper code.

    web3j solidity generate Contract.bin Contract.abi –o …

It is advisable to use **Maven** dependency, because it will make the work with web3j more easy. 

    <dependency> 
      <groupId>org.web3j</groupId> 
      <artifactId>core</artifactId> 
      <version>3.4.0</version> 
    </dependency>
    
![](/assets/server-side-ethereum-libraries-web3j-01.png)




We can create an instance of web3 using HTTP provider. In the example below we connect to Ganache CLI on port: 8545.

    Web3j web3 = Web3j.build(new HttpService("http://localhost:8545"));

We have a cretential object which actually is our wallet credentials. With this code we can load credentials by private key. 

    String privateKey = "0x6881c714c323c2f5798568866344…";
    Credentials credentials = Credentials.create(privateKey);

This is how we can deploy a contract. Here we have to specify gas limit, but actually the gas limit can be used from the contract wrapper. 


     ArrayOfFacts contract = ArrayOfFacts.deploy(web3, credentials, ManagedTransaction.GAS_PRICE,      Contract.GAS_LIMIT).send();

Load the Contract from an address. We must paste the address, the web3 provider, the credential, the gas price and the gas limit. *We can get gas limit and gas price by default if we get it from the manage transaction and the contract from the contract object we get the gas limit*. 

    String address = "0x356E7677971C952bAe7...";
    ArrayOfFacts contract = ArrayOfFacts.load(address, web3j, credentials, gasPrice, gasLimit);

Here is how we can write to the contract, wait until is mined. We have a **TransactionReceipt** object which is actually the response. We have a wrapper so we just use the native method of the contract. 

    String fact = "Random fact";
    TransactionReceipt tx = contract.addFact(fact).send();

Reading from a contract. Here again we use the contract method **getFact**. But we must pass bigIntegers as an input. Then we use **.send()**. 

    BigInteger index = new BigInteger("0");
    String fact = contract.getFact(index).send();

TODO: Exercise web3j and Infura.

##Web3.py
Python library for interaction with Ethereum. Web3.py API is derived from Web3.js and in whole the two libraries are very familiar. 
We can install Web3.py package via Python Package Manager **pip**. 

    pip install web3

This is haw we can import web3.py modules in a project.

    from web3 import Web3, HTTPProvider

We can create a new instance of web3 using HTTP provider. 

    Creating an instance of web3 using HTTP provider

This is how we can create an instance of already created smart contract. We need an address and ABI definition. 

    CONTRACT_ADDRESS = '0x356E767797774D9D231C56C94ac76951C952bAe7'
    ABI = '[{"constant":false,"inputs":[{"name":"newFact","type":"string"}],"name":"add","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"constant":true,"inputs":[],"name":"count","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"index","type":"uint256"}],"name":"getFact","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"function"}]'
    contract = web3.eth.contract(CONTRACT_ADDRESS, ABI)

Now if we want to **add a fact** in our contract we must call the function. All functions are stored in a function object, so if we call **contract.functions.add** we can invoke the **add** function. In python it's a bit complicated, so we have a **buildTransaction** method where we need to create a nonce with ourselves. Here we need to construct the transaction ourself which may result in some problems and wasting some more time to debug. Then we need to **signTransaction** and then to **sendRawTransaction** to the network. 

If we want to get facts from the Contract we must use the **.count()** and next **.call()** which is the equivalent of the **.send()** in web3j. 
If we want to invoke **get** methods we use **.call** method, if we want to **set** a value we must to **build a transaction** and send this transaction. 

    count = contract.functions.count().call()

