# Network Interface

## 1. abci\_info

Query world status information of the **bcchain** from BCBChain's nodes.

**. Request URI over HTTP/HTTPS**

```html
http://earth.bcbchain.io/abci_info
or
https://earth.bcbchain.io/abci_info
```

**.  Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "abci_info"
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | -------- |
| ——       | ——       | no parameters |

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "response": {
      "version": "1.0.2.3233",
      "last_block_height": 23032,
      "last_app_state": "eyJibG9ja19oZWlnaHQiOjIzMDMyLCJhcHBfaGFzaCI6IkFFQ0U2REQzRDlBQUQzQkIxNzQ5RTg2MkE4MjdCMzY2ODk4MEY1QTRCMDIyMjNFQjk3Rjg3NUE0QzA1QzMxQ0MiLCJ0eHNfaGFzaF9saXN0IjpbIkEwQzU1OTRBNkYzQjI0MDY0RTJGQkFGNjYyRjlCNEEyIl0sInJld2FyZHMiOlt7ImtleSI6IlltTmlNMHBwZG5SVlYybEVSelE0WkdKWFJIWkdRbFZJUkV3NGRtVkNOMHAyVVhaVCIsInZhbHVlIjoiQUFBQUFBQ1lsb0E9In0seyJrZXkiOiJZbU5pUzNVMllsaHJUamRpWmpGM1VUaHFlSGR4WlhWcFRXOVZXVloxVTFaRmFHUlgiLCJ2YWx1ZSI6IkFBQUFBQURrNGNBPSJ9LHsia2V5IjoiWW1OaVVUSk1TMUJuVlVweE9HVTVORlJCYmpOeU9FSTRaRFphZWpGRVRtcElhSGw0IiwidmFsdWUiOiJBQUFBQUFDWWxvQT0ifSx7ImtleSI6IlltTmlOMHQ0ZUZwTmQxTjBXVWRIYmt0cE0zaE9UbTA1Ylc1dE4zQmtWM1JHT1dkRSIsInZhbHVlIjoiQUFBQUFBRGs0Y0E9In1dLCJmZWUiOjUwMDAwMDAwfQ=="
    }
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**                |   **type**    | **comment** |
| ----------------------- | :-----------: | ------------------------------------------------------------ |
| response:   {           |    Object     | **bcchain** returned query result            |
| &nbsp;&nbsp;version           |    String     | **bcchain** the release version of the program             |
| &nbsp;&nbsp;last\_block\_height |    Uint64     | **bcchain** the height of the last confirmed block of the world state. |
| &nbsp;&nbsp;last\_app\_state  | Base64 String | **bcchain** The detailed world state data (including a tamper proof abci application layer hash value) when the world state is the last confirmed block is encoded with Base64.|
| }                       |               |                                                              |

**.The world state data(last\_app\_state) format is defined as a string in JSON format, as shown in the following table:**

| **Parameter**                                  |       **type**       | **comment**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
| ----------------------------------------- | :------------------: | ------------------------------------------------------------ |
| {                                         |        Object        |                                                              |
| &nbsp;&nbsp;block_height                  |        Uint64        | **bcbchain** The height of the last confirmation block of the state of the world.  |
| &nbsp;&nbsp;app\_hash                     |      HexString       | **bcbchain** The abci application layer root hash of the last acknowledgment block in the world state. |
| &nbsp;&nbsp;txs\_hash\_list               | Arrayof<br>HexString | Hash list of the transaction of the last confirmation block (MD5 is used for hash algorithm here) |
| &nbsp;&nbsp;rewards: [                    |  Arrayof<br>Object   | The last confirmation block reward allocation.                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;{                 |        Object        |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;key   |    Base64 String     | Base64 encoded reward address.                               |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value |    Base64 String     | Base64 encoded reward amount （uint: **cong**）     |
| &nbsp;&nbsp;&nbsp;&nbsp;}                 |                      |                                                              |
| &nbsp;&nbsp;]                             |                      |                                                              |
| &nbsp;&nbsp;fee                           |        Uint64        | Transaction cost of the last confirmed block （uint: **cong**）      |
| }                                         |                      |                                                              |

## 2. dump\_consensus\_state

Query the nodes of bcbchain for the current consensus status of bcbchain.

**\. Request URI over HTTP/HTTPS**

```html
http://earth.bcbchain.io/dump_consensus_state
or
https://earth.bcbchain.io/dump_consensus_state
```

