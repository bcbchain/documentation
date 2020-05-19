# hdWallet概述

本文旨在交易所本地安装hdWallet时起到流程指导的作用。流程包含安装，创建钱包，命令详解等，具体流程见下文。

如需使用hdWallet_RPC远程服务，参见： [hdWallet_RPC远程服务说明](./hdWallet_RPC远程服务.md) 

# 1 hdWallet安装&升级

## 1.1 hdWallet常规安装&升级

### 1.1.1 hdWallet常规安装

1. 从github下载hdwallet最新的安装包，并解压，为了好管理，移动至/home/bcb-hdwallet

```bash
github下载相应资源
wget https://github.com/bcbchain/hdwallet/releases/download/v1.0/bcb-hdWallet_1.0-x64.tar.gz

解压资源
tar xf bcb-hdWallet_1.0-x64.tar.gz

将解压后的资源转移至/home/bcb-hdwallet
mv bcb-hdWallet_xxxxx-x64 /home/bcb-hdwallet
```

2. 进到/home/bcb-hdwallet/目录,ll -ah查看，得到以下目录及文件

```bash
.config       //配置文件
hdWallet      //本地可执行文件
hdWallet_rpc  //RPC可执行文件
history.txt   //操作历史
version       //工具版本
```

3. 如果本机安装有bcb节点程序，需修改nodeAddrSlice为本地bcb节点。

```bash
cd /home/bcb-hdwallet
vim .config/hdWallet.yaml

//配置文件设置参考下方
```

4. 配置文件设置

   ```
   //区块链标识以及区块链版本根据节点的链信息进行调整,如节点为本地节点,则使用命令  
   curl http://127.0.0.1:46657/health查看，若nodeAddrSlice下的节点非本地,则需要根据实际情况进行查询
   //以本地local链为例:
   {
     "jsonrpc": "2.0",
     "id": "",
     "result": {
       "chain_id": "local",
       "version": "2.2.1.18922",
       "chain_version": 2,
       "last_block_height": 1790,
       "validator_count": 1
     }
   }
   
   #区块链标识
   chainID: "local"  
   
   #区块链版本
   chainVersion: 2         //根据节点的链信息进行调整
   
   # 本地服务监听地址:端口
   serverAddr: "tcp://0.0.0.0:37657"
   
   # 是否使用
   httpsuseHttps: false
   
   //外部证书路径以.config目录下的.rpc.key文件为例:
   [root@localhost .config]# ls
   hdWallet.web.rpc.crt  hdWallet.web.rpc.key  hdWallet.yaml  version
   
   # 外部证书路径
   outCerPath: "./.config/hdWallet.web.rpc"
   #日志配置信息
   loggerScreen: true
   loggerFile: true
   loggerLevel: "debug"
   
   # 账户数据库存位置
   keyStorePath: "./.keystore"
   
   //若想接入的是本地节点,则需要修改ip为127.0.0.1:46657,其余节点注释掉
   #指定创智区块链节点的接入URL，热钱包需要此参数，冷钱包可以忽略此参数；
   nodeAddrSlice:   
   - "http://127.0.0.1:46657"
   - "https://earth.bcbchain.io"    
   - "https://mars.bcbchain.io"    
   - "https://mercury.bcbchain.io"    
   - "https://jupiter.bcbchain.io"    
   - "https://venus.bcbchain.io"    
   - "https://moon.bcbchain.io"    
   - "https://sirius.bcbchain.io"    
   - "https://vaga.bcbchain.io"    
   - "https://altair.bcbchain.io"
   ```

   

注： <font color=red>初次启动成功后生成.keystore目录；日志在log目录下面。</font>

### 1.1.2. hdWallet常规升级

注意：<font color=red>在生成助记词并生成密码后必须牢记助记词。根据助记词生成的钱包需要牢记其分层路径。密码丢失可以根据助记词再次随机生成，但助记词丢失后无法找回！</font>

1. 先停止程序

   ```
   ps -ef|grep hdWallet_rpc
   kill -9 pid
   ```

2. 升级hdWallet程序：下载最新的hdWallet程序包后解压，替换原有程序目录的hdWallet、hdWallet_rpc、version三个文件即可（替换前先停止程序再备份），提示全覆盖。注意.keystore和.config不可更改。

   ```
   cp -a hdWallet /home/bcb-hdwallet/
   cp -a hdWallet_rpc /home/bcb-hdwallet/
   cp -a version /home/bcb-hdwallet/
   ```

3. 启动

   ```
   ./hdWallet_rpc &
   ```

