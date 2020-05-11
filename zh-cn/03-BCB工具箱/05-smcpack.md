
# smcpack

smcpack：

打包合约，指定合约目录，打包成 .tar.gz, 只打包合约代码，去掉测试文件；

合约签名，输入.tar.gz 输出签名文件（对codehash签名）

## 1. 使用方法

命令运行格式如下：

```
Usage:
  smcpack --path=dice2win/v2.0/dice2win  --name=hotwal001 [--password=aBig62_123]
  
Flags:
  -h, --help   help for smcpack
```

## 2. 命令详解

- **command**

  ```
  smcpack --path=dice2win/v2.0/dice2win  --name=hotwal001 [--password=aBig62_123]
  ```

- **Input Parameters**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | path     |  String  | 合约代码的目录                                               |
  | name     |  String  | 钱包名称。                                                   |
  | password |  String  | 可选项，钱包密码，长度8-20字符（可由任意可打印ASCII字符组成，要求至少有一个小写字母、至少一个大写字母、至少一个数字、至少一个非字母数字字符）。<br>如果命令行不指定密码，程序会提示用户输入密码。 |

- **Output SUCCESS Result**

  ```
  OK
  TarFile: dice2win.tar.gz
  ```