**\. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "dump_consensus_state"
}
```

**\. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| ——       | ——       | no parameters                                                     |

**\. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "round_state": {
      "height": 299272,
      "round": 0,
      "step": 2,
      "start_time": "2018-10-17T23:13:48.311608186-04:00",
      "commit_time": "2018-10-17T23:13:47.311608186-04:00",
      "validators": {
        "validators": [
          {
            "address": "bcbASX7yURtV7yTRHjF6HMtef5SdverDw1ee",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "mGQPP0w2BBoZSwwJLvA/EVmu3nJvcWdv+7vi8rfxV0Y="
            },
            "voting_power": 10,
            "reward_addr": "bcb85DQBafrtMwkiXq2kgwxwAWnsf3hmRinX",
            "name": "moon",
            "accum": 40
          },
          {
            "address": "bcbCUh7Zsb7PBgLwHJVok2QaMhbW64HNK4FU",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "ZBOerhcnAVySTmbsXv3B0qVmJVy75aLyq5eGvU86y0s="
            },
            "voting_power": 10,
            "reward_addr": "bcbDYZbi3b8kfAYJepGVu8GuBTbiDPGe5T9G",
            "name": "vaga",
            "accum": -30
          },
          {
            "address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "AOHXEMLtWLyq7jPNkiZ2hdG9KZwxHUwBF9Tyll8RFoE="
            },
            "voting_power": 10,
            "reward_addr": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV",
            "name": "venus",
            "accum": -40
          },
          {
            "address": "bcbGMKrue1tabboHwokE2WDshAhVD98XbJjH",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "0AvM3BXo6sZmxc3Br566T2G/KBKJiTl2kcZqAcICM80="
            },
            "voting_power": 10,
            "reward_addr": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm",
            "name": "earth",
            "accum": 50
          },
          {
            "address": "bcbHS2RUcXpKVLSK4djJzzXmX25mdskgxpes",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "2KKGQ0wIa9j+zr/yg73RYmwMM73cwkvG067eE+Ndeo0="
            },
            "voting_power": 10,
            "reward_addr": "bcb8CGg4LxELkwxuK1z9GfjLJGy3NqueqGLa",
            "name": "saturn",
            "accum": -10
          },
          {
            "address": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "XJiVuLIlA/K29i6htCIAI/YsrcOepVADr4KqZG8wUK4="
            },
            "voting_power": 10,
            "reward_addr": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4",
            "name": "mercury",
            "accum": 50
          },
          {
            "address": "bcbK1gpGpeWcydGM3Lpure4JiYjnwa7xj5Bm",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "1vcMBnBBbcGj3DXrdqX6Wi9nIW68kQjWlwUzA2hCg+I="
            },
            "voting_power": 10,
            "reward_addr": "bcbJJvGCZaZ1YgSCMAKipL1s4jRhnkujGb4w",
            "name": "sirius",
            "accum": 40
          },
          {
            "address": "bcbKVNSGbPEC6PULyJDAc2s4aUQ6oDPAArNX",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "FxWAGICI+N6jLFXWB838YAYFkA9ef/YLVwaRU/X+fmI="
            },
            "voting_power": 10,
            "reward_addr": "bcbAcaXUTwhVH8kFEVg3RU7ySSEd7Uspd11d",
            "name": "altair",
            "accum": -40
          },
          {
            "address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "hzOstmpgwv4UcA/nc/OFsc7mdv8B5T6XpBiZLlq6OgE="
            },
            "voting_power": 10,
            "reward_addr": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS",
            "name": "jupiter",
            "accum": 30
          },
          {
            "address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "dX5u+aaEBARI6/Jh8MCe0FPNChPjqtT7JViwIbBoVOI="
            },
            "voting_power": 10,
            "reward_addr": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB",
            "name": "mars",
            "accum": 30
          }
        ],
        "proposer": {
          "address": "bcbKVNSGbPEC6PULyJDAc2s4aUQ6oDPAArNX",
          "pub_key": {
            "type": "AC26791624DE60",
            "value": "FxWAGICI+N6jLFXWB838YAYFkA9ef/YLVwaRU/X+fmI="
          },
          "voting_power": 10,
          "reward_addr": "bcbAcaXUTwhVH8kFEVg3RU7ySSEd7Uspd11d",
          "name": "altair",
          "accum": -40
        }
      },
      "proposal": null,
      "proposal_block": null,
      "proposal_block_parts": null,
      "locked_round": 0,
      "locked_block": null,
      "locked_block_parts": null,
      "valid_round": 0,
      "valid_block": null,
      "valid_block_parts": null,
      "votes": [
        {
          "round": 0,
          "prevotes": "__________",
          "precommits": "__________"
        },
        {
          "round": 1,
          "prevotes": "__________",
          "precommits": "__________"
        }
      ],
      "commit_round": -1,
      "last_commit": {
        "votes": [
          "Vote{0:5452486A4636 299271/00/2(Precommit) 96DD31906843 /717813DF4930.../ @ 2018-10-18T03:13:47.031Z}",
          "Vote{1:4C77484A566F 299271/00/2(Precommit) 96DD31906843 /85DB0DCCB274.../ @ 2018-10-18T03:13:47.031Z}",
          "Vote{2:5A36694C4379 299271/00/2(Precommit) 96DD31906843 /36145780B8F5.../ @ 2018-10-18T03:13:47.030Z}",
          "Vote{3:6F48776F6B45 299271/00/2(Precommit) 96DD31906843 /83895753FD27.../ @ 2018-10-18T03:13:47.109Z}",
          "Vote{4:534B34646A4A 299271/00/2(Precommit) 96DD31906843 /6AB72A137429.../ @ 2018-10-18T03:13:47.038Z}",
          "Vote{5:775A41326477 299271/00/2(Precommit) 96DD31906843 /BD8458648B9A.../ @ 2018-10-18T03:13:47.022Z}",
          "Vote{6:474D334C7075 299271/00/2(Precommit) 96DD31906843 /05DA25B4E553.../ @ 2018-10-18T03:13:47.035Z}",
          "Vote{7:554C794A4441 299271/00/2(Precommit) 96DD31906843 /E89DA00E076E.../ @ 2018-10-18T03:13:47.122Z}",
          "Vote{8:57326B565462 299271/00/2(Precommit) 96DD31906843 /9AB4FF53A863.../ @ 2018-10-18T03:13:47.067Z}",
          "Vote{9:5A7A6B437370 299271/00/2(Precommit) 96DD31906843 /524825FED0C4.../ @ 2018-10-18T03:13:47.137Z}"
        ],
        "votes_bit_array": "xxxxxxxxxx",
        "peer_maj_23s": {}
      },
      "last_validators": {
        "validators": [
          {
            "address": "bcbASX7yURtV7yTRHjF6HMtef5SdverDw1ee",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "mGQPP0w2BBoZSwwJLvA/EVmu3nJvcWdv+7vi8rfxV0Y="
            },
            "voting_power": 10,
            "reward_addr": "bcb85DQBafrtMwkiXq2kgwxwAWnsf3hmRinX",
            "name": "moon",
            "accum": 30
          },
          {
            "address": "bcbCUh7Zsb7PBgLwHJVok2QaMhbW64HNK4FU",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "ZBOerhcnAVySTmbsXv3B0qVmJVy75aLyq5eGvU86y0s="
            },
            "voting_power": 10,
            "reward_addr": "bcbDYZbi3b8kfAYJepGVu8GuBTbiDPGe5T9G",
            "name": "vaga",
            "accum": -40
          },
          {
            "address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "AOHXEMLtWLyq7jPNkiZ2hdG9KZwxHUwBF9Tyll8RFoE="
            },
            "voting_power": 10,
            "reward_addr": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV",
            "name": "venus",
            "accum": -50
          },
          {
            "address": "bcbGMKrue1tabboHwokE2WDshAhVD98XbJjH",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "0AvM3BXo6sZmxc3Br566T2G/KBKJiTl2kcZqAcICM80="
            },
            "voting_power": 10,
            "reward_addr": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm",
            "name": "earth",
            "accum": 40
          },
          {
            "address": "bcbHS2RUcXpKVLSK4djJzzXmX25mdskgxpes",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "2KKGQ0wIa9j+zr/yg73RYmwMM73cwkvG067eE+Ndeo0="
            },
            "voting_power": 10,
            "reward_addr": "bcb8CGg4LxELkwxuK1z9GfjLJGy3NqueqGLa",
            "name": "saturn",
            "accum": -20
          },
          {
            "address": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "XJiVuLIlA/K29i6htCIAI/YsrcOepVADr4KqZG8wUK4="
            },
            "voting_power": 10,
            "reward_addr": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4",
            "name": "mercury",
            "accum": 40
          },
          {
            "address": "bcbK1gpGpeWcydGM3Lpure4JiYjnwa7xj5Bm",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "1vcMBnBBbcGj3DXrdqX6Wi9nIW68kQjWlwUzA2hCg+I="
            },
            "voting_power": 10,
            "reward_addr": "bcbJJvGCZaZ1YgSCMAKipL1s4jRhnkujGb4w",
            "name": "sirius",
            "accum": 30
          },
          {
            "address": "bcbKVNSGbPEC6PULyJDAc2s4aUQ6oDPAArNX",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "FxWAGICI+N6jLFXWB838YAYFkA9ef/YLVwaRU/X+fmI="
            },
            "voting_power": 10,
            "reward_addr": "bcbAcaXUTwhVH8kFEVg3RU7ySSEd7Uspd11d",
            "name": "altair",
            "accum": 50
          },
          {
            "address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "hzOstmpgwv4UcA/nc/OFsc7mdv8B5T6XpBiZLlq6OgE="
            },
            "voting_power": 10,
            "reward_addr": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS",
            "name": "jupiter",
            "accum": 20
          },
          {
            "address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
            "pub_key": {
              "type": "AC26791624DE60",
              "value": "dX5u+aaEBARI6/Jh8MCe0FPNChPjqtT7JViwIbBoVOI="
            },
            "voting_power": 10,
            "reward_addr": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB",
            "name": "mars",
            "accum": 20
          }
        ],
        "proposer": {
          "address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
          "pub_key": {
            "type": "AC26791624DE60",
            "value": "AOHXEMLtWLyq7jPNkiZ2hdG9KZwxHUwBF9Tyll8RFoE="
          },
          "voting_power": 10,
          "reward_addr": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV",
          "name": "venus",
          "accum": -50
        }
      }
    },
    "peer_round_states": [
      {
        "node_address": "bcb4xjc2PKdCeZLdYpsL5BgeUT9WiKRi2Bzp@altair-p2p.bcbchain.io:46656",
        "peer_round_state": {
          "height": 299272,
          "round": 0,
          "step": 1,
          "start_time": "2018-10-17T23:13:47.421309398-04:00",
          "proposal": false,
          "proposal_block_parts_header": {
            "total": 0,
            "hash": ""
          },
          "proposal_block_parts": null,
          "proposal_pol_round": -1,
          "proposal_pol": "__________",
          "prevotes": "__________",
          "precommits": "__________",
          "last_commit_round": 0,
          "last_commit": "xxxxxxxxxx",
          "catchup_commit_round": -1,
          "catchup_commit": "__________"
        }
      }
    ]
  }
}
```

