# BCB 节点

## 1. 概述

 BCB Node是BCB网络的全节点程序，可以存储 BCB 网络的全部数据，通过 P2P 的方式与BCB其他节点进行连接， 能够独立校验BCB区块链上的所有交易并实时更新数据，负责区块链的交易的广播和验证。 



## 2. 节点环境配置

### 2.1 系统要求

在搭建节点前需要准备如下环境：

```
操作系统：  CentOS 7 64 bit
硬件：		CPU 8核+，内存16GB+，硬盘512GB+（推荐SSD硬盘）
```



### 2.2 NTP服务安装

运行 BCBChain 节点需要保证节点时间同步，要求安装NTP服务：

```
sudo yum install ntp
```



### 2.3 docker环境安装

运行 BCBChain 节点需要安装 ```docker```，版本要求如下：

```
Docker 1.13.1 + 镜像：golang:alpine、alpine
```

BCBChain 已经为 ```docker``` 的安装准备了在线安装与离线安装资源，资源获取URL[在此](https://github.com/bcbchain/docker/releases/download/v1.0.11494/bcb-docker_setup_1.0.11494.tar.gz)。

下载完成 ```docker``` 资源后将资源解压到 ```docker``` 目录，执行离线安装 ```docker``` 运行环境及 BCBChain 需要用到的 ```docker``` 镜像的命令如下：

```
cd docker
./docker.offline-Install.sh
```

注: 上述离线安装脚本仅支持 ```CentOS 7-x86_64-1810``` 和 ```Ubuntu 18.04.2-x86_64```。



执行在线安装 ```docker``` 运行环境及 BCBChain 需要用到的 ```docker``` 镜像的命令如下：

```
cd docker
./docker.online-Install.sh
```

注:1 上述在线安装脚本仅支持 ```CentOS 7-x86_64``` 和 ```Ubuntu 18.04-x86_64```.

注2: 上述在线安装脚本将会自动升级操作系统到最新版本。



### 2.4  防火墙配置

运行 BCBChain 节点需要开放指定端口，命令如下：

```
firewall-cmd --add-port=32332/tcp --permanent
firewall-cmd --add-port=32333/tcp --permanent
firewall-cmd --add-port=46656/tcp --permanent
firewall-cmd --add-port=46657/tcp --permanent
firewall-cmd --reload
```



## 3. 节点安装

### 3.1 节点下载

节点程序下载链接：

```
https://github.com/bcbchain/bcbchain/releases
```

节点源码下载链接：

```
https://github.com/bcbchain/bcbchain
```

离线数据包下载链接：

```
http://211.154.140.124:43356/down/
```



### 3.2 全新安装

BCBChain 在 ```github.com``` 上发布了正式节点的安装包，以发布版本 ```2.0.1.13780``` 为例，安装包的下载URL如下：

```
https://github.com/bcbchain/docker/releases/download/v2.0.1.13780/bcb-node_2.0.1.13780-x64.tar.gz
```

下载安装包以后，安装一个全新的 BCBChain 节点需要执行如下的命令：

```
tar xvf bcb-node_2.0.1.13780-x64.tar.gz
./setup.sh
```

屏幕输出及交互过程示意如下：

```

SETUP bcchain...

Select which CHAINID to install
1) bcb
2) bcbtest
3) local
4) test
#? 1
You selected CHAINID=bcb

Start copying files ...
install sdk with version 2.0.1.13774
install thirdparty packages with version 2.0.1.12318
End of copy files.

Congratulation !!! BCCHAIN is successfully installed with version 2.0.1.13780.


SETUP tmcore...

Select which CHAINID to install
1) bcb
2) bcbtest
3) local
4) test
#? 1
You selected CHAINID=bcb

Start copying files ...
End of copy files.

Select which role that the node will run
1) UNOFFICIAL FOLLOWER
#? 1

You selected UNOFFICIAL follower

Please input the OFFICIAL follower's name[:port] you want to follow
Multi nodes can be separated by comma ,
for example "earth.bcbchain.io,mar.bcbchain.io:46657" or "venus.bcbchain.io"
officials to follow: earth.bcbchain.io

You selected "earth.bcbchain.io" to follow

Congratulation !!! TENDERMINT is successfully installed with version 2.0.1.13780.
```

安装完成以后，需要等待 BCBChain 区块同步完成（这需要几个小时到几天的时间）这个新搭建的节点才能对外提供交易服务。

### 3.3 快速同步

上面全新安装以后，BCBChain 区块同步比较慢，节点需要等待很长时间才能正常提供服务，我们在 BCBChain 官网提供官方认可的离线数据包，通过快速安装的方式可以快速完成 BCBChain 的区块同步，使节点快速对外提供服务。

下载安装包及离线数据包以后，快速安装一个全新的 BCBChain 节点需要执行如下的命令：

```
./setup.sh -t tmcore_data_20190717.tar.gz -c bcbchain_appstate.db_20190717.tar.gz
```

注：离线数据包文件名称为：tmcore_data_20190717.tar.gz 和 bcbchain_appstate.db_20190717.tar.gz

屏幕输出及交互过程同上。



### 3.4 升级程序

如果已经搭建好 BCBChain 的节点，只是需要升级新的程序，执行如下命令，依照交互提示可完成升级工作：

```
tar xvf bcb-node_2.0.1.13780-x64.tar.gz
./setup.sh
```

屏幕输出及交互过程示意如下：

```

SETUP bcchain...

Old data exists, do you want to remove all data to re-sync?
1) yes
2) no
#? 2
No, keep old data

Start copying files ...
End of copy files.

Congratulation !!! BCCHAIN is successfully updated from 2.0.1.13780 to version 2.0.1.13780.


SETUP tmcore...

Old data exists, do you want to remove all data to re-sync?
1) yes
2) no
#? 2
No, keep old data

Start copying files ...
End of copy files.

Congratulation !!! TENDERMINT is successfully updated from 2.0.1.13780 to version 2.0.1.13780.
```

安装或升级以后服务 BCBChain 的两个核心服务 `tmcore` 和 `bcchain` 将会自动启动。

执行如下命令可以控制共识引擎服务 `tmcore`的启动或停止：

```
systemctl start tmcoresystemctl stop tmcore
```

执行如下命令可以控制业务引擎服务 `bcchain` 的启动或停止：

```
systemctl start bcchainsystemctl stop bcchain
```

安装或升级完毕执行如下命令可以检测 BCBChain 的节点是否正常工作。

```
curl http://127.0.0.1:46657/health
```

屏幕输出示意如下：
```
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "chain_id": "bcb",
    "version": "2.0.1.13780",
    "chain_version": 0,
    "last_block_height": 153,
    "validator_count": 10
  }
}
```