# Frameworks
Truffle works with every JavaScript framework you can use **Vue.js, Angular,React** or other front end framework. 

### Truffle boxes
Truffle boxes are basic boilerplates that can help you with your project. The boxes contain **solidity contracts** and libraries, front-end frameworks and more. Boxes can save you a lot of time with the structure of your **dApp**.You can find full list of truffle boxes here https://truffleframework.com/boxes
You have a boxes for **react**, **vue** and many more.

One of the famous box is **Metacoin**. Metacoin is box that represent simple token, in the box you can find a smart-contract `MetaCoin.sol` and two test files `TestMetacoin.sol` and `metacoin.js`. We can install the project with
```
$ mkdir metacoin
$ cd metacoin
$ truffle unbox metacoin 
```
Output
```
Downloading...
Unpacking...
Setting up...
Unbox successful. Sweet!

Commands:

  Compile contracts: truffle compile
  Migrate contracts: truffle migrate
  Test contracts:    truffle test
```

Truffle generated for us project with this structure
```
+ contracts
  -- ConvertLib.sol
  -- MetaCoin.sol
  -- Migrations.sol
+ migrations
  -- 1_initial_migration.js
  -- 2_deploy_contracts.js
+ test
  -- metacoin.js
  -- TestMetacoin.sol
truffle.js
truffle-config.js
```
Now configure your **truffle.js** file to ganache-cli and migrate the contracts. 
```
$ truffle test
 TestMetacoin
    √ testInitialBalanceUsingDeployedContract (79ms)
    √ testInitialBalanceWithNewMetaCoin (53ms)

  Contract: MetaCoin
    √ should put 10000 MetaCoin in the first account
    √ should call a function that depends on a linked library (68ms)
    √ should send coin correctly (261ms)


  5 passing (1s)
```
If you want to learn how the tests work or to review a token contract it is perfect to start.

There are other useful boxes for :
  - React - http://truffleframework.com/boxes/react 
  - Vue - https://truffleframework.com/boxes/truffle-vue
  - Angular - https://truffleframework.com/boxes/angular-truffle-box
  


