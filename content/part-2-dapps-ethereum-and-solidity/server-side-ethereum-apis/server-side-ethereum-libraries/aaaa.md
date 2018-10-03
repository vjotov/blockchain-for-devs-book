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

Get the balance of the address.

    wallet.getBalance().then(console.log);
    
With next 

    let walle;



With next 

    let walle;



With next

    let walle;



With next  .

    let walle;



With next  .

    let walle;

 




