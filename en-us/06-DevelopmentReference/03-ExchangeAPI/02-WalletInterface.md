# Wallet Management Interface

## 1. bcb_walletCreate

Sends a request to bcbXwallet_rpc service to create a new wallet.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_walletCreate?name=_&password=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_walletCreate",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123"
    }
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | name     |  String  | Wallet name, 1-40 characters long, only upper case, lower case, digits, @, _, - , . allowed. |
  | password |  String  | Password for wallet,8-20 characters long（Any ASCII characters allowed, must contain at least one lower case, one upper case, one number, and one non-alphanumeric character). |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
     "walletAddr": "bcbES5d6kwoX4vMeNLENMee2Mnsf2KL9ZpWo",
     "accessKey": "ASwDbde7X6z7nnTo2NVLrXF7JXevxA9iPeiTjforkCCB"
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter**   | **Type** | **Description** |
  | ---------- | :------: | ------------------------------------------------------------ |
  | walletAddr | Address  | Address of the wallet. |
  | accessKey  |  String  | The wallet access key, which is randomly generated by the bcbXwallet_rpc service and used to encrypt the private key corresponding to the wallet. The key needs to be properly stored, as it can no longer be retrieved if lost. |

## 2. bcb_walletExport

Sends a request to bcbXwallet_rpc to export a wallet.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_walletExport?name=_&password=_&accessKey=_&plainText=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_walletExport",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123",
        "accessKey": "ASwDbde7X6z7nnTo2NVLrXF7JXevxA9iPeiTjforkCCB",
        "plainText": false
    }
  }
  ```

- **Request Parameters**

  | **Parameter**  | **Type** | **Description** |
  | --------- | :------: | ------------------------------------------------------------ |
  | name      |  String  | Wallet name                                                   |
  | password  |  String  | Password for wallet,8-20 characters long（Any ASCII characters allowed, must contain at least one lower case, one upper case, one number, and one non-alphanumeric character) |
  | accessKey |  String  | Access key of wallet                                               |
  | plainText |   Bool   | Whether to export the wallet’s private key in plaintext. true: plaintext, false:encrypted private key. |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
     "privateKey": "0xbf7cbe09d71a1bc…99b7abd8f8fd73cb4",
     "walletAddr": "bcbES5d6kwoX4vMeNLENMee2Mnsf2KL9ZpWo"
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter**   | **Type**  | **Description** |
  | ---------- | :-------: | ------------------------------------------------------------ |
  | privateKey | HexString | Wallet’s private key, in plaintext or encrypted depending on the plainText parameter in the request, with 0x as the header. |
  | walletAddr |  Address  | Wallet Address |

## 3. bcb_walletImport

Sends a request to bcbXwallet_rpc to import a new wallet.

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_walletImport?name=_&privateKey=_&password=_&accessKey=_
  &plainText=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_walletImport",
    "params": {
        "name": "hotwal001",
        "privateKey": "0xbf7cbe09d71a1bc…99b7abd8f8fd73cb4",
        "password": "aBig62_123",
        "accessKey": "ASwDbde7X6z7nnTo2NVLrXF7JXevxA9iPeiTjforkCCB",
        "plainText": false
    }
  }
  ```

- **Request Parameters**

  | **Parameter**   | **Type**  | **Description** |
  | ---------- | :-------: | ------------------------------------------------------------ |
  | name       |  String   | Wallet name, 1-40 characters long, only upper case, lower case, digits, @, _, - , . allowed. |
  | privateKey | HexString | Encrypted private key, starting with 0x |
  | password   |  String   | Password for wallet,8-20 characters long（Any ASCII characters allowed, must contain at least one lower case, one upper case, one number, and one non-alphanumeric character) |
  | accessKey  |  String   | Access key, optional if plainText is true              |
  | plainText  |   Bool    | Indicates whether the privateKey is plaintext, true for plaintext, and false for ciphertext |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
     "walletAddr": "bcbES5d6kwoX4vMeNLENMee2Mnsf2KL9ZpWo",
     "accessKey": "ASwDbde7X6z7nnTo2NVLrXF7JXevxA9iPeiTjforkCCB"
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter**   | **Type** | **Description** |
  | ---------- | :------: | ------------------------------------------------------------ |
  | walletAddr | Address  | Wallet Address                                                   |
  | accessKey  |  String  | The wallet access key, which is randomly generated by the bcbXwallet_rpc service and used to encrypt the private key corresponding to the wallet. The key needs to be properly stored, as it can no longer be retrieved if lost. |

