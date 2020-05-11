# bcc

bcc：可以查询链上信息，发交易，执行组合、合约等操作

## 1. 使用方法

命令运行格式如下：

```
Usage:
  bcc [command]

Available Commands:
  balance        Query balance information
  block          Query block information
  blockHeight    Query BlockChain current block height
  call           Call contract method
  commit         Commit transaction
  deployContract Deploy smart contract
  help           Help about any command
  nonce          Query account nonce
  registerOrg    Register organization
  registerToken  Register token
  transfer       transfer token to someone with value
  tx             Query transaction information
  version        Query version information

Flags:
  -h, --help   help for bcc

Use "bcc [command] --help" for more information about a command.
```

## 2. 命令详解

### 2.1 registerOrg

- 功能描述：注册组织

- **command**

  ```
  bcc registerOrg --name hotwal001 --password aBig62_123 --orgName example --gasLimit 1000000 [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | orgName      |  String  | *组织名称。                                                  |
  | gasLimit     |  String  | *交易的燃料限制。                                            |
  | note         |  String  | [选填]交易备注。                                             |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "orgID": "orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希。                                                 |
  | orgID              |  String   | 组织ID。                                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 2.2 setOrgSigners

- 功能描述：设置组织公钥

- **command**

  ```
  bcc setOrgSigners --name hotwal001 --password aBig62_123 --orgName example --pubKeys ["0x..."] --gasLimit 1000000 [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | orgName      |  String  | *组织名称。                                                  |
  | gasLimit     |  String  | *交易的燃料限制。                                            |
  | pubKeys      |  String  | *公钥列表。                                                  |
  | note         |  String  | [选填]交易备注。                                             |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希,以“0x”开头。                                      |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 2.3 setOrgDeployer

- 设置组织下部署合约权限

- **command**

  ```
  bcc setOrgDeployer --name hotwal001 --password aBig62_123 --orgName example --deployer local... --gasLimit 1000000 [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | orgName      |  String  | *组织名称。                                                  |
  | gasLimit     |  String  | *交易的燃料限制。                                            |
  | deployer     | Address  | *发布账号地址。                                              |
  | note         |  String  | [选填]交易备注。                                             |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希, 以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 2.4 deployContract

- 功能描述：部署合约

- **command**

  ```
  bcc deployContract --name hotwal001 --password aBig62_123 --contractName dice2win --version 2.0 --orgName genesis --codeFile ./example.tar.gz --effectHeight 100 --owner bcbES5d6kwoX4vMeNLENMee2Mnsf2KL9ZpWo --gasLimit 10000 [--chainid bcb] [--note ...] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | contractName |  String  | *合约名称。                                                  |
  | version      |  String  | *合约版本。                                                  |
  | orgName      |  String  | *组织名称。                                                  |
  | codeFile     |  String  | *合约源码文件路径。                                          |
  | effectHeight |  Uint64  | *合约生效高度。                                              |
  | owner        | Address  | *所有者地址。                                                |
  | gasLimit     |  String  | *交易的燃料限制。                                            |
  | note         |  String  | [选填]交易备注。                                             |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]钱包文件访问路径，默认为"./.keystore"。                |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "smcAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | smcAddress         |  Address  | 部署的合约的合约地址。                                       |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 2.5 registerToken

- 功能描述：注册代币

