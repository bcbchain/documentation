# sigorg

sigorg：Input the file name with `.tar.gz` and developer signature, verify signature and output organization signature file (sign developer signature data)

## 1. Usage

The format of the command is as follows:

```shell
Usage:
  sigorg --smc=./dapp_2.0.tar.gz  --name=hotwal001 [--password=aBig62_123]

Flags:
  -h, --help   help for sigorg
```

## 2. Detailed command

- **command**

  ```shell
  sigorg --smc=./dapp_2.0.tar.gz  --name=hotwal001 [--password=aBig62_123]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | name     |  String  | wallet name                                               |
  | password |  String  | optional, wallet password, 8-20 characters in length (it can be composed of any printable ASCII characters, and it is required to have at least one lowercase letter, at least one uppercase letter, at least one number, and at least one non alphanumeric character). <br>If the command line does not specify a password, the program prompts the user for the password. |

- **Output SUCCESS Result**

  ```shell
  OK
  SignatureFile: dapp_2.0.sig.sig
  ```
