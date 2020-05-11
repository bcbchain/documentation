# Blockchain Interface

## 1. genesis

Query the nodes of bcbchain for blockchain creation information.

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/genesis
or
https://earth.bcbchain.io/genesis
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "genesis"
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| ——       | ——       | no parameters                                               |

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "genesis": {
      "genesis_time": "2018-07-15T11:25:08.0515146+08:00",
      "chain_id": "bcb",
      "consensus_params": {
        "block_size_params": {
          "max_bytes": 22020096,
          "max_txs": 100000,
          "max_gas": -1
        },
        "tx_size_params": {
          "max_bytes": 10240,
          "max_gas": -1
        },
        "block_gossip_params": {
          "block_part_size_bytes": 65536
        },
        "evidence_params": {
          "max_age": 100000
        }
      },
      "validators": [
        {
          "reward_addr": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB",
          "pub_key": {
            "type": "AC26791624DE60",
            "value": "dX5u+aaEBARI6/Jh8MCe0FPNChPjqtT7JViwIbBoVOI="
          },
          "power": 10,
          "name": "mars"
        },
        {
          "reward_addr": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm",
          "pub_key": {
            "type": "AC26791624DE60",
            "value": "0AvM3BXo6sZmxc3Br566T2G/KBKJiTl2kcZqAcICM80="
          },
          "power": 10,
          "name": "earth"
        },
        {
          "reward_addr": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV",
          "pub_key": {
            "type": "AC26791624DE60",
            "value": "AOHXEMLtWLyq7jPNkiZ2hdG9KZwxHUwBF9Tyll8RFoE="
          },
          "power": 10,
          "name": "venus"
        },
        {
          "reward_addr": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS",
          "pub_key": {
            "type": "AC26791624DE60",
            "value": "hzOstmpgwv4UcA/nc/OFsc7mdv8B5T6XpBiZLlq6OgE="
          },
          "power": 10,
          "name": "jupiter"
        },
        {
          "reward_addr": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4",
          "pub_key": {
            "type": "AC26791624DE60",
            "value": "XJiVuLIlA/K29i6htCIAI/YsrcOepVADr4KqZG8wUK4="
          },
          "power": 10,
          "name": "mercury"
        },
        {
          "reward_addr": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8",
          "pub_key": {
            "type": "AC26791624DE60",
            "value": "N/wpx9qzyDrR/Vsy/saZMW2gXnEsamNn57VMAOZN5UE="
          },
          "power": 10,
          "name": "pluto"
        }
      ],
      "app_hash": "",
      "app_state": {
        "token": {
          "address": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
          "owner": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7",
          "version": "",
          "name": "BCB",
          "symbol": "BCB",
          "totalSupply": 5000000000000000000,
          "addSupplyEnabled": false,
          "burnEnabled": false,
          "gasPrice": 2500
        },
        "rewardStrategy": [
          {
            "name": "validators",
            "rewardPercent": "20.00",
            "address": ""
          },
          {
            "name": "r_d_team",
            "rewardPercent": "30.00",
            "address": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW"
          },
          {
            "name": "bonus_bcb",
            "rewardPercent": "20.00",
            "address": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx"
          },
          {
            "name": "bonus_token",
            "rewardPercent": "30.00",
            "address": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD"
          }
        ],
        "contracts": [
          {
            "name": "system",
            "address": "bcbBpZgwh9KbjXeXVDmHT9Tj1vnH1VcKtDEU",
            "owner": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7",
            "version": "",
            "codeHash": "B37E7627431FEB18123B81BCF1F41FFD37EFDB90513D48FF2C7F8A0C27A9D06C",
            "effectHeight": 1,
            "loseHeight": 0,
            "methods": [
              {
                "methodId": "1b0b7ce1",
                "prototype": "NewValidator(string,smc.PubKey,smc.Address,uint64)smc.Error",
                "gas": 50000
              },
              {
                "methodId": "bcc890f0",
                "prototype": "SetPower(smc.PubKey,uint64)smc.Error",
                "gas": 20000
              },
              {
                "methodId": "757a5721",
                "prototype": "SetRewardAddr(smc.PubKey,smc.Address)smc.Error",
                "gas": 20000
              },
              {
                "methodId": "52d1c625",
                "prototype": "ForbidInternalContract(smc.Address,uint64)smc.Error",
                "gas": 50000
              },
              {
                "methodId": "48c26f01",
                "prototype": "DeployInternalContract(string,string,[]string,[]uint64,smc.Hash,uint64)(smc.Address,smc.Error)",
                "gas": 50000
              },
              {
                "methodId": "92622878",
                "prototype": "SetRewardStrategy(string,uint64)smc.Error",
                "gas": 50000
              }
            ]
          },
          {
            "name": "token-basic",
            "address": "bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe",
            "owner": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7",
            "version": "",
            "codeHash": "F81574FFFACF4E3B401D9054B7BD082F42DF45B9DBFE2653811B18F507F56BDF",
            "effectHeight": 1,
            "loseHeight": 0,
            "methods": [
              {
                "methodId": "af0228bc",
                "prototype": "Transfer(smc.Address,big.Int)smc.Error",
                "gas": 500
              },
              {
                "methodId": "cc50053d",
                "prototype": "SetGasPrice(uint64)smc.Error",
                "gas": 2000
              },
              {
                "methodId": "adcf5578",
                "prototype": "SetGasBasePrice(uint64)smc.Error",
                "gas": 2000
              }
            ]
          },
          {
            "name": "token-issue",
            "address": "bcbALw9SqmqUWVjkB1bJUQyCKfnxDPhuN5Ej",
            "owner": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7",
            "version": "",
            "codeHash": "AA4A7218FE6AEFF137898E055BBA4E0EA78F9D9E8289463CFCD1BEAE42EBB595",
            "effectHeight": 1,
            "loseHeight": 0,
            "methods": [
              {
                "methodId": "825b55bb",
                "prototype": "NewToken(string,string,big.Int,bool,bool,uint64)(smc.Address,smc.Error)",
                "gas": 20000
              }
            ]
          },
          {
            "name": "token-templet",
            "address": "bcb9uDW7LLu5xuqvavcRbVCAr4f9eD4YnMaP",
            "owner": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7",
            "version": "",
            "codeHash": "DA9B15ACF6F4013B6FC6296E1C6694658CCFF9AFA6BF24D1C18ECC6DAAC12F55",
            "effectHeight": 1,
            "loseHeight": 0,
            "methods": [
              {
                "methodId": "af0228bc",
                "prototype": "Transfer(smc.Address,big.Int)smc.Error",
                "gas": 600
              },
              {
                "methodId": "b8f4b0d8",
                "prototype": "BatchTransfer([]smc.Address,big.Int)smc.Error",
                "gas": 6000
              },
              {
                "methodId": "4a439c44",
                "prototype": "AddSupply(big.Int)smc.Error",
                "gas": 2400
              },
              {
                "methodId": "5a0e0fa3",
                "prototype": "Burn(big.Int)smc.Error",
                "gas": 2400
              },
              {
                "methodId": "a6be2c35",
                "prototype": "SetOwner(smc.Address)smc.Error",
                "gas": 2400
              },
              {
                "methodId": "cc50053d",
                "prototype": "SetGasPrice(uint64)smc.Error",
                "gas": 2400
              },
              {
                "methodId": "54868e97",
                "prototype": "UdcCreate(smc.Address,big.Int,string)(smc.Hash,smc.Error)",
                "gas": 2400
              },
              {
                "methodId": "d0ef0ff4",
                "prototype": "UdcTransfer(smc.Hash,smc.Address,big.Int)(smc.Hash,smc.Hash,smc.Error)",
                "gas": 2400
              },
              {
                "methodId": "1a14fbcd",
                "prototype": "UdcMature(smc.Hash)smc.Error",
                "gas": 2400
              }
            ]
          },
          {
            "name": "token-trade",
            "address": "bcbAY6bGvscNUG4oXTiASYuoVTHB5LNdhFLh",
            "owner": "bcb8yNeqAixZ7DDQx1fHSvQdA3kKDQ48gci7",
            "version": "",
            "codeHash": "C67BD0296DDF597FAF3C1957336360006F8E37B54F1F80B4BC8001934BAC9C96",
            "effectHeight": 1,
            "loseHeight": 0,
            "methods": [
              {
                "methodId": "4b041bab",
                "prototype": "DealExchange(string,string)smc.Error",
                "gas": 2000
              }
            ]
          }
        ]
      }
    }
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**                      |   **type**    | **comment** |
| ----------------------------- | :-----------: | ------------------------------------------------------------ |
| genesis: { | Object | Genesis information. |
| &nbsp;&nbsp;genesis\_time | String | The genesis time, such as: **2018-07-15T11:25:08.0515146+08:00** |
| &nbsp;&nbsp;chain\_id | String | Chain ID of BCBChain |
| &nbsp;&nbsp;consensus\_params | Object | Consensus parameter object, which is used internally in blockchain, will not be described in detail here.     |
| &nbsp;&nbsp;validators: [               | Arrayof<br>Object | List of Creator verifier nodes. |
| &nbsp;&nbsp;&nbsp;&nbsp;{        | Object            | Verifier information for the node.                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;address                | Address        | Node address.                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pub\_key: {                | Object            | Public key object.                                                  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type                   | Base64<br>String |The signature type, that is the fixed string **ED25519** after Base64 decoding.|
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value                  | Base64<br>String | The public key data is 32 bytes binary data after Base64 decoding.              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}                            |                   |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;voting\_power           | Int               | The voting weight of the verifier node.                         |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;reward\_address        | Address        | The address where the verifier node receives the Commission reward. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name                   | String            | Verifier node name.                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;}                            |                   |                                                              |
| &nbsp;&nbsp;] | | |
| &nbsp;&nbsp;app\_hash           | String            | The creation application hash must be empty.                |
| &nbsp;&nbsp;app\_state: {           | Object            | The application state at the time of creation.          |
| &nbsp;&nbsp;&nbsp;&nbsp;token: {                | Object            | Detailed parameters of the basic token **BCB** defined at the time of bcbchain creation.|
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;address             | Address | The contract address of the token **BCB**.                   |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;owner               | Address | Address of the owner of the token **BCB**.                |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;version             | String            | Contract version.                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name             | String            | Token name                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;symbol           | String            | Token symbol                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;totalSupply   | Uint64            | Total supply of the token (uint: **cong**)                |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;addSupplyEnabled | Bool              | Whether the token supports mining.                         |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;burnEnabled      | String            | Whether the token supports burning                           |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gasPrice          | Int               | Standard gas price                                |
| &nbsp;&nbsp;&nbsp;&nbsp;}                         |                   |                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;rewardStrategy: [       | Arrayof <br> Object | Reward strategy table.                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{                         | Object |                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name        | String            | Name of award.                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rewardPercent  | String            | The percentage of bonus to be allocated, with the precision of two decimal places.  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;address             | Address | Address to receive the award.                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}                         |                   |                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;]                         |                   |                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;contracts: [            | Arrayof<br>Object | Built in contract table.                               |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{                         | Object |                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name          | String            | Contract name.                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;address             | Address | Contract address.                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;owner               | Address | Address of the contract owner.                            |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;version             | String            | Contract version.                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;codeHash            | HexString         | Contract code hash.                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;effectHeight         | Uint64            | Block height at which the contract is in effect.     |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loseHeight           | Uint64            | Block height of contract failure, 0 means no failure.         |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;methods: [              | Arrayof<br> Object | Method table for contract definition.                       |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;methodId    | HexString         | Method ID.                                      |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;prototype           | String            | Method prototype, directly involved in the calculation process of methodid.     |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gas              | Int               | The amount of gas the method needs to consume.  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]                         |                   |                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}                         |                   |                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;]                         |                   |                                               |
| &nbsp;&nbsp;}                         |                   |                                               |
| }                         |                   |                                               |

