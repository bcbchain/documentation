# Blockchain Interface

## 1. bcb_blockHeight

Sends a request to bcbXwallet_rpc to query the latest block height.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_blockHeight
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_blockHeight"
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | No parameters needed. |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "lastBlock": 2500
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter**  | **Type** | **Description** |
  | --------- | :------: | ------------------------------------------------------------ |
  | lastBlock |  Int64   | Latest block height |

## 2. bcb_block

Sends a request to bcbXwallet_rpc to query block data.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_block?height=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_block",
    "params": {
        "height": 68685
    }
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | height   |  Int64   | Specify the block height. 0 returns the block information of the latest height. |

- **Response SUCCESS Example**

  ```json
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

- **Response SUCCESS Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------------------------------------- | :----------: | ------------------------------------------------------------ |
  | blockHeight |    Int64     | Block height |
  | blockHash |  HexString   | Block hash, starting with 0x. |
  | parentHash |  HexString   | Parent Block hash, starting with 0x. |
  | chainID |    String    | Chain ID. |
  | validatorsHash                         |  HexString   | Validators hash, starting with 0x |
  | consensusHash                          |  HexString   | Consensus hash, starting with 0x                                 |
  | blockTime                              |    String    | Block Time.                                               |
  | blockSize                              |     Int      | Block Size.                                               |
  | proposerAddress                        |   Address    | Proposer Address. |
  | txs [                                  | Object Array | List of transactions                                                   |
  | &nbsp;&nbsp;{                          |    Object    | Transaction parameters                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;txHash         |  HexString   | Transaction Hash, starting with 0x |
  | &nbsp;&nbsp;&nbsp;&nbsp;txTime         |    String    | Transaction Time                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;code           |    Uint32    | Transaction response code, 200 means success, anything else means failure                |
  | &nbsp;&nbsp;&nbsp;&nbsp;log            |    String    | Description of transaction result.                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHash      |  HexString   | Block hash, starting with 0x.                             |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHeight    |    Int64     | Block height                                           |
  | &nbsp;&nbsp;&nbsp;&nbsp;from           |   Address    | Address of the transaction from party.                                             |
  | &nbsp;&nbsp;&nbsp;&nbsp;nonce          |    Uint64    | Nonce value of the transaction.                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;gasLimit&nbsp; |    Uint64    | Gas Limit.                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;fee            |    Uint64    | Transaction fee（Unit cong)                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;note           |    string    | note                                                       |
  | messages [{                            | Object Array | Message List                                                   |
  | smcAddress                             |   Address    | Smc Address.                                                   |
  | smcName                                |    String    | Smc Name.                                                   |
  | method                                 |    String    | method.                                                   |
  | to                                     |   Address    | Destination address, valid only when the transaction is a BRC20 standard transfer.            |
  | value                                  |    string    | Transaction total (unit: cong),valid only when the transaction is a BRC20 standard transfer.          |
  | &nbsp;}]&nbsp;                         |              |                                                              |
  | transferReceipts[                      | Object Array | Transfer receipt list                     |
  | {                                      |    Object    | Receipt parameters.                                                   |
  | token                                  |   Address    | Token address |
  | from                                   |   Address    | Address of the transaction from party.                                             |
  | to                                     |   Address    | Destination address, valid only when the transaction is a BRC20 standard transfer.            |
  | value                                  |  bn.Number   | Transaction total (unit: cong),valid only when the transaction is a BRC20 standard transfer..        |
  | note                                   |    string    | note                                                     |
  | }                                      |              |                                                              |
  | ]                                      |              |                                                              |

- PS ： The exchange can use the content of the transferReceipts module in the return result to make a judgment on the transaction account.

## 3. bcb_transaction

Sends a request to bcbXwallet_rpc to query a transaction details.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_transaction?txHash=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_transaction",
    "params": {
      "txHash": "0x4E456161A6580A1D34D86F1560DCFE6034F5E08FA31D7DCEBCCCC72A0DC73654"
    }
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type**  | **Description** |
  | -------- | :-------: | ------------------------------------------------------------ |
  | txHash   | HexString | Transaction hash                                 |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result":{
      "txHash": "0x4E456161A6580A1D34D86F1560DCFE6034F5E08FA31D7DCEBCCCC72A0DC73654",
      "txTime": "2018-12-27T14:26:19.251820644Z",
      "code": 200,
      "log": "Deliver tx succeed",
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
          "smcName": "token-templet-Diamond Coin",
          "method": "Transfer(smc.Address,big.Int)smc.Error",
          "to": "bcbKuqW1qdsnD7mRsRooXMEkCBj2s9GLF9pn",
          "value": "683000000000"
         }
      ]
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter**                           |   **Type**   | **Description** |
  | ---------------------------------- | :----------: | ------------------------------------------------------------ |
  | txHash                 |  HexString   | Transaction Hash, starting with 0x. |
  | txTime                 |    String    | Transaction Time                                                   |
  | code                   |    Uint32    | Transaction response code, 200 means success, anything else means failure                |
  | log                    |    String    | Description of transaction result.                                               |
  | blockHash              |  HexString   | Block hash, starting with 0x.                                 |
  | blockHeight            |    Int64     | Block height                                           |
  | from                   |   Address    | Address of the transaction from party.                                             |
  | nonce                  |    Uint64    | Nonce value of the transaction.                                       |
  | gasLimit&nbsp;         |    Uint64    | Gas Limit.                                               |
  | fee                    |    Uint64    | Transaction fee（Unit cong)                                     |
  | note                   |    String    | note                                                       |
  | messages [             | Object Array | Message List                                                   |
  | &nbsp;&nbsp;{                                  |    Object    | Message Parameter                                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;smcAddress |   Address    | Smc Address.                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;smcName    |    String    | Smc Name.                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;method     |    String    | method.                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;to         |   Address    | Destination address, valid only when the transaction is a BRC20 standard transfer.            |
  | &nbsp;&nbsp;&nbsp;&nbsp;value      |    String    | Transaction total (unit: cong),valid only when the transaction is a BRC20 standard transfer..        |
  | &nbsp;&nbsp;}                                  |              |                                                              |
  | ]                                  |              |                                                              |

## 4. bcb_balance

Sends a request to bcbXwallet_rpc to check the balance of the account BCB currency.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_balance?address=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_balance",
    "params": {
      "address": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7"
    }
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | address  | Address  | Address of account                                                   |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "balance": "2500000000"
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | balance  |  String  | Account balance (Unit: Cong)                                     |

## 5. bcb_balanceOfToken

Sends a request to bcbXwallet_rpc to check the balance of a token.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_balanceOfToken?address=_&tokenAddress=_&tokenName=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

- **Request Parameters**

  | **Parameter**     | **Type** | **Description** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | Address of account                                                   |
  | tokenAddress | Address  | Token address, can choose between this or token name, sometimes both need to be the same |
  | tokenName    |  String  | Token name, can choose between this or token address, sometimes both need to be the same |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "balance": "2500000000"
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | balance  |  String  | Account balance (Unit: Cong) |

## 6. bcb_allBalance

Sends a request to bcbXwallet_rpc to query all the tokens in an account.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_allBalance?address=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_allBalance",
    "params": {
        "address": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7"
    }
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | address  | Address  | Address of account                                                   |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": [
        {
          "tokenAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
          "tokenName": "BCB",
          "balance": "2500000000"
        },
        {
          "tokenAddress": "bcbJ4fKuUcC5TuzXNiHqT5jNxZBx2eUToyk1",
          "tokenName": "XT",
          "balance": "10000000",
        }
    ]
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter**     | **Type** | **Description** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | tokenAddress | Address  | Token address.                                                   |
  | tokenName    |  String  | Token name |
  | balance      |  String  | Account balance (Unit: Cong)                                     |

## 7. bcb_nonce

Sends a request to bcbXwallet_rpc to query the next transaction count value available on the blockchain for the account.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_nonce?address=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_nonce",
    "params": {
       "address": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7"
    }
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | address  | Address  | Address of account                                                   |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
     "nonce": 5000
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | nonce    |  Uint64  | Specify the next transaction count value available for the address on the blockchain |

## 8. bcb_commitTx

Sends a request to bcbXwallet_rpc to commit a transaction.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_commitTx?tx=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | tx       |  String  | Transaction data |

- **Response SUCCESS Example**

  ```json
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

- **Response SUCCESS Parameters**

  | **Parameter** | **Type**  | **Description** |
  | -------- | :-------: | ------------------------------------------------------------ |
  | code     |    Int    | Transaction response code, 200 means success, anything else means failure.                         |
  | log      |  String   | Error message when response code is not 200. |
  | txHash   | HexString | Transaction hash                                    |
  | height   |   Int64   | Block height of transaction                                 |

## 9. bcb_version

Sends a request to bcbXwallet_rpc to query the current version number.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_version
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_version"
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | None needed |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
      "version": "1.0.7.9636"
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | version  |  string  | Current version number |
