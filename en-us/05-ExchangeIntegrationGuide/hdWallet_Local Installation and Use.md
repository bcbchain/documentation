

#  1 hdWallet_RPC and hdWallet detailed explanation of local commands

hdWallet is an independent command-line program that provides local calls encapsulation of the rpc interface. It can be used for daily diagnosis and integration without the need to construct POST requests. 

## 1.1 hdWallet_rpc detailed command explanation

<font color=red>Note： Mnemonic words must be generated before starting the RPC service！</font>

### 1.1.1 createMnemonic

> Note: Danger!: Please make a backup of the mnemonic words after using the HD wallet to generate the mnemonic words. Otherwise, you would not be able to restore the wallet if the wallet is lost or you have forgotten the password. 

> Note: Since a HD wallet is able to generate sufficient multiple private key attributes, it is convenient to be used and managed by users. This version can only support a one time creation of the HD wallet.

- **command**

  ```
  ./hdWallet_rpc createMnemonic 
  ```

- **Input Parameters**

  | **Options** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | --       |    --    | --                                                           |

- **Output SUCCESS Example**

  ```
  {
    "mnemonic": "kitchen vast income save tail monitor kite outside volume chest bird master",
    "password": "3yeDJje6ZXGJ2oCdg15tTpY4R4MoctNApTVS3mg6mie3"
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | mnemonic      |  String  | 12 mnemonic words, separated by a single space.              |
  | password      |  String  | Randomly generated new mnemonic password.                    |

Note：<font color=red>After generating the mnemonic words, you are able to run ./hdWallet_rpc to start the client service. They cannot be done concurrently. Similarly, commands under./hdWallet_rpc such as changePassword/exportMnemonic/importMnemonic cannot be run concurrently.</font>

### 1.1.2 exportMnemonic

- **command**

  ```
  hdWallet_rpc exportMnemonic --password 9FPqXE82XLHwmoqK2TNXV9Lg45fhXcUREESzoK7JCcnX 
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | password      |  String  | Mnemonic password                                            |

- **Output SUCCESS Example**

  ```
  {
    "mnemonic": "craft toilet twist safe violin catch similar add friend lion fabric crisp"
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | mnemonic      |  String  | 12 mnemonic words, separated by a single space.              |



### 1.1.3 importMnemonic

> Note: After losing your password, you can only re-import the mnemonic to generate a new password. 

- **command**

  ```
  hdWallet_rpc importMnemonic --mnemonic “craft toilet ... crisp”
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | mnemonic      |  String  | 12 mnemonic words, separated by a single space.              |

- **Output SUCCESS Example**

  ```
  {
   "password":2oHQjWWKkGfUvWpeXV8qwgCTzrDh9fJ8hJV2L6gP6JeU
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | password      |  String  | Randomly generated new mnemonic password.                    |



### 1.1.4 changePassword

- **command**

  ```
  hdWallet_rpc changePassword --password 2oHQjWWKkGfUvWpeXV8qwgCTzrDh9fJ8hJV2L6gP6JeU 
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | password      |  String  | Mnemonic password.                                           |

- **Output SUCCESS Example**

  ```
  {
    "password":6eaN3vQjEW1ncCu4fYc9AvFFxFE4f4sY5HKw31X35zZ4
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | password      |  String  | Randomly generated new mnemonic password.                    |



## 2 Detailed explanation of hdWallet commands

### 2.1. Format for running  commands

```
Usage:
  hdWallet [command]

Available Commands:
  allBalance      Get all balance information
  balance         Get balance information
  balanceOfToken  Get balance information of address
  block           Get block information
  blockHeight     Get current block height
  commitTx        Commit transaction
  help            Help about any command
  nonce           Get account nonce
  setConfigPath   set config direction path
  transaction     Get transaction information
  transfer        Transfer token
  transferOffline Offline transaction
  walletCreate    Create wallet

Flags:
  -h, --help   help for hdWallet

Use "hdWallet [command] --help" for more information about a command.

