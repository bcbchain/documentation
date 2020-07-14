# hdWallet_RPC remote interface documentation

for details on hdWallet installation, upgrade and local commands，refer to： [hdWallet本地安装及使用](./hdWallet本地安装及使用.md) 

<div STYLE="page-break-after: always; "></div>
[TOC]

<script src="./github/ltview.js"></script>
<div STYLE="page-break-after: always; "></div>

# 1 Introduction

## 1.1 What is BCBChain

​	The blockchain system of BCBChain is developed based on Tendermint. Technological innovation is carried out with system security in mind and realises the value of effective transfer of information between objects and objects, and human and objects, to build high quality and easily scalable platforms that have high performance.

For a more detailed introduction, refer to《BCBChain_V1.0_Program_Reference》。

## 1.2 Summary

​	The procedure required for docking the BCBChain wallet assets and exchange are as follows：

* hdWallet_rpc 

  The BCBChain Exchange station docking service program is a service that provides secure generation of wallet private keys and outputs access keys. At the same time, it allows easy access to API interfaces for digital asset transactions.

* hdWallet

  BCBChain Exchange station docking service program's client is a command line tool that provides convenient access to the service program's open interface.

The basic relationship between the above components is depicted in the figure below.

![basic2](https://github.com/bcbchain/documentation/blob/master/zh-cn/05-交易所对接指南/p10/basic2.png)

<div STYLE="page-break-after: always; "></div>
<div STYLE="page-break-after: always; "></div>

# 2 Protocol

## 2.1 Protocol Overview

​	The hdWallet_rpc service procedure supports the following RPC communication protocol:

* URI over HTTPS

* JSONRPC over HTTPS

  All RPC interfaces and parameters supported by the hdWallet_rpc service can be obtained through this URL: https://ip:port.

  The list of RPC interfaces provided by the hdWallet_rpc service is as follows (supports HTTPS, the default port number is 37657):

![hdWallet_rpc](https://github.com/bcbchain/documentation/blob/master/zh-cn/05-交易所对接指南/p10/hdWallet_rpc.png)

## 2.2 URI over HTTP

 When using the HTTP GET method for RPC requests, the parameters must be URI encoded. For URL formats of RPC calls, refer to the above table. For specific services and paramter descriptions, refer to subsequent parts of this section.

## 2.3 JSONRPC over HTTP

​	When using the HTTP POST method for RPC requests, the JSONRPC application protocol is used. The format of the requested HTTP data is as follows:

``` json
Example：
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "bcb_block",
  "params": {
    "height": 2500
  }
}
```

​	For specific communication interface services and parameter descriptions, refer to the subsequent sections.

​	 The general format returned after successful execution of is as follows:

``` 
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    …		// JSON format returned by different APIs are customized
  }
}
```

​	The general format returned by execution failure is as follows (the format returned by failure is the same for all interfaces):

``` json
{
  "jsonrpc": "2.0",
  "id": "",
  "error": {
    "code": -32603,
    "message": "Invalid parameters.",
    "data": ""
  }
}
```

# 4 RPC interface

#### 4.1 bcb_walletCreate

​	Submit a request to the hdWallet_rpc service to create a new wallet.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_walletCreate?path=_&password=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_walletCreate",
    "params": {
        "path": "m/44'/60'/0'/0/1",
        "password": "aBig62_123"
    }
  }
```

* **Request Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|----------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| path     |  String | HD wallet path:"m/44'/60'/0'/0/#", where "#" is a number in the range：[0, 4294967295].                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| password |  String | Mnemonic password.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
    	"walletAddr": "bcbES5d6kwoX4vMeNLENMee2Mnsf2KL9ZpWo"
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters**   | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|------------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| walletAddr | Address | wallet address.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

#### 4.2 bcb_transfer

​	Submit an asset transfer request to the hdWallet_rpc service.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_transfer?path=_&password=_&walletParams=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_transfer",
    "params": {
      "path": "m/44'/60'/0'/0/1",
      "password": "aBig62_123",
      "walletParams": {
        "smcAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
        "gasLimit": "600",
        "note": "",
        "to": "bcbLocFJG5Q792eLQXhvNkG417kwiaaoPH5a",
        "value": "1500000000"
      }
    }
  }
```

* **Request Parameters**

| **Parameters**                 | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|--------------------------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| path                     |  String | HD wallet path:"m/44'/60'/0'/0/#", where "#" is a number in the range：[0, 4294967295].                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| password                 |  String | Mnemonic password.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| walletParams {           |  Object | Asset trading parameters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| &nbsp; &nbsp; smcAddress | Address | Token address of the transaction asset (local currency or token).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| &nbsp; &nbsp; gasLimit   |  String | The gas limit of transaction.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| &nbsp; note              |  String | Transaction remarks (up to 256 characters).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| &nbsp; &nbsp; to         | Address | Account address of the recipient.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| &nbsp; &nbsp; value      |  String | Amount of assets transferred (unit: Cong).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| }                        |         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "code": 200,
      "log": "succeed",
      "fee": "125000",
      "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584"
      "height": 234389
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters** |  **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:---------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| code    |    Int    | Transaction verification / endorsement status code, 200 means successful execution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| log     |   String  | A text description of the transaction verification / endorsement result, describing the specific error message when the code is not equal to 200.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| txHash  | HexString | hash of the transaction, starts with 0x.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| height  |   Int64   | The block at which the transaction was confirmed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

#### 4.3  <span id="jump">bcb_transferOffline</span>  

​	Submit a request to construct an offline asset transfer transaction to the hdWallet_rpc service.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_transferOffline?path=_&password=_&walletParam=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_transferOffline",
    "params": {
      "path": "m/44'/60'/0'/0/1",
      "password": "aBig62_123",
      "walletParams": {
        "smcAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
        "gasLimit": "600",
        "note": "",
        "nonce": 15,
        "to": "bcbLocFJG5Q792eLQXhvNkG417kwiaaoPH5a",
        "value": "1500000000"
      }
    }
  }
