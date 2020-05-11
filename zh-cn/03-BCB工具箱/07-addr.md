# addr

addr：输入链id和钱包名字，导出地址

## 1. 使用方法

命令运行格式如下：

```
Usage:
  addr --name=hotwal001 [--password=aBig62_123] --chainid=local

Flags:
  -h, --help   help for addr
```

## 2. 命令详解

- **command**

  ```
  addr --name=hotwal001 [--password=aBig62_123] --chainid=local
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | name     |  String  | 钱包名称。                                                   |
  | password |  String  | 可选项，钱包密码，长度8-20字符（可由任意可打印ASCII字符组成，要求至少有一个小写字母、至少一个大写字母、至少一个数字、至少一个非字母数字字符）。<br/>如果命令行不指定密码，程序会提示用户输入密码 |
  | chainid  |  String  | 链id                                                         |

- **Output SUCCESS Result**

  ```
  OK
  Address: localL9BzYNYns5VCRaJgfHEBJLzS1bhpHjx7j
  ```
