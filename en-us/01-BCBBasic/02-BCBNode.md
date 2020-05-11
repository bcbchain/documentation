# BCB Node

## 1. Overview

 BCB Node is a full node program of the BCB network. It can store all the data of the BCB network and connect with other BCB nodes through P2P. It can verify all transactions on the BCB blockchain independently, update data in real time and broadcast and verify transactions on the blockchain.

## 2. Node configuration

### 2.1 System Requirements

Before setting up a node, you need to prepare the following environment:

```shell
Operating system: CentOS 7 64 bit
Hardware: CPU 8 core +, memory 16GB +, HD 512GB + (SSD recommended)
```

### 2.2 Install NTP Service

In order to run a BCBChain node, you should ensure to sync the node time, so you must install NTP service:

```shell
sudo yum install ntp
```

### 2.3 Run With Docker

You need to install the `docker` to run a BCBChain node, the version requirements are:

```shell
Docker 1.13.1 + images: golang: alpine, alpine
```

We have prepared online and offline resources for the installation of `docker`, you can get at [here](https://github.com/bcbchain/docker/releases/download/v1.0.11494/bcb-docker_setup_1.0.11494.tar.gz).

After downloading, decompress the resource to the `docker` directory, and then run the following command to install `docker` runtime environment offline:

```shell
cd docker
./docker.offline-Install.sh
```

Notice 1: The above installation script only supports `CentOS 7-x86_64-1810` and `Ubuntu 18.04.2-x86_64`.

Notice 2: The above online installation script will automatically upgrade the operating system to the latest version.

### 2.4  Firewall Configuration

The BCBChain node needs to open the specified port. The commands are:

```shell
firewall-cmd --add-port=32332/tcp --permanent
firewall-cmd --add-port=32333/tcp --permanent
firewall-cmd --add-port=46656/tcp --permanent
firewall-cmd --add-port=46657/tcp --permanent
firewall-cmd --reload
```

## 3. Install Node

### 3.1 Download node

Download the node program by this link:

```html
https://github.com/bcbchain/bcbchain/releases
```

Download the node source by this link：

```html
https://github.com/bcbchain/bcbchain
```

Download the offline data by this link：

```html
http://211.154.140.124:43356/down/
```

### 3.2 Install

BCBChain released the installation package of the official node on `github.com`. Taking the release version `2.0.1.13780` as an example, you can download the installation package by this URL:

```html
https://github.com/bcbchain/docker/releases/download/v2.0.1.13780/bcb-node_2.0.1.13780-x64.tar.gz
```

After downloading, just run the command as follow:

```shell
tar xvf bcb-node_2.0.1.13780-x64.tar.gz
./setup.sh
```

You can see the following screen output and interactive process:

```shell
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
install third party packages with version 2.0.1.12318
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

After finishing the installation, you need to wait for the BCBChain block synchronization to complete (this takes several hours to several days). Then the new built node can provide external transaction services.

### 3.3 Quickly Sync

After installation is finished as above, you will notice the BCBChain block synchronization is relatively slow. So nodes need to wait for a long time before they can provide services normally. We provide officially recognized offline data packets on the BCBChain official website. The BCBChain block synchronization can be completed quickly by the quick installation method, then nodes can quickly provide services externally.

After downloading installation package and offline data, just run following command to install BCBChain quickly:

```shell
./setup.sh -t tmcore_data_20190717.tar.gz -c bcbchain_appstate.db_20190717.tar.gz
```

Notice: Offline data package file names are: `tmcore_data_20190717.tar.gz` and `bcbchain_appstate.db_20190717.tar.gz`

The screen output and interaction process are the same as above.

### 3.4 Upgrade Program

If the BCBChain node has been set up, you just need to upgrade the new program, execute the following command, and follow the interactive prompts to complete the upgrade:

```shell
tar xvf bcb-node_2.0.1.13780-x64.tar.gz
./setup.sh
```

You can see the following screen output and interactive process:

```shell

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

After installing or upgrading the service, BCBChain's two core services `tmcore` and`bcchain` will start automatically.

Run the following command to start or stop the consensus engine service `tmcore`：

```shell
systemctl start tmcoresystemctl stop tmcore
```

Run the following command to start or stop the business engine service `bcchain`：

```shell
systemctl start bcchainsystemctl stop bcchain
```

After installation or upgrade, execute the following command to check whether the BCBChain node is working properly.

```shell
curl http://127.0.0.1:46657/health
```

You can get the following screen output:

```shell
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