**\. Response SUCCESS Parameters**

  Consensus status information is used internally by bcbchain and is not described here.

## 3. health

Query the nodes of bcbchain for their health status.

**\. Request URI over HTTP/HTTPS**

```html
http://earth.bcbchain.io/health
or
https://earth.bcbchain.io/health
```

**\. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "health"
}
```

**\. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| ——       | ——       | no parameters                                                     |

**\. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "chain_id": "bcb",
    "version": "2.0.1.11319",
    "chain_version": 2,
    "last_block_height": 15703691,
    "validator_count": 10
  }
}
```

**\. Response SUCCESS Parameters**

| **Parameter**                        | **type** | **comment** |
| ------------------------------- | :------: | ------------------------------------------------------------ |
| {                               |          |                                                              |
| &nbsp;&nbsp;chain\_id           |  String  | Blockchain ID.                                     |
| &nbsp;&nbsp;version             |  String  | Blockchain program version.                        |
| &nbsp;&nbsp;chain\_version      |  String  | Blockchain Version (the version representing the implementation mechanism of the blockchain application World).          |
| &nbsp;&nbsp;last\_block\_height |  Uint64  | Latest block height.                            |
| &nbsp;&nbsp;validator\_count    |  Uint32  | Number of verifier nodes.                              |
| }                               |          |                                                              |

