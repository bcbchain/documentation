# bcw

bcw：wallet tool, used to create, import and export wallets, sign binary or text files, then generate corresponding signature files

## 1. Usage

Execute command is as follows:

```shell
Usage:
  bcw [command] [flags]

Available commands:
  create         create a new wallet
  export         export a wallet
  import         import a wallet
  signFile       sign a file
  signData       sign raw data

Global flags:
  -h, --help   help for bcw

Use "bcw <command> --help" for more information about a command.
```

## 2. Commands Details

### 2.1 create

- **command**

  ```]
  bcw create --name=hotwal001 [--password=aBig62_123] [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **Option**     | **Type** | **Comment**|
  | :------------ | :------: | :------------------------------------------------------------ |
  | name | String | Wallet name, 1-40 characters in length, can only be composed of `uppercase letter, lowercase letter, number, @, ', -,.' '`. |
  | password | String | Optional, wallet password, 8-20 characters in length (it can be composed of any printable ASCII characters, which requires at least one lowercase letter, at least one uppercase letter, at least one number, and at least one non alphanumeric character). If do not specify a password at the command line, the program will prompt the user to enter the password twice.|
  | keystorepath |  String  | Optional, wallet storage path, if not specified, the system will use the default path |

- **Output SUCCESS Result**

  ```shell
  OK
  Pubkey: 0x01bd6c29d63f5f32aa33955f2...ea4de517e77db33958e6e
  ```

### 2.2 export

- **command**

  ```shell
  bcw export --name=hotwal001 [--password=aBig62_123] [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **Grammar**     | **Type** | **Comment** |
  | :------------ | :------: | :------------------------------------------------------------ |
  | name         |  String  | Wallet name                                                   |
  | password     |  String  | Optional, wallet password, 8-20 characters in length (it can be composed of any printable ASCII characters, which requires at least one lowercase letter, at least one uppercase letter, at least one number, and at least one non alphanumeric character). If do not specify a password at the command line, the program will prompt the user to enter a password |
  | keystorepath |  String  | Optional, wallet storage path, if not specified, the system will use the default path          |

- **Output SUCCESS Result**

  ```shell
  OK
  PrivateKey: 0x832c3477b3a730e9601ed774a...ff7d0333c21721dd33697
  PubKey:     0x01bd6c29d63f5f32aa33955f2...ea4de517e77db33958e6e
  ```

### 2.3 import

- **command**

  ```shell
  bcw import --name=hotwal001 [--password=aBig62_123] --privatekey=0xad3abc... [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **Grammar**     | **Type** | **Comment** |
  | ------------ | :-------: | ------------------------------------------------------------ |
  | name         |  String   | Wallet name                                                  |
  | password     |  String   | Optional, wallet password, 8-20 characters in length (it can be composed of any printable ASCII characters, which requires at least one lowercase letter, at least one uppercase letter, at least one number, and at least one non alphanumeric character). If do not specify a password at the command line, the program will prompt the user to enter the password twice. |
  | privatekey   | HexString | The imported plain private key, it can be 32 bits, or a 64-bit private key + public key, starting with "0x" |
  | keystorepath |  String   | Optional, wallet storage path, if not specified, the system will use the default path          |

- **Output SUCCESS Result**

  ```shell
  OK
  PubKey: 0x01bd6c29d63f5f32aa33955f2...ea4de517e77db33958e6e
  ```

### 2.4  signFile

- **command**

  ```shell
  bcw signFile --name=hotwal001 [--password=aBig62_123] --file=genesis.json --mode=t  [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **Grammar**     | **Type** | **Comment** |
  | ------------ | :------: | ------------------------------------------------------------ |
  | name         |  String  | Wallet name                                                   |
  | password     |  String  | Optional, wallet password, 8-20 characters in length (it can be composed of any printable ASCII characters, which requires at least one lowercase letter, at least one uppercase letter, at least one number, and at least one non alphanumeric character). If do not specify a password at the command line, the program will prompt the user to enter a password |
  | file         |  String  | Full name of the file to sign                                             |
  | mode         |  String  | Signature mode：&nbsp;t:text files；&nbsp;b:binaries       |
  | keystorepath |  String  | Optional, wallet storage path, if not specified, the system will use the default path      |

- **Output SUCCESS Result**

  ```shell
  OK
  SignatureFile: genesis.json.sig
  ```

### 2.5 signData

- **command**

  ```shell
  bcw signData --name=hotwal001 [--password=aBig62_123] --data=abcd12... --file=a.sig  [--keystorepath=/wallet/sdfsdfds]
  ```

- **Input Parameters**

  | **Grammar**     | **Type** | **Comment** |
  | ------------ | :-------: | ------------------------------------------------------------ |
  | name         |  String   | Wallet name                                                   |
  | password     |  String   | Optional, wallet password, 8-20 characters in length (it can be composed of any printable ASCII characters, which requires at least one lowercase letter, at least one uppercase letter, at least one number, and at least one non alphanumeric character). If do not specify a password at the command line, the program will prompt the user to enter a password |
  | data         | HexString | Hexadecimal form of data to be signed                                      |
  | file         |  String   | output filename after signing                                           |
  | keystorepath |  String   | Optional, wallet storage path, if not specified, the system will use the default path      |

- **Output SUCCESS Result**

  ```shell
  OK
  SignatureFile: a.sig
  ```