```

* **Request Parameters**

| **Parameters**                 | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|--------------------------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| path                     |  String | HD wallet path: "m/44'/60'/0'/0/#", where "#" is a number in the range: [0, 4294967295].                                                                                                                                                                                                                                                                                                                                                                                      |
| password                 |  String | Mnemonic password.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| walletParams {           |  Object | Asset trading parameters.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| &nbsp; &nbsp; smcAddress | Address | Token address of the transaction asset (local currency or token).                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| &nbsp; &nbsp; gasLimit   |  String | Gas limit of the transaction.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| &nbsp; note              |  String | Transaction remarks (up to 256 characters).                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| &nbsp; &nbsp; nonce      |  Uint64 | Transaction count, can be obtained through ```bcb_nonce``` interface.                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| &nbsp; &nbsp; to         | Address | Address of the recipient account.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| &nbsp; &nbsp; value      |  String | Amount of assets transferred (unit: Cong).                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| }                        |         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "tx": "bcb<tx>.v2.AetboYAmy2TEyUbsR731FTLDLyHE1MVKsSd4v7hS1jFnNkrtmGEVxVmWHR3
      jVSUffxKgW7aPawnQaVrZ4gwMt6aogUAJjhvnukfPWnxmsybqDgdjgecjsXa94bamPqgPhTTZC9Sz
      b.<1>.YTgiA1gdDGi2L8iCryAn34dXVYKUEdmBxivyHbK57wKpBcX5KrKyn1vdmZTuKKZ7PotCjcb
      ASbesv61VLE8H38TDiopHrs2eHG9z9iEDDyLcN7giLPCgFiLN9LPRiYZgxwpR95echr2bRPbijnKW
      j" 
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| tx      |  String | Offline transaction data generated.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

# 5 Block Link

### 5.1 bcb_blockHeight

​	Query the hdWallet_rpc service for the latest height of the block.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_blockHeight
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_blockHeight"
  }
```

* **Request Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ——      |    ——   | No parameters required.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "lastBlock": 2500
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters**  | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|-----------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lastBlock |  Int64  | The latest block height.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

### 5.2 bcb_block

​	Query block data from hdWallet_rpc service.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_block?height=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_block",
    "params": {
        "height": 2500
    }
  }
