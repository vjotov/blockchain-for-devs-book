# Code coverage
Code coverage is testing determining how much code is being tested, with code coverage you can see how well your unit tests exercise your codebase. The library that we will use is **istanbul.js** 

We need a truffle project to use `solidity-coverage`, create a new project.
```
truffle init
```
After that we need to make **npm** package and install `solidity-coverage`. We can initialize new **npm** package with
```
npm init -y
```
The **-y** flag will skip questions like **What is the name of your package, version, github url etc. etc.**

Now let's write contract and test it after that. The contract that we will use is `SimpleStorage` which we have used before.
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
Create a new file in the test directory
```js
const SimpleStorage = artifacts.require('SimpleStorage')

contract('Simple Storage contract', (accounts) => {
    let contract; // empty variable for our instance

    it('Should set X correctly', async () => {
	contract = await SimpleStorage.deployed()
	contract.set(4, { from: accounts[0] })
	let result = await contract.get()
	assert.equal(result, 4, "Amount was not correct")
    })
})
```

Now let's install `solidity-coverage` and check our coverage score. 
Run
```
npm install --save solidity-coverage
```
Now you have `solidity-coverage` attached in your **cmd** and when we run the command we will see our coverage score.

 