- **command**

  ```
  bcc registerToken --name hotwal001 --password aBig62_123 --tokenName xt --tokenSymbol xt --totalSupply 1000000000000 --addSupplyEnabled true --burnEnabled true --gasPrice 2500 --gasLimit 10000 [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**         | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------------- | :------: | ------------------------------------------------------------ |
  | name             |  String  | *钱包名称。                                                  |
  | password         |  String  | *钱包密码。                                                  |
  | tokenName        |  String  | *代币名称。                                                  |
  | tokenSymbol      |  String  | *代币符号。                                                  |
  | totalSupply      |  Number  | *代币发行总量。                                              |
  | addSupplyEnabled |   Bool   | *代币是否可增发标志。                                        |
  | burnEnabled      |   Bool   | *代币是否可燃烧标志。                                        |
  | gasPrice         |  Int64   | *燃料价格。                                                  |
  | gasLimit         |  String  | *交易的燃料限制。                                            |
  | note             |  String  | [选填]交易备注。                                             |
  | chainid          |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath     |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "tokenAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | tokenAddress       |  Address  | 代币地址。                                                   |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 2.6 transfer

- 功能描述：转账交易

- **command**

  ```
  bcc transfer --name hotwal001 --password aBig62_123 --token bcb 
  --gasLimit 600 [--note hello] --to bcbLocFJG5Q792eLQXhvNkG417kwiaaoPH5a --value 1500000000 [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Request Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | token        |  String  | *交易的资产（本币或代币）对应的名称。                        |
  | gasLimit     |  String  | *交易的燃料限制。                                            |
  | note         |  String  | [选填]交易备注（最长256字符），默认为空。                    |
  | to           | Address  | *接收转账的账户地址。                                        |
  | value        |  String  | *转账的资产数量（单位：Cong）。                              |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
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
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 2.7 call

- 功能描述：根据组织名、合约名调取合约方法

- **command**

  ```
  bcc call --name hotwal001 --password aBig62_123 --orgName example --contract dice2win --method placeBet --gasLimit 5000 [--splitBy @] [--params @ --paramsFile ./params] [--note ...]  [--pay 1.003(loc)] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包访问密码。                                              |
  | orgName      |  String  | *组织名称。                                                  |
  | contract     |  String  | *合约名称。                                                  |
  | gasLimit     |  Int64   | *交易的燃料限制。                                            |
  | note         |  String  | [选填]交易备注，内容自定义。                                 |
  | method       |  String  | *方法名称。                                                  |
  | params       |  String  | [与paramsFile二选一]输入参数值列表，规则见*输入参数格式规定*。 |
  | paramsFile   |  String  | [与params二选一]输入参数值列表所在文件。                     |
  | splitBy      |  String  | [选填]分隔符，默认为"#"。                                    |
  | pay          |  String  | [选填]如遇调用合约方法前需要转账时，可使用该选项标注需要转账的数量和币种，该选项标注的值只向合约账户转账，默认为空。 |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **输入参数格式规定**

  1. 参数顺序必须与方法的输入参数顺序一致并且使用选定的分隔符分隔；
  2. 如果输入参数中包含"\\"，则需要输入双反斜杠"\\\\"；
  3. 当输入类型为字节/字节切片时，将字节/字节切片转换为0x开头的十六进制字符串后输入；
  4. 当输入类型为map时，按json串格式输入，且双引号前加反斜线，如：{\\"key1\\":\\"value1\\",\\"key2\\":\\"value2\\"}（key和value之间不能有额外的空格，如{"test": 123}则为错误格式）;
  5. 如果输入字符串值中含有双引号，则需要在双引号前加反斜线，否则命令行无法正确输入双引号；
  6. 如果输入参数过长导致超过命令行长度限制，则按如上规则将输入参数列表写入文件，并使用--file选项标注输入参数文件路径。

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389E
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 2.8 contractInfo

- 功能描述：查询合约信息
- 模式：(orgName+contractName=指定合约信息);(orgID+contractName=指定合约信息)<br>(contractAddr=指定合约信息);(无参数=打印所有合约地址)

- **command**

```
bcc contractInfo [--orgName example] [--orgID orgBtjf...] [--contractName mydice2win]
[--contractAddr localKkpg...]
```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | orgName      |  String  | *组织名称。                                                  |
  | contractName |  String  | *合约名称。                                                  |
  | orgID        |  String  | *组织ID                                                      |
  | contractAddr | Address  | *合约地址                                                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: 
    Version: "1.0"
    Name: "mydice2win"
    OrgID: "orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer"
    Address: "local2H5hxpzfuDqvd2uc8DqhF5sgwe7GyDEGP"
    Account: "localKkpgMAtPE9wUvtdY9xnN31zRVP3AaoJwA"
    Owner: "localL9BzYNYns5VCRaJgfHEBJLzS1bhpHjx7j"
    CodeHash: "61BEDF2AFB9CABCBAF0FC104C9C675DD4A522AA39DE07E696F40E84317711B9A"
    EffectHeight: 34
    LoseHeight: 0
    KeyPrefix: "/orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer/mydice2win"
    Token: ""
    Interfaces: [
    {
      "methodId": "d517c92",
      "gas": 400,
      "prototype": "PlaceBet(bn.Number,int64,int64,[]byte,[]byte,types.Address)"
    }
  ]
    Method: 
      SetSecretSigner(types.PubKey)
      Params： 01bd6c29d63f5f32aa33955f26a28459988edea4de517f77372e77db33958e6e
  
      SetSettings(string)
      Params： example
  
      SetRecvFeeInfos(string)
      Params： example
  
      WithdrawFunds(string,types.Address,bn.Number)
      Params： example@localL9BzYNYns5VCRaJgfHEBJLzS1bhpHjx7j@1000000000000
  
      PlaceBet(bn.Number,int64,int64,[]byte,[]byte,types.Address)
      Params： 1000000000000@200000@200000@0x01bd6c29d63f5f32aa33955f26a28459988edea4de517f77372e77db33958e6e@0x01bd6c29d63f5f32aa33955f26a28459988edea4de517f77372e77db33958e6e@localL9BzYNYns5VCRaJgfHEBJLzS1bhpHjx7j
  
      SettleBet([]byte)
      Params： 01bd6c29d63f5f32aa33955f26a28459988edea4de517f77372e77db33958e6e
  
      RefundBet([]byte)
      Params： 01bd6c29d63f5f32aa33955f26a28459988edea4de517f77372e77db33958e6e
  
  PS: If the string is just a string, Example: "example"
   If the string is a special string, Example: "recvFeeRatio":[500,500], "recvFeeAddr":["localKrHJUVGAt4R9gcfsBthu3dWJR7bAYq1c8","localNwdwjpDotDDLGiB9pARk1CcSM71bdgTef"]
  
  ```

- **Output SUCCESS Result**

  | **语法**                                                    |   **类型**    | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ----------------------------------------------------------- | :-----------: | ------------------------------------------------------------ |
  | Version                                                     |    string     | 合约所有迭代版本                                             |
  | Name                                                        |    string     | 合约名称                                                     |
  | OrgID                                                       |    string     | 组织ID                                                       |
  | Address                                                     | types.Address | 合约地址                                                     |
  | Account                                                     | types.Address | 合约的账户地址                                               |
  | Owner                                                       | types.Address | 合约拥有者的账户地址                                         |
  | CodeHash                                                    |  types.Hash   | 合约代码的哈希。                                             |
  | EffectHeight                                                |     int64     | 合约生效的区块高度                                           |
  | LoseEffect                                                  |     int64     | 合约失效的区块高度                                           |
  | KeyPrefix                                                   |    string     | 合约在状态数据库中KEY值的前缀                                |
  | Token                                                       | types.Address | 合约代币地址                                                 |
  | Interfaces                                                  |   []Method    | 合约提供的跨合约调用的方法列表                               |
  | Method                                                      |   []Method    | 合约对外提供接口的方法列表                                   |
  | SetSecretSigner(types.PubKey)                               |    String     | SetSecretSigner方法原型。                                    |
  | SetSettings(string)                                         |    String     | SetSettings方法原型。                                        |
  | SetRecvFeeInfos(string)                                     |    String     | SetRecvFeeInfos方法原型。                                    |
  | WithdrawFunds(string,<br/>types.Address,bn.Number)          |    String     | WithdrawFunds方法原型。                                      |
  | PlaceBet(bn.Number,int64,int64,[]byte,[]byte,types.Address) |    String     | PlaceBet方法原型。                                           |
  | SettleBet([]byte)                                           |    String     | SettleBet方法原型。                                          |
  | RefundBet([]byte)                                           |    String     | RefundBet方法原型。                                          |



### 2.8 blockHeight

- 功能描述：查询区块高度

- **command**

  ```
  bcc blockHeight  [--chainid bcb]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | chainid  |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
      "lastBlock": 2500
  }
  ```

- **Output SUCCESS Result**

  | **语法**  | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | --------- | :------: | ------------------------------------------------------------ |
  | lastBlock |  Int64   | 最新区块高度。                                               |



### 2.9 block

- 功能描述：查询指定区块信息

- **command**

  ```
  bcc block [--height 2500]|[--rt "2019-05-10 09:37:14"] [--chainid bcb] 
  bcc block [--height 2500]|[--rt "2019-05-10 09:37:14"] [--num 3] [--chainid bcb]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | height   |  int64   | 指定区块高度。                                               |
  | rt       |  string  | 指定区块时间，采用UTC时间，返回的区块时间大于并且最接近输入时间的区块。 |
  | num      |  int64   | 指定区块数量，为空的话返回一个区块详细信息，否则返回多个区块的简要信息。 |
  | chainid  |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |

  注：时间和高度是互斥参数；如果高度和时间为空，返回最新区块信息。

- **Output SUCCESS Example1**（详细信息）

  ```
  OK
  Response: {
    "blockHeight": 2500,
    "blockHash": "0x476dc319f4d3ad9b8c4c4ab03edcc100bb7c90da",
    "parentHash": "0x95880ac3be0a89aa2c82fa5e9dadf95a0e99dc3c",
    "chainID": "test",
    "validatorHash": "0x771543e3773dfebdcc5f3d4ce42c39c29a543218",
    "consensusHash": "0xf66ef1df8ba6dac7a1ecce40cc84e54a1cebc6a5",
    "blockTime": "2019-05-10 09:37:14.923456881 +0000 UTC",
    "blockSize": 988,
    "proposerAddress": "testHs1N4Yudisgo5pqZw8AXE66Taq776H3PK",
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
        "note":"hello",
        "messages": [
          {
           "smcAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
           "smcName": "token-basic",
           "method": "Transfer(smc.Address,big.Int)smc.Error",
           "to": "bcbKuqW1qdsnD7mRsRooXMEkCBj2s9GLF9pn",
           "value": "683000000000"
          }
        ]
      }
    ]
  }
  ```

- **Output SUCCESS Example2**（简要信息）

```
OK
Response: {
 "result": [
 	{
 	 "blockHeight": 2500,
	 "blockHash": "0x95880AC3BE0A89AA2C82FA5E9DADF95A0E99DC3C",
 	 "blockTime": "2019-05-10T09:37:14.923456881Z",
  	},
  	{
 	 "blockHeight": 2501,
	 "blockHash": "0x476DC319F4D3AD9B8C4C4AB03EDCC100BB7C90DA",
 	 "blockTime": "2019-05-10T09:39:16.234023422Z",
  	},
  	{
 	 "blockHeight": 2502,
	 "blockHash": "0xCF499509BF839A3083B954F409742C3C9AF93367",
 	 "blockTime": "2019-05-10T09:41:17.544988709Z",
  	}
  ]
}
```

- **Output SUCCESS Result**

  | **语法**                                       |   **类型**   | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------------------------------------------- | :----------: | ------------------------------------------------------------ |
  | blockHeight                                    |    Int64     | 区块高度。                                                   |
  | blockHash                                      |  HexString   | 区块哈希值，以“0x”开头。                                     |
  | parentHash                                     |  HexString   | 父区块哈希值，以“0x”开头。                                   |
  | chainID                                        |    String    | 链ID。                                                       |
  | validatorsHash                                 |  HexString   | 验证者列表哈希值，以“0x”开头。                               |
  | consensusHash                                  |  HexString   | 共识信息哈希值，以“0x”开头。                                 |
  | blockTime                                      |    String    | 区块打包时间。                                               |
  | blockSize                                      |     Int      | 当前区块大小。                                               |
  | proposerAddress                                |   Address    | 提案人地址。                                                 |
  | txs [                                          | Object Array | 交易列表。                                                   |
  | &nbsp;&nbsp;{                                  |    Object    | 交易参数。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;txHash                 |  HexString   | 交易哈希值，以“0x”开头。                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;txTime                 |    String    | 交易时间。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;code                   |    Uint32    | 交易结果码，200表示交易成功，其它值表示失败。                |
  | &nbsp;&nbsp;&nbsp;&nbsp;log                    |    String    | 交易结果描述。                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHash              |  HexString   | 交易所在区块哈希值，以“0x”开头。                             |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHeight            |    Int64     | 交易所在区块高度。                                           |
  | &nbsp;&nbsp;&nbsp;&nbsp;from                   |   Address    | 交易签名人地址。                                             |
  | &nbsp;&nbsp;&nbsp;&nbsp;nonce                  |    Uint64    | 交易签名人交易计数值。                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;gasLimit&nbsp;         |    Uint64    | 最大燃料数量。                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;fee                    |    Uint64    | 交易手续费（单位cong）。                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;note                   |    String    | 备注。                                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;messages [             | Object Array | 消息列表。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smcAddress |   Address    | 合约地址。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smcName    |    String    | 合约名称。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;method     |    String    | 方法原型。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to         |   Address    | 转账目的账户地址，仅当交易是BRC20标准转账时有效。            |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value      |    String    | 转账金额（单位cong），仅当交易是BRC20标准转账时有效。        |
  | &nbsp;&nbsp;}                                  |              |                                                              |
  | ]                                              |              |                                                              |



### 2.10 transaction

- 功能描述：查询交易信息

- **command**

  ```
  bcc tx --txHash 0x4E456161... [--chainid bcb]
  ```

- **Input Parameters**

  | **语法** | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :-------: | ------------------------------------------------------------ |
  | txHash   | HexString | *指定交易哈希值，以“0x”开头。                                |
  | chainid  |  String   | [选填]链ID，默认以配置文件中的配置为准。                     |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "txHash": "0xc2d613b000c56b53099b3668664c44f1395406a6e8b8f288fb0e045f72a3c83c",
    "txTime": "2019-05-08 09:38:05.521987701 +0000 UTC",
    "code": 200,
    "log": "",
    "blockHash": "0xd4f0257eb95de4c2584013f84acf6ae5311bca91",
    "blockHeight": 86,
    "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
    "nonce": 11,
    "gasLimit": 600,
    "fee": 1250000,
    "note": "",
    "messages": [
      {
        "smcAddress": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
        "smcName": "token-basic",
        "method": "Transfer(types.Address,bn.Number)",
        "to": "local3pw2Lgbb83JV5HpoRhM5eCCYS4jtoxxJx",
        "value": "150000000000000"
      }
    ],
    "tags": {
      "/0/std::fee": {
        "Name": "std::fee",
        "ContractAddr": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidmFsdWUiOjEyNTAwMDB9",
        "ReceiptHash": "18B3A7A65CA224B94C90200EC59029B3E94D8A74D853052E67F8F657BD95FB66",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": null,
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 1250000
        }
      },
      "/1/std::transfer": {
        "Name": "std::transfer",
        "ContractAddr": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbDNwdzJMZ2JiODNKVjVIcG9SaE01ZUNDWVM0anRveHhKeCIsInZhbHVlIjoxNTAwMDAwMDAwMDAwMDB9",
        "ReceiptHash": "BB599A08525D3F8293B3695E1C79B05316BE0C0B5B2FE24F4E67CB5C686A27C8",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "local3pw2Lgbb83JV5HpoRhM5eCCYS4jtoxxJx",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 150000000000000
        }
      },
      "/2/totalFee": {
        "Name": "totalFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidmFsdWUiOjEyNTAwMDB9",
        "ReceiptHash": "F1359BC1665022CB77DA69FCCFA4AC60FA0FD00CE09CB897830083E76F7E31E6",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": null,
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 1250000
        }
      },
      "/3/transferFee": {
        "Name": "transferFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbDhMdFQ4QW9uV2dKOG5NQ0VkQVI1VUdyYlJmVW11b2VpeiIsInZhbHVlIjoyNTAwMDB9",
        "ReceiptHash": "D872750193DA93BA345DE11A546CBA0BD6A7AE3F68745C537CECE432A047ADDD",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "local8LtT8AonWgJ8nMCEdAR5UGrbRfUmuoeiz",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 250000
        }
      },
      "/4/transferFee": {
        "Name": "transferFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbEVtbUxrNEdpSkNrWk5aY0hoVENYaWhFWm9MSmRENG9RRCIsInZhbHVlIjoyNTAwMDB9",
        "ReceiptHash": "21AA7212F6F9BCB38C01FDC8C0F2CD82A47068DCD535389F34E7493F9CED9571",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "localEmmLk4GiJCkZNZcHhTCXihEZoLJdD4oQD",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 250000
        }
      },
      "/5/transferFee": {
        "Name": "transferFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbEhZRHdSU29ORXlDc1o4S1lhdnlSQlpzR0hEN2lMeGpuWCIsInZhbHVlIjozNzUwMDB9",
        "ReceiptHash": "90B62B8DCBA1E351452D0C0FD430E83C84FDF89CC580022C93B0476B3CD86068",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "localHYDwRSoNEyCsZ8KYavyRBZsGHD7iLxjnX",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 375000
        }
      },
      "/6/transferFee": {
        "Name": "transferFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbHpWdDNwZmU3NWN1VmR2d3paTGtBU1FzS2MzYmY5M2ZpIiwidmFsdWUiOjM3NTAwMH0=",
        "ReceiptHash": "8E95324BA76072616AFE77B99A9CB7BD477BFEFAAFB3C1162DC77689EAA95560",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "localzVt3pfe75cuVdvwzZLkASQsKc3bf93fi",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 375000
        }
      }
    }
  }
  ```