```

* **Request Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| height  |  Int64  | Specifies the block height. When it is 0, the latest block information is returned.                                                                                                                                                                                                                                                                                                                                                                                                                  |

* **Response SUCCESS Example**

  + The following are example queries of different chain versions. All exchanges need to be compatible with these two formats when determining the crediting.

* **V1.0 version format**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result":{
      "blockHeight": 2495461,
      "blockHash": "0x583E820E58D2FD00B1A7D66CDBB6B7C26B207925",
      "parentHash": "0xE250D6EAA2AF05EEF18438F4B0811A09E6F90CDD",
      "chainID": "bcb",
      "validatorsHash": "0xC19638A1E31F030030505680C47A0EF9BB5DC58E",
      "consensusHash": "0xF66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
      "blockTime": "2018-12-27T14:26:19.251820644Z",
      "blockSize": 2866,
      "proposerAddress": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
      "txs": [
      {
        "txHash": "0x4E456161A6580A1D34D86F1560DCFE6034F5E08FA31D7DCEBCCCC72A0DC73654",
        "txTime": "2018-12-27T14:26:19.251820644Z",
        "code": 200,
        "log": "Deliver tx succeed"
        "blockHash": "0x583E820E58D2FD00B1A7D66CDBB6B7C26B207925",
        "blockHeight": 2495461,
        "from": "bcbAkTDzHLf5udamub38GdepKe7nek66EHqY",
        "nonce": 117510,
        "gasLimit": 2500,
        "fee": 1500000,
        "note":"agree",
        "messages": [
          {
           "smcAddress": "bcbCsRXXMGkUJ8wRnrBUD7mQsMST4d53JRKJ",
           "smcName": ""token-templet-Diamond Coin",
           "method": "Transfer(smc.Address,big.Int)smc.Error",
           "to": "bcbKuqW1qdsnD7mRsRooXMEkCBj2s9GLF9pn",
           "value": "683000000000"
          }
        ]
       }
      ]
    }
  }
```