## 2. genesis_pkg

Download all the files required for node creation from the bcbchain node.

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/genesis_pkg
or
https://earth.bcbchain.io/genesis_pkg
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "genesis_pkg"
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| ——       | ——       | no parameters                                               |

**. Response SUCCESS Example**

```json
{
    "jsonrpc": "2.0",
    "id": "",
    "result": {
        "f": "H4sICAAAAAAA/2JjYlt5eV0udGFyAOz7d1gVydY3DKMggpKUJKASFDAQOgdy797dIFFyUnFv9t7knAREVBARjKhgQETMgI..."
    }
}
```

- **Response SUCCESS Parameters**

  | **Parameter**      |    **type**     | **comment** |
  | ------------- | :-------------: | ------------------------------------------------------------ |
  | results: {    |     Object      | Execution results.                                |
  | &nbsp;&nbsp;f | json.RawMessage | Genesis information packs data in `tar.gz` format.            |
  | }             |                 |                                                              |

## 3. block

Query the order of bcbchain for the specified height block data (including metadata and transaction data).

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/block?height=1882
or
https://earth.bcbchain.io/block?height=1882
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "block",
  "params": {
    "height": 1882
  }
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| height   | Uint64   | Specify block height, optional parameter, default to query the latest block height.           |

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "block_meta": {
      "block_id": {
        "hash": "735C4C8BE388215E0295B46A31902CC024E898B2",
        "parts": {
          "total": 1,
          "hash": "12BFECE3D1135321D0A7F1662CAFBDC36AFB0EE3"
        }
      },
      "header": {
        "chain_id": "bcb",
        "height": 1882,
        "time": "2018-07-16T15:21:51.359923728Z",
        "num_txs": 1,
        "last_block_id": {
          "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
          "parts": {
            "total": 1,
            "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
          }
        },
        "total_txs": 877,
        "last_commit_hash": "645617624A1367158740270B89F36792EBDDA9CC",
        "data_hash": "6E88F5C5D7A9CB33DF187651ACF4CDC97F280B29",
        "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
        "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
        "last_app_hash": "3F2FF012707B214CCF74488E0034125FBFA3678D676CA8B76FFA61977B6041DC",
        "last_results_hash": "",
        "evidence_hash": "",
        "last_fee": 0,
        "last_allocation": null,
        "proposer_address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
        "reward_address": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS"
      }
    },
    "block": {
      "header": {
        "chain_id": "bcb",
        "height": 1882,
        "time": "2018-07-16T15:21:51.359923728Z",
        "num_txs": 1,
        "last_block_id": {
          "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
          "parts": {
            "total": 1,
            "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
          }
        },
        "total_txs": 877,
        "last_commit_hash": "645617624A1367158740270B89F36792EBDDA9CC",
        "data_hash": "6E88F5C5D7A9CB33DF187651ACF4CDC97F280B29",
        "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
        "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
        "last_app_hash": "3F2FF012707B214CCF74488E0034125FBFA3678D676CA8B76FFA61977B6041DC",
        "last_results_hash": "",
        "evidence_hash": "",
        "last_fee": 0,
        "last_allocation": null,
        "proposer_address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
        "reward_address": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS"
      },
      "data": {
        "txs": [
          "YmNiPHR4Pi52MS5DWnhHd0g1VWdZSzFudjJrSkt2WjdXVnNOekhTR2ZIbUxnOTRjc1NaODM2NW9SZUxyZjJjdXFZRWpVYUhCU21ZYzFVSzc5UzZjckRKcEtYSlhoeUtkdm93VUNSb25US0hDOWhVenpuS0VKVkN0QjU1b2Y0M1A4elQyWm8xVGNvU0d1VmJ5aFp4WnkyV1MyNW5TMVhBb2lzcUg5aXpzblpuTmNTUEtwcy48MT4uWVRnaUExZ2RER2kyTDhoeUNrTDJ5Nlg2aWNMU1p1MWVBMXlUTFo4UkNxUnZ1QXBNbTU4dDRCR3JKZG00d3BVTnlxQTdraEdoaE1VN0JEUTdxWHJCWUdWMmV0QVV4R2c0QU1DRHRHNVBYOXpSWE53ZXBvV3pUZ3U1MWdQTVVIQ3NLYjlUa00zQUZ4Y2VOb0NlY0huRXA="
        ],
        "lastTxsHashList": null
      },
      "evidence": {
        "evidence": null
      },
      "last_commit": {
        "block_id": {
          "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
          "parts": {
            "total": 1,
            "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
          }
        },
        "precommits": [
          {
            "validator_address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
            "validator_index": 0,
            "height": 1881,
            "round": 0,
            "timestamp": "2018-07-16T15:21:50.735378944Z",
            "type": 2,
            "block_id": {
              "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
              "parts": {
                "total": 1,
                "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "xhZwLCfpqkO69RZG0t4FkZ3D3kDi1qzvPfrmnlhleImCgEe4eMAjWzJnI7Pm8FJdtL8RhvmL8CHYsjsbt/8ZBg=="
            }
          },
          {
            "validator_address": "bcbGMKrue1tabboHwokE2WDshAhVD98XbJjH",
            "validator_index": 1,
            "height": 1881,
            "round": 0,
            "timestamp": "2018-07-16T15:21:50.784812178Z",
            "type": 2,
            "block_id": {
              "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
              "parts": {
                "total": 1,
                "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "VRcc+sqfuQGGfdENgdgJuSrPhuM/Y9k8+SPUTyy8hWHCDC2En5U3nhQyV5xEB5QBMweZErJizhAjfMafttMLBQ=="
            }
          },
          {
            "validator_address": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
            "validator_index": 2,
            "height": 1881,
            "round": 0,
            "timestamp": "2018-07-16T15:21:50.748300828Z",
            "type": 2,
            "block_id": {
              "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
              "parts": {
                "total": 1,
                "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "AjfuMt0fbtCDxSUhuC7+UEFWuL4ke0zgWmWwoSdtzINjTD8inbXGc4G+upeRXufowltIR23HV4DItL7Rb8JyDw=="
            }
          },
          {
            "validator_address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
            "validator_index": 3,
            "height": 1881,
            "round": 0,
            "timestamp": "2018-07-16T15:21:50.737399332Z",
            "type": 2,
            "block_id": {
              "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
              "parts": {
                "total": 1,
                "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "6GhInCqZzn9OOrxp79k1zKdb1IIqdI/SmqU7Q2ePQ426tIU8Ap1AzjIyWlH+ctHgC9UMASWvnQzfX4yJTn53Bg=="
            }
          },
          {
            "validator_address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
            "validator_index": 4,
            "height": 1881,
            "round": 0,
            "timestamp": "2018-07-16T15:21:50.751551591Z",
            "type": 2,
            "block_id": {
              "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
              "parts": {
                "total": 1,
                "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "8sJ4K7TotstJbcgtxYZsOG9QGYLcVrDGBRYIATGlsx9F8ux2NXyNKWADX3Yj+R9sLtpwyhJZljzmDwJlnFRICQ=="
            }
          },
          {
            "validator_address": "bcbP2gPSpJkm4RXevJdAXr2cdoXbiZdRg9t7",
            "validator_index": 5,
            "height": 1881,
            "round": 0,
            "timestamp": "2018-07-16T15:21:50.688632577Z",
            "type": 2,
            "block_id": {
              "hash": "C59087AC460E8EA6D2A034F7A5ED03D28F5F76E7",
              "parts": {
                "total": 1,
                "hash": "1D7077487120F2FFAEBC4E7462121F341B72B872"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "FvHbqm8NC6/W6ZzI9Bj4fcL8opkSK+n6qe42tIOR0x+I0CcTxr/Yt8KRyn7UY0rFlHCIBMrZJe47AHT9iaIPDA=="
            }
          }
        ]
      }
    },
    "block_size": 1854
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**                  | **type**                   | **comment** |
| ------------------------- | :------------------------: | ------------------------------------------------------------ |
| block\_meta: {            | Object                     |Metadata for the block.                                            |
| &nbsp;&nbsp;block\_id: {              | Address          | Blockchain ID.                                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;hash                      | HexString                  | The block hash of the current block.                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;parts                     | Object                     | Bcbchain is used internally and is not described here.       |
| &nbsp;&nbsp;}                         |                            |                                                              |
| &nbsp;&nbsp;header                    | Object                     | Block head, see the description of block head in block description below.                   |
| }                         |                            |                                                              |
| block: {                  | Object                     | Block data.                                                   |
| &nbsp;&nbsp;header: {                 | Object                     | Block header information.                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;chain\_id                 | String                     | Chain ID.                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;height                    | Uint64                     | The block height of the current block.                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;time                      | String                     | The block out time of the current block, such as:   **2018-07-17T01:34:47.385918218Z** |
| &nbsp;&nbsp;&nbsp;&nbsp;num\_txs                  | Int                        | The number of transactions contained in the current block.                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;last\_block\_id: {        | Object                     | Blockchain ID of the previous block.                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hash                      | HexString                  | Blockchain hash of the previous block.                                |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;parts                     | Object                     | Bcbchain is used internally and is not described here.       |
| &nbsp;&nbsp;&nbsp;&nbsp;}                         |                            |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;total\_txs                | Int64                      | Bcbchain cumulative total number of transactions that have occurred.                    |
| &nbsp;&nbsp;&nbsp;&nbsp;data\_hash                | HexString                  | Hash of  field named **data** in block.              |
| &nbsp;&nbsp;&nbsp;&nbsp;validators\_hash          | HexString                  | Hash of verifier data.                                          |
| &nbsp;&nbsp;&nbsp;&nbsp;consensus\_hash           | HexString                  | Hash of consensus data                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;evidence\_hash            | HexString                  | Hash of evidence data.                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;proposer\_address         | Address          | Address of the block proponent.                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;reward\_address           | Address          |Reward address of block proponent                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;last\_commit\_hash        | HexString                  | Hash of the last block validation data.                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;last\_app\_hash           | HexString                  | The **bcchain** world state application layer hash of the previous block.          |
| &nbsp;&nbsp;&nbsp;&nbsp;last\_results\_hash       | HexString                  | Hash of the transaction execution result data for the previous block.  |
| &nbsp;&nbsp;&nbsp;&nbsp;last\_fee                 | Int64                      | All handling charges (uint: **cong**) incurred by the transacions of the previous block.           |
| &nbsp;&nbsp;&nbsp;&nbsp;last\_allocation: [       | Arrayof Object             | Distribution result table of handling fees collected in the previous block.                |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{                         | Object | Distribution information of handling charges. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;addr                      | Address                 | Address to receive handling charges.             |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fee                       | Int64                      | received fee(uint:**cong**)                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}                         |                            |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;]                         |                            |                                                              |
| &nbsp;&nbsp;}                         |                            |                                                              |
| &nbsp;&nbsp;data: {                   | Object                     | Block data.                                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;txs                       | Arrayof<br>Base64<br>String | Transaction list. Each transaction is encoded with Base64.          |
| &nbsp;&nbsp;&nbsp;&nbsp;lastTxsHashList           | Arrayof<br> HexString      | Hash list of all transaction execution results in the previous block, where MD5 is used for hash calculation. |
| &nbsp;&nbsp;}                         |                            |                                                              |
| &nbsp;&nbsp;evidence                  | Object                     | Evidence data, used internally by bcbchain, is not described here.       |
| &nbsp;&nbsp;last\_commit              | Object                     | The confirmation data of the previous block, which is used internally by bcbchain, will not be described here.  |
| }                         |                            |                                                              |
| block\_size               | Int                        | Block size.                                                  |

## 4. block_results

Query the nodes of bcbchain for the execution results of all transactions in the specified height block.

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/block_results?height=1882
or
https://earth.bcbchain.io/block_results?height=1882
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "block_results",
  "params": {
    "height": 1882
  }
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | :------: | ------------------------------------------------------------ |
| height   |  Uint64  | Specify block height, optional parameter, default to query the latest block height.           |

**. Response SUCCESS for Empty Block Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "height": 1881,
    "results": {
      "DeliverTx": null,
      "EndBlock": {
        "validator_updates": null
      }
    }
  }
}
```

**. Response SUCCESS for Block with Txs Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "height": 1882,
    "results": {
      "DeliverTx": [
        {
          "code": 200,
          "log": "Deliver tx succeed",
          "gas_limit": 2500,
          "gas_used": 500,
          "fee": 1250000,
          "tx_hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7"
        }
      ],
      "EndBlock": {
        "validator_updates": null
      }
    }
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**          | **type**          | **comment** |
| ----------------- | :---------------: | ------------------------------------------------------------ |
| height            | Uint64            | Block height.                                             |
| results: {        | Object            | Execution results.                                                |
| &nbsp;&nbsp;DeliverTx: [      | Arrayof Object | List of execution results for the transaction.                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;{                 | Object            | The execution result of a transaction.                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;code              | Int               | Transaction execution result code, 200 indicates success.          |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;log               | String            | The description of the transaction result, when the code is not equal to 200, it will show the specific error information. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gas\_limit        | Int64             | The gas limit specified by the transaction sponsor.    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gas\_used         | Int64             | The gas limit at which the transaction is executed. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fee               | Int64             | the transaction fee (uint: **cong**).                          |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tx\_hash          | HexString         | transaction hash                                                |
| &nbsp;&nbsp;&nbsp;&nbsp;}                 |                   |                                                              |
| &nbsp;&nbsp;]                 |                   |                                                              |
| &nbsp;&nbsp;EndBlock          | Object            | BCBChain is used internally (for example, adding or removing verifier nodes), which is not described here. |
| }                 |                   |                                                              |


## 5. blockchain

A request to query the nodes of bcbchain for block metadata of a specified height range (up to 21 blocks at a time).

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/blockchain?minHeight=10000&maxHeight=10020
or
https://earth.bcbchain.io/blockchain?minHeight=10000&maxHeight=10020
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "blockchain",
  "params": {
    "minHeight": 10000,
    "maxHeight": 10020
  }
}
```

**. Request Parameters**

| **Parameter**  | **type** | **comment** |
| --------- | :------: | ------------------------------------------------------------ |
| minHeight |  Uint64  | Specifies the minimum block height.                  |
| maxHeight |  Uint64  | Specifies the maximum block height.             |

* Note:
* Based on the parameter maxheight, 21 blocks can be returned at most;
* Returns the last 21 blocks when there are no parameters, or when only the minheight parameter is specified.

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "last_height": 24070,
    "block_metas": [
      {
        "block_id": {
          "hash": "2220D3F1DCA5BF12A11EDE90D887B5DF5AC886DD",
          "parts": {
            "total": 1,
            "hash": "7593339CF7F8F47FB37C4AB3530BC4A534D35444"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10020,
          "time": "2018-07-17T01:35:01.719681218Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "D03844AAAF48652AC9DA73764976F11F1C2C2745",
            "parts": {
              "total": 1,
              "hash": "CCB1708C44345E8FD9C169FB28F23DDC5DBCC7BA"
            }
          },
          "total_txs": 5114,
          "last_commit_hash": "F90BB8E0FAB0BEA63C69F194D861159BEFBDE5BC",
          "data_hash": "59FE33CAAF0C77E0846E1619D92DA7B720EE4A02",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "0A5E60D7F1B99D7D7346E4EE2BB6B6E52C79B7F2CF56D45156EA5DAB94718911",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbP2gPSpJkm4RXevJdAXr2cdoXbiZdRg9t7",
          "reward_address": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8"
        }
      },
      {
        "block_id": {
          "hash": "D03844AAAF48652AC9DA73764976F11F1C2C2745",
          "parts": {
            "total": 1,
            "hash": "CCB1708C44345E8FD9C169FB28F23DDC5DBCC7BA"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10019,
          "time": "2018-07-17T01:35:00.918255252Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "AF28C86DBD61C7A25D41DD6EE2BFD94DCB1B83BF",
            "parts": {
              "total": 1,
              "hash": "6031A283BFFFBC60055FC5718FF2A8E9703CF13E"
            }
          },
          "total_txs": 5113,
          "last_commit_hash": "C453980F41D65A7086C8F03D7D6923BD5BF77D98",
          "data_hash": "C2C9BF0A869338EAB1A89298E9A1A74F934B7D58",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "F25A09CC2B0F1B305341A977DD66567E235AC480FBBCDF86724666DA358A6C92",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
          "reward_address": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB"
        }
      },
      {
        "block_id": {
          "hash": "AF28C86DBD61C7A25D41DD6EE2BFD94DCB1B83BF",
          "parts": {
            "total": 1,
            "hash": "6031A283BFFFBC60055FC5718FF2A8E9703CF13E"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10018,
          "time": "2018-07-17T01:35:00.159601728Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "BCF92FC810E3BB0360589935155F0EA71B03714C",
            "parts": {
              "total": 1,
              "hash": "EB8D6760711A705AA55B80A8052ABCCD0A89CEB0"
            }
          },
          "total_txs": 5112,
          "last_commit_hash": "EA6826C0797703C7358011EFD58B2EE36627C168",
          "data_hash": "D8A2FB2211651E574B1DD702C583F61C8DBAC0BC",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "994DCE0FE7928CACE1E27BD39519D4EBA0A9B75C94901D8682E8CA8F49E8AAFF",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
          "reward_address": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS"
        }
      },
      {
        "block_id": {
          "hash": "BCF92FC810E3BB0360589935155F0EA71B03714C",
          "parts": {
            "total": 1,
            "hash": "EB8D6760711A705AA55B80A8052ABCCD0A89CEB0"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10017,
          "time": "2018-07-17T01:34:59.293967272Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "FCEC447F756BE0A13D4A3FA8348CABA7E3CB217F",
            "parts": {
              "total": 1,
              "hash": "21BFEB20A297B91C2A517A2EC72B812488FB3D31"
            }
          },
          "total_txs": 5111,
          "last_commit_hash": "3A1E4F084575BF589CBBCAD72131C105E55DE29C",
          "data_hash": "5849E10BA61E664BA14555DD9CCD7EC84C61CC92",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "6470E0874D0C3D8C7D4539DB3E61EDC6EB7CEC08F8BA84FD9872B06C6FDCBBAB",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
          "reward_address": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4"
        }
      },
      {
        "block_id": {
          "hash": "FCEC447F756BE0A13D4A3FA8348CABA7E3CB217F",
          "parts": {
            "total": 1,
            "hash": "21BFEB20A297B91C2A517A2EC72B812488FB3D31"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10016,
          "time": "2018-07-17T01:34:58.65538342Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "22BD6E3035F0F52EA3DD949D1AED795E20B59BD6",
            "parts": {
              "total": 1,
              "hash": "092838BD0C018970394275E6337D37BACA776284"
            }
          },
          "total_txs": 5110,
          "last_commit_hash": "2D7EC8F7ACF7DEBCF8A74AF0FEFE15EB448643A6",
          "data_hash": "A89A7F72E8A9AA6A1759287586029AA3D1C85D3B",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "882B1AE5464B35E9B7316B19C0E334514DA05CA81011123BF69B9071841BC1B2",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbGMKrue1tabboHwokE2WDshAhVD98XbJjH",
          "reward_address": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm"
        }
      },
      {
        "block_id": {
          "hash": "22BD6E3035F0F52EA3DD949D1AED795E20B59BD6",
          "parts": {
            "total": 1,
            "hash": "092838BD0C018970394275E6337D37BACA776284"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10015,
          "time": "2018-07-17T01:34:57.900812481Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "7A19B8EEE194F2229A9BBB1A8AB8B7B682D79B5F",
            "parts": {
              "total": 1,
              "hash": "BEC086C3F4C92CDD8A3932D6F71D46F81652D422"
            }
          },
          "total_txs": 5109,
          "last_commit_hash": "9F77A795DD9F1D02D8FFAFE8E47B82EFC8C2F3C2",
          "data_hash": "E04F77301C4CA657F736872A9DE96E739D8D9889",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "79173809CE0BE77627D2AF7545CABC52B050F221EC1DC6023A44108C1A1FE89C",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
          "reward_address": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV"
        }
      },
      {
        "block_id": {
          "hash": "7A19B8EEE194F2229A9BBB1A8AB8B7B682D79B5F",
          "parts": {
            "total": 1,
            "hash": "BEC086C3F4C92CDD8A3932D6F71D46F81652D422"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10014,
          "time": "2018-07-17T01:34:57.050164218Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "F7DE2C808B55E3191B2FB53FD12892BEE40E09FE",
            "parts": {
              "total": 1,
              "hash": "DD004A1F5D202855E4BF458FA9EC7D9C86E64117"
            }
          },
          "total_txs": 5108,
          "last_commit_hash": "7C5F2A50623A5B9CCF53D755AE241DEB5190046C",
          "data_hash": "02B49941A16EF65E49DDEE3B0EC0EB7C3C22A194",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "23A5F03CA869BB850AFF258529511EA7C95F61E9D5B850592549963BE72D7E13",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbP2gPSpJkm4RXevJdAXr2cdoXbiZdRg9t7",
          "reward_address": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8"
        }
      },
      {
        "block_id": {
          "hash": "F7DE2C808B55E3191B2FB53FD12892BEE40E09FE",
          "parts": {
            "total": 1,
            "hash": "DD004A1F5D202855E4BF458FA9EC7D9C86E64117"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10013,
          "time": "2018-07-17T01:34:56.212691801Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "E638FD12B3370EBF8E41A3A1B6EF4CCC25C7A929",
            "parts": {
              "total": 1,
              "hash": "AD907B2FEDD4054F233CE3D1189B6342C34C6FF6"
            }
          },
          "total_txs": 5107,
          "last_commit_hash": "CDB3C3E799FD25BD7C96C8982340247817A417F2",
          "data_hash": "D80DD252B0E74F25C814D77BC29E463EC03413CF",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "355CCC888D4BC06BC03306809E61E7F1573A8B62BDC396168DC2B26A755570B3",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
          "reward_address": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB"
        }
      },
      {
        "block_id": {
          "hash": "E638FD12B3370EBF8E41A3A1B6EF4CCC25C7A929",
          "parts": {
            "total": 1,
            "hash": "AD907B2FEDD4054F233CE3D1189B6342C34C6FF6"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10012,
          "time": "2018-07-17T01:34:55.52265266Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "E45084DE9F8D160F39B971C0B96F5F19F3ADFC24",
            "parts": {
              "total": 1,
              "hash": "F80044AD2F5C4FCB104250303FDEDCF37475B661"
            }
          },
          "total_txs": 5106,
          "last_commit_hash": "86FF5D1C55BA215FD59A57C2A98C3154B5553F96",
          "data_hash": "1D03368CC4536AFE7C3CF98468E3791F26D7DCF1",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "F2B686D676F62EFBC9B4A0B7CAF667AA250792146E0CA499824B71D12738B3C4",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
          "reward_address": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS"
        }
      },
      {
        "block_id": {
          "hash": "E45084DE9F8D160F39B971C0B96F5F19F3ADFC24",
          "parts": {
            "total": 1,
            "hash": "F80044AD2F5C4FCB104250303FDEDCF37475B661"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10011,
          "time": "2018-07-17T01:34:54.686601303Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "9BABC4B846561E3C25FCC4C8B5F225638069AE74",
            "parts": {
              "total": 1,
              "hash": "32E39FFAA7AA9314C7B1E8FDC52DC8309700BCA7"
            }
          },
          "total_txs": 5105,
          "last_commit_hash": "93324E260383BB92E4E687BC082AF61A7B9ADBAE",
          "data_hash": "D81472A25B76EE2A72AE6B29C008F5D8D5763BB3",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "6CC53A1AEF2FA968E2D701A77340019852BF1EF3BCF7A9180FCCC8D1FF6E4166",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
          "reward_address": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4"
        }
      },
      {
        "block_id": {
          "hash": "9BABC4B846561E3C25FCC4C8B5F225638069AE74",
          "parts": {
            "total": 1,
            "hash": "32E39FFAA7AA9314C7B1E8FDC52DC8309700BCA7"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10010,
          "time": "2018-07-17T01:34:54.01175582Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "7E2705B74C381E5DB7CEC14ABDC169BA493E6732",
            "parts": {
              "total": 1,
              "hash": "00375138B293CE0285B565B7B367EB39CC4B92AC"
            }
          },
          "total_txs": 5104,
          "last_commit_hash": "E0B145B629BE90ADAEA05D526F7EA376A99C7B7A",
          "data_hash": "15496821523950C54B13BF82BDE25EEC42950E1D",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "8943169DF4FF505ABF18A400457BC4843B03B02009D5403C59B87136067F1AEC",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbGMKrue1tabboHwokE2WDshAhVD98XbJjH",
          "reward_address": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm"
        }
      },
      {
        "block_id": {
          "hash": "7E2705B74C381E5DB7CEC14ABDC169BA493E6732",
          "parts": {
            "total": 1,
            "hash": "00375138B293CE0285B565B7B367EB39CC4B92AC"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10009,
          "time": "2018-07-17T01:34:53.147904084Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "5EDB2853BE93F914FE4D9B48C758AAD6420D65A4",
            "parts": {
              "total": 1,
              "hash": "B076E50FC87249C91485B3A92558F6135813664A"
            }
          },
          "total_txs": 5103,
          "last_commit_hash": "0D1C5848C951318ABAAEC4DB68234946A6B709EF",
          "data_hash": "438AD7C384B930C53217D823589603A91ABE7025",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "750935A4327341673A05A52B796BA23A96846BE8125E6882ADE887305FA287B4",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
          "reward_address": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV"
        }
      },
      {
        "block_id": {
          "hash": "5EDB2853BE93F914FE4D9B48C758AAD6420D65A4",
          "parts": {
            "total": 1,
            "hash": "B076E50FC87249C91485B3A92558F6135813664A"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10008,
          "time": "2018-07-17T01:34:52.247073418Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "54DBC143E7C9FF5A1259397A7089965BEF5C1C00",
            "parts": {
              "total": 1,
              "hash": "BC8214EF95180331723402E380E895C102381331"
            }
          },
          "total_txs": 5102,
          "last_commit_hash": "0E3B107CD6C90ED6E8397177CF41DB1934D50562",
          "data_hash": "A875B5B614FC145C7577D0F35127F8FA6D29792D",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "81336892BD61AF8574092C39B29E88D26B19FE6672EDA1B7A9C4F3ED1AB29522",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbP2gPSpJkm4RXevJdAXr2cdoXbiZdRg9t7",
          "reward_address": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8"
        }
      },
      {
        "block_id": {
          "hash": "54DBC143E7C9FF5A1259397A7089965BEF5C1C00",
          "parts": {
            "total": 1,
            "hash": "BC8214EF95180331723402E380E895C102381331"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10007,
          "time": "2018-07-17T01:34:51.407687288Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "C9645D5B432133CC598C7DC4103019D6AAECC95A",
            "parts": {
              "total": 1,
              "hash": "E7C3CB896535CEB9CE5435C0655844BC8709256B"
            }
          },
          "total_txs": 5101,
          "last_commit_hash": "B639026274ED6F6315A2891F053B98086C705186",
          "data_hash": "65CC1B32A9B505FFBDF1A30AE4552FCA6A5199EB",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "06F00EDDAF9546358CBB0A42DC83625290B21A396F5AB5299893C5591A043F1A",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
          "reward_address": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB"
        }
      },
      {
        "block_id": {
          "hash": "C9645D5B432133CC598C7DC4103019D6AAECC95A",
          "parts": {
            "total": 1,
            "hash": "E7C3CB896535CEB9CE5435C0655844BC8709256B"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10006,
          "time": "2018-07-17T01:34:50.571481594Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "78016C3CBD97EFAB5F2075676E31F691AD2A88A2",
            "parts": {
              "total": 1,
              "hash": "E159C23C9D627B2353F7FF30D7CF80C7A8728F2D"
            }
          },
          "total_txs": 5100,
          "last_commit_hash": "09281F312D7A0A0A98987A3EFB603B2F53FA58CD",
          "data_hash": "228E978F8D41456F31DF5035C77A6B8D542ABF2C",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "8496C405A290D1B3CDC0AB1313297996561A232E9DCD4C7282F5EECD0EB27791",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
          "reward_address": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS"
        }
      },
      {
        "block_id": {
          "hash": "78016C3CBD97EFAB5F2075676E31F691AD2A88A2",
          "parts": {
            "total": 1,
            "hash": "E159C23C9D627B2353F7FF30D7CF80C7A8728F2D"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10005,
          "time": "2018-07-17T01:34:49.894301961Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "F568A5283AB30C0A50CFCECF00A59F6CF38D9487",
            "parts": {
              "total": 1,
              "hash": "6454998AF6B13FEFA0744888C726FBA1A7E96B23"
            }
          },
          "total_txs": 5099,
          "last_commit_hash": "6A3160DDD7171DC7FF5648A3478BBD818EBC0BD0",
          "data_hash": "548B56B81214799541E2311D26B3DA47AF70DF93",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "06DB780167CFF23BEB56D8612B9689778B66005DC9BB8771AED8C0326CD1880C",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
          "reward_address": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4"
        }
      },
      {
        "block_id": {
          "hash": "F568A5283AB30C0A50CFCECF00A59F6CF38D9487",
          "parts": {
            "total": 1,
            "hash": "6454998AF6B13FEFA0744888C726FBA1A7E96B23"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10004,
          "time": "2018-07-17T01:34:49.06382272Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "633B9FCEBAC4D6ABB842C6CC943AB6FC96901DF4",
            "parts": {
              "total": 1,
              "hash": "BA70F7F63F06A671BFB6209A32FCD72DE01D230E"
            }
          },
          "total_txs": 5098,
          "last_commit_hash": "3E24C9338A6F483D5385D814D239CC15871C5F9E",
          "data_hash": "45E14A8EC07D8BB2DFBF26A15D94DE4962B632AA",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "8C9261F78DDA5223E1086AFB5D86EDCEDFEDB76BC42E4B0275E5F19F8305D9E1",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV",
              "fee": 250000
            }
          ],
          "proposer_address": "bcbGMKrue1tabboHwokE2WDshAhVD98XbJjH",
          "reward_address": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm"
        }
      },
      {
        "block_id": {
          "hash": "633B9FCEBAC4D6ABB842C6CC943AB6FC96901DF4",
          "parts": {
            "total": 1,
            "hash": "BA70F7F63F06A671BFB6209A32FCD72DE01D230E"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10003,
          "time": "2018-07-17T01:34:48.275665587Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "7A94A1F0F415EC980CDF02ECBF9DA3FD696A49B8",
            "parts": {
              "total": 1,
              "hash": "4929AB4A19538959CA94B2DAFE06B695B6843F1E"
            }
          },
          "total_txs": 5097,
          "last_commit_hash": "50C4435FDEB2489B75A7425932C2906EE489BD0C",
          "data_hash": "19FEA6C964A9BCE9C9E8A747286B42965985E069",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "3D1BB9DD77F1AAEAE98F4F0B4F81CF03D57EBED5F44C52ED0E8835E1E9B79564",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
          "reward_address": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV"
        }
      },
      {
        "block_id": {
          "hash": "7A94A1F0F415EC980CDF02ECBF9DA3FD696A49B8",
          "parts": {
            "total": 1,
            "hash": "4929AB4A19538959CA94B2DAFE06B695B6843F1E"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10002,
          "time": "2018-07-17T01:34:47.385918218Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "359525AD496DE771597B3503ADAF7D89A1976058",
            "parts": {
              "total": 1,
              "hash": "A8FCDACD3F3186A58F6343828FE247BE542C3E61"
            }
          },
          "total_txs": 5096,
          "last_commit_hash": "5F3130B12F4897A2FD2BD287B486C82C95C79248",
          "data_hash": "6FD150D2A7715BE45C69653B64BA9E963528BCD8",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "C0173105DD21D4DE70B6AF3D2FA4EE8EE8081B1C5CC8A4A6E0B3004949DDAC6F",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            },
            {
              "addr": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbP2gPSpJkm4RXevJdAXr2cdoXbiZdRg9t7",
          "reward_address": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8"
        }
      },
      {
        "block_id": {
          "hash": "359525AD496DE771597B3503ADAF7D89A1976058",
          "parts": {
            "total": 1,
            "hash": "A8FCDACD3F3186A58F6343828FE247BE542C3E61"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10001,
          "time": "2018-07-17T01:34:46.583451744Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "C10A13157F7BEA30A90EDDF2DD2D1C409F83B52D",
            "parts": {
              "total": 1,
              "hash": "24EB53F598A24CDEACC425E86AE3F4FF37163254"
            }
          },
          "total_txs": 5095,
          "last_commit_hash": "462DAF750E731B8B2D037CAE2FF550A968F684D3",
          "data_hash": "C83B13751C628D719DE2B858963C06A0DDD60770",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "2C689C190D849D07D0A0F27B0C7A3F6CF8AD1A272C69A1C97EA71819EFC27763",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
          "reward_address": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB"
        }
      },
      {
        "block_id": {
          "hash": "C10A13157F7BEA30A90EDDF2DD2D1C409F83B52D",
          "parts": {
            "total": 1,
            "hash": "24EB53F598A24CDEACC425E86AE3F4FF37163254"
          }
        },
        "header": {
          "chain_id": "bcb",
          "height": 10000,
          "time": "2018-07-17T01:34:45.758835702Z",
          "num_txs": 1,
          "last_block_id": {
            "hash": "56FD2475DBE833FCC29ECBABBF3B321B26DABBA7",
            "parts": {
              "total": 1,
              "hash": "DD79B09ABF3DB1D6E5067A9400C0A7BD0A69B80E"
            }
          },
          "total_txs": 5094,
          "last_commit_hash": "8B607619755FC1A1C0FC8AB53FE9A5B718C9EA1A",
          "data_hash": "F7A08368E48889217DEBE35792655D67331AD945",
          "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
          "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
          "last_app_hash": "5EF194A8CB207E8ED108D55447F3E645AD62AD61471461FC0FC09C35670FD909",
          "last_results_hash": "71DE9575B3B55EF064BDBF9446324E9E3FFD95F3",
          "evidence_hash": "",
          "last_fee": 1250000,
          "last_allocation": [
            {
              "addr": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4",
              "fee": 250000
            },
            {
              "addr": "bcbKu6bXkN7bf1wQ8jxwqeuiMoUYVuSVEhdW",
              "fee": 375000
            },
            {
              "addr": "bcbQ2LKPgUJq8e94TAn3r8B8d6Zz1DNjHhyx",
              "fee": 250000
            },
            {
              "addr": "bcb7KxxZMwStYGGnKi3xNNm9mnm7pdWtF9gD",
              "fee": 375000
            }
          ],
          "proposer_address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
          "reward_address": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS"
        }
      }
    ]
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**                  | **type**          | **comment** |
| ------------------------- | :---------------: | ------------------------------------------------------------ |
| last\_height      | Uint64            | Block height of the last block.                            |
| block\_metas: [       | Arrayof<br>Object |Metadata list for the block.                                 |
| &nbsp;&nbsp;{                         | Object            |Metadata for the block.                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;block\_id: {          | Address        | Blockchain ID.                                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hash                 | HexString         | The block hash of the current block.                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;parts            | Object            | Bcbchain is used internally and is not described here.       |
| &nbsp;&nbsp;&nbsp;&nbsp;}                         |                   |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;header: {             | Object            | Block header information.                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;chain\_id        | String            | Chain ID.                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;height         | Uint64            | The block height of the current block.                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;time                 | String            | The block out time of the current block, such as:   **2018-07-17T01:34:47.385918218Z** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;num\_txs              | Int               | The number of transactions contained in the current block.                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;last\_block\_id: {    | Object            | Blockchain ID of the previous block.                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hash                 | HexString         | Blockchain hash of the previous block.                                |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;parts               | Object            | Bcbchain is used internally and is not described here.       |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}                         |                   |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;total\_txs         | Int64             | Bcbchain cumulative total number of transactions that have occurred.                    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data\_hash           | HexString         | Hash of  field named **data** in block.              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;validators\_hash     | HexString         | Hash of verifier data.                                          |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;consensus\_hash      | HexString         | Hash of consensus data                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;evidence\_hash       | HexString         | Hash of evidence data.                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proposer\_address    | Address        | Address of the block proponent.                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;reward\_address      | Address        |Reward address of block proponent                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;last\_commit\_hash   | HexString         | Hash of the last block validation data.                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;last\_app\_hash      | HexString         | The **bcchain** world state application layer hash of the previous block.          |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;last\_results\_hash  | HexString         | Hash of the transaction execution result data for the previous block.  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;last\_fee            | Int64             | All handling charges (uint: **cong**) incurred by the transacions of the previous block.           |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;last\_allocation: [   | Arrayof<br>Object | Distribution result table of handling fees collected in the previous block.                |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{                         |                   |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;addr                 | Address        | Address to receive handling charges.             |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fee                  | Int64             | received fee(uint:**cong**)                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}                         |                   |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]                         |                   |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;}                         |                   |                                                              |
| &nbsp;&nbsp;}                         |                   |                                                              |
| ]                         |                   |                                                              |

## 6. commit

Query the nodes of bcbchain for the confirmation information of the specified block.

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/commit?height=24103
or
https://earth.bcbchain.io/commit?height=24103
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "commit",
  "params": {
    "height": 24103
  }
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | :------: | ------------------------------------------------------------ |
| height   |  Uint64  | Specify block height, optional parameter, default to query the latest block height.           |

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "SignedHeader": {
      "header": {
        "chain_id": "bcb",
        "height": 24103,
        "time": "2018-07-19T10:52:46.522487761Z",
        "num_txs": 0,
        "last_block_id": {
          "hash": "BC547EF2C00CD6FFC12924F1FD8AF71F21F8E194",
          "parts": {
            "total": 1,
            "hash": "A880FB0FDFE01F73AEBBC8F467BCC292C566EE29"
          }
        },
        "total_txs": 17461,
        "last_commit_hash": "F3713D4C6B6E844A845DE4C12ADDE4DF5D713C5F",
        "data_hash": "",
        "validators_hash": "26D659FF2053EE752F747B4483AF4B0FCE096A00",
        "consensus_hash": "F66EF1DF8BA6DAC7A1ECCE40CC84E54A1CEBC6A5",
        "last_app_hash": "9DE509567ACE6D6571C0DB93183E765B5FBB80B592C868AE4C1FE1A6BA457671",
        "last_results_hash": "",
        "evidence_hash": "",
        "last_fee": 0,
        "last_allocation": null,
        "proposer_address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
        "reward_address": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV"
      },
      "commit": {
        "block_id": {
          "hash": "70FA9EC62ED66BCDBB342BCC12BCE508E1EF9A4C",
          "parts": {
            "total": 1,
            "hash": "7270083A5B368812216D87E287E184D88ED1B4DE"
          }
        },
        "precommits": [
          {
            "validator_address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
            "validator_index": 0,
            "height": 24103,
            "round": 0,
            "timestamp": "2018-07-19T10:52:46.795353861Z",
            "type": 2,
            "block_id": {
              "hash": "70FA9EC62ED66BCDBB342BCC12BCE508E1EF9A4C",
              "parts": {
                "total": 1,
                "hash": "7270083A5B368812216D87E287E184D88ED1B4DE"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "fBcgTLsasQwaOmU2LTlkZ4r9LRL0pYVj6c4Hn1DCS7Bbm2wmn6nycqx1YWZ7Mn8IQVpiUBVdfQUQAjoYdPyhAA=="
            }
          },
          {
            "validator_address": "bcbGMKrue1tabboHwokE2WDshAhVD98XbJjH",
            "validator_index": 1,
            "height": 24103,
            "round": 0,
            "timestamp": "2018-07-19T10:52:46.791398762Z",
            "type": 2,
            "block_id": {
              "hash": "70FA9EC62ED66BCDBB342BCC12BCE508E1EF9A4C",
              "parts": {
                "total": 1,
                "hash": "7270083A5B368812216D87E287E184D88ED1B4DE"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "SAuYty3UaSIivpsKXNg0UaXlVCYdI5G0dxp5J+NAGsVcls4gkHjrLhfSpFSaUM6ZT1gDT3+FvyEEAAIiRg3GCg=="
            }
          },
          {
            "validator_address": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
            "validator_index": 2,
            "height": 24103,
            "round": 0,
            "timestamp": "2018-07-19T10:52:46.782043166Z",
            "type": 2,
            "block_id": {
              "hash": "70FA9EC62ED66BCDBB342BCC12BCE508E1EF9A4C",
              "parts": {
                "total": 1,
                "hash": "7270083A5B368812216D87E287E184D88ED1B4DE"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "pHcPPfdwf2BMN4q/+n7ejnCW2TyMduNtpQM67EVpPe4PTebXLFX0gu5JorMcwQCw63MWjXYeIsGOxHrPUsPJBg=="
            }
          },
          {
            "validator_address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
            "validator_index": 3,
            "height": 24103,
            "round": 0,
            "timestamp": "2018-07-19T10:52:46.778048334Z",
            "type": 2,
            "block_id": {
              "hash": "70FA9EC62ED66BCDBB342BCC12BCE508E1EF9A4C",
              "parts": {
                "total": 1,
                "hash": "7270083A5B368812216D87E287E184D88ED1B4DE"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "K1FBZjhJGfnaI0l1L6VKBRkNibjYTzWQg/2KtzSJLLw98SSnQUAKZKQt945NxKGdkqcbLfuc4j6KpE3ZFOZ7CQ=="
            }
          },
          {
            "validator_address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
            "validator_index": 4,
            "height": 24103,
            "round": 0,
            "timestamp": "2018-07-19T10:52:46.768854258Z",
            "type": 2,
            "block_id": {
              "hash": "70FA9EC62ED66BCDBB342BCC12BCE508E1EF9A4C",
              "parts": {
                "total": 1,
                "hash": "7270083A5B368812216D87E287E184D88ED1B4DE"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "sbmv37exmUPJUdpQomINnKFTkI1nKgZyQ7ioku9XMPgTtsaZengm6A+nm/+l9u1nDo5mKIbhRruRbWbbxvAbBg=="
            }
          },
          {
            "validator_address": "bcbP2gPSpJkm4RXevJdAXr2cdoXbiZdRg9t7",
            "validator_index": 5,
            "height": 24103,
            "round": 0,
            "timestamp": "2018-07-19T10:52:46.790148859Z",
            "type": 2,
            "block_id": {
              "hash": "70FA9EC62ED66BCDBB342BCC12BCE508E1EF9A4C",
              "parts": {
                "total": 1,
                "hash": "7270083A5B368812216D87E287E184D88ED1B4DE"
              }
            },
            "signature": {
              "type": "6BF5903DA1DB28",
              "value": "MQQrcd38fWRF8vAPYQDHA/ZiNmGn30k2tCc+fS8levpB6GBgNVRv1a+zuADGLVa520x3GtR2kt7w8TdWhNL+BQ=="
            }
          }
        ]
      }
    },
    "canonical": true
  }
}
```

**. Response SUCCESS Parameters**

Confirmation information is used internally by bcbchain and is not described here.