- **Output SUCCESS Result**

  | **语法**       |        **类型**        | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------------- | :--------------------: | ------------------------------------------------------------ |
  | txHash         |       HexString        | 交易哈希值，以“0x”开头。                                     |
  | txTime         |         String         | 交易时间。                                                   |
  | code           |         Uint32         | 交易结果码，200表示交易成功，其它值表示失败。                |
  | log            |         String         | 交易结果描述。                                               |
  | blockHash      |       HexString        | 交易所在区块哈希值，以“0x”开头。                             |
  | blockHeight    |         Int64          | 交易所在区块高度。                                           |
  | from           |        Address         | 交易签名人地址。                                             |
  | nonce          |         Uint64         | 交易签名人交易计数值。                                       |
  | gasLimit&nbsp; |         Uint64         | 最大燃料数量。                                               |
  | fee            |         Uint64         | 交易手续费（单位cong）。                                     |
  | note           |         String         | 备注。                                                       |
  | messages       |      Object Array      | 消息列表。                                                   |
  | smcAddress     |        Address         | 合约地址。                                                   |
  | smcName        |         String         | 合约名称。                                                   |
  | method         |         String         | 方法原型。                                                   |
  | to             |        Address         | 转账目的账户地址，仅当交易是BRC20标准转账时有效。            |
  | value          |         String         | 转账金额（单位cong），仅当交易是BRC20标准转账时有效。        |
  | Tags           |        []string        | 收据列表 。                                                  |
  | Name           |         string         | 收据名称。                                                   |
  | ContractAddr   |         string         | 合约地址。                                                   |
  | ReceiptBytes   |         []byte         | 收据数据原型。                                               |
  | ReceiptHash    |         string         | 收据hash。                                                   |
  | Receipt        | map[string]interface{} | 收据解析结果。                                               |
  | from           |         string         | 交易签名人地址。                                             |
  | to             |         string         | 每笔收据的目的账户地址。                                     |
  | token          |         string         | 代币地址。                                                   |
  | value          |         string         | 每笔收据的金额。                                             |



