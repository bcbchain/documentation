# sigorg

sigorg：输入.tar.gz文件名和开发者签名文件文件名，验签并输出组织签名文件（对开发者签名数据进行签名）

## 1. 使用方法

命令运行格式如下：

```
Usage:
  sigorg --smc=./dice2win_2.0.tar.gz  --name=hotwal001 [--password=aBig62_123]

Flags:
  -h, --help   help for sigorg
```

## 2. 命令详解

- **command**

  ```
  sigorg --smc=./dice2win_2.0.tar.gz  --name=hotwal001 [--password=aBig62_123]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | name     |  String  | 钱包名称。                                                   |
  | password |  String  | 可选项，钱包密码，长度8-20字符（可由任意可打印ASCII字符组成，要求至少有一个小写字母、至少一个大写字母、至少一个数字、至少一个非字母数字字符）。<br>如果命令行不指定密码，程序会提示用户输入密码。 |

- **Output SUCCESS Result**

  ```
  OK
  SignatureFile: dice2win_2.0.sig.sig
  ```
