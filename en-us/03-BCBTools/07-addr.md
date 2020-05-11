# addr

addr：input chain id and wallet name, then export address

## 1. Usage

The format of the command is as follows:

```shell
Usage:
  addr --name=hotwal001 [--password=aBig62_123] --chainid=local

Flags:
  -h, --help   help for addr
```

## 2. Detailed command

- **command**

  ```shell
  addr --name=hotwal001 [--password=aBig62_123] --chainid=local
  ```

- **Input Parameters**

  | **Parameter** | **Type** | **Comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | name     |  String  | wallet name                                               |
  | password |  String  | optional, wallet password, 8-20 characters in length (it can be composed of any printable ASCII characters, and it is required to have at least one lowercase letter, at least one uppercase letter, at least one number, and at least one non alphanumeric character). <br>If the command line does not specify a password, the program prompts the user for the password. |
  | chainid  |  String  | chain id                                                        |

- **Output SUCCESS Result**

  ```shell
  OK
  Address: localL9BzYNYns5VCRaJgfHEBJLzS1bhpHjx7j
  ```