### 2.11 balance

- 功能描述：查询账户余额

- **command**

  ```
  bcc balance [--address bcbAkTD... | --name hotwal-001 --password aBig62_123] [--token bcb] [--all false] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | [与钱包信息二选一]账户地址，默认为空。                       |
  | name         |  String  | [与账户地址二选一]钱包名称，默认为空。                       |
  | password     |  String  | [与账户地址二选一]钱包密码，默认为空。                       |
  | token        |  String  | [选填]代币名称，默认为基础代币。                             |
  | all          |   Bool   | [选填]是否查询所有资产余额标记，默认为false。                |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]访问钱包路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: [
    {
      "tokenAddress": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
      "tokenName": "LOC",
      "balance": "119997371250000"
    }
  ]
  ```

- **Output SUCCESS Result**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | token        |  String  | 代币名称。                                                   |
  | tokenAddress |  String  | 代币地址。                                                   |
  | balance      |  String  | 账户余额（单位：Cong）。                                     |



### 2.12 nonce

- 查询nonce值

- **command**

  ```
  bcc nonce [--address bcbAkTD... | --name hotwal-001 --password aBig62_123]  [--chainid local] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | [与钱包二选一]账户地址。                                     |
  | name         |  String  | [与账户地址二选一]钱包地址。                                 |
  | password     |  String  | [与账户地址二选一]钱包密码                                   |
  | chainid      |  String  | [选填]链ID，默认值以配置文件中的配置为准。                   |
  | keystorepath |  String  | [选填]访问钱包路径，默认"./.keystore"                        |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "nonce": 5000
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | nonce    |  Uint64  | 指定地址在区块链上可用的下一个交易计数值。                   |



### 2.13 commitTx

- 功能描述：提交交易数据

- **command**

  ```
  bcc commitTx [--tx bcb<tx>.v1.AetboY...] [--file xxxxx] [--chainid bcb] 
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | tx       |  String  | 交易数据。                                                   |
  | chainid  |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | file     |  String  | 交易数据文件（文本文件），一行一个交易。                     |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
     "code": 200,
     "log": "Deliver tx succeed",
     "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
     "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易校验/背书结果代码，200表示成功。                         |
  | &nbsp;&nbsp;log    |  String   | 对交易校验/背书结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 2.14 version

- 功能描述：查询版本信息

- **command**

  ```
  bcc version [--chainid bcb] 
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | chainid  |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
  	version: 1.0.7.9636
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | version  |  string  | 当前程序版本号。                                             |



### 2.15 runAsRPCService

- 功能描述：启动RPC服务

- **command**

  ```
  bcc runAsRPCService
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | ——                                                           |

- **Output SUCCESS Example**

  ```
  OK
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | ——                                                           |



### 2.15 query

- 功能描述：根据指令查询指定信息

- **command**

  ```
  bcc query [--path /contract/all/0] [--chainid bcb]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | path     |  string  | [必填]查询指定信息的key。                                    |
  | chainid  |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |

