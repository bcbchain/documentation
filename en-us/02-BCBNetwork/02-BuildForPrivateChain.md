# Private Chain Building Guide

## 1. Environment

As for node programs downloading and installation environment configuration, please refer to the `BCB Node` section.

## 2. Build A Single Node

The IP of the default single node when installs is `127.0.0.1`, if you want to use a real IP when deploy, please modify the genesis node profile in the installation directory:

`install-tmcore/pieces/local/v2/local-nodes.json`

Execute the following commands, and in the interactive state, select the chain id, note type in turn, and then wait for about 10s to finish the installation of the test chain consensus engine, once installed successfully, the consensus engine will automatically start the service.

```shell
cd install-tmcore
./install.sh
```

You can see the following screen output:

```shell
Select which CHAINID to install
1) local
#? 1
You selected CHAINID=local

Start copying files ...
End of copy files.

Select which role that the node will run
1) VALIDATOR -- be sure all the validator nodes are installing at the same time
2) UNOFFICIAL FOLLOWER
#? 1
You selected VALIDATOR node

Initializing all genesis node...
Listen @ :46656
notifiedMap: map[node1:true]
doneSent: map[127.0.0.1:true]
all finished ,gracefully quit
10..9..sendResult: node1:{pub:true,pri:true,},
8..7..sendResult: node1:{pub:true,pri:true,},
6..sendResult: node1:{pub:true,pri:true,},
5..sendResult: node1:{pub:true,pri:true,},
4..3..sendResult: node1:{pub:true,pri:true,},
2..sendResult: node1:{pub:true,pri:true,},
1..

Congratulation !!! TENDERMINT is successfully installed with version 2.0.1.13780.
```

If the test chain has been built, you just need to upgrade the node program, execute the following commands, follow the interactive prompt to complete the upgrade:

```shell
cd install-tmcore
./update.sh
```

You can see the following screen output:

```shell
Old data exists, do you want to remove all data to re-sync?
1) yes
2) no
#? 2
No, keep old data

Start copying files ...
End of copy files.

Congratulation !!! TENDERMINT is successfully updated from 2.0.1.13780 to version 2.0.1.13780.
```

After installing or upgrading the service, BCBChain's service `tmcore` will start automatically. Run the following command to start or stop it：

```shell
systemctl start tmcore
systemctl stop tmcore
```

Execute the following commands to finish the build of the test chain business engine `bcchain` installation directory.

```shell
mkdir install-bcchain
mkdir install-bcchain/pieces
mkdir install-bcchain/pieces/local
mkdir install-bcchain/pieces/local/.config
cp -r bcbchain/bundle/setup/linux/bcchain/* install-bcchain/
cp -r bcbchain/bundle/.config/local/* install-bcchain/pieces/local/.config
cp bcbchain/bin/bcchain install-bcchain/pieces/
cp bcbchain/version install-bcchain/pieces/
cp sdk/version install-bcchain/pieces/version_sdk
cp thirdparty/version install-bcchain/pieces/version_thirdparty
version=$(cat sdk/version | tr -d "\r")
tar cvfz install-bcchain/pieces/sdk_${version}.tar.gz sdk
version=$(cat thirdparty/version | tr -d "\r")
tar cvfz install-bcchain/pieces/thirdparty_${version}.tar.gz thirdparty
```

Execute the following commands, and in the interactive state, select the chain id: `local`, then you can finish the installation of the test chain business engine, and once it's installed successfully, the business engine `bccchain` will automatically start the service.

```shell
cd install-bcchain
./install.sh
```

You can see the following screen output:

```shell
Select which CHAINID to install
1) local
#? 1
You selected CHAINID=local

Start copying files ...
install sdk with version 2.0.1.13774
install thirdparty packages with version 2.0.1.12318
End of copy files.

Congratulation !!! BCCHAIN is successfully installed with version 2.0.1.13780.
```

If the test chain has been built, you just need to upgrade the node program, execute the following commands, follow the interactive prompt to complete the upgrade:

```shell
cd install-bcchain
./update.sh
```

You can see the following screen output:

```shell
Old data exists, do you want to remove all data to re-sync?
1) yes
2) no
#? 2
No, keep old data

Start copying files ...
End of copy files.

Congratulation !!! BCCHAIN is successfully updated from 2.0.1.13780 to version 2.0.1.13780.
```

After installing or upgrading the service `bcchain`, it will start automatically. Run the following command to start or stop it：

```shell
systemctl start bcchain
systemctl stop bcchain
```

After installation, wait for genesis block creation to complete(this will cost some minutes), execute the following command to check whether the test chain is working properly.

```shell
curl http://127.0.0.1:46657/health
```

You can see the following screen output:

```shell
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "chain_id": "local",
    "version": "2.0.1.13780",
    "chain_version": 2,
    "last_block_height": 1,
    "validator_count": 1
  }
}
```

## 3. Build Four-Nodes Test chain

BCBChain's open source code comes with a full set of creation parameters to build a four-node test chain, and noce the source code is compiled, executing the following commands to finish the build of the installation directory of the consensus engine `tendermint`.

```shell
mkdir install-tmcore install-tmcore/pieces install-tmcore/pieces/test
cp -r bcbchain/bundle/setup/linux/tmcore/* install-tmcore/
cp -r bcbchain/bundle/genesis/test/v2 install-tmcore/pieces/test/v2
cp bcbchain/bundle/.config/test/tendermint-forks.* install-tmcore/pieces/test/v2
cp bcbchain/bin/tendermint install-tmcore/pieces/
cp bcbchain/bin/p2p_ping install-tmcore/pieces/
cp bcbchain/version install-tmcore/pieces/

```

Notice: The default node IPs of the four-node test chain with open source code are:

```html
192.168.1.101,
192.168.1.102、
192.168.1.103、
192.168.1.104
```

If you want to use a real IP when deploy, please modify the genesis node profile in the installation directory:

```shell
install-tmcore/pieces/test/v2/test-nodes.json
```

Copy the installation directory to the planned node, execute the following commands, and in the interactive state, select the chain id: `test`, note type: `VALIDATOR` in turn, and then wait for about 10s to finish the installation of the test chain consensus engine, once installed successfully, the consensus engine will automatically start the service `tmcore`.

```shell
cd install-tmcore
./install.sh
```

You can see the following screen output:

```shell
Select which CHAINID to install
1) test
#? 1
You selected CHAINID=test

Start copying files ...
End of copy files.

Select which role that the node will run
1) VALIDATOR -- be sure all the validator nodes are installing at the same time
2) UNOFFICIAL FOLLOWER
#? 1
You selected VALIDATOR node

Initializing all genesis node...
Listen @ :46656
notifiedMap: map[node3:true node4:true node1:true node2:true]
doneSent: map[192.168.1.101:true 192.168.1.102:true 192.168.1.103:true 192.168.1.104:true]
all finished ,gracefully quit
10..sendResult: node1:{pub:true,pri:true,}, node2:{pub:true,pri:true,}, node3:{pub:true,pri:true,}, node4:{pub:true,pri:true,},
9..8..sendResult: node1:{pub:true,pri:true,}, node2:{pub:true,pri:true,}, node3:{pub:true,pri:true,}, node4:{pub:true,pri:true,},
7..sendResult: node1:{pub:true,pri:true,}, node2:{pri:true,pub:true,}, node3:{pub:true,pri:true,}, node4:{pub:true,pri:true,},
6..5..sendResult: node1:{pub:true,pri:true,}, node2:{pub:true,pri:true,}, node3:{pub:true,pri:true,}, node4:{pub:true,pri:true,},
4..sendResult: node1:{pub:true,pri:true,}, node2:{pub:true,pri:true,}, node3:{pri:true,pub:true,}, node4:{pub:true,pri:true,},
3..2..sendResult: node1:{pri:true,pub:true,}, node2:{pub:true,pri:true,}, node3:{pub:true,pri:true,}, node4:{pub:true,pri:true,},
1..sendResult: node1:{pub:true,pri:true,}, node2:{pub:true,pri:true,}, node3:{pub:true,pri:true,}, node4:{pub:true,pri:true,},

Congratulation !!! TENDERMINT is successfully installed with version 2.0.1.13780.
```

If the test chain has been built, you just need to upgrade the node program, execute the following commands, follow the interactive prompt to complete the upgrade:

```shell
cd install-tmcore
./update.sh
```

You can see the following screen output:

```shell
Old data exists, do you want to remove all data to re-sync?
1) yes
2) no
#? 2
No, keep old data

Start copying files ...
End of copy files.

Congratulation !!! TENDERMINT is successfully updated from 2.0.1.13780 to version 2.0.1.13780.
```

After installing or upgrading the service, BCBChain's service `tmcore` will start automatically. Run the following command to start or stop it：

```shell
systemctl start tmcore
systemctl stop tmcore
```

Execute the following commands to finish the build of the test chain business engine `bcchain` installation directory.

```shell
mkdir install-bcchain
mkdir install-bcchain/pieces
mkdir install-bcchain/pieces/test
mkdir install-bcchain/pieces/test/.config
cp -r bcbchain/bundle/setup/linux/bcchain/* install-bcchain/
cp -r bcbchain/bundle/.config/test/* install-bcchain/pieces/test/.config
cp bcbchain/bin/bcchain install-bcchain/pieces/
cp bcbchain/version install-bcchain/pieces/
cp sdk/version install-bcchain/pieces/version_sdk
cp thirdparty/version install-bcchain/pieces/version_thirdparty
version=$(cat sdk/version | tr -d "\r")
tar cvfz install-bcchain/pieces/sdk_${version}.tar.gz sdk
version=$(cat thirdparty/version | tr -d "\r")
tar cvfz install-bcchain/pieces/thirdparty_${version}.tar.gz thirdparty

```

Copy the installation directory to the planned node, execute the following commands, and in the interactive state, select the chain id: `test`, then you can finish the installation of the test chain business engine, and once it's installed successfully, the business engine `bccchain` will automatically start the service.

```shell
cd install-bcchain
./install.sh
```

You can see the following screen output:

```shell
Select which CHAINID to install
1) test
#? 1
You selected CHAINID=test

Start copying files ...
install sdk with version 2.0.1.13774
install thirdparty packages with version 2.0.1.12318
End of copy files.

Congratulation !!! BCCHAIN is successfully installed with version 2.0.1.13780.
```

If the test chain has been built, you just need to upgrade the node program, execute the following commands, follow the interactive prompt to complete the upgrade:

```shell
cd install-bcchain
./update.sh
```

You can see the following screen output:

````shell
Old data exists, do you want to remove all data to re-sync?
1) yes
2) no
#? 2
No, keep old data

Start copying files ...
End of copy files.

Congratulation !!! BCCHAIN is successfully updated from 2.0.1.13780 to version 2.0.1.13780.
````

After installing or upgrading the service `bcchain`, it will start automatically. Run the following command to start or stop it：

```shell
systemctl start bcchain
systemctl stop bcchain
```

After installation, wait for genesis block creation to complete(this will cost some minutes), execute the following command to check whether the test chain is working properly.

```shell
curl http://192.168.1.101:46657/health
```

You can see the following screen output:

```shell
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "chain_id": "test",
    "version": "2.0.1.13780",
    "chain_version": 2,
    "last_block_height": 1,
    "validator_count": 4
  }
}
```