## 4. net\_info

Query the nodes of bcbchain for their P2P network connection status with all other nodes.

**\. Request URI over HTTP/HTTPS**

```html
http://earth.bcbchain.io/net_info
or
https://earth.bcbchain.io/net_info
```

**\. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "net_info"
}
```

**\. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| ——       | ——       | no parameters                                                     |

**\. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "listening": true,
    "listeners": [
      "earth-p2p.bcbchain.io:46656"
    ],
    "peers": [
      {
        "node_info": {
          "id": "bcb4xjc2PKdCeZLdYpsL5BgeUT9WiKRi2Bzp",
          "listen_addr": "altair-p2p.bcbchain.io:46656",
          "network": "bcb",
          "channels": "4020212223303800",
          "version": "1.0.6.6078",
          "base_version": "0.19.1",
          "moniker": "tmcore02",
          "other": [
            "amino_version=0.9.7",
            "p2p_version=0.5.0",
            "consensus_version=v1/0.2.2",
            "rpc_version=0.7.0/3",
            "tx_index=on",
            "rpc_addr=tcp://0.0.0.0:37827"
          ]
        },
        "is_outbound": true,
        "connection_status": {
          "Duration": 9223372036854775807,
          "SendMonitor": {
            "Active": true,
            "Start": "2018-10-17T13:22:04.8-04:00",
            "Duration": 35557780000000,
            "Idle": 260000000,
            "Bytes": 8114951,
            "Samples": 23646,
            "InstRate": 554,
            "CurRate": 182,
            "AvgRate": 228,
            "PeakRate": 51900,
            "BytesRem": 0,
            "TimeRem": 0,
            "Progress": 0
          },
          "RecvMonitor": {
            "Active": true,
            "Start": "2018-10-17T13:22:04.8-04:00",
            "Duration": 35557780000000,
            "Idle": 120000000,
            "Bytes": 7934624,
            "Samples": 22358,
            "InstRate": 0,
            "CurRate": 64,
            "AvgRate": 223,
            "PeakRate": 74550,
            "BytesRem": 0,
            "TimeRem": 0,
            "Progress": 0
          },
          "Channels": [
            {
              "ID": 48,
              "SendQueueCapacity": 1,
              "SendQueueSize": 0,
              "Priority": 5,
              "RecentlySent": 0
            },
            {
              "ID": 64,
              "SendQueueCapacity": 1000,
              "SendQueueSize": 0,
              "Priority": 10,
              "RecentlySent": 0
            },
            {
              "ID": 32,
              "SendQueueCapacity": 100,
              "SendQueueSize": 0,
              "Priority": 5,
              "RecentlySent": 720
            },
            {
              "ID": 33,
              "SendQueueCapacity": 100,
              "SendQueueSize": 0,
              "Priority": 10,
              "RecentlySent": 4
            },
            {
              "ID": 34,
              "SendQueueCapacity": 100,
              "SendQueueSize": 0,
              "Priority": 5,
              "RecentlySent": 11
            },
            {
              "ID": 35,
              "SendQueueCapacity": 2,
              "SendQueueSize": 0,
              "Priority": 1,
              "RecentlySent": 0
            },
            {
              "ID": 56,
              "SendQueueCapacity": 1,
              "SendQueueSize": 0,
              "Priority": 5,
              "RecentlySent": 6
            },
            {
              "ID": 0,
              "SendQueueCapacity": 10,
              "SendQueueSize": 0,
              "Priority": 1,
              "RecentlySent": 0
            }
          ]
        }
      }
    ]
  }
}
```