- **Output SUCCESS Example**

  ```
  OK
  response: {
     "code"	:  200
     "key"	:  "L2NvbnRyYWN0L2FsbC8w"
     "value"  :	"WyJ0ZXN0NVpYaG8zdUw1WlNCV3BIMmlmbmJzQmFRY3k1NTNnWDhGIiwidGVzdEFSUlZm
  				na3V4ekE1VlpGaGhvNjUxYkZGZ21ncyIsInRlc3Q2cnlWS1NnZFpCZ2NnUjNhV2djbWRa
   				WEpLaDFRSnoiLCJ0ZXN0QWlXdXNuc0ZzVVFXa2ZIR1NLNXpoNjNGb3pDUFY1UGlCIiwid
   				Es2a2pnQ2tBQm5TVFMxTUI4NkNpeEVRV005Nlpic1A5IiwidGVzdFA4ZEMyUHVCcHNVQ
   				Dhqb0t1RjFFdXpaTFhGbXg1NyJd"
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | code     |   Int    | 交易校验/背书结果代码，200表示成功。                         |
  | key      |  string  | base64编码格式的String，由输入的参数（path）编码而成。       |
  | value    |  string  | base64编码格式的String，由输出的结果编码而成。               |



### 2.16 solDeploy

- 功能描述：根据指令查询指定信息

- **command**

  ```
  bcc solDeploy --name hotwal001 --password aBig62_123 --gasLimit 1000000 [--tokenAddr bcbaabdf...]|[--tokenName bcb] [--abiFile ./test.abi] [--binFile ./test.bin]|[--sourceFile ./test.sol] [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**         | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------------- | :------: | ------------------------------------------------------------ |
  | name             |  String  | *钱包名称。                                                  |
  | password         |  String  | *钱包密码。                                                  |
  | tokenName        |  String  | 合约绑定的代币名称。                                         |
  | tokenAddr        |  String  | [与tokenName二选一]合约绑定的代币名称。                      |
  | abiFile          |  Number  | 合约abi文件的路径                                            |
  | addSupplyEnabled |   Bool   | 合约binCode文件的路径                                        |
  | burnEnabled      |  string  | [与binFile二选一]合约源码文件路径                            |
  | gasLimit         |  String  | *交易的燃料限制。                                            |
  | note             |  String  | [选填]交易备注。                                             |
  | chainid          |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath     |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "",
    "fee": 1039902500,
    "txHash": "0x0041656D5CA3DC79451B8FAB431902E3EDF1A7913840A2CFDEBAB049A2717288",
    "height": 48980,
    "data": "localGP7ktCj3HwY14EQQZPXxNTWhkL3G4QvDP"
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |
  | data               |  Address  | 合约地址                                                     |



### 2.16 solCall

- 功能描述：根据指令查询指定信息

- **command**

  ```
  bcc solCall --name hotwal001 --password aBig62_123 --gasLimit 1000000 --contractAddr bcbGP7ktCj3HwY1... --method getValue [--paramsArr hello] [--abiFile ./test.abi] [--value 1000] [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **语法**         | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------------- | :------: | ------------------------------------------------------------ |
  | name             |  String  | *钱包名称。                                                  |
  | password         |  String  | *钱包密码。                                                  |
  | contractAddr     |  String  | *合约地址。                                                  |
  | method           |  String  | [与tokenName二选一]合约绑定的代币名称。                      |
  | abiFile          |  Number  | 合约abi文件的路径                                            |
  | addSupplyEnabled |   Bool   | 合约参数                                                     |
  | burnEnabled      |  string  | 转账的资产数量。                                             |
  | gasLimit         |  String  | *交易的燃料限制。                                            |
  | note             |  String  | [选填]交易备注。                                             |
  | chainid          |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath     |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "",
    "fee": 3607500,
    "txHash": "0x7B57ECDD0744618881C84B7E8951FD1EC8CFC2743A97082E05A8FDA9A93B1278",
    "height": 49092,
    "data": "0000000000000000000000000000000000000000000000000000000000000040"
  }
  
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |
  | data               |  Address  | 函数返回值                                                   |



## 3. 接口详解



### 3.1 registerOrg

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_registerOrg?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_registerOrg",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123",
        "bccParams": {
        	  "gasLimit": "1000000",
        	  "note": "",
            "orgName": "example",
            "chainID": "bcb",
            "keyStorePath": "./.keystore"
      	}
    	}
  }
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | orgName      |  String  | *组织名称。                                                  |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "orgID": "orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer",
    "height": 234389
  }
  
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | orgID              |  String   | 组织ID。                                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 3.2 setOrgSigners

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_setOrgSigners?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_setOrgSigners",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123",
        "bccParams": {
        	  "gasLimit": "1000000",
        	  "note": "",
            "orgName": "example",
            "pubKeys": ["0x..."],
            "chainID": "bcb",
            "keyStorePath": "./.keystore"
      	}
    	}
  }
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | orgName      |  String  | *组织名称。                                                  |
  | gasLimit     |  String  | *交易的燃料限制。                                            |
  | pubKeys      |  String  | *公钥列表。                                                  |
  | note         |  String  | [选填]交易备注。                                             |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 3.3 setOrgDeployer

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_setOrgDeployer?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_setOrgDeployer",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123",
        "bccParams": {
        	  "gasLimit": "1000000",
        	  "note": "",
            "orgName": "example",
            "deployer": local...,
            "chainID": "bcb",
            "keyStorePath": "./.keystore"
      	}
    	}
  }
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | orgName      |  String  | *组织名称。                                                  |
  | gasLimit     |  String  | *交易的燃料限制。                                            |
  | deployer     | Address  | *发布账号地址。                                              |
  | note         |  String  | [选填]交易备注。                                             |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 3.4 deployContract

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_deployContract?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_deployContract",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123",
        "bccParams": {
        	  "gasLimit": "100000",
        	  "note": "",
            "contractName": "dice2win",
            "version": "1.0",
            "orgName": "genesis",
            "codeFile": "./example.tar.gz",
            "effectHeight": 100,
            "owner": "bcbES5d6kwoX4vMeNLENMee2Mnsf2KL9ZpWo",
            "chainID": "bcb",
            "keyStorePath": "./.keystore"
      	}
    	}
  }
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | contractName |  String  | *合约名称。                                                  |
  | version      |  String  | *合约版本。                                                  |
  | orgName      |  String  | *组织名称。                                                  |
  | codeFile     |  String  | *合约源码文件路径。                                          |
  | effectHeight |  Uint64  | *合约生效高度。                                              |
  | owner        | Address  | *所有者地址。                                                |
  | gasLimit     |  int64   | *交易的燃料限制。                                            |
  | note         |  String  | [选填]交易备注。                                             |
  | chainID      |  String  | [选填]链ID。                                                 |
  | keystorepath |  String  | [选填]钱包文件访问路径，默认为"./.keystore"。                |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "smcAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | smcAddress         |  Address  | 部署的合约的合约地址。                                       |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 3.5 registerToken

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_registerToken?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_registerToken",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123",
        "bccParams": {
            "tokenName": "tx",
            "tokenSymbol": "tx",
            "totalSupply": "1000000000",
            "addSupplyEnabled": true,
            "burnEnabled": true,
            "gasPrice": 2500,
            "gasLimit": "100000",
        	  "note": "",
            "chainID": "bcb",
            "keyStorePath": "./.keystore"
      	}
    	}
  }
  ```

- Input Parameters**

  | **语法**         | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------------- | :------: | ------------------------------------------------------------ |
  | name             |  String  | *钱包名称。                                                  |
  | password         |  String  | *钱包密码。                                                  |
  | tokenName        |  String  | *代币名称。                                                  |
  | tokenSymbol      |  String  | *代币符号。                                                  |
  | totalSupply      |  Number  | *代币发行总量。                                              |
  | addSupplyEnabled |   Bool   | *代币是否可增发标志。                                        |
  | burnEnabled      |   Bool   | *代币是否可燃烧标志。                                        |
  | gasPrice         |  Int64   | *燃料价格。                                                  |
  | keystorepath     |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "tokenAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
    "height": 234389
  }
  
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | tokenAddress       |  String   | 代币地址。                                                   |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 3.6 transfer

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_transfer?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_transfer",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123",
        "bccParams": {
            "token": "bcb",
            "gasLimit": "1000",
            "note": "",
            "to": "bcbLocFJG5Q792eLQXhvNkG417kwiaaoPH5a",
            "value": "150000000",
            "chainID": "bcb",
            "keyStorePath": "./.keystore"
      	}
    	}
  }
  ```

- **Request Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包密码。                                                  |
  | token        |  String  | *交易的资产（本币或代币）对应的名称。                        |
  | gasLimit     |  String  | *交易的燃料限制。                                            |
  | note         |  String  | [选填]交易备注（最长256字符），默认为空。                    |
  | to           | Address  | *接收转账的账户地址。                                        |
  | value        |  String  | *转账的资产数量（单位：Cong）。                              |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
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
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 3.7 call

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_call?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_call",
    "params": {
        "name": "hotwal001",
        "password": "aBig62_123",
        "bccParams": {
            "orgName": "example",
            "contract": "dice2win",
            "method": "placeBet",
            "gasLimit": "10000",
            "splitBy": ";",
            "params": "1,2,100,0x234...,0xjsdj...,bcbLocF...",
            "paramsFile": "./params",
            "note": "",
            "pay": "1.002bcb",
            "chainID": "bcb",
            "keyStorePath": "./.keystore"
      	}
    	}
  }
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *钱包名称。                                                  |
  | password     |  String  | *钱包访问密码。                                              |
  | orgName      |  String  | *组织名称。                                                  |
  | contract     |  String  | *合约名称。                                                  |
  | gasLimit     |  Int64   | *交易的燃料限制。                                            |
  | note         |  String  | [选填]交易备注，内容自定义。                                 |
  | method       |  String  | *方法名称。                                                  |
  | params       |  String  | [与paramsFile二选一]输入参数值列表，规则见*输入参数格式规定*。 |
  | paramsFile   |  String  | [与params二选一]输入参数值列表所在文件。                     |
  | splitBy      |  String  | [选填]分隔符，默认为";"。                                    |
  | pay          |  String  | [选填]如遇调用合约方法前需要转账时，可使用该选项标注需要转账的数量和币种，该选项标注的值只向合约账户转账，默认为空。 |
  | keystorepath |  String  | [选填]钱包访问路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易执行结果代码，200表示成功。                              |
  | &nbsp;&nbsp;log    |  String   | 对交易执行结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 3.8 contractInfo

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_contractInfo?orgName=_&contractName=_&orgID=_&contractAddr=_&chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_contractInfo",
    "params": {
    	"orgName": "jiujiu"
    	"contractName": "excellencies"
    	"orgID": "orgCZkw5xz9DYa3h5pJ2CzZSuGHRCj2ot5xq"
    	"contractAddr": "devtest7rXz2j8Vv1ZnawYMi3vswQ1ra2Lt33LTs"
    	"chainID": "devtest"
    }
  }
  ```

