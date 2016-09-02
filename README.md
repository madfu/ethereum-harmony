# Ethereum Harmony

Application for demonstrating EthereumJ features. It runs local Java based node https://github.com/ethereum/ethereumj and expose web interface for monitoring and interact. 
Next features were implemented:

 * **JSON-RPC 2.0** implementation and usage statistics. Note, that some JSON-RPC methods are not implemented yet;
 
 * Keeping private keys in filesystem **keystore** compatible with go-ethereum;
 
 * Browser based **terminal** for calling JSON-RPC methods;
 
 * Display blockchain info, like last block details, **blocks hierarchy**;  
 
 * Display physical machine info;
  
 * Connected peers displayed in list view and visualized on world map;
 
 * Monitoring system logs in web browser;
 
 * Ether wallet with abilities to view balance, and send amount with private key, keystore, mnemonic phrases.

Application is not designed for public access as may expose private info without restriction.

## Usage

To run application locally, system should have already installed: Java 8, Bower

First `bower install`

Then to run server: `gradlew bootRun`

Navigate to `http://localhost:8080`

JSON-RPC is available at `http://localhost:8080/rpc`

Use `gradlew bootRun -Dserver.port=9999` option to change web interface port number.

## Command line options

There are ways to connect to other networks:

`gradlew runMorden` will start server and tell ethereum node to connect to Morden network

`gradlew runTest` will start server and tell ethereum node to connect to Test network

`gradlew runClassic` will start server and tell ethereum node to connect to classic fork

`gradlew runPrivate` will start server without connecting to network. Mining will be enabled after start.

## Importing project to IntelliJ IDEA: 

Idea should have next plugins to be installed:
 
 - Gradle Plugin;
 
 - Lombok Plugin. Annotation processing should be turned on in IDEA compiler. Otherwise compiler will raise compile errors `java: cannot find symbol variable log`;

Checkout and build:

```
> git clone https://github.com/ether-camp/ethereum-harmony.git
> cd ethereum-harmony
> gradlew build
```

IDEA: 

* File -> New -> Project from existing sources…
* Select ethereum-harmony/build.gradle
* Dialog “Import Project from gradle”: press “OK”
* After building run either Gradle launcher with task bootRun 


## Implementation details

Application is built with Spring Boot and Angular 1. Websocket messaging and REST methods are used for client-server communication.
Lombok library is used to avoid writing generic code over data objects.
 
Original JSON-RPC specification located here: https://github.com/ethereum/wiki/wiki/JSON-RPC .   
Harmony contains improved copy of *jsonrpc* package from *ethereumj-core*.   
 
### Not implemented JSON-RPC methods:
  - *eth_hashrate*
  - *eth_compileLLL*
  - *eth_compileSerpent*
  - *eth_resend*
  - *eth_getWork*
  - *eth_submitWork*
  - *eth_submitHashrate*
  - *db_** set of calls
  - *shh_** set of calls
  - *admin_** set of calls
  - *debug_** set of calls
  
### New JSON-RPC methods:
 - *ethj_getTransactionReceipt* - method useful for debugging sending transactions. Shows cause message in case of transaction has been rejected by node verification.
  
### Testing JSON-RCP
  
Testing JSON-RPC is tricky because tests are NodeJS based and located in https://github.com/ethereum/rpc-tests

Harmony should be started with main class *com.ethercamp.harmony.jsonrpc.TestApplication*. Then *rpc-tests* should be configured launched.
More description located in *TestApplication* class. 