**\. Response SUCCESS Parameters**

P2P network information is used internally by bcbchain and will not be described here.

## 5. status

Query the nodes of bcbchain for the current status of blockchain.

**\. Request URI over HTTP/HTTPS**

```html
http://earth.bcbchain.io/status
or
https://earth.bcbchain.io/status
```

**\. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "status"
}
```

**\. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| ——       | ——       | no parameters                                                     |

**\. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "node_info": {
      "id": "bcbEg1qrJ8vobRn8vMG2n8WdrqvH5g1fhmCr",
      "listen_addr": "earth-p2p.bcbchain.io:46656",
      "network": "bcb",
      "channels": "4020212223303800",
      "version": "1.0.6.6078",
      "base_version": "0.19.1",
      "moniker": "tmcore02",
      "other": [
        "amino_version=0.9.7",
        "p2p_version=0.5.0",
        "consensus_version=v1/0.2.2",
        "rpc_version=0.7.0/3",
        "tx_index=on",
        "rpc_addr=tcp://0.0.0.0:37827"
      ]
    },
    "sync_info": {
      "latest_block_hash": "54CBE1374807ED5F76C03851548F4BB90FDCC00F",
      "latest_app_hash": "FC3F02F4219788B7EA67CA9F14CD840E9C8BB2EA5EE6E2E7912D6EBBC80DA002",
      "latest_block_height": 299305,
      "latest_block_time": "2018-10-17T23:37:33.038958573-04:00",
      "syncing": false
    },
    "validator_info": {
      "address": "bcbNVDh8ZPgshTJ7U21ZGFpUxwMvAmXqkHKB",
      "pub_key": {
        "type": "AC26791624DE60",
        "value": "lz67BUTnfSZlsFEN8OsXBmzi1Qm7Kb5PUlZ3Fgi8Etk="
      },
      "voting_power": 0,
      "reward_addr": "",
      "name": ""
    }
  }
}
```

**\. Response SUCCESS Parameters**

