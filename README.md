# LearningEthereum
My road map to figuring out Ethereum

## Installation on Ubuntu 16.04

### Install Packages
Update and install packages

```
# sudo apt-get update && sudo apt-get -y upgrade
# sudo apt-get -y install curl git vim build-essential
```
### Install NodeJs
Install NodeJs to execute the DAPP

```
# curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
# sudo apt-get install -y nodejs
# sudo npm install -g express
```
### Install Truffle
Install Truffle packages

```
# sudo npm install -g truffle
```

### Install testrpc
testrpc uses ethereumjs to simulate full client behavior and make developing Ethereum
```
# sudo npm install -g ethereumjs-testrpc
```
To launch 
```
# testrpc
```
Output should display something like
```
EthereumJS TestRPC v3.0.5
Available Accounts
==================
(0) 0x2742c08e81208d01ff48a8c0f7d7c738625f92f5
(1) 0x7947d5e07ab4736edbdfdd421e60ca42205a097f
```

## Create a project

Init a Truffle Project
```
# mkdir myproject
# cd myprojet/
# truffle init
```
### Create a contract

Creating a contract "HelloWorld" using text editor
```
# cd myproject/contracts
# gedit HelloWorld.sol 
```
This is where you code your contract. Online compiler avaliable at: https://ethereum.github.io/browser-solidity

For this example we will use the following code
```
pragma solidity ^0.4.8;

contract HelloWorld{
    uint public balance;

    function HelloWorld(){
        balance = 123;
    }
}
```

Save the file.

### Setting up Deployment
Configuring the Truffle Deployment

We need to configure the deployment file
```
# cd myproject/migrations
# gedit 2_deploy_contracts.js
```
We now need add our contract as a variable and comment out the template contracts
```
//var ConvertLib = artifacts.require("./ConvertLib.sol");
//var MetaCoin = artifacts.require("./MetaCoin.sol");
var HelloWorld = artifacts.require("./HelloWorld.sol");

module.exports = function(deployer) {
//  deployer.deploy(ConvertLib);
  //deployer.link(ConvertLib, MetaCoin);
  //deployer.deploy(MetaCoin);
  deployer.deploy(HelloWorld);
};
```
Save the file

### Deploying the contract on testrpc

Open a new terminal and run the following command to start testrpc

```
testrpc -a
```
In our original terminal, in the myproject folder run the truffle compile command to compile your code and the truffle migrate command to deploy the contract

```
# truffle compile
# truffle migrate
```
The output should be similar to
```
Running migration: 1_initial_migration.js
  Deploying Migrations...
  Migrations: 0x2d7d9d80525ad7f7379edccbb1277014b209281d
Saving successful migration to network...
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Deploying HelloWorld...
  HelloWorld: 0xed6ccd21eb35b378ae1b42b5f7585b3d936fcb92
Saving successful migration to network...
Saving artifacts...
```

## Accessing the Contract

To interact with the contract, we access it through the truffle console
```
# truffle console
```
The interaction is similar to JavaScript.....
To access the balance variable of the contract we run the following command
```
# HelloWorld.deployed().then(a => console.log(a.balance().then(console.log)))
```

# To be continued...