4. 查看hdwallet获取bcb区块高度和版本号是否正常，为此次升级的版本号

   ```
   curl http://127.0.0.1:37657/bcb_blockHeight
   curl http://127.0.0.1:37657/bcb_version
   ```



# 2  hdWallet创建

 查询RPC服务是否开启  开启需要关闭   关闭后直接生成助记词

```
ps -ef | grep rpc  //查询hdWallet_rpc服务是否开启

显示如下，不存在./hdWallet_rpc时，说明服务未开启：
root        977      2  0 10:46 ?        00:00:00 [rpciod]
***        66314  50954  0 17:09 pts/1    00:00:00 grep --color=auto rpc

显示如下，存在./hdWallet_rpc时，说明服务已开启：
root        977      2  0 10:46 ?        00:00:00 [rpciod]
root      #######      1  0 17:10 pts/0    00:00:00 ./hdWallet_rpc
***        66506  50954  0 17:11 pts/1    00:00:00 grep --color=auto rpc

```

如果服务已开启， 则关闭RPC服务

```
kill #######(为./hdWallet_rpc进程pid)
```

## 2.1 生成助记词

> 注：危险！：在使用HD钱包生成助记词之后必须进行助记词备份，否则钱包丢失或忘记密码后无法恢复钱包。

> 注：因为一个HD钱包可生成足够多私钥的属性，以及方便使用和管理，本版本只支持创建一次HD钱包。

- **command**

  ```
  ./hdWallet_rpc createMnemonic 
  ```

- **Output SUCCESS Example**

  ```
  {
    "mnemonic": "kitchen vast income save tail monitor kite outside volume chest bird master",
    "password": "3yeDJje6ZXGJ2oCdg15tTpY4R4MoctNApTVS3mg6mie3"
  }
  ```

- **Output SUCCESS Result**

  | **语法** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | mnemonic |  String  | 12个助记词，以单个空格隔开。                                 |
  | password |  String  | 随机生成的新助记词密码                                       |

注意：<font color=red>在生成助记词后，再调用./hdWallet_rpc开启客户端服务，两者无法同时开启。同样的，在./hdWallet_rpc下的changePassword/exportMnemonic/importMnemonic等命令也无法同时启动。</font>

## 2.2 启动RPC服务

```
./hdWallet_rpc  
```

## 2.3 生成钱包

- **command**

  ```
  hdWallet walletCreate --password 2oHQjWWKkGfUvWpeXV8qwgCTzrDh9fJ8hJV2L6gP6JeU [--path "m/44'/60'/0'/0/1"] [--url https://...]
  ```

- **Input Parameters**

  | **选项** | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | password |  String  | 助记词密码。<font color=red>助记词密码生成过程参见hdWallet_rpc命令详解。</font> |
  | path     |  String  | <font color=red>HD钱包路径:"m/44'/60'/0'/0/#"</font>, 其中”#“为数字，范围：[0, 4294967295]。 |
  | url      |  String  | 钱包服务地址，可选项，默认调用本地服务。                     |

- **Output FAILED Example**

  ```
  {
    "code": -32603,
    "message": "Invalid parameters.",
    "data": ""
  }
  ```

  注：所有命令执行错误返回格式相同，后面不再进行说明。

- **Output SUCCESS Example**

  返回：

  ```
  WalletCreate finish, [path=m/44'/60'/0'/0/1], [password=********]
  {
    "walletAddr": "localDhUdogRbcr8iT7hK8YJDdy6dRt2Nhm47g"
  }
  ```

- **Output SUCCESS Result**

  | **语法**   | **类型** | **注释**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------- | :------: | ------------------------------------------------------------ |
  | walletAddr | Address  | 钱包地址。                                                   |

### 2.3.1 示例

```
[root@localhost bin]# ./hdWallet walletCreate --password "3yeDJje6ZXGJ2oCdg15tTpY4R4MoctNApTVS3mg6mie3" --path "m/44'/60'/0'/0/1"

//返回信息如下:

[2020-05-12 11:24:27.285][+08][Info ][ 1] [http_server.go:29] Starting RPC HTTP server on tcp://0.0.0.0:37657
[2020-05-12 11:24:27.287][+08][Info ][ 24] [handler.go:23] WalletCreate begin, [password=********], [path=m/44'/60'/0'/0/1]
[2020-05-12 11:24:27.288][+08][Info ][ 24] [wallet.go:225] createAccount, [password=********], [path=m/44'/60'/0'/0/1]
[2020-05-12 11:24:27.355][+08][Info ][ 24] [handler.go:47] WalletCreate finish, [path=m/44'/60'/0'/0/1], [password=********]
{
  "walletAddr": "local4LBnSWWJu5pha6Us3o9VzaYToA8y9Bc6S"
}
```

