

#  1 hdWallet_RPC及hdWallet本地命令详解

hdWallet是一个独立的命令行程序，提供了对rpc接口的本地调用封装。便于日常性的诊断、集成，不需要再去构造POST请求。

## 1.1 hdWallet_rpc 命令详解

<font color=red>注： 必须先生成助记词再启动RPC服务！</font>

### 1.1.1 createMnemonic

> 注：危险！：在使用HD钱包生成助记词之后必须进行助记词备份，否则钱包丢失或忘记密码后无法恢复钱包。

> 注：因为一个HD钱包可生成足够多私钥的属性，以及方便使用和管理，本版本只支持创建一次HD钱包。

- **command**

  ```
  ./hdWallet_rpc createMnemonic 
  ```

- **Input Parameters**

  | **选项** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
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

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | mnemonic |  String  | 12个助记词，以单个空格隔开。                                 |
  | password |  String  | 随机生成的新助记词密码。                                     |

注意：<font color=red>在生成助记词后，再调用./hdWallet_rpc开启客户端服务，两者无法同时开启。同样的，在./hdWallet_rpc下的changePassword/exportMnemonic/importMnemonic等命令也无法同时启动。</font>

### 1.1.2 exportMnemonic

- **command**

  ```
  hdWallet_rpc exportMnemonic --password 9FPqXE82XLHwmoqK2TNXV9Lg45fhXcUREESzoK7JCcnX 
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | password |  String  | 助记词密码。                                                 |

- **Output SUCCESS Example**

  ```
  {
    "mnemonic": "craft toilet twist safe violin catch similar add friend lion fabric crisp"
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | mnemonic |  String  | 12个助记词，以单个空格隔开。                                 |



### 1.1.3 importMnemonic

> 注：密码遗失后，只能重新导入助记词生成新的密码。

- **command**

  ```
  hdWallet_rpc importMnemonic --mnemonic “craft toilet ... crisp”
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | mnemonic |  String  | 12个助记词，以单个空格隔开。                                 |

- **Output SUCCESS Example**

  ```
  {
   "password":2oHQjWWKkGfUvWpeXV8qwgCTzrDh9fJ8hJV2L6gP6JeU
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | password |  String  | 随机生成新的助记词密码。                                     |



### 1.1.4 changePassword

- **command**

  ```
  hdWallet_rpc changePassword --password 2oHQjWWKkGfUvWpeXV8qwgCTzrDh9fJ8hJV2L6gP6JeU 
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | password |  String  | 助记词密码。                                                 |

- **Output SUCCESS Example**

  ```
  {
    "password":6eaN3vQjEW1ncCu4fYc9AvFFxFE4f4sY5HKw31X35zZ4
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | password |  String  | 随机生成的新助记词密码。                                     |



## 2 hdWallet命令详解

### 2.1. 命令运行格式

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

### 2.2 hdWallet命令详解

#### 2.2.1 walletCreate

- **command**

  ```
  hdWallet walletCreate --password 2oHQjWWKkGfUvWpeXV8qwgCTzrDh9fJ8hJV2L6gP6JeU [--path "m/44'/60'/0'/0/1"] [--url https://...]
  ```

- **Input Parameters**

  | **选项** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | password |  String  | 助记词密码。<font color=red>助记词密码生成过程参见hdWallet_rpc命令详解。</font> |
  | path     |  String  | <font color=red>HD钱包路径:"m/44'/60'/0'/0/#"</font>, 其中”#“为数字，范围：[0, 4294967295]。 |
  | url      |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |
  
- **Output FAILED Example**

  ```
  {
    "code": -32603,
    "message": "Invalid parameters.",
    "data": ""
  }
  ```

  注：所有命令执行错误返回格式相同，后面不再进行说明。

- **Output SUCCESS Example**

  返回：

  ```
  WalletCreate finish, [path=m/44'/60'/0'/0/1], [password=********]
  {
    "walletAddr": "localDhUdogRbcr8iT7hK8YJDdy6dRt2Nhm47g"
  }
  ```

- **Output SUCCESS Result**

  | **语法**   | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------- | :------: | ------------------------------------------------------------ |
  | walletAddr | Address  | 钱包地址。                                                   |

#### 2.2.2 transfer

- **command**

  ```
  hdWallet transfer [--password BYd...] [--path "m/44'/60'/0'/0/1"] --smcAddress bcbLVgb... --gasLimit 600 [--note hello] --to bcbLocFJG5Q792eLQXhvNkG417kwiaaoPH5a --value 1500000000 [--url https://...]
  ```
  
- **Request Parameters**

  | **语法**   | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------- | :------: | ------------------------------------------------------------ |
  | password   |  String  | HD钱包助记词密码。                                           |
  | path       |  String  | HD钱包路径:"m/44'/60'/0'/0/#", 其中”#“为数字。               |
  | smcAddress | Address  | 交易资产（本币或代币）的token地址。                          |
  | gasLimit   |  String  | 交易的燃料限                                                 |
  | note       |  String  | 交易备注（最长256字符），可选项。                            |
  | to         | Address  | 接收转账的账户地址。                                         |
  | value      |  String  | 转账的资产数量（单位：Cong）。                               |
  | url        |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |
  
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

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以 0x 开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |

#### 2.2.3 transferOffline

- **command**

  ```
  hdWallet transferOffline  [--password BYd...] [--path "m/44'/60'/0'/0/1"] 
  --smcAddress bcbLVgb... --gasLimit 600 [--note hello] --nonce 1500 --to bcbLocF... --value 1500000000 [--url https://...]
  ```

- **Request Parameters**

  | **语法**   | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------- | :------: | ------------------------------------------------------------ |
  | password   |  String  | HD钱包助记词密码。                                           |
  | path       |  String  | HD钱包路径:"m/44'/60'/0'/0/#", 其中”#“为数字。               |
  | smcAddress | Address  | 交易资产（本币或代币）的token地址。                          |
  | gasLimit   |  String  | 交易的燃料限制。                                             |
  | note       |  String  | 交易备注（最长256字符），可选项。                            |
  | nonce      |  String  | 交易计数值。                                                 |
  | to         | Address  | 接收转账的账户地址。                                         |
  | value      |  String  | 转账的资产数量（单位：Cong）。                               |
  | url        |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |
  
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

  | **语法**       | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------------- | :------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;tx |  String  | 生成的离线交易数据。                                         |

#### 2.2.4 blockHeight

- **command**

  ```
  hdWallet blockHeight [--url https://...]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | url      |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |

- **Output SUCCESS Example**

  ```
  {
      "lastBlock": 2500
  }
  ```

- **Output SUCCESS Result**

  | **语法**  | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | --------- | :------: | ------------------------------------------------------------ |
  | lastBlock |  Int64   | 最新区块高度。                                               |

#### 2.2.5 block

- **command**

  ```
  hdWallet block --height 68685 [--url https://...]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | height   |  int64   | 指定区块高度，为0时返回最新高度的区块信息。                  |
  | url      |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |

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

| **语法**          | **类型**     | **注释**                                              |
| ----------------- | ------------ | ----------------------------------------------------- |
| blockHeight       | Int64        | 区块高度。                                            |
| blockHash         | HexString    | 区块哈希值，以 0x 开头。                              |
| parentHash        | HexString    | 父区块哈希值，以 0x 开头。                            |
| chainID           | String       | 链ID。                                                |
| validatorsHash    | HexString    | 验证者列表哈希值，以 0x 开头。                        |
| consensusHash     | HexString    | 共识信息哈希值，以 0x 开头。                          |
| blockTime         | String       | 区块打包时间。                                        |
| blockSize         | Int          | 当前区块大小。                                        |
| proposerAddress   | Address      | 提案人地址。                                          |
| txs [             | Object Array | 交易列表。                                            |
| {                 | Object       | 交易参数。                                            |
| txHash            | HexString    | 交易哈希值，以 0x 开头。                              |
| txTime            | String       | 交易时间。                                            |
| code              | Uint32       | 交易结果码，200表示交易成功，其它值表示失败。         |
| log               | String       | 交易结果描述。                                        |
| blockHash         | HexString    | 交易所在区块哈希值，以 0x 开头。                      |
| blockHeight       | Int64        | 交易所在区块高度。                                    |
| from              | Address      | 交易签名人地址。                                      |
| nonce             | Uint64       | 交易签名人交易计数值。                                |
| gasLimit          | Uint64       | 最大燃料数量。                                        |
| fee               | Uint64       | 交易手续费（单位cong）。                              |
| note              | string       | 备注。                                                |
| messages [{       | Object Array | 消息列表。                                            |
| smcAddress        | Address      | 合约地址。                                            |
| smcName           | String       | 合约名称。                                            |
| method            | String       | 方法原型。                                            |
| to                | Address      | 转账目的账户地址，仅当交易是BRC20标准转账时有效。     |
| value             | string       | 转账金额（单位cong），仅当交易是BRC20标准转账时有效   |
| }]                |              |                                                       |
| transferReceipts[ | Object Array | 收据列表。                                            |
| {                 | Object       | 收据参数。                                            |
| token             | Address      | 代币地址                                              |
| from              | Address      | 交易签名人地址。                                      |
| to                | Address      | 转账目的账户地址，仅当交易是BRC20标准转账时有效。     |
| value             | bn.Number    | 转账金额（单位cong），仅当交易是BRC20标准转账时有效。 |
| note              | string       | 收据备注                                              |
| }                 |              |                                                       |
| ]                 |              |                                                       |

#### 2.2.6 transaction

- **command**

  ```
  hdWallet transaction --txHash 0x4E456161... [--url https://...]
  ```

- **Input Parameters**

  | **语法** | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :-------: | ------------------------------------------------------------ |
  | txHash   | HexString | 指定交易哈希值，以 0x 开头。                                 |
  | url      |  String   | 钱包服务地址，可选项，默认调用本地服务。                     |

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

  | **语法**                           |   **类型**   | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------------------------------- | :----------: | ------------------------------------------------------------ |
  | txHash                             |  HexString   | 交易哈希值，以 0x 开头。                                     |
  | txTime                             |    String    | 交易时间。                                                   |
  | code                               |    Uint32    | 交易结果码，200表示交易成功，其它值表示失败。                |
  | log                                |    String    | 交易结果描述。                                               |
  | blockHash                          |  HexString   | 交易所在区块哈希值，以 0x 开头。                             |
  | blockHeight                        |    Int64     | 交易所在区块高度。                                           |
  | from                               |   Address    | 交易签名人地址。                                             |
  | nonce                              |    Uint64    | 交易签名人交易计数值。                                       |
  | gasLimit&nbsp;                     |    Uint64    | 最大燃料数量。                                               |
  | fee                                |    Uint64    | 交易手续费（单位cong）。                                     |
  | note                               |    String    | 备注。                                                       |
  | messages [                         | Object Array | 消息列表。                                                   |
  | &nbsp;&nbsp;{                      |    Object    | 消息参数                                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;smcAddress |   Address    | 合约地址。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;smcName    |    String    | 合约名称。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;method     |    String    | 方法原型。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;to         |   Address    | 转账目的账户地址。                                           |
  | &nbsp;&nbsp;&nbsp;&nbsp;value      |    String    | 转账金额（单位cong）。                                       |
  | &nbsp;&nbsp;}                      |              |                                                              |
  | ]                                  |              |                                                              |

#### 2.2.7 balance

- **command**

  ```
  hdWallet balance --address bcbAkTD... [--url https://...]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | address  | Address  | 账户地址。                                                   |
  | url      |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |

- **Output SUCCESS Example**

  ```
  {
     "balance": "2500000000"
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | balance  |  String  | 账户余额（单位：Cong）。                                     |

#### 2.2.8 balanceOfToken

- **command**

  ```
  hdWallet balanceOfToken --address bcbAkTD... --tokenAddress bcbCsRX... --tokenNa
  me XT [--url https://...]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | 账户地址。                                                   |
  | tokenAddress | Address  | 代币地址，与代币名称可以二选一，两个都有时必须一致。         |
  | tokenName    |  String  | 代币名称，与代币地址可以二选一，两个都有时必须一致。         |
  | url          |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |

- **Output SUCCESS Example**

  ```
  {
     "balance": "2500000000"
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | balance  |  String  | 账户余额（单位：Cong）。                                     |

#### 2.2.9 allBalance

- **command**

  ```
  hdWallet allBalance --address bcbAkTD... [--url https://...]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | address  | Address  | 账户地址。                                                   |
  | url      |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |

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

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | tokenAddress | Address  | 代币地址。                                                   |
  | tokenName    |  String  | 代币名称。                                                   |
  | balance      |  String  | 账户余额（单位：Cong）。                                     |

#### 2.2.10 nonce

- **command**

  ```
  hdWallet nonce --address bcbAkTD... [--url https://...]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | address  | Address  | 账户地址。                                                   |
  | url      |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |

- **Output SUCCESS Example**

  ```
  {
    "nonce": 5000
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | nonce    |  Uint64  | 指定地址在区块链上可用的下一个交易计数值。                   |

#### 2.2.11 commitTx

- **command**

  ```
  hdWallet commitTx --tx "bcb<tx>.v2.AetboY... [--url https://...]"
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | tx       |  String  | 交易数据。                                                   |
  | url      |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |

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

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易校验/背书结果代码，200表示成功。                         |
  | &nbsp;&nbsp;log    |  String   | 对交易校验/背书结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以 0x 开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |

#### 2.2.12 setConfigPath

- **command**

  ```
  hdWallet setConfigPath --configPath "./.config"
  ```

- **Input Parameters**

  | **语法**   | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------- | :------: | ------------------------------------------------------------ |
  | configPath |  String  | 钱包配置文件地址，可选项，默认设置为同级目录下.config中。    |

- **Output SUCCESS Example**

  ```
  Starting RPC HTTP server on tcp://0.0.0.0:37657
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | version  |  String  | 当前程序版本号。                                             |