| **Parameter**                | **type** | **comment** |
| ----------------------- | :------: | ------------------------------------------------------------ |
| node\_info:   {         |  Object  | Node information.                                         |
| &nbsp;&nbsp;id          | Address  | Node ID.                                           |
| &nbsp;&nbsp;listen\_addr |  String  | P2P network monitoring address, format: IP: port.      |
| &nbsp;&nbsp;network     |  String  | Take the chain ID of bcbchain as the network name.        |
| &nbsp;&nbsp;channels         | String            | Channel, used internally by bcbchain.                 |
| &nbsp;&nbsp;version                | String            | Release version of bcbchain.                            |
| &nbsp;&nbsp;base\_version          | String            |The extended version of bcbchain integration.                     |
| &nbsp;&nbsp;moniker                | String            | Internal name.                                               |
| &nbsp;&nbsp;others               | Arrayof<br>String | It supports the internal module version information of tendermint, as well as information about some internal features, such as the listening address of RPC service. |
| }                            |                   |                                                              |
| sync\_info:   {            | Object            | Synchronize information.                                |
| &nbsp;&nbsp;latest\_block\_hash    | Address        | Block hash of the last block.                                  |
| &nbsp;&nbsp;latest\_app\_hash      | HexString         | The **bcchain** world state of the last block applies the hash.             |
| &nbsp;&nbsp;latest\_block\_height | Uint64            | The height of the last block.                                 |
| &nbsp;&nbsp;latest\_block\_time    | String            | The block out time of the last block.                         |
| &nbsp;&nbsp;syncing             | String            | Whether the node is synchronizing blocks.                             |
| }                            |                   |                                                              |
| validator\_info:   {       | Object            | Verifier information for the node.                                   |
| &nbsp;&nbsp;address                | Address        |Node address.                                       |
| &nbsp;&nbsp;pub\_key: {                | Object            | Public key object.                                             |
| &nbsp;&nbsp;&nbsp;&nbsp;type                   | Base64 String   | The signature type, Base64 decoded, is a fixed string **ED25519**        |
| &nbsp;&nbsp;&nbsp;&nbsp;value                  | Base64 String   | The public key data is 32 bytes binary data after Base64 decoding.                |
| &nbsp;&nbsp;}                            |                   |                                                              |
| &nbsp;&nbsp;voting\_power           | Int               | Voting weight, observer node is 0.                                  |
| &nbsp;&nbsp;reward\_address        | Address        | The address where the verifier node receives the Commission reward, and the observer node is empty.             |
| &nbsp;&nbsp;name                   | String            | Verifier node name.                                       |
| }                            |                   |                                                              |



## 6. num\_unconfirmed\_txs

Query the node of bcbchain for the number of unconfirmed transactions.



**\. Request URI over HTTP/HTTPS**

```
http://earth.bcbchain.io/num_unconfirmed_txs
or
https://earth.bcbchain.io/num_unconfirmed_txs
```

**\. Request JSONRPC over HTTP/HTTPS**

```
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "num_unconfirmed_txs"
}
```

**\. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| ——       | ——       | no parameters                                                     |



**\. Response SUCCESS Example**

```
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "n_txs": 5,
    "txs": null
  }
}
```

**\. Response SUCCESS Parameters**

| **Parameter** | **type** | **comment** |
| -------- | :------: | ------------------------------------------------------------ |
| n_txs    |   Int    | number of unconfirmed transactions                   |
| txs      |   null   | reserved                                                      |



## 7. unconfirmed\_txs

Query the node of bcbchain for unconfirmed transaction details.



**\. Request URI over HTTP/HTTPS**

```
http://earth.bcbchain.io/unconfirmed_txs
or
https://earth.bcbchain.io/unconfirmed_txs
```

**\. Request JSONRPC over HTTP/HTTPS**

```
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "unconfirmed_txs"
}
```

**\. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| ——       | ——       | no parameters                                                     |

