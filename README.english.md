# fabric-iot is based on the Hyperledger Fabric framework of the implementation of the IOT Access Control and management of the block chain simulation platform
[English](/README.en.md)  
> **WHAT WE HAVE**:  
> 1. Using ABAC as access control method, with the go to achieve the chaincode.
> 2. Write a complete script, easy to start-fabric-iot network.
> 3. Step-by-step instructions, easy to understand. 

## 0.Ready to work
### 0.0.Official website
[ github : hyperledger-fabric](https://github.com/hyperledger/fabric)  
[ doc 1.4 ](https://hyperledger-fabric.readthedocs.io/en/release-1.4/)
[ node-sdk 1.4 ](https://hyperledger.github.io/fabric-sdk-node/release-1.4/module-fabric-network.html)

### 0.1.Operating system
OS|Version
-|-
mac os|>=10.13
ubuntu|16.04  

### 0.2.Software:  
Software|Version
-|-
git|>=2.0.0
docker|>=19
docker-compose|>=1.24
node|>=12
golang|>=1.10
Hyperledger Fabric|=1.4.*

***Please Added The golang、node \bin PATH**

*** This experiment is based on the Fabric 1.4.3， The default download of the Fabric Version 1.4.3**

*** If you need a modified version of the，Please change the `bootstrap.sh`**
```
VERSION=1.4.3

CA_VERSION=1.4.3
```


### 0.3. Download the software
```go
go get github.com/newham/fabric-iot
```

### 0.4.Download and configure the Hyperledger Fabric
Download the source code and bin  
```bash
./bootstrap.sh
```
export PATH
```bash
export PATH=$PATH:$(pwd)/fabric-samples/bin
```
***After such as [start network, install the chain code and other operations need to first export PATH, which is to let the system know the Hyperledger Fabric bin directory】**  

***Also can be added to the path**

## 1.Directory structure

|-chaincode....................................chaincode folder  
|--go..........................................chaincode in golang  
|-client.......................................client of blockchain  
|--nodejs......................................code in nodejs of client  
|-network......................................fabric-iot network module folder,genesis.block  
|--channel-artifacts...........................channel comfig folder  
|--compose-files...............................docker-compose folder  
|--conn-conf...................................connection config of docker  
|--crypto-config...............................certs folder    
|--scripts.....................................shell scrpits of cli  
|--ccp-generate.sh.............................generate certs and blockchain config shell  
|--ccp-template.json...........................json template of connection config  
|--ccp-template.yaml...........................template of connection config  
|--clear-docker.sh.............................clearn docker images  
|--configtx.yaml...............................config of configtxgen  
|--crypto-config.yaml..........................config of ccp-generate.sh  
|--down.sh.....................................shutdown the network  
|--env.sh......................................environment of other shell scripts  
|--generate.sh.................................init config  
|--install-cc.sh...............................install chaincode  
|--rm-cc.sh....................................delete chaincode  
|--up.sh.......................................start network  

## 2.Build a network of [distributed version](https://github.com/newham/fabric-iot/tree/distributed)
### 2.1.To generate a certificate, configuration file, etc.
Enter the directory  
```shell
cd network
```
Run the script  
```shell
./generate.sh
```
Start the network `crypto-config`In
### 2.2. Start the network
```shell
./up.sh
```
### 2.3.Install Chaincode
```shell
./cc-install.sh
```
### 2.4.Update the chain code of the step in the modified chain code code before execution, [new version]is greater than the previous version
```shell
./cc-upgrade.sh [new version]
```
*chaincode is saved to `/chaincode/go` we only support write code with golang now. 
### 2.5.Close Network
```shell
./down.sh
```
*all the stoped docker containers or images will be delete ，be carefull before you do this
## 3.Interacting with the Blockchain

## 3.1. Use a shell script called chain code
Into the shell script directory
```bash
cd network
```
The call chain code(The sample code in the`cc-test.sh`)
```bash
# invoke
# shell|action|cc_name|cc_version|cc_src|fname|args
# add policy
./cc.sh invoke pc 1.0 go/pc AddPolicy '"{\"AS\":{\"userId\":\"13800010001\",\"role\":\"u1\",\"group\":\"g1\"},\"AO\":{\"deviceId\":\"D100010001\",\"MAC\":\"00:11:22:33:44:55\"}}"'
# query policy
./cc.sh invoke pc 1.0 go/pc QueryPolicy '"40db810e4ccb4cc1f3d5bc5803fb61e863cf05ea7fc2f63165599ef53adf5623"'
```
## 3.2. Use the Node JS client calling the chain code
### 3.2.1 initialization code
Enter the client code directory  
*Currently only implements nodejs client  

```shell
cd client/nodejs
```
Install dependencies
```shell
npm install
```
### 3.2.2.Create a user
Create administrator account
```shell
node ./enrollAdmin.js
```
Use the administrator account to create a sub-user
```shell
node ./registerUser.js
```
### 3.2.3.call chaincode
```shell
node ./invoke.js [chaincode_name] [function_name] [args]
```

<br>
<br>
©2019 <a href="mailto:liuhanshmtu@163.com">liuhanshmtu@163.com</a> all rights reserved.
