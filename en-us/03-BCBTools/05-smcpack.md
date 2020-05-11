
# smcpack

smcpack：

Package the contract, specify the contract directory, package it into `.tar.gz`, only package the contract code, and remove the test file;

Sign contract, input `.tar.gz`, output signature file (for codehash signature)

## 1. Usage

The format of the command is as follows:

```shell
Usage:
  smcpack --path=dice2win/v2.0/dice2win  --name=hotwal001 [--password=aBig62_123]

Flags:
  -h, --help   help for smcpack
```

## 2. Detailed command

- **command**

  ```shell
  smcpack --path=dice2win/v2.0/dice2win  --name=hotwal001 [--password=aBig62_123]
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | path     |  String  | directory of contract code                                    |
  | name     |  String  | wallet name                                               |
  | password |  String  | optional, wallet password, 8-20 characters in length (it can be composed of any printable ASCII characters, and it is required to have at least one lowercase letter, at least one uppercase letter, at least one number, and at least one non alphanumeric character). <br>If the command line does not specify a password, the program prompts the user for the password. |

- **Output SUCCESS Result**

  ```shell
  OK
  TarFile: dice2win.tar.gz
  ```
