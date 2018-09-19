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
		await contract.set(4, { from: accounts[0] })
		let result = await contract.get.call()
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
```
$ solidity coverage
Contract: Simple Storage contract
    √ Should set X correctly (73ms)
    
--------------------|----------|----------|----------|----------|----------------|
File                |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
--------------------|----------|----------|----------|----------|----------------|
 contracts\         |      100 |      100 |      100 |      100 |                |
  SimpleStorage.sol |      100 |      100 |      100 |      100 |                |
--------------------|----------|----------|----------|----------|----------------|
All files           |      100 |      100 |      100 |      100 |                |
--------------------|----------|----------|----------|----------|----------------|
```

 We have 100 percent coverage because we tested every line of our contract, the contract is simple but if you have many complex contracts will be harder. Sometimes is **impossible** to reach 100% code coverage.

Let's make new contract in the contract directory and see what will happen.
SimpleToken.sol
```js
pragma solidity ^0.4.20;

contract SimpleToken {
    /* This creates an array with all balances */
    mapping (address => uint256) public balanceOf;

    /* Initializes contract with initial supply tokens to the creator of the contract */
    constructor(
        uint256 initialSupply
        ) public {
        balanceOf[msg.sender] = initialSupply;              // Give the creator all initial tokens
    }

    /* Send coins */
    function transfer(address _to, uint256 _value) public returns (bool success) {
        require(balanceOf[msg.sender] >= _value);           // Check if the sender has enough
        require(balanceOf[_to] + _value >= balanceOf[_to]); // Check for overflows
        balanceOf[msg.sender] -= _value;                    // Subtract from the sender
        balanceOf[_to] += _value;                           // Add the same to the recipient
        return true;
    }
}

```
Now if we run `solidity-coverage` the coverage will be 50% because we have tests only for one contract of two.
```
--------------------|----------|----------|----------|----------|----------------|
File                |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
--------------------|----------|----------|----------|----------|----------------|
 contracts\         |       50 |      100 |       50 |       50 |                |
  SimpleStorage.sol |      100 |      100 |      100 |      100 |                |
  SimpleToken.sol   |        0 |      100 |        0 |        0 |           7,11 |
--------------------|----------|----------|----------|----------|----------------|
All files           |       50 |      100 |       50 |       50 |                |
--------------------|----------|----------|----------|----------|----------------|
```
Now let's test second contract and reach high coverage.
```js
const SimpleToken = artifacts.require('SimpleToken')

contract('Simple Token contract', (accounts) => {
	let contract; // empty variable for our instance

	it('Should transfer correctly', async () => {
		contract = await SimpleToken.deployed(1000)
		let result = await contract.transfer(accounts[1], 10)
		assert.isNotNull(result.receipt.blockNumber, "Transfer is successfull")
	})
})
```
We tested the transfer function and is the transaction has included in block and the coverage is 100% again.
```
--------------------|----------|----------|----------|----------|----------------|
File                |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
--------------------|----------|----------|----------|----------|----------------|
 contracts\         |      100 |       50 |      100 |      100 |                |
  SimpleStorage.sol |      100 |      100 |      100 |      100 |                |
  SimpleToken.sol   |      100 |       50 |      100 |      100 |                |
--------------------|----------|----------|----------|----------|----------------|
All files           |      100 |       50 |      100 |      100 |                |
--------------------|----------|----------|----------|----------|----------------|
```
The tool generates **html** report in your truffle project in the **coverage** folder. When we open the **index.html** file in the browser we will see the same stats but in the browser.
![](/assets/ganache-truffle-images/code-coverage.png)
