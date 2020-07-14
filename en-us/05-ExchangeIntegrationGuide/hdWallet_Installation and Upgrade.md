# Overview of hdWallet

This document serves as a guide for the installation of hdWallet. It includes installation, creation of hdWallet, and detailed explanation of each command. Specifications of each process are below. 

For details on hdWallet_RPC remote interface, please refer to [hdWallet_RPC Remote Interface Documentation](./hdWallet_RPC english.md)


# 1 hdWallet Installation & Upgrade

## 1.1 hdWallet Regualr Installation & Upgrade

### 1.1.1 hdWallet Regular Installation

1. Download and unzip the latest hdWallet installation package from GitHub and move to /home/bcb-hdwallet

```bash
Download the corresponding file from github
wget https://github.com/bcbchain/hdwallet/releases/download/v1.0/bcb-hdWallet_1.0-x64.tar.gz

Upzip the following file
tar xf bcb-hdWallet_1.0-x64.tar.gz

Once unzipped, move the file to /home/bcb-hdwallet
mv bcb-hdWallet_xxxxx-x64 /home/bcb-hdwallet
```

2. Go to /home/bcb-hdwallet/table of contents and check that the following files are present

```bash
.config       //Configuration
hdWallet      //Local Executable file
hdWallet_rpc  //RPC Executable file
history.txt   //Execution history
version       //Version
```

3. If installation requires bcb node program, you have to modify the nodeAddrSlice to the local bcb node

```bash
cd /home/bcb-hdwallet
vim .config/hdWallet.yaml

//Please refer below for more details on the configuraiton file setting

```

4. Configuration Setting

   ```
   //The blockchain logo and blockchain version are adjusted according to the node's chain information. If it is a local node, please use the command 
   curl http://127.0.0.1:46657/health. If the node under nodeAddrSlice is not local, you are required to query accordingly. 
   //Example of a local chain:
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
   
   #Blockchain Logo
   chainID: "local"  
   
   #Blockchain Version
   chainVersion: 2         //Adjust according to the node's chain information
   
   # Local Listener Address: port
   serverAddr: "tcp://0.0.0.0:37657"
   
   # Whether in use 
   httpsuseHttps: false
   
   //For example, using .rpc.key file found in .config directory in the external certification path: 
   [root@localhost .config]# ls
   hdWallet.web.rpc.crt  hdWallet.web.rpc.key  hdWallet.yaml  version
   
   # External Certification Path
   outCerPath: "./.config/hdWallet.web.rpc"
   #Configuration Information Log
   loggerScreen: true
   loggerFile: true
   loggerLevel: "debug"
   
   # Location of the account data inventory
   keyStorePath: "./.keystore"
   
   //To access the local node, you are require to modify the IP to 127.0.0.1:46657 and comment out any remaining nodes
   #URL for the access to ChuangZhi blockchain node. This parameter is only required for hot wallets. It can be ignored for cold wallet. 
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

   

Note: <font color=red>The .keystore directory is generated after the initial set up is successful; Log is under the log directory.</font>

### 1.1.2. hdWallet Regular Upgrade

Note: <font color=red>Please remember the mnemonic after generating the mnemonic and the password. Please also keep in mind the layered paths of the wallet generated from the mnemonic words. A new password could be generated using the mnemonic words but it is impossible to recover lost mnemonic words! </font>

1. Stop Program

   ```
   ps -ef|grep hdWallet_rpc
   kill -9 pid
   ```

2. Procedure to upgrade hdWallet: Download and unzip the latest hdWallet package and replace the old hdWallet, hdWallet_rpc and version with the 3 new files in the latest hdWallet package (back up and stop the program before replacing the new files) for full coverage. Note that .keystor and .config cannot be changed. 

   ```
   cp -a hdWallet /home/bcb-hdwallet/
   cp -a hdWallet_rpc /home/bcb-hdwallet/
   cp -a version /home/bcb-hdwallet/
   ```

3. Start up

   ```
   ./hdWallet_rpc &
   ```

4. Check that the hdWallet is able to obtain the correct bcb height and version with reference to the version number of the upgrade. 

   ```
   curl http://127.0.0.1:37657/bcb_blockHeight
   curl http://127.0.0.1:37657/bcb_version
   ```



# 2  Create hdWallet

 Please check that the RPC service is disabled and generate mnemonic words directly once RPC service is disabled.

```
ps -ef | grep rpc  //Check if hdWallet_rpc service is enabled