* **V2.0  version format**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "",
    "result": {
      "blockHeight": 21552804,
      "blockHash": "0x3f661b9bf0c9cb45cc7b4147a04b743ea216c474",
      "parentHash": "0x6373f672dbbd301a18c8edb8dc2c9ac5d93f76e7",
      "chainID": "bcb",
      "validatorHash": "0xc19638a1e31f030030505680c47a0ef9bb5dc58e",
      "consensusHash": "0xf66ef1df8ba6dac7a1ecce40cc84e54a1cebc6a5",
      "blockTime": "2019-08-22 03:11:08.902084792 +0000 UTC",
      "blockSize": 2722,
      "proposerAddress": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
      "txs": [
        {
          "txHash": "0x6b62ad71d296288b5524648b0e424d03e002874f406347bc676663f95914c66e",
          "txTime": "2019-08-22 03:11:08.902084792 +0000 UTC",
          "code": 200,
          "log": "",
          "blockHash": "0x3f661b9bf0c9cb45cc7b4147a04b743ea216c474",
          "blockHeight": 21552804,
          "from": "bcbLZUr2gD5w3sZLNycjQ8GzMGtPWUmuXnMs",
          "nonce": 13,
          "gasLimit": 100000,
          "fee": 1500000,
          "note": "",
          "messages": [
            {
              "smcAddress": "bcbCsRXXMGkUJ8wRnrBUD7mQsMST4d53JRKJ",
              "smcName": "token-templet-Diamond Coin",
              "method": "Transfer(types.Address,bn.Number)",
              "to": "bcbQ2fxvopeLy5wLSXM58ajacuoGyAmvUmwB",
              "value": "27340000000"
            }
          ]
        }
      ]
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters**                                       |   **Type**   | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| ---------------------------------------------------- | :----------: | ------------------------------------------------------------ |
| blockHeight                                          |    Int64     | Block height.                                                |
| blockHash                                            |  HexString   | Block hash value, starts with 0x.                            |
| parentHash                                           |  HexString   | ash of the parent block, starts with 0x.                     |
| chainID                                              |    String    | Chain ID.                                                    |
| validatorsHash                                       |  HexString   | Hash of list of validators, starts with 0x.                  |
| consensusHash                                        |  HexString   | hash of consensus information, starts with 0x.               |
| blockTime                                            |    String    | Block packing time.                                          |
| blockSize                                            |     Int      | The current block size.                                      |
| proposerAddress                                      |   Address    | Addres of proposer                                           |
| txs [                                                | Object Array | Transactions list.                                           |
| &nbsp; &nbsp; {                                      |    Object    | Trading parameters.                                          |
| &nbsp; &nbsp; &nbsp; &nbsp; txHash                   |  HexString   | Transaction hash, starts with 0x.                            |
| &nbsp; &nbsp; &nbsp; &nbsp; txTime                   |    String    | Time of transaction.                                         |
| &nbsp; &nbsp; &nbsp; &nbsp; code                     |    Uint32    | Transaction status code, 200 indicates successful transaction, other values indicate failure. |
| &nbsp; &nbsp; &nbsp; &nbsp; log                      |    String    | Transaction result description.                              |
| &nbsp; &nbsp; &nbsp; &nbsp; blockHash                |  HexString   | Transaction hashes in block, starts with 0x.                 |
| &nbsp; &nbsp; &nbsp; &nbsp; blockHeight              |    Int64     | Block height of all transactions.                            |
| &nbsp; &nbsp; &nbsp; &nbsp; from                     |   Address    | Address of transaction signer.                               |
| &nbsp; &nbsp; &nbsp; &nbsp; nonce                    |    Uint64    | Transaction count of transaction signer.                     |
| &nbsp; &nbsp; &nbsp; &nbsp; gasLimit&nbsp;           |    Uint64    | Maximum gas limit.                                           |
| &nbsp; &nbsp; &nbsp; &nbsp; fee                      |    Uint64    | Transaction fee (unit: cong).                                |
| &nbsp; &nbsp; &nbsp; &nbsp; note                     |    string    | Remarks.                                                     |
| &nbsp; &nbsp; &nbsp; &nbsp; messages [               | Object Array | List of messages.                                            |
| &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; smcAddress |   Address    | Address of contract.                                         |
| &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; smcName    |    String    | Name of contract.                                            |
| &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; method     |    String    | Method prototype.                                            |
| &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; to         |   Address    | The account address of the transfer destination, valid only when the transaction is a BRC20 standard transfer. |
| &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; value      |    string    | Transfer amount (unit: cong), valid only when the transaction is a BRC20 standard transfer. |
| &nbsp; &nbsp; }                                      |              |                                                              |
| ]                                                    |              |                                                              |

### 5.3 bcb_transaction

​	Query transaction data from hdWallet_rpc service.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_transaction?txHash=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_transaction",
    "params": {
      "txHash": "0x4E456161A6580A1D34D86F1560DCFE6034F5E08FA31D7DCEBCCCC72A0DC73654"
    }
  }
```

* **Request Parameters**

| **Parameters** |  **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:---------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| txHash  | HexString | Hash of transaction, starts with 0x.                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result":{
      "txHash": "0x4E456161A6580A1D34D86F1560DCFE6034F5E08FA31D7DCEBCCCC72A0DC73654",
      "txTime": "2018-12-27T14:26:19.251820644Z",
      "code": 200,
      "log": ""
      "blockHash": "0x583E820E58D2FD00B1A7D66CDBB6B7C26B207925",
      "blockHeight": 2495461,
      "from": "bcbAkTDzHLf5udamub38GdepKe7nek66EHqY",
      "nonce": 117510,
      "gasLimit": 2500,
      "fee": 1500000,
      "note":"agree",
      "messages": [
         {
          "smcAddress": "bcbCsRXXMGkUJ8wRnrBUD7mQsMST4d53JRKJ",
          "smcName": ""token-templet-Diamond Coin",
          "method": "Transfer(smc.Address,big.Int)smc.Error",
          "to": "bcbKuqW1qdsnD7mRsRooXMEkCBj2s9GLF9pn",
          "value": "683000000000"
         }
      ]
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters**                         |   **Type**   | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| -------------------------------------- | :----------: | ------------------------------------------------------------ |
| txHash                                 |  HexString   | Transaction hash, starts with 0x.                            |
| txTime                                 |    String    | Time of transaction.                                         |
| code                                   |    Uint32    | Transaction result code, 200 means successful transaction, other values ​​mean failure. |
| log                                    |    String    | Transaction result description.                              |
| blockHash                              |  HexString   | Hashes of transactions in the block, starts with 0x.         |
| blockHeight                            |    Int64     | Block height of the transaction.                             |
| from                                   |   Address    | Address of transaction signer.                               |
| nonce                                  |    Uint64    | Transaction count of the transaction signer.                 |
| gasLimit&nbsp;                         |    Uint64    | Maximum gas limit.                                           |
| fee                                    |    Uint64    | Transaction fee (unit: cong).                                |
| note                                   |    String    | Remarks.                                                     |
| messages [                             | Object Array | Messages list.                                               |
| &nbsp; &nbsp; {                        |    Object    | Message parameter.                                           |
| &nbsp; &nbsp; &nbsp; &nbsp; smcAddress |   Address    | Contract address.                                            |
| &nbsp; &nbsp; &nbsp; &nbsp; smcName    |    String    | Contract name.                                               |
| &nbsp; &nbsp; &nbsp; &nbsp; method     |    String    | Method prototype.                                            |
| &nbsp; &nbsp; &nbsp; &nbsp; to         |   Address    | The account address of the transfer destination, valid only when the transaction is a BRC20 standard transfer. |
| &nbsp; &nbsp; &nbsp; &nbsp; value      |    String    | Transfer amount (unit: cong), valid only when the transaction is a BRC20 standard transfer. |
| &nbsp; &nbsp; }                        |              |                                                              |
| ]                                      |              |                                                              |

### 5.4 bcb_balance

​	Query the balance of the account BCB currency with the hdWallet_rpc service.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_balance?address=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_balance",
    "params": {
      "address": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7"
    }
  }
```

* **Request Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| address | Address | Account address.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "balance": "2500000000"
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| balance |  String | Account balance (unit: Cong).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

### 5.5 bcb_balanceOfToken

​	Query the hdWallet_rpc service for the balance of the specified token in the account.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_balanceOfToken?address=_&tokenAddress=_&tokenName=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_balanceOfToken",
    "params": {
      "address": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7",
      "tokenAddress": "bcbJ4fKuUcC5TuzXNiHqT5jNxZBx2eUToyk1",
      "tokenName": "XT"
    }
  }