- **Input Parameters**

| **语法**     | **类型** | **注释**                                 |
| ------------ | -------- | ---------------------------------------- |
| orgName      | String   | *组织名称。                              |
| contractName | String   | *合约名称。                              |
| orgID        | String   | *组织ID                                  |
| contractAddr | Address  | *合约地址                                |
| chainid      | String   | [选填]链ID，默认以配置文件中的配置为准。 |

- **Output SUCCESS Example**

  ```
  {
    "jsonrpc": "2.0",
    "id": "",
    "result": {
      "address": "devtest7rXz2j8Vv1ZnawYMi3vswQ1ra2Lt33LTs",
      "account": "devtestR2FF1eA9KrdPP3HyD1B8ZoA6Mun272de",
      "owner": "devtestLve7gJUkNkNYV8uVs2zW3UBZWEbVThnND",
      "name": "excellencies",
      "version": "4.0",
      "codeHash": "0x1A78E2F6F6A87B1563480EA41B2046D0813F6D929D0A05D748C7D4F85B1F941D",
      "effectHeight": 119,
      "loseHeight": 0,
      "keyPrefix": "/orgCZkw5xz9DYa3h5pJ2CzZSuGHRCj2ot5xq/excellencies",
      "methods": [
        {
          "methodId": "e786362c",
          "gas": 5000,
          "prototype": "SetManager([]types.Address)"
        },
        {
          "methodId": "d373a935",
          "gas": 5000,
          "prototype": "SetSecretSigner(types.PubKey)"
        },
        {
          "methodId": "44f1b25c",
          "gas": 5000,
          "prototype": "SetSettings(string)"
        },
        {
          "methodId": "9fe1c79c",
          "gas": 5000,
          "prototype": "SetRecFeeInfo(string)"
        },
        {
          "methodId": "ec4a2a7e",
          "gas": 500,
          "prototype": "PlaceBet(string,int64,[]byte,[]byte,types.Address,types.Address)"
        },
        {
          "methodId": "2316ef3a",
          "gas": 500,
          "prototype": "SettleBet([]byte,int64)"
        },
        {
          "methodId": "d32a5fe6",
          "gas": 500,
          "prototype": "WithdrawWin([]byte)"
        },
        {
          "methodId": "ac8151c9",
          "gas": 500,
          "prototype": "RefundBets([]byte,int64)"
        }
      ],
      "interfaces": [],
      "mine": null,
      "token": "",
      "orgID": "orgCZkw5xz9DYa3h5pJ2CzZSuGHRCj2ot5xq",
      "chainVersion": 2
    }
  }
  ```

- **Output SUCCESS Result**

| **语法**                                                    | **类型**      | **注释**                       |
| ----------------------------------------------------------- | ------------- | ------------------------------ |
| Version                                                     | string        | 合约所有迭代版本               |
| Name                                                        | string        | 合约名称                       |
| OrgID                                                       | string        | 组织ID                         |
| Address                                                     | types.Address | 合约地址                       |
| Account                                                     | types.Address | 合约的账户地址                 |
| Owner                                                       | types.Address | 合约拥有者的账户地址           |
| CodeHash                                                    | types.Hash    | 合约代码的哈希，以“0x”开头。   |
| EffectHeight                                                | int64         | 合约生效的区块高度             |
| LoseEffect                                                  | int64         | 合约失效的区块高度             |
| KeyPrefix                                                   | string        | 合约在状态数据库中KEY值的前缀  |
| Token                                                       | types.Address | 合约代币地址                   |
| Interfaces                                                  | []Method      | 合约提供的跨合约调用的方法列表 |
| Method                                                      | []Method      | 合约对外提供接口的方法列表     |
| SetSecretSigner(types.PubKey)                               | String        | SetSecretSigner方法原型。      |
| SetSettings(string)                                         | String        | SetSettings方法原型。          |
| SetRecvFeeInfos(string)                                     | String        | SetRecvFeeInfos方法原型。      |
| WithdrawFunds(string, types.Address,bn.Number)              | String        | WithdrawFunds方法原型。        |
| PlaceBet(bn.Number,int64,int64,[]byte,[]byte,types.Address) | String        | PlaceBet方法原型。             |
| SettleBet([]byte)                                           | String        | SettleBet方法原型。            |
| RefundBet([]byte)                                           | String        | RefundBet方法原型。            |



### 3.8 blockHeight

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_blockHeight?chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_blockHeight",
    "params": {
    	"chainID": "bcb"
    }
  }
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | ——                                                           |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
      "lastBlock": 2500
  }
  ```

- **Output SUCCESS Result**

  | **语法**  | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | --------- | :------: | ------------------------------------------------------------ |
  | lastBlock |  Int64   | 最新区块高度。                                               |



### 3.9 block

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_block?height=_&rt=_&num=_&chainID=_
  ```

