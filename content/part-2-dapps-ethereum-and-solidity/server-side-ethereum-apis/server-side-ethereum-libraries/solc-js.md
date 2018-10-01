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


## Web3.js
Web3.js is a library that interacts with the ethereum nodes. 
It can be installed with node package manager. 

      npm install -g web3

This is how we can create an instance of web3 and define the provider.  

      let Web3 = require('web3');

      let web3 = new Web3("http://localhost:8545");

If we provide the provider only with the URL it defaults to HTTP provider. If the user wants, for example, WebSocket provider he needs to declare it in the constructor of the web3 object instance.

In web3 we have a large variety of methods. The web3-eth package allows you to interact with an Ethereum blockchain and Ethereum smart contracts.
This are examples of some basic methods. With first of them we can get the coinbase address to which mining rewards will go. In the second example we will get balance for the given address.

      web3.eth.getCoinbase().then(console.log)
      
      web3.eth.getBalance("0xc0bd7545d126d14c39e5f2a28744bac2641b94bc").then(console.log)

## Installing Web3 in Windows

For Windows we need to install first **Windows build tools**, then configure a target and then install the "web3" package. 