```

* **Request Parameters**

| **Parameters**     | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|--------------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| address      | Address | Account address.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| tokenAddress | Address | Token address. Can be taken from either the tokenAddress of tokenName. At times, they must be the same.                                                                                                                                                                                                                                                                                                                                                                                            |
| tokenName    |  String | Token name. Can be taken from either the tokenAddress of tokenName. At times, they must be the same.                                                                                                                                                                                                                                                                                                                                                                                         |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "balance": "2500000000"
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| balance |  String | Account balance (unit: Cong).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### 5.6 bcb_allBalance

​	Query for the balance of all tokens in the specified account from the hdWallet_rpc service.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_allBalance?address=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_allBalance",
    "params": {
        "address": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7"
    }
  }
```

* **Request Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| address | Address | Account address.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": [
        {
          "tokenAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe"，
          "tokenName": "BCB"，
          "balance": "2500000000"
        },
        {
          "tokenAddress": "bcbJ4fKuUcC5TuzXNiHqT5jNxZBx2eUToyk1",
          "tokenName": "XT"，
          "balance": "10000000",
        }
    ]
  }
```

* **Response SUCCESS Parameters**

| **Parameters**     | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|--------------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| tokenAddress | Address | Token address.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| tokenName    |  String | Token name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| balance      |  String | Account balance (unit: Cong).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### 5.7 bcb_nonce

​	Query the hdWallet_rpc service for the account's next transaction count value available on the blockchain.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_nonce?address=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_nonce",
    "params": {
       "address": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7"
    }
  }
```

* **Request Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| address | Address | Account address.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
    	"nonce": 5000
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| nonce   |  Uint64 | The next transaction count available on the blockchain at the specified address.                                                                                                                                                                                                                                                                                                                                                                                                                          |

### 5.8  <span id="jump2">bcb_commitTx</span> 

​	Query the hdWallet_rpc service to perform a transaction on the smart contract on the blockchain。

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_commitTx?tx=_
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_commitTx",
    "params": {
      "tx": "bcb<tx>.v2.AetboYAmy2TEyUbsR731FTLDLyHE1MVKsSd4v7hS1jFnNkrtmGEVxVmWHR
      3jVSUffxKgW7aPawnQaVrZ4gwMt6aogUAJjhvnukfPWnxmsybqDgdjgecjsXa94bamPqgPhTTZC9
      Szb.<1>.YTgiA1gdDGi2L8iCryAn34dXVYKUEdmBxivyHbK57wKpBcX5KrKyn1vdmZTuKKZ7PotC
      jcbASbesv61VLE8H38TDiopHrs2eHG9z9iEDDyLcN7giLPCgFiLN9LPRiYZgxwpR95echr2bRPbi
      jnKWj"
    }
  }
  
```

* **Request Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| tx      |  String | Transaction data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
    	"code": 200,
    	"log": "succeed",
    	"txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    	"height": 234389
    }
  }
  
```

* **Response SUCCESS Parameters**