- **Request JSONRPC over HTTPS1**（详细信息参数）

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_block",
    "params": {
       "height": 2500,
       "chainID": "bcb"
    } 
  }
  ```

- **Request JSONRPC over HTTPS2**（简要信息参数）

```
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "bcc_block",
  "params": {
   	 "rt": "2019-05-10 09:37:14",
     "num": "3"
  } 
}
```

- **Input Parameters**

| **语法** | **类型** | **注释**                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| height   | int64    | 指定区块高度。                                               |
| rt       | string   | 指定区块时间，采用UTC时间，返回的区块时间大于并且最接近输入时间的区块。 |
| num      | int64    | 指定区块数量，为空的话返回一个区块详细信息，否则返回多个区块的简要信息。 |
| chainid  | String   | [选填]链ID，默认以配置文件中的配置为准。                     |

注：时间和高度是互斥参数；如果高度和时间为空，返回最新区块信息。

- **Output SUCCESS Example1**（详细信息结果）

  ```
  OK
  Response: {
    "blockHeight": 2500,
    "blockHash": "0x476dc319f4d3ad9b8c4c4ab03edcc100bb7c90da",
    "parentHash": "0x95880ac3be0a89aa2c82fa5e9dadf95a0e99dc3c",
    "chainID": "test",
    "validatorHash": "0x771543e3773dfebdcc5f3d4ce42c39c29a543218",
    "consensusHash": "0xf66ef1df8ba6dac7a1ecce40cc84e54a1cebc6a5",
    "blockTime": "2019-05-10 09:37:14.923456881 +0000 UTC",
    "blockSize": 988,
    "proposerAddress": "testHs1N4Yudisgo5pqZw8AXE66Taq776H3PK",
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
        "note":"hello",
        "messages": [
          {
           "smcAddress": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
           "smcName": "token-basic",
           "method": "Transfer(smc.Address,big.Int)smc.Error",
           "to": "bcbKuqW1qdsnD7mRsRooXMEkCBj2s9GLF9pn",
           "value": "683000000000"
          }
        ]
      }
    ]
  }
  ```

- **Output SUCCESS Example2**（简要信息结果）

```
OK
Response: {
 [
 	{
 	 "blockHeight": 2500,
	 "blockHash": "0x95880AC3BE0A89AA2C82FA5E9DADF95A0E99DC3C",
 	 "blockTime": "2019-05-10T09:37:14.923456881Z",
  	},
  	{
 	 "blockHeight": 2501,
	 "blockHash": "0x476DC319F4D3AD9B8C4C4AB03EDCC100BB7C90DA",
 	 "blockTime": "2019-05-10T09:39:16.234023422Z",
  	},
  	{
 	 "blockHeight": 2502,
	 "blockHash": "0xCF499509BF839A3083B954F409742C3C9AF93367",
 	 "blockTime": "2019-05-10T09:41:17.544988709Z",
  	}
  ]
}
```

- **Output SUCCESS Result**

  | **语法**                                       |   **类型**   | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------------------------------------------- | :----------: | ------------------------------------------------------------ |
  | blockHeight                                    |    Int64     | 区块高度。                                                   |
  | blockHash                                      |  HexString   | 区块哈希值，以“0x”开头。                                     |
  | parentHash                                     |  HexString   | 父区块哈希值，以“0x”开头。                                   |
  | chainID                                        |    String    | 链ID。                                                       |
  | validatorsHash                                 |  HexString   | 验证者列表哈希值，以“0x”开头。                               |
  | consensusHash                                  |  HexString   | 共识信息哈希值，以“0x”开头。                                 |
  | blockTime                                      |    String    | 区块打包时间。                                               |
  | blockSize                                      |     Int      | 当前区块大小。                                               |
  | proposerAddress                                |   Address    | 提案人地址。                                                 |
  | txs [                                          | Object Array | 交易列表。                                                   |
  | &nbsp;&nbsp;{                                  |    Object    | 交易参数。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;txHash                 |  HexString   | 交易哈希值，以“0x”开头。                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;txTime                 |    String    | 交易时间。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;code                   |    Uint32    | 交易结果码，200表示交易成功，其它值表示失败。                |
  | &nbsp;&nbsp;&nbsp;&nbsp;log                    |    String    | 交易结果描述。                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHash              |  HexString   | 交易所在区块哈希值，以“0x”开头。                             |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHeight            |    Int64     | 交易所在区块高度。                                           |
  | &nbsp;&nbsp;&nbsp;&nbsp;from                   |   Address    | 交易签名人地址。                                             |
  | &nbsp;&nbsp;&nbsp;&nbsp;nonce                  |    Uint64    | 交易签名人交易计数值。                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;gasLimit&nbsp;         |    Uint64    | 最大燃料数量。                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;fee                    |    Uint64    | 交易手续费（单位cong）。                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;note                   |    String    | 备注。                                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;messages [             | Object Array | 消息列表。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smcAddress |   Address    | 合约地址。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smcName    |    String    | 合约名称。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;method     |    String    | 方法原型。                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to         |   Address    | 转账目的账户地址，仅当交易是BRC20标准转账时有效。            |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value      |    String    | 转账金额（单位cong），仅当交易是BRC20标准转账时有效。        |
  | &nbsp;&nbsp;}                                  |              |                                                              |
  | ]                                              |              |                                                              |



### 3.10 transaction

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_transaction?txHash=_&chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_transaction",
    "params": {
        "txHash": "0x4E456161...",
    	"chainID": "bcb"
    } 
  }
  ```