The ./hdWallet_rpc is disabled if the display is as follows: 
root        977      2  0 10:46 ?        00:00:00 [rpciod]
***        66314  50954  0 17:09 pts/1    00:00:00 grep --color=auto rpc

The ./hdWallet_rpc is enabled if the display is as follows: 
root        977      2  0 10:46 ?        00:00:00 [rpciod]
root      #######      1  0 17:10 pts/0    00:00:00 ./hdWallet_rpc
***        66506  50954  0 17:11 pts/1    00:00:00 grep --color=auto rpc

```

Please disable the RPC service if it is currently enabled. 

```
kill #######(For ./hdWallet_rpc process pid)
```

## 2.1 Generate mnemonic words

> Note: Danger!: Please make a backup of the mnemonic words after using the HD wallet to generate the mnemonic words. Otherwise, you would not be able to restore the wallet if the wallet is lost or you have forgotten the password. 

> Note: As the HD wallet is able to generate multiple private key attributes and is convenient to be used and managed by users, this version can only support a one time creation of the HD wallet.

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

  | **Name** | **Type** | **Annotation**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | mnemonic |  String  | 12 mnemonic words, separated by a single space.              |
  | password |  String  | Randomly generated new mnemonic password.                    |

Note: <font color=red>After generating the mnemonic words, you are able to run ./hdWallet_rpc to start the client service. They cannot be done concurrently. Similarly, commands under./hdWallet_rpc such as changePassword/exportMnemonic/importMnemonic cannot be run concurrently.</font>
## 2.2 Start RPC service

```
./hdWallet_rpc  
```

## 2.3 Create Wallet

- **command**

  ```
  hdWallet walletCreate --password 2oHQjWWKkGfUvWpeXV8qwgCTzrDh9fJ8hJV2L6gP6JeU [--path "m/44'/60'/0'/0/1"] [--url https://...]
  ```

- **Input Parameters**

  | **Options** | **Type** | **Annotation**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | -------- | :------: | ------------------------------------------------------------ |
  | password |  String  | Mnemonic password. <font color=red>Please refer to the hdWallet_rpc command for a detailed description of the mnemonic password generation process</font> |
  | path | String | <font color=red>HD Wallet path:"m/44'/60'/0'/0/#"</font>, where ”#“ is a number in the range: [0, 4294967295]. |
  | url | String | Wallet service address. Optional, the default is local service. |


  

- **Output FAILED Example**

  ```
  {
    "code": -32603,
    "message": "Invalid parameters.",
    "data": ""
  }
  ```

  Note: All command execution errors are return as the same format and there will be no further explanation.

- **Output SUCCESS Example**

  Return：

  ```
  WalletCreate finish, [path=m/44'/60'/0'/0/1], [password=********]
  {
    "walletAddr": "localDhUdogRbcr8iT7hK8YJDdy6dRt2Nhm47g"
  }
  ```

- **Output SUCCESS Result**

  | **Name**   | **Type** | **Annotation**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | ---------- | :------: | ------------------------------------------------------------ |
  | walletAddr | Address  | Wallet address.                                              |

### 2.3.1 Example

```
[root@localhost bin]# ./hdWallet walletCreate --password "3yeDJje6ZXGJ2oCdg15tTpY4R4MoctNApTVS3mg6mie3" --path "m/44'/60'/0'/0/1"

//Information returned are as follows:

[2020-05-12 11:24:27.285][+08][Info ][ 1] [http_server.go:29] Starting RPC HTTP server on tcp://0.0.0.0:37657
[2020-05-12 11:24:27.287][+08][Info ][ 24] [handler.go:23] WalletCreate begin, [password=********], [path=m/44'/60'/0'/0/1]
[2020-05-12 11:24:27.288][+08][Info ][ 24] [wallet.go:225] createAccount, [password=********], [path=m/44'/60'/0'/0/1]
[2020-05-12 11:24:27.355][+08][Info ][ 24] [handler.go:47] WalletCreate finish, [path=m/44'/60'/0'/0/1], [password=********]
{
  "walletAddr": "local4LBnSWWJu5pha6Us3o9VzaYToA8y9Bc6S"
}
```