| **Parameters** |  **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:---------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| code    |    Int    | Transaction verification / endorsement status code, 200 means successful execution.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| log     |   String  | A text description of the transaction verification / endorsement result, describing the specific error message when the code is not equal to 200.                                                                                                                                                                                                                                                                                                                                |
| txHash  | HexString | Hash of the transaction, starts with 0x.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| height  |   Int64   | Block height at which transaction is confirmed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### 5.9 bcb_version

​	Query version number from hdWallet_rpc service.

* **Request URI over HTTPS**

  

``` 
  https://localhost:37657/bcb_version
```

* **Request JSONRPC over HTTPS**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_version"
  }
```

* **Request Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ——      |    ——   | No parameters required.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

* **Response SUCCESS Example**

  

``` 
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "version": "1.0.7.9636"
    }
  }
```

* **Response SUCCESS Parameters**

| **Parameters** | **Type** | **Description**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
|---------|:-------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| version |  string | Current version number.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

# 6 How to  Setup Transaction

## 6.1 **Setup using Address Labelling**

**Explanation for Setup using Address Labelling:**

​	BCBChain Transaction provides support for address labelling. Hence, the management can look into cryptocurrencies such as XRP and EOS.

​	The transaction only needs to generate multiple hot wallet addresses, which can be shared between multiple different accounts. Each user can assign their own remark (commonly known as address label) to the wallet. Since different users can share the same currency address, the exchange does not need to perform time-consuming operations such as fund collection.

​	Users top up their values and make withdrawals through these hot wallets. This satisfies the internal cycle.

 

The four main considerations with regards to the transaction are as follows:

* From the BCBChain, multiple hot wallet addresses can be generated to form the coin address. Different users share these hot wallet addresses. The transaction generates a different address label for every user. This way, even when different users use the same address, they can be identified based on their address label.
* To account for every user’s account activity, the transaction will retrieve the latest block at fixed intervals. Based on the transfer type recorded in the block’s transaction, identify if there was a transaction at that address. If there is, parse it and identify which user's address label it is and the corresponding currency, then credit the corresponding account.
* Regarding withdrawal for users, the transaction only needs to call the bcbXwallet_rpc to withdraw from the hot wallet.
* Regarding wallet security, since access keys are randomly generated, the transaction will need to store the encrypted password and access key of the wallets. The transaction must use its own protection mechanisms to store these keys and encrypted passwords in a secure manner.

The detailed steps are explained the diagram below:

![1. Address Label Scheme](https://github.com/bcbchain/documentation/blob/master/zh-cn/05-交易所对接指南/p10/hdWallet地址标签方案.jpg)

## 6.2 **Setup without Address Label**

**Explanation for Setup without Address Labelling:**：

​	When the address label feature in BCBChain is not in use, you cannot distinguish the activities of the users in the account by the exchange hot wallet address; in this case, when the user performs a deposit, there is a need to generate a unique deposit account as a unique collection address. Then, periodically collect the deposit addresses in their wallet and distribute the user's deposit to each deposit address in the transaction hot wallet.

The four main considerations with regards to transaction are as follows:

* The user's address and the transaction's hot wallet cannot be the same. At the same time, the user will have to properly manage the distribution and aggregation of tokens in the wallet to ensure smooth operation.
* It is necessary to deposit money for users and withdraw money from users. Thus, it is not possible to avoid internal circulation. It is also necessary to always pay attention to the balance in the hot wallet for withdrawal to ensure that the user has enough balance when withdrawing.
* When charging the wallet, users only need to be mindful of the address of the wallet to be charged.
* Due to the increased number of wallets that need to be managed, more care needs to be taken so that the wallet’s encrypted password and access key are secured.

The detailed steps are explained the diagram below：

![2. No Address Label Scheme](https://github.com/bcbchain/documentation/blob/master/zh-cn/05-交易所对接指南/p10/hdWallet无地址标签方案.jpg)

## 6.3 Transfer from cold wallet to hot wallet

****Explanation for transfering from cold wallet to hot wallet:****

​	When transferring from the cold wallet to the hot wallet, the transaction cannot be completed online to package and sign. In this case, there is a need to use the offline cold wallet to package and sign the transaction. Refer to 4.3  [bcb_transferOffline](#jump) generate packaged and signed offline transactionsTx，then, go to 5.8  [bcb_commitTx](#jump2)

The detailed steps are explained the diagram below：

![3. Scheme Of Transfering From cold wallet To hot wallet](https://github.com/bcbchain/documentation/blob/master/zh-cn/05-交易所对接指南/p10/hdWallet冷钱包向热钱包转账.jpg)

 
