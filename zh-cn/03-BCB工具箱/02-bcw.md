# bcw

bcw：钱包工具，用于创建、导入、导出钱包，和对二进制文件或者文本文件签名，并生成相应的签名文件

## 1. 使用方法

命令运行格式如下：

```
Usage:
  bcw [command] [flags]

Available commands:
  create         create a new wallet
  export  		 export a wallet
  import         import a wallet
  signFile       sign a file
  signData       sign raw data

Global flags:
  -h, --help   help for bcw

Use "bcw <command> --help" for more information about a command.
```



## 2. 命令详解

### 2.1 create

- **command**

  ```]
  bcw create --name=hotwal001 [--password=aBig62_123] [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **选项**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | 钱包名称，长度1-40字符，只能由```大写字母、小写字母、数字、@、_、-、. ```组成。 |
  | password     |  String  | 可选项，钱包密码，长度8-20字符（可由任意可打印ASCII字符组成，要求至少有一个小写字母、至少一个大写字母、至少一个数字、至少一个非字母数字字符）。<br>如果命令行不指定密码，程序会提示用户输入两遍密码。 |
  | keystorepath |  String  | 可选项，钱包存储路径，如果不指定，系统就采用默认路径         |

- **Output SUCCESS Result** 

  ```
  OK
  Pubkey: 0x01bd6c29d63f5f32aa33955f2...ea4de517e77db33958e6e
  ```


### 2.2  export

- **command**

  ```
  bcw export --name=hotwal001 [--password=aBig62_123] [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | 钱包名称。                                                   |
  | password     |  String  | 可选项，钱包密码，长度8-20字符（可由任意可打印ASCII字符组成，要求至少有一个小写字母、至少一个大写字母、至少一个数字、至少一个非字母数字字符）。<br>如果命令行不指定密码，程序会提示用户输入密码。 |
  | keystorepath |  String  | 可选项，钱包存储路径，如果不指定，系统就采用默认路径         |

- **Output SUCCESS Result**

  ```
  OK
  PrivateKey: 0x832c3477b3a730e9601ed774a...ff7d0333c21721dd33697
  PubKey:     0x01bd6c29d63f5f32aa33955f2...ea4de517e77db33958e6e
  ```



### 2.3  import

- **command**

  ```
  bcw import --name=hotwal001 [--password=aBig62_123] --privatekey=0xad3abc... [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **语法**     | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :-------: | ------------------------------------------------------------ |
  | name         |  String   | 钱包名称。                                                   |
  | password     |  String   | 可选项，钱包密码，长度8-20字符（可由任意可打印ASCII字符组成，要求至少有一个小写字母、至少一个大写字母、至少一个数字、至少一个非字母数字字符）。<br/>如果命令行不指定密码，程序会提示用户输入两遍密码。 |
  | privatekey   | HexString | 导入的私钥明文，可以为32位私钥，也可以是64位私钥+公钥,以“0x”开头 |
  | keystorepath |  String   | 可选项，钱包存储路径，如果不指定，系统就采用默认路径         |

- **Output SUCCESS Result**

  ```
  OK
  PubKey: 0x01bd6c29d63f5f32aa33955f2...ea4de517e77db33958e6e
  ```


### 2.4  signFile

- **command**

  ```
  bcw signFile --name=hotwal001 [--password=aBig62_123] --file=genesis.json --mode=t  [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **语法**     | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | 钱包名称。                                                   |
  | password     |  String  | 可选项，钱包密码，长度8-20字符（可由任意可打印ASCII字符组成，要求至少有一个小写字母、至少一个大写字母、至少一个数字、至少一个非字母数字字符）。<br/>如果命令行不指定密码，程序会提示用户输入密码。 |
  | file         |  String  | 要签名的文件全名                                             |
  | mode         |  String  | 签名模式：<br>&nbsp;t:文本文件；<br>&nbsp;b:二进制文件       |
  | keystorepath |  String  | 可选项，钱包存储路径，如果不指定，系统就采用默认路径         |

- **Output SUCCESS Result**

  ```
  OK
  SignatureFile: genesis.json.sig
  ```


### 2.5  signData

- **command**

  ```
  bcw signData --name=hotwal001 [--password=aBig62_123] --data=abcd12... --file=a.sig  [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **语法**     | **类型**  | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ------------ | :-------: | ------------------------------------------------------------ |
  | name         |  String   | 钱包名称。                                                   |
  | password     |  String   | 可选项，钱包密码，长度8-20字符（可由任意可打印ASCII字符组成，要求至少有一个小写字母、至少一个大写字母、至少一个数字、至少一个非字母数字字符）。<br>如果命令行不指定密码，程序会提示用户输入密码。 |
  | data         | HexString | 待签名数据的16进制形式                                       |
  | file         |  String   | 签名后输出的文件名                                           |
  | keystorepath |  String   | 可选项，钱包存储路径，如果不指定，系统就采用默认路径         |

- **Output SUCCESS Result**

  ```
  OK
  SignatureFile: a.sig
  ```
