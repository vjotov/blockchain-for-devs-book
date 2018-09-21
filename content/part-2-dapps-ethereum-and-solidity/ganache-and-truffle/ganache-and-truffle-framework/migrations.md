# Migrations
Migrations are JavaScript files that help you deploy contracts. These files are responsible for our deployment tasks, and the `Migration.sol` contract will keep a record of them (on the various networks that we have deployed to).

In the `migrations` folder you can find the tasks for deployment. Truffle automatically makes `1_initial_migration.js` when you initialize the project.

When we open the file we will see this code:
```js
var Migrations = artifacts.require("./Migrations.sol");

module.exports = function(deployer) {
  deployer.deploy(Migrations);
};
```
In the first line we are getting an instance of our smart contract's code:

```js
var Migrations = artifacts.require("./Migrations.sol")
```

After that we are deploying the contract with these lines:
```js
module.exports = function(deployer) {
  deployer.deploy(Migrations);
};
```
This is just a simple deployment script - if we need we can create more complex deployment tasks, with parameters, linked libraries, and we can pass the addresses in other contracts that we will deploy as well.

### Let's Migrate a Contract
Let's make it from scratch - first we will write a contract, then we will write a migration for it, and then we will run it. When we finish with this contract, we will write a more advanced migration.

```js
pragma solidity ^0.4.24;

contract SimpleStorage {
    uint storedData;

    function set(uint x) public {
        storedData = x;
    }

    function get() public constant returns (uint) {
        return storedData;
    }
}
```

 Save the contract in the `contracts` folder and make new file in the `migrations` folder. We have a naming convention for the migrations; we have a sequential number (1,2,3...) - this is the order of execution, **1** - will run first, **2** - will run after that etc., then underscore and the name of the script. 
For example, `2_deploy_simple_storage.js`

  ```js
var SimpleStorage = artifacts.require("./SimpleStorage");

module.exports = function(deployer) {
  deployer.deploy(SimpleStorage);
};
```
Now we can **migrate** our contracts. 

```
$ truffle migrate
```
Output:
```
using Network 'development'
Deploying SimpleStorage...
... 0xdaa98dc88755201b99e66213a975542116a2b8a373d89c5a6edd40094a05f52f
Saving successful migration to network...
 ... 0x6e5c6f83b928a01e5b283562bb7b3e6b9142896da0f675912d80668728e289d4
Saving artifacts...
```

Our contracts are deployed to the network and we can see the transactions and find the addresses of the contracts.

### Advanced Migration
Now we will make our migration script more complex. We will deploy the script and after that will set value for the `x` variable.
Open `2_deploy_simple_storage.js` again and change content of the file:
 
```js
var SimpleStorage = artifacts.require("./SimpleStorage");

module.exports = function(deployer) {
  deployer.deploy(SimpleStorage).then( (instance) => {
  	instance.set(4)
  })
};
```
**Note**: you may need to reset your Ganache blockchain, because the `Migrations.sol` will refuse to execute a migration that starts with the number "2" (because it sees it has already done such a migration).

Now we deployed the contract and after that we called a contract method. It is possible to migrate more than one contract:
```js
var SimpleStorage = artifacts.require("./SimpleStorage");
var SecondContract = artifacts.require("./SecondContract");
```
You can deploy in the module exports function:
```js
module.exports = function(deployer) {
  deployer.deploy(SimpleStorage);
  deployer.deploy(SecondContract);
};
```