## 4. bcb_walletList

Sends a request to bcbXwallet_rpc to list out all the wallet information

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_walletList?pageNum=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_walletList",
    "params": {
        "pageNum": "1"
    }
  }
  ```

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | pageNum  |  uint64  | Paginate the results, default max 1000 per page |

- **Response SUCCESS Example**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
     "total": 2,
     "walletList": [
        {
          "name": "hotwal001",
          "walletAddr": "bcbES5d6kwoX4vMeNLENMee2Mnsf2KL9ZpWo"
        },
        {
          "name": "hotwal002",
          "walletAddr": "bcbLvBTGZCrLG3AMuyjD7eSqwQnBrq6CHc59"
        }
      ]
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter**   | **Type** | **Description** |
  | ---------- | :------: | ------------------------------------------------------------ |
  | total      |   Int    | Total number of wallets |
  | name       |  String  | Wallet name |
  | walletAddr | Address  | Wallet Address |

## 5. bcb_transfer

Sends a request to bcbXwallet_rpc to request a single transfer

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_transfer?name=_&accessKey=_&walletParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_transfer",
    "params": {
      "name": "hotwal001",
      "accessKey": "ASwDbde7X6z7nnTo2NVLrXF7JXevxA9iPeiTjforkCCB",
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

- **Request Parameters**

  | **Parameter**               | **Type** | **Description** |
  | ---------------------- | :------: | ------------------------------------------------------------ |
  | name                   |  String  | Wallet name                                                   |
  | accessKey              |  String  | Access key of wallet                                               |
  | walletParams {         |  Object  | Parameters for the transfer                                             |
  | &nbsp;&nbsp;smcAddress | Address  | The smart contract address corresponding to the traded currency (fiat or crypto) |
  | &nbsp;&nbsp;gasLimit   |  String  | Gas limit for the transaction                                             |
  | &nbsp; note            |  String  | Transaction note (max 255 characters)                                    |
  | &nbsp;&nbsp;to         | Address  | Address of recipient.                                         |
  | &nbsp;&nbsp;value      |  String  | Amount of currency transferred（Unit：Cong)                               |
  | }                      |          |                                                              |

- **Response SUCCESS Example**

  ```json
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

- **Response SUCCESS Parameters**

  | **Parameter** | **Type**  | **Description** |
  | -------- | :-------: | ------------------------------------------------------------ |
  | code     |    Int    | Transaction execution response code, 200 indicates success |
  | log      |  String   | Error message when response code is not 200 |
  | txHash   | HexString | Transaction hash, beginning with 0x |
  | height   |   Int64   | Height of the block that first confirmed this transfer |

## 6. bcb_transferOffline

Sends a request to bcbXwallet_rpc to transfer currency offline

- **Request URI over HTTPS**

  ```html
  https://localhost:37657/bcb_transferOffline?name=_&accessKey=_&walletParam=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcb_transferOffline",
    "params": {
      "name": "hotwal001",
      "accessKey": "ASwDbde7X6z7nnTo2NVLrXF7JXevxA9iPeiTjforkCCB",
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

- **Request Parameters**

  | **Parameter** | **Type** | **Description** |
  | ---------------------- | :------: | ------------------------------------------------------------ |
  | name                   |  String  | Wallet name                                                   |
  | accessKey              |  String  | Access key of wallet                                               |
  | walletParams {         |  Object  | Parameters for the transfer                                             |
  | &nbsp;&nbsp;smcAddress | Address  | The smart contract address corresponding to the traded currency (fiat or crypto)                          |
  | &nbsp;&nbsp;gasLimit   |  String  | Gas limit for the transaction                                             |
  | &nbsp; note            |  String  | Transaction note (max 255 characters) |
  | &nbsp;&nbsp;nonce      |  Uint64  | This value can be obtained through the ```bcb_nonce``` interface |
  | &nbsp;&nbsp;to         | Address  | Address of recipient. |
  | &nbsp;&nbsp;value      |  String  | Amount of currency transferred（Unit：Cong) |
  | } | | |

- **Response SUCCESS Example**

  ```json
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

- **Response SUCCESS Parameters**

  | **Parameter** | **Type** | **Description** |
  | -------- | :------: | ------------------------------------------------------------ |
  | tx       |  String  | Generated offline transaction data |