```

### 2.2 Detailed explanation of hdWallet commands

#### 2.2.1 walletCreate

- **command**

  ```
  hdWallet walletCreate --password 2oHQjWWKkGfUvWpeXV8qwgCTzrDh9fJ8hJV2L6gP6JeU [--path "m/44'/60'/0'/0/1"] [--url https://...]
  ```

- **Input Parameters**

  | **Options** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | password |  String  | Mnemonic password. <font color=red>Please refer to hdWallet_rpc command for a detailed explanation of the mnemonic password generation process.</font> |
  | path     |  String  | <font color=red>HDWallet path:"m/44'/60'/0'/0/#"</font>, Where ”#“ is a number in the range: [0, 4294967295]. |
  | url      |  String  | Wallet service address. Optional, local service is the default. |
  
- **Output FAILED Example**

  ```
  {
    "code": -32603,
    "message": "Invalid parameters.",
    "data": ""
  }
  ```

Note: All command execution errors are returned in the same format. There will be no further explanation.

- **Output SUCCESS Example**

  Return：

  ```
  WalletCreate finish, [path=m/44'/60'/0'/0/1], [password=********]
  {
    "walletAddr": "localDhUdogRbcr8iT7hK8YJDdy6dRt2Nhm47g"
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | walletAddr    | Address  | Wallet address.                                              |

#### 2.2.2 transfer

- **command**

  ```
  hdWallet transfer [--password BYd...] [--path "m/44'/60'/0'/0/1"] --smcAddress bcbLVgb... --gasLimit 600 [--note hello] --to bcbLocFJG5Q792eLQXhvNkG417kwiaaoPH5a --value 1500000000 [--url https://...]
  ```
  
- **Request Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | password      |  String  | HDWallet mnemonic password.                                  |
  | path          |  String  | HDWallet path:"m/44'/60'/0'/0/#", where ”#“ is a number.     |
  | smcAddress    | Address  | Token address of the transaction asset (local currency or token). |
  | gasLimit      |  String  | Transaction gas limit.                                       |
  | note          |  String  | Transaction remarks (up to 256 characters), optional.        |
  | to            | Address  | Recipient's address.                                         |
  | value         |  String  | Number of assets transferred (Unit: Cong).                   |
  | url           |  String  | Wallet service address. Optional, the default is local service. |
  
- **Output SUCCESS Example**

  ```
  {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584"
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**      | **Type**  | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | Transaction execution result code. 200, means successful     |
  | &nbsp;&nbsp;log    |  String   | A description of the transaction execution result. A specific error message will be shown when the code is not equal to 200. |
  | &nbsp;&nbsp;txHash | HexString | Hash of the transaction，starts with 0x.                     |
  | &nbsp;&nbsp;height |   Int64   | The height of the block in which the transaction is confirmed |

#### 2.2.3 transferOffline

- **command**

  ```
  hdWallet transferOffline  [--password BYd...] [--path "m/44'/60'/0'/0/1"] 
  --smcAddress bcbLVgb... --gasLimit 600 [--note hello] --nonce 1500 --to bcbLocF... --value 1500000000 [--url https://...]
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | password      |  String  | HDWallet mnemonic password.                                  |
  | path          |  String  | HDWallet path:"m/44'/60'/0'/0/#", where ”#“ is a number.     |
  | smcAddress    | Address  | Token address of the transaction asset (local currency or token). |
  | gasLimit      |  String  | Transaction gas limit.                                       |
  | note          |  String  | Transaction remarks (up to 256 characters), optional.        |
  | nonce         |  String  | Transaction count.                                           |
  | to            | Address  | Recipient's address.                                         |
  | value         |  String  | Number of assets transferred (Unit：Cong).                   |
  | url           |  String  | Wallet service address. Optional, the default is local service. |
  
- **Output SUCCESS Example**

  ```
  {
    "tx": "bcb<tx>.v2.AetboYAmy2TEyUbsR731FTLDLyHE1MVKsSd4v7hS1jFnNkrtmGEVxVmWHR3jVSU
    ffxKgW7aPawnQaVrZ4gwMt6aogUAJjhvnukfPWnxmsybqDgdjgecjsXa94bamPqgPhTTZC9Szb.<1>.YT
    giA1gdDGi2L8iCryAn34dXVYKUEdmBxivyHbK57wKpBcX5KrKyn1vdmZTuKKZ7PotCjcbASbesv61VLE8
    H38TDiopHrs2eHG9z9iEDDyLcN7giLPCgFiLN9LPRiYZgxwpR95echr2bRPbijnKWj" 
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**  | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------------- | :------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;tx |  String  | The offline transaction data generated.                      |

#### 2.2.4 blockHeight

- **command**

  ```
  hdWallet blockHeight [--url https://...]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | url           |  String  | Wallet service address. Optional, the local service is default. |

- **Output SUCCESS Example**

  ```
  {
      "lastBlock": 2500
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | lastBlock     |  Int64   | Latest block height.                                         |

#### 2.2.5 block

- **command**

  ```
  hdWallet block --height 68685 [--url https://...]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | height        |  int64   | Specify the block height. Return the latest block information when it is 0. |
  | url           |  String  | Wallet service address. Optional, the default is local service. |

- **Output SUCCESS Example**

  ```
  {
    "blockHeight": 68685,
    "blockHash": "0x206e6bcfd17e1a64390e61c69468faee5a11faea",
    "parentHash": "0x05d7d5ff4a6d9a83da4c5b6f5913959a667b3b7b",
    "chainID": "devtest",
    "validatorHash": "0xd0d9a92830046e4abe4959be18ad0d8440dd33af",
    "consensusHash": "0xf66ef1df8ba6dac7a1ecce40cc84e54a1cebc6a5",
    "blockTime": "2019-10-28 08:34:33.134876793 +0000 UTC",
    "blockSize": 1615,
    "proposerAddress": "devtest4JjGSRE7QpWHgixhDTodsih1joE9uHN16",
    "txs": [
      {
        "txHash": "0xc8dbcfbe10fc7e935c2a29dd3aeb8ca08042a654332389d157f347a98231338e",
        "txTime": "2019-10-28 08:34:33.134876793 +0000 UTC",
        "code": 200,
        "log": "",
        "blockHash": "0x206e6bcfd17e1a64390e61c69468faee5a11faea",
        "blockHeight": 68685,
        "from": "devtestQ4suFdGVB4AbDnNLJ2xP9RXmqro6XtQXX",
        "nonce": 49,
        "gasLimit": 1000000,
        "fee": 1250000,
        "note": "transfer",
        "messages": [
          {
            "smcAddress": "devtestLL6sMXu8s2hhFRoZH67Q8fig9djogVi3H",
            "smcName": "token-basic",
            "method": "Transfer(types.Address,bn.Number)",
            "to": "devtestP4qDrEyBZegP5whAMmB1yy3c36HVCAWc",
            "value": "1000000000"
          }
        ],
        "transferReceipts": [
          {
            "token": "devtestLL6sMXu8s2hhFRoZH67Q8fig9djogVi3H",
            "from": "devtestQ4suFdGVB4AbDnNLJ2xP9RXmqro6XtQXX",
            "to": "devtestP4qDrEyBZegP5whAMmB1yy3c36HVCAWc",
            "value": 1000000000,
            "note": "transfer"
          }
        ]
      }
    ]
  }
  ```

- **Output SUCCESS Result**

| **Parameter**     | **Type**     | **Description**                                              |
| ----------------- | ------------ | ------------------------------------------------------------ |
| blockHeight       | Int64        | Block height.                                                |
| blockHash         | HexString    | Hash of the transaction，starts with 0x.                     |
| parentHash        | HexString    | Hash value of parent block, starts with 0x.                  |
| chainID           | String       | Chain ID.                                                    |
| validatorsHash    | HexString    | Hash value of validator list, starts with 0x                 |
| consensusHash     | HexString    | Hash of consensus information, starts with 0x.               |
| blockTime         | String       | Block packing time.                                          |
| blockSize         | Int          | Current block size.                                          |
| proposerAddress   | Address      | Address of the proposer.                                     |
| txs [             | Object Array | Transactions list.                                           |
| {                 | Object       | Transaction parameters.                                      |
| txHash            | HexString    | Transaction hash, starts with 0x.                            |
| txTime            | String       | Time of transaction.                                         |
| code              | Uint32       | Transaction execution result code, 200, means successful     |
| log               | String       | Transaction result description.                              |
| blockHash         | HexString    | Hash of the transaction, starts with 0x.                     |
| blockHeight       | Int64        | Block height.                                                |
| from              | Address      | Address of transaction signer.                               |
| nonce             | Uint64       | Transaction count of the transaction signer.                 |
| gasLimit          | Uint64       | Maximum gas limit.                                           |
| fee               | Uint64       | Transaction fee (Unit: cong).                                |
| note              | string       | Remarks.                                                     |
| messages [{       | Object Array | Messages list.                                               |
| smcAddress        | Address      | Address of the contract.                                     |
| smcName           | String       | Name of the contract.                                        |
| method            | String       | Prototype method                                             |
| to                | Address      | The account address of the transfer destination is only valid when the transaction is a BRC20 standard transfer. |
| value             | string       | Transfer amount (Unit: cong) is only valid when the transaction is a BRC20 standard transfer. |
| }]                |              |                                                              |
| transferReceipts[ | Object Array | List of receipts.                                            |
| {                 | Object       | Receipt parameters.                                          |
| token             | Address      | Token address.                                               |
| from              | Address      | Address of transaction signer.                               |
| to                | Address      | The account address of the transfer destination is only valid when the transaction is a BRC20 standard transfer. |
| value             | bn.Number    | Transfer amount (Unit: cong) is only valid when the transaction is a BRC20 standard transfer. |
| note              | string       | Receipt remarks.                                             |
| }                 |              |                                                              |
| ]                 |              |                                                              |

#### 2.2.6 transaction

- **command**

  ```
  hdWallet transaction --txHash 0x4E456161... [--url https://...]
  ```

- **Input Parameters**

  | **Parameter** | **Type**  | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :-------: | ------------------------------------------------------------ |
  | txHash        | HexString | Transaction hash, starts with 0x.                            |
  | url           |  String   | Wallet service address. Optional, the default is local service. |

- **Output SUCCESS Example**

  ```
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
    "note":"hello",
    "messages": [
      {
        "smcAddress": "bcbCsRXXMGkUJ8wRnrBUD7mQsMST4d53JRKJ",
        "smcName": "token-basic",
        "method": "Transfer(smc.Address,big.Int)smc.Error",
        "to": "bcbKuqW1qdsnD7mRsRooXMEkCBj2s9GLF9pn",
        "value": "683000000000"
      }
    ]
  }
  ```


- **Output SUCCESS Result**

  | **Parameter**                      |   **Type**   | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------------------------------- | :----------: | ------------------------------------------------------------ |
  | txHash                             |  HexString   | Transaction hash, starts with 0x.                            |
  | txTime                             |    String    | Time of transaction.                                         |
  | code                               |    Uint32    | Transaction result code. 200 means successful, and other values indicate failure. |
  | log                                |    String    | Transaction result description.                              |
  | blockHash                          |  HexString   | Transaction hashes in the block, starts with 0x.             |
  | blockHeight                        |    Int64     | Transaction block height.                                    |
  | from                               |   Address    | Transaction signer's address.                                |
  | nonce                              |    Uint64    | Transaction count.                                           |
  | gasLimit&nbsp;                     |    Uint64    | Maximum gas limit.                                           |
  | fee                                |    Uint64    | Transaction fees (Unit: Cong).                               |
  | note                               |    String    | Remarks.                                                     |
  | messages [                         | Object Array | Messages list.                                               |
  | &nbsp;&nbsp;{                      |    Object    | Message parameters.                                          |
  | &nbsp;&nbsp;&nbsp;&nbsp;smcAddress |   Address    | Address of the contract.                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;smcName    |    String    | Name of the contract.                                        |
  | &nbsp;&nbsp;&nbsp;&nbsp;method     |    String    | Prototype method.                                            |
  | &nbsp;&nbsp;&nbsp;&nbsp;to         |   Address    | Recipient's address.                                         |
  | &nbsp;&nbsp;&nbsp;&nbsp;value      |    String    | Transfer amount (Unit: Cong).                                |
  | &nbsp;&nbsp;}                      |              |                                                              |
  | ]                                  |              |                                                              |

#### 2.2.7 balance

- **command**

  ```
  hdWallet balance --address bcbAkTD... [--url https://...]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | address       | Address  | Account address.                                             |
  | url           |  String  | Wallet service address. Optional, the default is local service. |

- **Output SUCCESS Example**

  ```
  {
     "balance": "2500000000"
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | balance       |  String  | Account balance (Unit: Cong).                                |

#### 2.2.8 balanceOfToken

- **command**

  ```
  hdWallet balanceOfToken --address bcbAkTD... --tokenAddress bcbCsRX... --tokenNa
  me XT [--url https://...]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | address       | Address  | Account address.                                             |
  | tokenAddress  | Address  | Choose between the token address and token name. Both must be the same. |
  | tokenName     |  String  | Choose between the token address and token name. Both must be the same. |
  | url           |  String  | Wallet service address. Optional, the default is local service. |

- **Output SUCCESS Example**

  ```
  {
     "balance": "2500000000"
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | balance       |  String  | Account balance (Unit: Cong).                                |

#### 2.2.9 allBalance

- **command**

  ```
  hdWallet allBalance --address bcbAkTD... [--url https://...]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | address       | Address  | Account address.                                             |
  | url           |  String  | Wallet service address. Optional, the default is local service. |

- **Output SUCCESS Example**

  ```
  [
     {
        "tokenAddress": "bcbALw9SqmqUWVjkB1bJUQyCKfnxDPhuN5Ej"，
        "tokenName": "bcb"，
        "balance": "2500000000"
     },
     {
        "tokenAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe"，
        "tokenName": "XT"，
        "balance": "10000000",
     }
  ]
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | tokenAddress  | Address  | Token address.                                               |
  | tokenName     |  String  | Token name.                                                  |
  | balance       |  String  | Account balance (Unit: Cong).                                |

#### 2.2.10 nonce

- **command**

  ```
  hdWallet nonce --address bcbAkTD... [--url https://...]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | address       | Address  | Account address.                                             |
  | url           |  String  | Wallet service address. Optional, the default is local service. |

- **Output SUCCESS Example**

  ```
  {
    "nonce": 5000
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | nonce         |  Uint64  | Transaction count made available on the blockchain for the specified address. |

#### 2.2.11 commitTx

- **command**

  ```
  hdWallet commitTx --tx "bcb<tx>.v2.AetboY... [--url https://...]"
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | tx            |  String  | Transaction data.                                            |
  | url           |  String  | Wallet service address. Optional, the default is local service. |

- **Output SUCCESS Example**

  ```
  {
     "code": 200,
     "log": "Deliver tx succeed",
     "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584"
     "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**      | **Type**  | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | Transaction verification/ endorsement result code. 200 means successful. |
  | &nbsp;&nbsp;log    |  String   | Description of the transaction verification/ endorsement results, describing the specific error message when code is not equal to 200. |
  | &nbsp;&nbsp;txHash | HexString | Hash of transaction, starts with 0x.                         |
  | &nbsp;&nbsp;height |   Int64   | The height of the block in which the transaction is confirmed. |

#### 2.2.12 setConfigPath

- **command**

  ```
  hdWallet setConfigPath --configPath "./.config"
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | configPath    |  String  | Address of the wallet configuration file. Optional, the default setting is in the .config directory. |

- **Output SUCCESS Example**

  ```
  Starting RPC HTTP server on tcp://0.0.0.0:37657
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Description**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------- | :------: | ------------------------------------------------------------ |
  | version       |  String  | Current program version number.                              |









