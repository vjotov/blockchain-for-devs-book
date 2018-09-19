# Connect Ganache to Remix
We used **remix** a lot in the solidity chapters and with it is very easy to start developing smart-contracts without any additional software, just browser. We can connect our Ganache-cli or Ganache GUI to remix and deploy contracts to our network very easy and fast. In this example we will use ganache-cli but you can use GUI version if you prefer.
```
$ ganache-cli
```
Output
```
Listening on 127.0.0.1:8545
```
Now when ganache is running we need to go to the Remix IDE (https://remix.ethereum.org) and select **Web3 provider** from the "**Run**" tab.
![](/assets/ganache-truffle-images/ganache-connect-to-remix.png)

After that remix will ask you about the provider, you need to fill the Url of the instance in our case is **http://localhost:8545** or **http://127.0.0.1:8545**
Now when remix is connected the transaction will be executed in your local environment immediately.
```
Transaction: 0xb28540fc23a7f0dafaac3f0fd5d6905bb0d75832798ebf4f2426b980191e8733
  Contract created: 0x77d19fa305440e35ca79b05d9c56e5504ed38213
  Gas usage: 88269
  Block Number: 1
  Block Time: Tue Sep 18 2018 17:23:53 GMT+0300 (FLE Daylight Time)
```
