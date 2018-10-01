# Unit Testing
<div class="video-player">
  Watch the video: <a target="_blank" href="https://www.youtube.com/watch?v=Z4mPF1XGZaU">https://www.youtube.com/watch?v=Z4mPF1XGZaU</a>.
</div>
<script src="/assets/js/video.js"></script>

Truffle uses the Mocha testing framework and Chai for assertions. If you are not familiar with Mocha go to https://mochajs.org and read the "Getting Started" section, it will help you to understand the tests better.

In the `test` directory, add new file. There is no convention, if you want you can add `test` to the contract name, e.g. `SimpleStorageTest.js`.

```js
const SimpleStorage = artifacts.require('SimpleStorage')`
```

You can use `artifacts` to get the contract, same as in the **Migrations** chapter.

```js
contract('Simple Storage contract', (accounts) => {
    // The tests should be here
}
```
In **Mocha** we have `describe` and for Truffle it is modified to `contract`. We can add multiple contracts in one file, but keep it clear and use one file per contract. When you run `truffle test` Mocha will loop through all files in the directory and run them.

Now inside the contract we will write our test cases; the contract is simple and we will check the `set` function and we will compare the result from the `get` function.

```js

it('Should set X correctly', () => {
    let contract = await SimpleStorage.deployed()
    contract.set(4, { from: accounts[0] })
    let result = await contract.get()
    assert.equal(result, 4, "Amount was not correct")
})	
```

In the first line we waited for the contract to be deployed:
```js
let contract = await SimpleStorage.deployed()
```
When we have the contract, we can interact with it. We will `set` the variable:
```js
contract.set(4, { from: accounts[0] })
```

After that we can call the getter method and compare the result with assert:
```js
let result = await contract.get()
assert.equal(result, 4, "Amount was not correct")
```

Now we have our first test and we can run it to test if our contract is working correctly. Go to the terminal and run:
```
$ truffle test
Using network 'development'.
Compiling .\contracts\SimpleStorage.sol...

   Contract: Simple Storage contract
      √ Should set X correctly
  
  1 passing (78ms)
```
If you have similar output, everything is working correctly.

### Test Token Contract
Now we will make a simple token contract and we will test it.
The contract will have a mapping of balances and method which returns the balance of the sender.

```js
pragma solidity ^0.4.24;

contract Token {
    address owner;
    mapping (address => uint) balances;
    
    constructor(uint256 totalSupply) public {
        owner = msg.sender;   
        balances[owner] = totalSupply;
    }
    
    function getBalance() public view returns(uint256){
        return balances[msg.sender];
    }
}
```
When we have the contract we can write the tests for it. Create a new file `TokenTest.js` file for the tests: 

```js
const Token = artifacts.require('Token')

contract('Token contract', (accounts) => {

    beforeEach(async function () {
	    token = await Token.new(1000);
	})
	
	it('should start with a totalSupply of 1000', async () => {
        let balance = await token.getBalance()
		assert.equal(balance.toNumber(), 1000 , "The totalSupply is different")
	})
})
```
We are deploying the contract with **1000** for the total supply **before each test** and after that checking the balance.
```
$ truffle test
```
Output 
```
Using network 'development'.
    Contract: Simple Storage contract
       √ Should set X correctly (66ms)
    Contract: Token contract
       √ should start with a totalSupply of 0
       
   2 passing (199ms)
```
## Time Travel
Sometimes testing your contract can be a big challenge. Sometimes you need to check what will happen after **100** blocks or **10 minutes** and it is tricky to do that. For example, if you want to check the expiration of a crowdfunding campaign, or burn some tokens. Time travel is not available in Ethereum Mainnet and all Testnet networks; you should use **Ganache** to test it.

The functions that can help us are `evm_increaseTime` and `evm_mine`. These functions can be triggered with a normal transaction. 

With **evm_increaseTime** you are increasing the time, but in older versions of Ganache this might not take effect immediately.

```js
web3.currentProvider.send({
     jsonrpc: "2.0",
     method: "evm_increaseTime",
     params: [600],
     id: 123
 })
```
You can use **evm_mine** to force the time increase to take effect (if you're on one of these older versions):
```js
web3.currentProvider.send({
     jsonrpc: "2.0",
     method: "evm_mine",
     id: 123
 })
```
Let's create a folder with name `helpers` and create a file named `timeTravelHelper.js`.
```js
const timeTravel = function (time) {
  return new Promise((resolve, reject) => {
    web3.currentProvider.sendAsync({
      jsonrpc: "2.0",
      method: "evm_increaseTime",
      params: [time], // 86400 is num seconds in day
      id: new Date().getTime()
    }, (err, result) => {
      if(err){ return reject(err) }
      return resolve(result)
    });
  })
}

const mine = function () {
  return new Promise((resolve, reject) => {
    web3.currentProvider.sendAsync({
      jsonrpc: "2.0",
      method: "evm_mine",
      params: [], // 86400 is num seconds in day
      id: new Date().getTime()
    }, (err, result) => {
      if(err){ return reject(err) }
      return resolve(result)
    });
  })
}

module.exports = {
    timeTravel,
    mine
}
```
With these functions we can test what will happen in the network after some time. Now let's try it - create a file in the `test` folder named `testTimeTravel.js`:

```js
const helper = require('../helpers/timeTravelHelper.js')

describe("Testing helper functions", () => {
	it("Should advance the blockchain forward a block", async () => {
		const originalBlockHash = web3.eth.getBlock('latest').hash
		
		await helper.timeTravel(86400)
		await helper.mine()

		let newBlockHash = web3.eth.getBlock('latest').hash
		assert.notEqual(originalBlockHash, newBlockHash)
	})
})
``` 
It is a very simple test, we just compare the hash of the latest block plus the hash of the block tomorrow. 
```js
await helper.timeTravel(86400)
await helper.mine()
```
Here is the magic, we set the time in seconds and after that mine the block. 


## Solidity Tests
We learned how we can use JavaScript tests, now we will learn how to write Solidity tests. The feature that we have with Solidity tests is that we have an isolated environment without the need for **web3**, and we can concentrate on the components of the contract. You do not need to choose between **Solidity** and **JavaScript** you can use the both.

Now we will create our first Solidity test - in the `test` folder create `SimpleStorageTest.sol`; the name needs to end with **Test**:
```js
pragma solidity ^0.4.24;

import "truffle/Assert.sol";
import "truffle/DeployedAddresses.sol";
import "../contracts/SimpleStorage.sol";

contract SimpleStorageTest {

    function testSetValue() public {
	SimpleStorage myContract = SimpleStorage(DeployedAddresses.SimpleStorage());
	myContract.set(4);
	uint256 value = myContract.get();
	Assert.equal(value, 4, "The value is setted correctly");
	}
}
```

In the first lines we imported these libraries:

```js
import "truffle/Assert.sol";
import "truffle/DeployedAddresses.sol";
import "../contracts/SimpleStorage.sol";
```
- **Assert.sol**: Library from Truffle that adds support for assertions.
- **DeployedAddresses.sol**: The addresses of all contracts that are deployed from migrations, you can use it with `DeployedAddresses.<contract name>()`
- **SimpleStorage.sol**: This is the contract that we will test.

After that you need to add the tests. Each method in the contract is a **Test** scenario and the name of the methods should start with **test**; in our case, `testSetValue`:

```js
SimpleStorage myContract = SimpleStorage(DeployedAddresses.SimpleStorage());
```
In this line we are getting instance of the contract that is already deployed.
```js
myContract.set(4);
uint256 value = myContract.get();
```
In this line we make transaction to set value and read the value from the contract.
```js
Assert.equal(value, 4, "The value was set correctly");
```
Finally we are asserting that the returned value is correct.

Let's run the tests and check if everything is working:
```
$ truffle test
Using network 'development'.
Compiling .\contracts\SimpleStorage.sol...
Compiling .\test\SimpleStorageTest.sol...
Compiling truffle/Assert.sol...
Compiling truffle/DeployedAddresses.sol...

 SimpleStorageTest
    √ testSetValue (41ms)

  Contract: Simple Storage contract
    √ Should set X correctly

  Testing helper functions
    √ Should advance the blockchain forward a block (458ms)
    √ should be able to advance time and block together (450ms)

  Contract: Token contract
    √ should start with a totalSupply of 0


  5 passing (2s)
```