- **Input Parameters**

  | **语法** | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :-------: | ------------------------------------------------------------ |
  | txHash   | HexString | *指定交易哈希值，以“0x”开头。                                |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "txHash": "0xc2d613b000c56b53099b3668664c44f1395406a6e8b8f288fb0e045f72a3c83c",
    "txTime": "2019-05-08 09:38:05.521987701 +0000 UTC",
    "code": 200,
    "log": "",
    "blockHash": "0xd4f0257eb95de4c2584013f84acf6ae5311bca91",
    "blockHeight": 86,
    "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
    "nonce": 11,
    "gasLimit": 600,
    "fee": 1250000,
    "note": "",
    "messages": [
      {
        "smcAddress": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
        "smcName": "token-basic",
        "method": "Transfer(types.Address,bn.Number)",
        "to": "local3pw2Lgbb83JV5HpoRhM5eCCYS4jtoxxJx",
        "value": "150000000000000"
      }
    ],
    "tags": {
      "/0/std::fee": {
        "Name": "std::fee",
        "ContractAddr": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidmFsdWUiOjEyNTAwMDB9",
        "ReceiptHash": "18B3A7A65CA224B94C90200EC59029B3E94D8A74D853052E67F8F657BD95FB66",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": null,
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 1250000
        }
      },
      "/1/std::transfer": {
        "Name": "std::transfer",
        "ContractAddr": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbDNwdzJMZ2JiODNKVjVIcG9SaE01ZUNDWVM0anRveHhKeCIsInZhbHVlIjoxNTAwMDAwMDAwMDAwMDB9",
        "ReceiptHash": "BB599A08525D3F8293B3695E1C79B05316BE0C0B5B2FE24F4E67CB5C686A27C8",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "local3pw2Lgbb83JV5HpoRhM5eCCYS4jtoxxJx",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 150000000000000
        }
      },
      "/2/totalFee": {
        "Name": "totalFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidmFsdWUiOjEyNTAwMDB9",
        "ReceiptHash": "F1359BC1665022CB77DA69FCCFA4AC60FA0FD00CE09CB897830083E76F7E31E6",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": null,
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 1250000
        }
      },
      "/3/transferFee": {
        "Name": "transferFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbDhMdFQ4QW9uV2dKOG5NQ0VkQVI1VUdyYlJmVW11b2VpeiIsInZhbHVlIjoyNTAwMDB9",
        "ReceiptHash": "D872750193DA93BA345DE11A546CBA0BD6A7AE3F68745C537CECE432A047ADDD",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "local8LtT8AonWgJ8nMCEdAR5UGrbRfUmuoeiz",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 250000
        }
      },
      "/4/transferFee": {
        "Name": "transferFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbEVtbUxrNEdpSkNrWk5aY0hoVENYaWhFWm9MSmRENG9RRCIsInZhbHVlIjoyNTAwMDB9",
        "ReceiptHash": "21AA7212F6F9BCB38C01FDC8C0F2CD82A47068DCD535389F34E7493F9CED9571",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "localEmmLk4GiJCkZNZcHhTCXihEZoLJdD4oQD",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 250000
        }
      },
      "/5/transferFee": {
        "Name": "transferFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbEhZRHdSU29ORXlDc1o4S1lhdnlSQlpzR0hEN2lMeGpuWCIsInZhbHVlIjozNzUwMDB9",
        "ReceiptHash": "90B62B8DCBA1E351452D0C0FD430E83C84FDF89CC580022C93B0476B3CD86068",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "localHYDwRSoNEyCsZ8KYavyRBZsGHD7iLxjnX",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 375000
        }
      },
      "/6/transferFee": {
        "Name": "transferFee",
        "ContractAddr": "",
        "ReceiptBytes": "eyJ0b2tlbiI6ImxvY2FsTlZVM0xlWDdTaFZVemFxRk51NUM4R1g4czhUaUxRVHNuIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbHpWdDNwZmU3NWN1VmR2d3paTGtBU1FzS2MzYmY5M2ZpIiwidmFsdWUiOjM3NTAwMH0=",
        "ReceiptHash": "8E95324BA76072616AFE77B99A9CB7BD477BFEFAAFB3C1162DC77689EAA95560",
        "Receipt": {
          "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
          "to": "localzVt3pfe75cuVdvwzZLkASQsKc3bf93fi",
          "token": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
          "value": 375000
        }
      }
    }
  }
  ```

- **Output SUCCESS Result**

| **语法**     | **类型**               | **注释**                                              |
| ------------ | ---------------------- | ----------------------------------------------------- |
| txHash       | HexString              | 交易哈希值，以“0x”开头。                              |
| txTime       | String                 | 交易时间。                                            |
| code         | Uint32                 | 交易结果码，200表示交易成功，其它值表示失败。         |
| log          | String                 | 交易结果描述。                                        |
| blockHash    | HexString              | 交易所在区块哈希值，以“0x”开头。                      |
| blockHeight  | Int64                  | 交易所在区块高度。                                    |
| from         | Address                | 交易签名人地址。                                      |
| nonce        | Uint64                 | 交易签名人交易计数值。                                |
| gasLimit     | Uint64                 | 最大燃料数量。                                        |
| fee          | Uint64                 | 交易手续费（单位cong）。                              |
| note         | String                 | 备注。                                                |
| messages     | Object Array           | 消息列表。                                            |
| smcAddress   | Address                | 合约地址。                                            |
| smcName      | String                 | 合约名称。                                            |
| method       | String                 | 方法原型。                                            |
| to           | Address                | 转账目的账户地址，仅当交易是BRC20标准转账时有效。     |
| value        | String                 | 转账金额（单位cong），仅当交易是BRC20标准转账时有效。 |
| Tags         | []string               | 收据列表 。                                           |
| Name         | string                 | 收据名称。                                            |
| ContractAddr | string                 | 合约地址。                                            |
| ReceiptBytes | []byte                 | 收据数据原型。                                        |
| ReceiptHash  | string                 | 收据hash。                                            |
| Receipt      | map[string]interface{} | 收据解析结果。                                        |
| from         | string                 | 交易签名人地址。                                      |
| to           | string                 | 每笔收据的目的账户地址。                              |
| token        | string                 | 代币地址。                                            |
| value        | string                 | 每笔收据的金额。                                      |



### 3.11 balance

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_balance?address=_&name=_&password=_&token=_&all=_&chainID=_&keyStorePath=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_balance",
    "params": {
        "address": "bcbAkTD...",
        "name": "hotwal001",
        "password": "aBig62_123",
        "token": "bcb",
        "all": true,
    	  "chainID": "bcb",
        "keyStorePath": "./.keystore"
    } 
  }
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | [与钱包信息二选一]账户地址，默认为空。                       |
  | name         |  String  | [与账户地址二选一]钱包名称，默认为空。                       |
  | password     |  String  | [与账户地址二选一]钱包密码，默认为空。                       |
  | token        |  String  | [选填]代币名称，默认为基础代币。                             |
  | all          |   Bool   | [选填]是否查询所有资产余额标记，默认为false。                |
  | chainid      |  String  | [选填]链ID，默认以配置文件中的配置为准。                     |
  | keystorepath |  String  | [选填]访问钱包路径，默认为"./.keystore"。                    |

- **Output SUCCESS Example**

  ```
  OK
  Response: [
    {
      "tokenAddress": "localNVU3LeX7ShVUzaqFNu5C8GX8s8TiLQTsn",
      "tokenName": "LOC",
      "balance": "119997371250000"
    }
  ]
  ```

- **Output SUCCESS Result**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | token        |  String  | 代币名称。                                                   |
  | tokenAddress |  String  | 代币地址。                                                   |
  | balance      |  String  | 账户余额（单位：Cong）。                                     |



### 3.12 nonce

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_nonce?address=_&name=_&password=_&chainID=_&keyStorePath=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_nonce",
    "params": {
        "address": "bcbAkTD...",
        "name": "hotwal001",
        "password": "aBig62_123",
    	  "chainID": "bcb",
        "keyStorePath": "./.keystore"
    } 
  }
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | [与钱包二选一]账户地址。                                     |
  | name         |  String  | [与账户地址二选一]钱包地址。                                 |
  | password     |  String  | [与账户地址二选一]钱包密码                                   |
  | chainid      |  String  | [选填]链ID，默认值以配置文件中的配置为准。                   |
  | keystorepath |  String  | [选填]访问钱包路径，默认"./.keystore"                        |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    "nonce": 5000
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | nonce    |  Uint64  | 指定地址在区块链上可用的下一个交易计数值。                   |



### 3.13 commitTx

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_commitTx?tx=_&chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_commitTx",
    "params": {
        "tx": "bcb<tx>.v1.AetboY...",
        "chainID": "bcb"
    } 
  }
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | tx       |  String  | *交易数据。                                                  |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
     "code": 200,
     "log": "Deliver tx succeed",
     "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
     "height": 234389
  }
  
  ```

- **Output SUCCESS Result**

  | **语法**           | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | 交易校验/背书结果代码，200表示成功。                         |
  | &nbsp;&nbsp;log    |  String   | 对交易校验/背书结果进行的文字描述，当code不等于200时描述具体的错误信息。 |
  | &nbsp;&nbsp;txHash | HexString | 交易的哈希，以“0x”开头。                                     |
  | &nbsp;&nbsp;height |   Int64   | 交易在哪个高度的区块被确认。                                 |



### 3.14 version

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_version?chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_version",
    "params": {
        "chainID": "bcb"
    }
  }
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | ——                                                           |

- **Output SUCCESS Example**

  ```
  OK
  Response: {
    version: 1.0.7.9636
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | version  |  string  | 当前程序版本号。                                             |



### 3.15 query

- **Request URI over HTTPS**

  ```
  https://localhost:37658/bcc_query?path=_
  ```

- **Request JSONRPC over HTTPS**

  ```
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_query",
    "params": {
        "path": "/contract/all/0"
    }
  }
  ```

- **Input Parameters**

| **语法** | **类型** | **注释**                  |
| -------- | -------- | ------------------------- |
| path     | string   | [必填]查询指定信息的key。 |

- **Output SUCCESS Example**

  ```
  OK
  response: {
     "code"	:  200
     "key"	:  "L2NvbnRyYWN0L2FsbC8w"
     "value"  :	"WyJ0ZXN0NVpYaG8zdUw1WlNCV3BIMmlmbmJzQmFRY3k1NTNnWDhGIiwidGVzdEFSUlZm
  				na3V4ekE1VlpGaGhvNjUxYkZGZ21ncyIsInRlc3Q2cnlWS1NnZFpCZ2NnUjNhV2djbWRa
   				WEpLaDFRSnoiLCJ0ZXN0QWlXdXNuc0ZzVVFXa2ZIR1NLNXpoNjNGb3pDUFY1UGlCIiwid
   				Es2a2pnQ2tBQm5TVFMxTUI4NkNpeEVRV005Nlpic1A5IiwidGVzdFA4ZEMyUHVCcHNVQ
   				Dhqb0t1RjFFdXpaTFhGbXg1NyJd"
  }
  ```

- **Output SUCCESS Result**

| **语法** | **类型** | **注释**                                               |
| -------- | -------- | ------------------------------------------------------ |
| code     | Int      | 交易校验/背书结果代码，200表示成功。                   |
| key      | string   | base64编码格式的String，由输入的参数（path）编码而成。 |
| value    | string   | base64编码格式的String，由输出的结果编码而成。         |