**\. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "n_txs": 5,
    "txs": [
      "YmNiJTNDdHglM0UudjEuVmpwa0dqcFcxcDVwekNmVFMyZUFabVc5RGJZOHdmaWRyMWl0OWlKWHE0VEtNUXE1Rm9jcVRjdWVhMmJwOXU3elcxOUNNY3g0UEh4TkxOdzdqNUZuanFiREI5Uk50ZFd1WG83VGpEYnY0NjN0QWlDRUpSRXJQYmhEbjNiNXc4MXBuYndITW0uJTNDMSUzRS5ZVGdpQTFnZERHaTJMOGhwZ1dEMkJCTWgzSlYyNXByd0x6OEdKN1Eya0RuN0RvWHhuM3plU1pDVGpxV1F3dG10TVpRUGVSSzRFYlBOeFNYblBuemR6NzZCVEN4M3ZkZTRVMkJ2a0Q5YWhkNEtuYjkxOFY2NWs4N29adXF0cDFlRmMzY1FMYnRuVHoyWmtuWTZzRzhLUw==",
      "YmNiJTNDdHglM0UudjEuVmpwaXRwVXlNdHhaZWFWc0V3Vzdqbk1kNENBQnN1UEJuRENzTFMyNm5HNURiY3Y1dm5EcXBHOVFKbmNRcnZBZ0pkUzRTc2lXbjRzVHlLWUo4UjlYaWVzdEF0cTVxeE5aOWk5eUh0YUNwWks5Unk5dXNpa1d2M3k4TDNxVlFtTkpFcEFEeDcuJTNDMSUzRS5ZVGdpQTFnZERHaTJMOGhwZ1dEMkJCTWgzSlYyNXByd0x6OEdKN1Eya0RuN0RvWHhuM3plU1pDVGpxV1F3eThoejl2WHBEQ1Jhb3ZoZ1JRdm15WkplWGc0TDdWWHkzcnpDVVFDbndwUHZIamthbW40VEZaY1M5RVluY0pUYkNZc0xLTXptWnpIMTh2aEhFZW80UVFhNw==",
      "YmNiJTNDdHglM0UudjEuVmpwakVvS01YTmpzeXozR0hpSGRTbjlGYllXQjlMeTNvQUxOWUZiRDNUZmszNHRxRzM1NkU2cVRzYmNHQmZRV01VTXF2WlhRQk5lQzRhdFcyYWc2VVQ0RFJUVWY3OEE5RkVQcXVEcThkU1ZxN2V1elV0c2JuU1E5aDNtdFlNWGdObTZ6SlguJTNDMSUzRS5ZVGdpQTFnZERHaTJMOGhwZ1dEMkJCTWgzSlYyNXByd0x6OEdKN1Eya0RuN0RvWHhuM3plU1pDVGpxV1F3eG9pNVZ6UWtBNFhmbjJCNWJjRGpYZHZESFQzNFdISld3YVdIdVdONFg1UzRYV1ROMmh6dVZYQkNOQXdjdFFyUmlybm93a3VBQVRZMWJQbXdvNG9EbnFKWA==",
      "YmNiJTNDdHglM0UudjEuVmpwamFuOWpnclhDS1BhZkxWNTk5bXZ0OHRyQVFuWXVwN1RzazVBS0pmR0dVV3NhYkh2TGR3WFhTUWM3V1FlTFFLSGRRRkxIYWdRdjlyRWh2a0NmRUZFWWcyOEVOSHdqTGtkaVdaNjRTS2dXb0xnNTY0emdlcHFCNDNpSGZ3aDRXaTNrZXcuJTNDMSUzRS5ZVGdpQTFnZERHaTJMOGhwZ1dEMkJCTWgzSlYyNXByd0x6OEdKN1Eya0RuN0RvWHhuM3plU1pDVGpxV1F3eTkxNFp3VzdrVFBuV0VZWTkxVVR4U2V5RFVva0JjRWhhNnNNUEtzNHN0Ykxnd0NKZVNBdnVEQkhmUlVqZ1dSeFFKOVlKUTVqRVVQS0Y0eE5LOVBZY0xyUw==",
      "YmNiJTNDdHglM0UudjEuVmpwanZrejdyTEpXZW84NFBGcmVybWlXZ0ZDOWdFOG1xNGJOd3RqUlpycm51eHJLdlltYjNuRGIxRGJ4cTl0QVRBRFFzdzlBeXpCZUY3YXVwdWpEejNRc3ZhbW9kVGpLU0dzYjd0THpGQ3NDVjJTOWhGN21YREdDUjNlZ29YclNlZXpYMU0uJTNDMSUzRS5ZVGdpQTFnZERHaTJMOGhwZ1dEMkJCTWgzSlYyNXByd0x6OEdKN1Eya0RuN0RvWHhuM3plU1pDVGpxV1F3eUFtZjV2ZDM4NFN2Z0JkbmFqSmNrVkdxaU5iUDlRZlRBSnpYb0pvZllrV21ZMlZ6eUI5QTZMeERyR0FQdVdDTVF4VGcxUEFpaDYxU1RlaENzS3BnMmM4TQ=="
    ]
  }
}
```

**\. Response SUCCESS Parameters**

| **Parameter** |       **type**       | **comment** |
| -------- | :------------------: | ------------------------------------------------------------ |
| n_txs    |         Int          | number of unconfirmed transactions.                         |
| txs      | Arrayof Base64String | unconfirmed transaction data table. The original data corresponding to each Base64 string in the table is a string that follows the message format defined in Chapter 5 of this article. The message type is limited to "bcb\<tx>"|

## 8. validators

Queries the bcbchain's nodes for details of all valid verifier nodes in the bcbchain when the block height is specified.

**\. Request URI over HTTP/HTTPS**

```
http://earth.bcbchain.io/validators?height=20000
or
https://earth.bcbchain.io/validators?height=20000
```

**\. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "validators"
}
```

