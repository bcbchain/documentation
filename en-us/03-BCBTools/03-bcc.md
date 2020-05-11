# bcc

bcc：it can query the information on the chain, send transactions, execute combination, contract and other operations

## 1. Usage

Execute command is as follows:

```shell
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

## 2. Commands Details

### 2.1 registerOrg

- Function Description: Register organization

- **command**

  ```shell
  bcc registerOrg --name hotwal001 --password aBig62_123 --orgName example --gasLimit 1000000 [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet password                                                  |
  | orgName      |  String  | *organization name                                                  |
  | gasLimit     |  String  | *gas limit for trading                                            |
  | note         |  String  | [optional] transaction notes                                             |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file |
  | keystorepath |  String  | [optional] wallet access path, default is `./. keystore`                   |

- **Output SUCCESS Example**

  ```shell
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success                             |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe|
  | &nbsp;&nbsp;txHash | HexString | transaction hash                                                 |
  | orgID              |  String   | organization id                                                     |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                                 |

### 2.2 setOrgSigners

- Function Description: set organization public key

- **command**

  ```shell
  bcc setOrgSigners --name hotwal001 --password aBig62_123 --orgName example --pubKeys ["0x..."] --gasLimit 1000000 [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet password                                                  |
  | orgName      |  String  | *organization name                                                   |
  | gasLimit     |  String  | *gas limit for trading                                            |
  | pubKeys      |  String  | *public key list.                                                  |
  | note         |  String  | [optional] transaction notes                                             |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file |
  | keystorepath |  String  | wallet access path, default is `./.keystore`                   |

- **Output SUCCESS Example**

  ```shell
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**     | **Type** | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success                              |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`                                   |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                                 |

### 2.3 setOrgDeployer

- Set deployment contract permissions under the organization

- **command**

  ```shell
  bcc setOrgDeployer --name hotwal001 --password aBig62_123 --orgName example --deployer local... --gasLimit 1000000 [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                   |
  | password     |  String  | *wallet password                                                  |
  | orgName      |  String  | *organization name                                                  |
  | gasLimit     |  String  | *gas limit for trading                                            |
  | deployer     | Address  | *publish account address.                                              |
  | note         |  String  | [optional] transaction notes                                             |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file |
  | keystorepath |  String  | wallet access path, default is `./.keystore`                   |

- **Output SUCCESS Example**

  ```shell
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**     | **Type** | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success                              |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`                                     |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                                 |

### 2.4 deployContract

- Function Description: deploy contract

- **command**

  ```shell
  bcc deployContract --name hotwal001 --password aBig62_123 --contractName dice2win --version 2.0 --orgName genesis --codeFile ./example.tar.gz --effectHeight 100 --owner bcbES5d6kwoX4vMeNLENMee2Mnsf2KL9ZpWo --gasLimit 10000 [--chainid bcb] [--note ...] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                   |
  | password     |  String  | *wallet password                                                  |
  | contractName |  String  | *contract name                                                  |
  | version      |  String  | *contract version                                                  |
  | orgName      |  String  | *organization name                                                  |
  | codeFile     |  String  | *contract source file path                                          |
  | effectHeight |  Uint64  | *contract effective block number                                              |
  | owner        | Address  | *owner address                                                |
  | gasLimit     |  String  | *gas limit for trading                                            |
  | note         |  String  | [optional] transaction notes                                             |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file |
  | keystorepath |  String  | [optional]wallet access path, default is `./.keystore`                |

- **Output SUCCESS Example**

  ```shell
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

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success  |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`                     |
  | smcAddress         |  Address  | deployed contract address                                       |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                                   |

### 2.5 registerToken

- Function Description: register token

- **command**

  ```shell
  bcc registerToken --name hotwal001 --password aBig62_123 --tokenName xt --tokenSymbol xt --totalSupply 1000000000000 --addSupplyEnabled true --burnEnabled true --gasPrice 2500 --gasLimit 10000 [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**         | **Type** | **Comment** |
  | ---------------- | :------: | ------------------------------------------------------------ |
  | name             |  String  | *wallet name                                                  |
  | password         |  String  | *wallet password                                                  |
  | tokenName        |  String  | *token name                                                  |
  | tokenSymbol      |  String  | *token symbol                                                  |
  | totalSupply      |  Number  | *token total amount                                              |
  | addSupplyEnabled |   Bool   | *flag of whether token can be increased                                        |
  | burnEnabled      |   Bool   | *flag of whether token can be burned                                        |
  | gasPrice         |  Int64   | *gas price                                                  |
  | gasLimit         |  String  | *gas limit for trading                                            |
  | note             |  String  | [optional] transaction notes                                             |
  | chainid          |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath     |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```shell
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

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | tokenAddress       |  Address  | token address                        |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 2.6 transfer

- Function Description: transfer transaction

- **command**

  ```shell
  bcc transfer --name hotwal001 --password aBig62_123 --token bcb
  --gasLimit 600 [--note hello] --to bcbLocFJG5Q792eLQXhvNkG417kwiaaoPH5a --value 1500000000 [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Request Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet password                                                  |
  | token        |  String  | *the name of the asset (currency or token) to be traded                      |
  | gasLimit     |  String  | *gas limit for trading                                            |
  | note         |  String  | [optional] transaction note (maximum 256 characters), which is blank by default           |
  | to           | Address  | *recipient address                                        |
  | value        |  String  | *transfer asset amount (unit: cong)               |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```shell
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584"
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 2.7 call

- Function Description: call contract function by the organization name and contract name

- **command**

  ```shell
  bcc call --name hotwal001 --password aBig62_123 --orgName example --contract dice2win --method placeBet --gasLimit 5000 [--splitBy @] [--params @ --paramsFile ./params] [--note ...]  [--pay 1.003(loc)] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet access password                                       |
  | orgName      |  String  | *organization name                                                  |
  | contract     |  String  | *contract name                                                  |
  | gasLimit     |  Int64   | *gas limit for trading                                            |
  | note         |  String  | [optional] transaction notes, customized content                     |
  | method       |  String  | *function name                                                  |
  | params       |  String  | [select one from paramsfile] input parameter list, see *input parameter format specification* for rules.  |
  | paramsFile   |  String  | [one of two choices with params] the file where the input parameter value list is located            |
  | splitBy      |  String  | [optional] separator, default is `#`                                  |
  | pay          |  String  | [optional] if you need to transfer before calling the contract method, you can use this option to mark the quantity and currency to be transferred. The value marked in this option only transfers to the contract account, which is blank by default |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **input parameter format specification**

  1. The parameter order must be consistent with the input parameter order of the function and separated by the selected separator;
  2. If the input parameter contains "\\", you need to enter double backslash "\\\\";
  3. When the input type is byte/byte slice, convert the byte/byte slice to the hexadecimal string starting with 0x and input;
  4. When the input type is map, input in the JSON string format, and double quotation marks are preceded by backslashes, such as: {\\"key1\\":\\"value1\\",\\"key2\\":\\"value2\\"} (no extra space is allowed between key and value, for example, {"test": 123} is the wrong format);
  5. If the input string value contains double quotation marks, you need to add a backslash before the double quotation marks, otherwise the command line cannot input the double quotation marks correctly;
  6. If the input parameter is too long, resulting in exceeding the command line length limit, then write the input parameter list to the file according to the above rules, and use the option `--file` to mark the path of the input parameter file.

- **Output SUCCESS Example**

  ```shell
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389E
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**     | **Type** | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 2.8 contractInfo

- Function Description: query contract information
- Mode: (orgName+contractName=specify contract information);(orgID+contractName=specify contract information)(contractAddr=specify contract information);(no parameter = print all contract addresses)

- **command**

```
bcc contractInfo [--orgName example] [--orgID orgBtjf...] [--contractName mydice2win]
[--contractAddr localKkpg...]
```

- **Input Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | orgName      |  String  | *organization name                                                  |
  | contractName |  String  | *contract name                                                  |
  | orgID        |  String  | *organization ID                                                      |
  | contractAddr | Address  | *contract address                                                    |

- **Output SUCCESS Example**

  ```shell
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

  | **Parameter**                                                    |   **Type**    | **Comment** |
  | ----------------------------------------------------------- | :-----------: | ------------------------------------------------------------ |
  | Version                                                     |    string     | contract all iteration versions                                             |
  | Name                                                        |    string     | contract name                                                     |
  | OrgID                                                       |    string     | organization ID                                                       |
  | Address                                                     | types.Address | contract address                                                     |
  | Account                                                     | types.Address | account address of the contract                                               |
  | Owner                                                       | types.Address | account address of contract owner                                         |
  | CodeHash                                                    |  types.Hash   | hash of contract code                                             |
  | EffectHeight                                                |     int64     | block height of contract effectiveness                                           |
  | LoseEffect                                                  |     int64     | block height of contract expiration                                           |
  | KeyPrefix                                                   |    string     | prefix of key value of contract in state database                                |
  | Token                                                       | types.Address | contract token address                                                 |
  | Interfaces                                                  |   []Method    | list of methods called across contracts provided by contracts                               |
  | Method                                                      |   []Method    | Method list of interfaces provided by contract                                   |
  | SetSecretSigner(types.PubKey)                               |    String     | SetSecretSigner method prototype                                    |
  | SetSettings(string)                                         |    String     | SetSettings method prototype                                        |
  | SetRecvFeeInfos(string)                                     |    String     | SetRecvFeeInfos method prototype                                    |
  | WithdrawFunds(string,<br/>types.Address,bn.Number)          |    String     | WithdrawFunds method prototype                                      |
  | PlaceBet(bn.Number,int64,int64,[]byte,[]byte,types.Address) |    String     | PlaceBet method prototype                                           |
  | SettleBet([]byte)                                           |    String     | SettleBet method prototype                                          |
  | RefundBet([]byte)                                           |    String     | RefundBet method prototype                                          |

### 2.8 blockHeight

- Function Description: query block height

- **command**

  ```shell
  bcc blockHeight  [--chainid bcb]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | chainid  |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
      "lastBlock": 2500
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**  | **Type** | **Comment** |
  | --------- | :------: | ------------------------------------------------------------ |
  | lastBlock |  Int64   | latest block height.                                               |

### 2.9 block

- Function Description: query specific block information

- **command**

  ```shell
  bcc block [--height 2500]|[--rt "2019-05-10 09:37:14"] [--chainid bcb]
  bcc block [--height 2500]|[--rt "2019-05-10 09:37:14"] [--num 3] [--chainid bcb]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | height   |  int64   | specifies the block height                                  |
  | rt       |  string  | specifies the block time. UTC time is used. The block time returned is greater than and closest to the input time |
  | num      |  int64   | specifies the number of blocks. If it is empty, it will return the details of one block, otherwise, it will return the brief information of multiple blocks |
  | chainid  |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |

  Notice: time and height are mutually exclusive parameters; if height and time are empty, the latest block information will be returned.

- **Output SUCCESS Example1**（detailed information）

  ```json
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

- **Output SUCCESS Example2**(brief information）

```json
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

  | **Parameter**                                       |   **Type**   | **Comment** |
  | ---------------------------------------------- | :----------: | ------------------------------------------------------------ |
  | blockHeight                                    |    Int64     | block height                                                   |
  | blockHash                                      |  HexString   | block hash value, starting with '0x'                          |
  | parentHash                                     |  HexString   | parent block hash, starting with '0x'                        |
  | chainID                                        |    String    | chain ID                                                      |
  | validatorsHash                                 |  HexString   | verifier list hash, starting with '0x'.                       |
  | consensusHash                                  |  HexString   | consensus information hash value                       |
  | blockTime                                      |    String    | block packing time                                      |
  | blockSize                                      |     Int      | current block size.                                        |
  | proposerAddress                                |   Address    | proposer address.                                          |
  | txs [                                          | Object Array | transaction list                                                   |
  | &nbsp;&nbsp;{                                  |    Object    | transaction parameter                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;txHash                 |  HexString   | transaction hash, starting with '0x'                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;txTime                 |    String    | transaction time                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;code                   |    Uint32    | transaction result code, 200 indicates successful, and other values indicate failure                |
  | &nbsp;&nbsp;&nbsp;&nbsp;log                    |    String    | transaction result description                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHash              |  HexString   | the block hash of the transaction exixts, starting with '0x'                             |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHeight            |    Int64     | the block height of the transaction exixts                                           |
  | &nbsp;&nbsp;&nbsp;&nbsp;from                   |   Address    | address of transaction signer                                           |
  | &nbsp;&nbsp;&nbsp;&nbsp;nonce                  |    Uint64    | transaction signer transaction count.                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;gasLimit&nbsp;         |    Uint64    | maximum gas amount                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;fee                    |    Uint64    | transaction fee (unit: cong)                                    |
  | &nbsp;&nbsp;&nbsp;&nbsp;note                   |    String    | notes                                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;messages [             | Object Array | message list                                            |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smcAddress |   Address    | contract address                                          |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smcName    |    String    | contract name                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;method     |    String    |  method prototype                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to         |   Address    | transfer destination account address, only valid when the transaction is a standard brc20 transfer |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value      |    String    | transfer amount (unit: cong), valid only when the transaction is standard brc20 transfer        |
  | &nbsp;&nbsp;}                                  |              |                                                              |
  | ]                                              |              |                                                              |

### 2.10 transaction

- Function Description: query transaction information

- **command**

  ```shell
  bcc tx --txHash 0x4E456161... [--chainid bcb]
  ```

- **Input Parameters**

  | **Parameter** | **Type**  | **Comment** |
  | -------- | :-------: | ------------------------------------------------------------ |
  | txHash   | HexString | specifies the transaction hash, starting with '0x'                                |
  | chainid  |  String   | [optional] Chain ID, the default is the configuration in the configuration file                     |

- **Output SUCCESS Example**

  ```json
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

  | **Parameter**       |        **Type**        | **Comment** |
  | -------------- | :--------------------: | ------------------------------------------------------------ |
  | txHash         |       HexString        | transaction hash, starting with '0x'                                     |
  | txTime         |         String         | transaction time                                                   |
  | code           |         Uint32         | transaction result code, 200 indicates successful, and other values indicate failure                |
  | log            |         String         | transaction result description                                               |
  | blockHash      |       HexString        | the block hash of the transaction exixts, starting with '0x'                             |
  | blockHeight    |         Int64          | the block height of the transaction exixts                                           |
  | from           |        Address         | address of transaction signer                                           |
  | nonce          |         Uint64         | transaction signer transaction count.                                       |
  | gasLimit&nbsp; |         Uint64         | maximum gas amount                                               |
  | fee            |         Uint64         | transaction fee (unit: cong)                                    |
  | note           |         String         | notes                                                       |
  | messages       |      Object Array      | message list                                            |
  | smcAddress     |        Address         | contract address                                          |
  | smcName        |         String         | contract name                                                   |
  | method         |         String         |  method prototype                                                   |
  | to             |        Address         | transfer destination account address, only valid when the transaction is a standard brc20 transfer |
  | value          |         String         | transfer amount (unit: cong), valid only when the transaction is standard brc20 transfer        |
  | Tags           |        []string        | list of receipts                                        |
  | Name           |         string         | receipt name                                        |
  | ContractAddr   |         string         | contract address                                          |
  | ReceiptBytes   |         []byte         | receipt data prototype                                |
  | ReceiptHash    |         string         | receipt hash                                        |
  | Receipt        | map[string]interface{} | analytic receipt result                                 |
  | from           |         string         | address of transaction signer                                           |
  | to             |         string         | destination account address of each receipt                   |
  | token          |         string         | token address                        |
  | value          |         string         | the amount of each receipt                 |



### 2.11 balance

- Function Description: query account balance

- **command**

  ```shell
  bcc balance [--address bcbAkTD... | --name hotwal-001 --password aBig62_123] [--token bcb] [--all false] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | [choose one from wallet information] account address, which is blank by default    |
  | name         |  String  | [choose one from account address] wallet name, which is blank by default       |
  | password     |  String  | [choose one from account address] wallet password, which is blank by default.    |
  | token        |  String  | [optional] token name, default to base token         |
  | all          |   Bool   | [optional] whether to query all asset balance marks. The default value is false     |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath |  String  | access wallet path, default is "./.keystore"              |

- **Output SUCCESS Example**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | token        |  String  | token name                                                   |
  | tokenAddress |  String  | token address                        |
  | balance      |  String  | account balance (unit: cong)                       |

### 2.12 nonce

- Query nonce value

- **command**

  ```shell
  bcc nonce [--address bcbAkTD... | --name hotwal-001 --password aBig62_123]  [--chainid local] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | [choose one from wallet] account address                           |
  | name         |  String  | [choose one from account address] wallet address                       |
  | password     |  String  | [choose one from account address] wallet password                       |
  | chainid      |  String  | [optional] chain ID. the default value is the configuration in the configuration file      |
  | keystorepath |  String  | [optional] access wallet path, default "./.keystore"    |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
    "nonce": 5000
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | nonce    |  Uint64  | next available transaction count value of a specific address  on the blockchain                  |

### 2.13 commitTx

- Function Description: submit transaction data

- **command**

  ```shell
  bcc commitTx [--tx bcb<tx>.v1.AetboY...] [--file xxxxx] [--chainid bcb]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | tx       |  String  | transaction data.                                                   |
  | chainid  |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | file     |  String  | transaction data file (text file), one transaction per line              |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
     "code": 200,
     "log": "Deliver tx succeed",
     "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
     "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction verification / endorsement result code, 200 indicates success               |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction verification / endorsement result. When the code is not equal to 200, it will describe a specific error information |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 2.14 version

- Function Description: query version information

- **command**

  ```shell
  bcc version [--chainid bcb]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | chainid  |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
    version: 1.0.7.9636
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | version  |  string  | the current program version number                               |

### 2.15 runAsRPCService

- Function Description: start RPC service

- **command**

  ```shell
  bcc runAsRPCService
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | ——                                                           |

- **Output SUCCESS Example**

  ```json
  OK
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | ——                                                           |



### 2.15 query

- Function Description: query the specified information according to the instruction

- **command**

  ```shell
  bcc query [--path /contract/all/0] [--chainid bcb]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | path     |  string  | [required] the key to query the specified information                   |
  | chainid  |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |

- **Output SUCCESS Example**

  ```json
  OK
  response: {
     "code" :  200,
     "key" :  "L2NvbnRyYWN0L2FsbC8w",
     "value" : "WyJ0ZXN0NVpYaG8zdUw1WlNCV3BIMmlmbmJzQmFRY3k1NTNnWDhGIiwidGVzdEFSUlZmna3V4ekE1VlpGaGhvNjUxYkZGZ21ncyIsInRlc3Q2cnlWS1NnZFpCZ2NnUjNhV2djbWRaWEpLaDFRSnoiLCJ0ZXN0QWlXdXNuc0ZzVVFXa2ZIR1NLNXpoNjNGb3pDUFY1UGlCIiwidEs2a2pnQ2tBQm5TVFMxTUI4NkNpeEVRV005Nlpic1A5IiwidGVzdFA4ZEMyUHVCcHNVQDhqb0t1RjFFdXpaTFhGbXg1NyJd"
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | code     |   Int    | transaction verification / endorsement result code, 200 indicates success               |
  | key      |  string  | Base64 encoded string, encoded by the input parameter (path)       |
  | value    |  string  | Base64 encoded string, encoded by the output result          |

### 2.16 solDeploy

- Function Description: query the specified information according to the instruction

- **command**

  ```shell
  bcc solDeploy --name hotwal001 --password aBig62_123 --gasLimit 1000000 [--tokenAddr bcbaabdf...]|[--tokenName bcb] [--abiFile ./test.abi] [--binFile ./test.bin]|[--sourceFile ./test.sol] [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**         | **Type** | **Comment** |
  | ---------------- | :------: | ------------------------------------------------------------ |
  | name             |  String  | *wallet name                                                  |
  | password         |  String  | *wallet password                                                  |
  | tokenName        |  String  | token name of the contract binding                                 |
  | tokenAddr        |  String  | [choose one from token name] token name of the contract binding                     |
  | abiFile          |  Number  | path to contract ABI file                                  |
  | addSupplyEnabled |   Bool   | path to bin code file                           |
  | burnEnabled      |  string  | [choose one from bin file] contract source file path                  |
  | gasLimit         |  String  | *gas limit for trading                                            |
  | note             |  String  | [optional] transaction notes                                             |
  | chainid          |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath     |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```json
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

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |
  | data               |  Address  | contract address                                                     |

### 2.16 solCall

- Function Description: query the specified information according to the instruction

- **command**

  ```shell
  bcc solCall --name hotwal001 --password aBig62_123 --gasLimit 1000000 --contractAddr bcbGP7ktCj3HwY1... --method getValue [--paramsArr hello] [--abiFile ./test.abi] [--value 1000] [--note ...] [--chainid bcb] [--keystorepath ./.keystore]
  ```

- **Input Parameters**

  | **Parameter**         | **Type** | **Comment** |
  | ---------------- | :------: | ------------------------------------------------------------ |
  | name             |  String  | *wallet name                                                  |
  | password         |  String  | *wallet password                                                  |
  | contractAddr     |  String  | *contract address                                         |
  | method           |  String  | [choose one from token name] token name of the contract binding                 |
  | abiFile          |  Number  | path to contract ABI file                                  |
  | addSupplyEnabled |   Bool   | contract parameter                                            |
  | burnEnabled      |  string  | transfer amount                                             |
  | gasLimit         |  String  | *gas limit for trading                                            |
  | note             |  String  | [optional] transaction notes                                             |
  | chainid          |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath     |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```json
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

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |
  | data               |  Address  | function return value                                    |

## 3. Interface details

### 3.1 registerOrg

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_registerOrg?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet password                                                 |
  | orgName      |  String  | *organization name                                               |
  | keystorepath |  String  | [optional]wallet access path, default is `./.keystore`           |

- **Output SUCCESS Example**

  ```json
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

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | orgID              |  String   | organization ID                                         |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 3.2 setOrgSigners

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_setOrgSigners?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet password                                                  |
  | orgName      |  String  | *organization name                                                  |
  | gasLimit     |  String  | *gas limit for trading                                            |
  | pubKeys      |  String  | *public key list                                           |
  | note         |  String  | [optional] transaction notes                                             |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 3.3 setOrgDeployer

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_setOrgDeployer?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet password                                                  |
  | orgName      |  String  | *organization name                                                  |
  | gasLimit     |  String  | *gas limit for trading                                            |
  | deployer     | Address  | *publish account address                                             |
  | note         |  String  | [optional] transaction notes                                             |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }

  ```

- **Output SUCCESS Result**

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 3.4 deployContract

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_deployContract?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet password                                                  |
  | contractName |  String  | *contract name                                                  |
  | version      |  String  | *contract version                                            |
  | orgName      |  String  | *organization name                                                  |
  | codeFile     |  String  | *contract source file path                                        |
  | effectHeight |  Uint64  | *contract effective block height                                             |
  | owner        | Address  | *owner address                                           |
  | gasLimit     |  int64   | *gas limit for trading                                            |
  | note         |  String  | [optional] transaction notes                                             |
  | chainID      |  String  | [optional] chain ID                                          |
  | keystorepath |  String  |  [optional] wallet file access path,default is"./.keystore"              |

- **Output SUCCESS Example**

  ```json
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

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | smcAddress         |  Address  | address of deployed contract                                 |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 3.5 registerToken

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_registerToken?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**         | **Type** | **Comment** |
  | ---------------- | :------: | ------------------------------------------------------------ |
  | name             |  String  | *wallet name                                                  |
  | password         |  String  | *wallet password                                                  |
  | tokenName        |  String  | *token name                                                  |
  | tokenSymbol      |  String  | *token symbol                                                  |
  | totalSupply      |  Number  | *token total amount                                              |
  | addSupplyEnabled |   Bool   | *flag of whether token can be increased                                        |
  | burnEnabled      |   Bool   | *flag of whether token can be burned                                        |
  | gasPrice         |  Int64   | *gas price                                                  |
  | keystorepath     |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```json
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

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | tokenAddress       |  String   | token address                        |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 3.6 transfer

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_transfer?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet password                                                  |
  | token        |  String  | *the name of the asset (currency or token) to be traded                      |
  | gasLimit     |  String  | *gas limit for trading                                            |
  | note         |  String  | [optional] transaction note (maximum 256 characters), which is blank by default           |
  | to           | Address  | *recipient address                                        |
  | value        |  String  | *transfer asset amount (unit: cong)               |
  | keystorepath |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584"
    "height": 234389
  }

  ```

- **Output SUCCESS Result**

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 3.7 call

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_call?name=_&password=_&bccParams=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | *wallet name                                                  |
  | password     |  String  | *wallet access password                                              |
  | orgName      |  String  | *organization name                                                  |
  | contract     |  String  | *contract name                                                  |
  | gasLimit     |  Int64   | *gas limit for trading                                            |
  | note         |  String  | [optional] transaction notes, customized content                     |
  | method       |  String  | *function name                                                  |
  | params       |  String  | [select one from paramsfile] input parameter list, see *input parameter format specification* for rules.  |
  | paramsFile   |  String  | [one of two choices with params] the file where the input parameter value list is located            |
  | splitBy      |  String  | [optional] separator, default is';'                                   |
  | pay          |  String  | [optional] if you need to transfer before calling the contract method, you can use this option to mark the quantity and currency to be transferred. The value marked in this option only transfers to the contract account, which is blank by default |
  | keystorepath |  String  | [optional]wallet access path, default is `./.keystore`                    |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
    "code": 200,
    "log": "Check tx succeed",
    "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
    "height": 234389
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction execution result code, 200 indicates success            |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction execution result. When the code is not equal to 200, it will show a specific error information to describe |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 3.8 contractInfo

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_contractInfo?orgName=_&contractName=_&orgID=_&contractAddr=_&chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "bcc_contractInfo",
    "params": {
      "orgName": "jiujiu",
      "contractName": "excellencies",
      "orgID": "orgCZkw5xz9DYa3h5pJ2CzZSuGHRCj2ot5xq",
      "contractAddr": "devtest7rXz2j8Vv1ZnawYMi3vswQ1ra2Lt33LTs",
      "chainID": "devtest"
    }
  }
  ```

- **Input Parameters**

| **Parameter**     | **Type** | **Comment**                                 |
| ------------ | -------- | ---------------------------------------- |
| orgName      | String   | *organization name                              |
| contractName | String   | *contract name                              |
| orgID        | String   | *organization ID                                  |
| contractAddr | Address  | *contract address                                |
| chainid      | String   | [optional] Chain ID, the default is the configuration in the configuration file |

- **Output SUCCESS Example**

  ```json
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

| **Parameter**                                                    | **Type**      | **Comment**                       |
| ----------------------------------------------------------- | ------------- | ------------------------------ |
| Version                                                     | string        | contract all iteration versions               |
| Name                                                        | string        | contract name                       |
| OrgID                                                       | string        | organization ID                         |
| Address                                                     | types.Address | contract address                       |
| Account                                                     | types.Address | account address of the contract                 |
| Owner                                                       | types.Address | account address of contract owner           |
| CodeHash                                                    | types.Hash    | the hash of the contract code, start with "0x"   |
| EffectHeight                                                | int64         | block height of contract effectiveness             |
| LoseEffect                                                  | int64         | block height of contract expiration             |
| KeyPrefix                                                   | string        | prefix of key value of contract in state database  |
| Token                                                       | types.Address | contract token address                  |
| Interfaces                                                  | []Method      | list of methods called across contracts provided by contracts |
| Method                                                      | []Method      | method list of interfaces provided by contract     |
| SetSecretSigner(types.PubKey)                               | String        | SetSecretSigner method prototype      |
| SetSettings(string)                                         | String        | SetSettings method prototype          |
| SetRecvFeeInfos(string)                                     | String        | SetRecvFeeInfos method prototype      |
| WithdrawFunds(string, types.Address,bn.Number)              | String        | WithdrawFunds method prototype        |
| PlaceBet(bn.Number,int64,int64,[]byte,[]byte,types.Address) | String        | PlaceBet method prototype             |
| SettleBet([]byte)                                           | String        | SettleBet method prototype            |
| RefundBet([]byte)                                           | String        | RefundBet method prototype            |

### 3.8 blockHeight

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_blockHeight?chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | ——                                                           |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
      "lastBlock": 2500
  }
  ```

- **Output SUCCESS Result**

  | **Parameter**  | **Type** | **Comment** |
  | --------- | :------: | ------------------------------------------------------------ |
  | lastBlock |  Int64   | latest block height                                               |

### 3.9 block

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_block?height=_&rt=_&num=_&chainID=_
  ```

- **Request JSONRPC over HTTPS1**（detailed information parameter）

  ```json
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

- **Request JSONRPC over HTTPS2**（brief information parameter）

```json
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

| **Parameter** | **Type** | **Comment**                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| height   | int64    | specific block height                                               |
| rt       | string   | specifies the block time. UTC time is used. The block time returned is greater than and closest to the input time |
| num      | int64    | specifies the number of blocks. If it is empty, it will return the details of one block, otherwise, it will return the brief information of multiple blocks |
| chainid  | String   | [optional] Chain ID, the default is the configuration in the configuration file                     |

Notice: time and height are mutually exclusive parameters; if height and time are empty, the latest block information will be returned.

- **Output SUCCESS Example1**（detailed information parameter）

  ```json
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

- **Output SUCCESS Example2**(brief information parameter）

```json
OK
Response:{
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

  | **Parameter**                                       |   **Type**   | **Comment** |
  | ---------------------------------------------- | :----------: | ------------------------------------------------------------ |
  | blockHeight                                    |    Int64     | block height                                                   |
  | blockHash                                      |  HexString   | block hash, starting with '0x'                          |
  | parentHash                                     |  HexString   | parent block hash, starting with '0x'                        |
  | chainID                                        |    String    | chain ID                                                      |
  | validatorsHash                                 |  HexString   | verifier list hash, starting with '0x'.                               |
  | consensusHash                                  |  HexString   | consensus information hash value                       |
  | blockTime                                      |    String    | block packing time                                      |
  | blockSize                                      |     Int      | current block size.                                        |
  | proposerAddress                                |   Address    | proposer address.                                          |
  | txs [                                          | Object Array |  transaction list                                                 |
  | &nbsp;&nbsp;{                                  |    Object    |  transaction parameter                                            |
  | &nbsp;&nbsp;&nbsp;&nbsp;txHash                 |  HexString   | transaction hash, starting with '0x'                                     |
  | &nbsp;&nbsp;&nbsp;&nbsp;txTime                 |    String    | transaction time                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;code                   |    Uint32    | transaction result code, 200 indicates successful, and other values indicate failure                |
  | &nbsp;&nbsp;&nbsp;&nbsp;log                    |    String    | transaction result description                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHash              |  HexString   | the block hash of the transaction exixts, starting with '0x'                             |
  | &nbsp;&nbsp;&nbsp;&nbsp;blockHeight            |    Int64     | the block height of the transaction exixts                                           |
  | &nbsp;&nbsp;&nbsp;&nbsp;from                   |   Address    | address of transaction signer                                           |
  | &nbsp;&nbsp;&nbsp;&nbsp;nonce                  |    Uint64    | transaction signer transaction count.                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;gasLimit&nbsp;         |    Uint64    | maximum gas amount                                               |
  | &nbsp;&nbsp;&nbsp;&nbsp;fee                    |    Uint64    | transaction fee (unit: cong)                                    |
  | &nbsp;&nbsp;&nbsp;&nbsp;note                   |    String    | notes                                                       |
  | &nbsp;&nbsp;&nbsp;&nbsp;messages [             | Object Array | message list                                            |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smcAddress |   Address    | contract address                                          |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smcName    |    String    | contract name                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;method     |    String    |  method prototype                                                   |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to         |   Address    | transfer destination account address, only valid when the transaction is a standard brc20 transfer |
  | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value      |    String    | transfer amount (unit: cong), valid only when the transaction is standard brc20 transfer        |
  | &nbsp;&nbsp;}                                  |              |                                                              |
  | ]                                              |              |                                                              |

### 3.10 transaction

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_transaction?txHash=_&chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter** | **Type**  | **Comment** |
  | -------- | :-------: | ------------------------------------------------------------ |
  | txHash   | HexString | specifies the transaction hash, starting with '0x'                                |

- **Output SUCCESS Example**

  ```json
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

| **Parameter**     | **Type**               | **Comment**                                              |
| ------------ | ---------------------- | ----------------------------------------------------- |
| txHash       | HexString              | transaction hash, starting with '0x'                              |
| txTime       | String                 | transaction time                                            |
| code         | Uint32                 | transaction result code, 200 indicates successful, and other values indicate failure         |
| log          | String                 | transaction result description                                        |
| blockHash    | HexString              | the block hash of the transaction exixts, starting with '0x'                      |
| blockHeight  | Int64                  | the block height of the transaction exixts                                    |
| from         | Address                | address of transaction signer                                    |
| nonce        | Uint64                 | transaction signer transaction count.                                |
| gasLimit     | Uint64                 | maximum gas amount                                        |
| fee          | Uint64                 | transaction fee (unit: cong)                             |
| note         | String                 | notes                                                |
| messages     | Object Array           | message list                                     |
| smcAddress   | Address                | contract address                                   |
| smcName      | String                 | contract name                                            |
| method       | String                 |  method prototype                                            |
| to           | Address                | transfer destination account address, only valid when the transaction is a standard brc20 transfer |
| value        | String                 | transfer amount (unit: cong), valid only when the transaction is standard brc20 transfer |
| Tags         | []string               | list of receipts                                 |
| Name         | string                 | receipt name                                 |
| ContractAddr | string                 | contract address                                   |
| ReceiptBytes | []byte                 | receipt data prototype                         |
| ReceiptHash  | string                 | receipt hash                                 |
| Receipt      | map[string]interface{} | analytic receipt result                          |
| from         | string                 | address of transaction signer                                    |
| to           | string                 | destination account address of each receipt            |
| token        | string                 | token address                 |
| value        | string                 | the amount of each receipt          |



### 3.11 balance

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_balance?address=_&name=_&password=_&token=_&all=_&chainID=_&keyStorePath=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | [choose one from wallet information] account address, which is blank by default    |
  | name         |  String  | [choose one from account address] wallet name, which is blank by default       |
  | password     |  String  | [choose one from account address] wallet password, which is blank by default.    |
  | token        |  String  | [optional] token name, default to base token         |
  | all          |   Bool   | [optional] whether to query all asset balance marks. The default value is false     |
  | chainid      |  String  | [optional] Chain ID, the default is the configuration in the configuration file                     |
  | keystorepath |  String  | access wallet path, default is "./.keystore"              |

- **Output SUCCESS Example**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | token        |  String  | token name                                                   |
  | tokenAddress |  String  | token address                        |
  | balance      |  String  | account balance(uint: cong)                                  |

### 3.12 nonce

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_nonce?address=_&name=_&password=_&chainID=_&keyStorePath=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | address      | Address  | [choose one from wallet] account address                           |
  | name         |  String  | [choose one from account address] wallet address                       |
  | password     |  String  | [choose one from account address] wallet password                       |
  | chainid      |  String  | [optional] chain ID. the default value is the configuration in the configuration file      |
  | keystorepath |  String  | [optional] access wallet path, default "./.keystore"    |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
    "nonce": 5000
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | nonce    |  Uint64  | next available transaction count value of a specific address  on the blockchain                  |

### 3.13 commitTx

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_commitTx?tx=_&chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | tx       |  String  | *transaction data                                            |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
     "code": 200,
     "log": "Deliver tx succeed",
     "txHash": "0xA1C960B9D5DB633A6E45B45015A722A2C516B392F93C9BF41F5DAA1197030584",
     "height": 234389
  }

  ```

- **Output SUCCESS Result**

  | **Parameter**           | **Type**  | **Comment** |
  | ------------------ | :-------: | ------------------------------------------------------------ |
  | &nbsp;&nbsp;code   |    Int    | transaction verification / endorsement result code, 200 indicates success               |
  | &nbsp;&nbsp;log    |  String   | the description of the transaction verification / endorsement result. When the code is not equal to 200, it will describe a specific error information |
  | &nbsp;&nbsp;txHash | HexString | transaction hash, starting with `0x`           |
  | &nbsp;&nbsp;height |   Int64   | confirmed block number                     |

### 3.14 version

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_version?chainID=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | ——       |    ——    | ——                                                           |

- **Output SUCCESS Example**

  ```json
  OK
  Response: {
    version: 1.0.7.9636
  }
  ```

- **Output SUCCESS Result**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | version  |  string  | the current program version number                               |

### 3.15 query

- **Request URI over HTTPS**

  ```html
  https://localhost:37658/bcc_query?path=_
  ```

- **Request JSONRPC over HTTPS**

  ```json
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

| **Parameter** | **Type** | **Comment**                  |
| -------- | -------- | ------------------------- |
| path     | string   |[require] query the key for the specified information |

- **Output SUCCESS Example**

  ```json
  OK
  response: {
     "code"	:  200
     "key" : "L2NvbnRyYWN0L2FsbC8w"
     "value" : "WyJ0ZXN0NVpYaG8zdUw1WlNCV3BIMmlmbmJzQmFRY3k1NTNnWDhGIiwidGVzdEFSUlZmna3V4ekE1VlpGaGhvNjUxYkZGZ21ncyIsInRlc3Q2cnlWS1NnZFpCZ2NnUjNhV2djbWRaWEpLaDFRSnoiLCJ0ZXN0QWlXdXNuc0ZzVVFXa2ZIR1NLNXpoNjNGb3pDUFY1UGlCIiwidEs2a2pnQ2tBQm5TVFMxTUI4NkNpeEVRV005Nlpic1A5IiwidGVzdFA4ZEMyUHVCcHNVQDhqb0t1RjFFdXpaTFhGbXg1NyJd"
  }
  ```

- **Output SUCCESS Result**

| **Parameter** | **Type** | **Comment**                                               |
| -------- | -------- | ------------------------------------------------------ |
| code     | Int      | transaction verification / endorsement result code, 200 indicates success         |
| key      | string   | Base64 encoded string, encoded by the input parameter (path) |
| value    | string   | Base64 encoded string, encoded by the output result    |
