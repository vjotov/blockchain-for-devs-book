# Unit Testing
Truffle uses Mocha testing framework and Chai for assertions. If you are not familiar with Mocha go to https://mochajs.org and read the getting started section, it will help you to understand the tests better. In the test directory add new file. There is no convension, if you want to make it clearer with `test` in the name`SimpleStorageTest.js`.

`const SimpleStorage = artifacts.require('SimpleStorage')`
You can use artifacts to get the contract, same as in the **Migrations** chapter.

```js
contract('Simple Storage contract', (accounts) => {
    // The tests should be here
}
```
In **mocha** we have `describe` and for truffle is modified as `contract`. We can add multiple contracts in one file, but keep it clear and use one file per contract.

Now inside the contract we will write our test cases, the contract is simple and we will check the **set** function and we will compare the result from the **get** function.