**\. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | -------- | ------------------------------------------------------------ |
| height   | Uint64   | Specify block height, optional parameter, default to query the latest block height  |

**\. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "block_height": 20000,
    "validators": [
      {
        "address": "bcbG6WixauSd9RZ6iLCygSYZdZ7bttmhQ2zh",
        "pub_key": {
          "type": "AC26791624DE60",
          "value": "AOHXEMLtWLyq7jPNkiZ2hdG9KZwxHUwBF9Tyll8RFoE="
        },
        "voting_power": 10,
        "reward_addr": "bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV",
        "name": "venus",
        "accum": -50
      },
      {
        "address": "bcbGMKrue1tabboHwokE2WDshAhVD98XbJjH",
        "pub_key": {
          "type": "AC26791624DE60",
          "value": "0AvM3BXo6sZmxc3Br566T2G/KBKJiTl2kcZqAcICM80="
        },
        "voting_power": 10,
        "reward_addr": "bcb5xjCpYJrKkyM3kgo5Jk8Pge7XDTwuvSUm",
        "name": "earth",
        "accum": 10
      },
      {
        "address": "bcbJofNo2NYSv1wZA2dwQa59MCGxaBSEkRgh",
        "pub_key": {
          "type": "AC26791624DE60",
          "value": "XJiVuLIlA/K29i6htCIAI/YsrcOepVADr4KqZG8wUK4="
        },
        "voting_power": 10,
        "reward_addr": "bcbKG7Y7hWLhjxiBNZ8UBgja4ocLcSHKW4b4",
        "name": "mercury",
        "accum": 10
      },
      {
        "address": "bcbNUjCm1i8RcoW2kVTbDw4vKW6jzfMxewJH",
        "pub_key": {
          "type": "AC26791624DE60",
          "value": "hzOstmpgwv4UcA/nc/OFsc7mdv8B5T6XpBiZLlq6OgE="
        },
        "voting_power": 10,
        "reward_addr": "bcb3JivtUWiDG48dbWDvFBUHDL8veB7JvQvS",
        "name": "jupiter",
        "accum": 10
      },
      {
        "address": "bcbNt6gNp1C6mSZzkCspqnu99wD7TAbtS7Ug",
        "pub_key": {
          "type": "AC26791624DE60",
          "value": "dX5u+aaEBARI6/Jh8MCe0FPNChPjqtT7JViwIbBoVOI="
        },
        "voting_power": 10,
        "reward_addr": "bcbAb65XuCz8bWHB1ittqMQSRyLvDmb74KRB",
        "name": "mars",
        "accum": 10
      },
      {
        "address": "bcbP2gPSpJkm4RXevJdAXr2cdoXbiZdRg9t7",
        "pub_key": {
          "type": "AC26791624DE60",
          "value": "N/wpx9qzyDrR/Vsy/saZMW2gXnEsamNn57VMAOZN5UE="
        },
        "voting_power": 10,
        "reward_addr": "bcbCfciTQNLQGwRWadxXg6ms8dBguP5sooX8",
        "name": "pluto",
        "accum": 10
      }
    ]
  }
}
```

**\. Response SUCCESS Parameters**

| **Parameter**                      |   **type**    | **comment**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
| ----------------------------- | :-----------: | ------------------------------------------------------------ |
| height                 |  Uint64 | Block height.                   |
| validators: [               | Arrayof<br>Object |Verifier node list. |
| &nbsp;&nbsp;{        | Object            | Verifier information for the node.                              |
| &nbsp;&nbsp;&nbsp;&nbsp;address                | Address        | Node address.                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;pub\_key: {                | Object            | Public key object.                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type                   | Base64<br>String | The signature type, Base64 decoded, is a fixed string **ED25519**.        |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value                  | Base64<br>String | The public key data is 32 bytes binary data after Base64 decoding.               |
| &nbsp;&nbsp;&nbsp;&nbsp;}                            |                   |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;voting\_power           | Int               | Voting weight, observer node is 0.                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;reward\_address        | Address        | The address where the verifier node receives the Commission reward.            |
| &nbsp;&nbsp;&nbsp;&nbsp;name                   | String            | Verifier node name.                                             |
| &nbsp;&nbsp;&nbsp;&nbsp;accum | Int | Used to calculate the dynamic parameters of the next round of proponents, which are used internally in the blockchain. |
| &nbsp;&nbsp;}                            |                   |                                                              |
| ] | | |
