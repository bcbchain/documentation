# Side Chain Governance

## 1. Quick start for the side chain governance

### 1.1  Adjust the side chain public URL

Query the account balance of the side chain owner `scowner` on the main chain `local` to ensure that the `gas` needed to set the side chain `OpenURLs` is paid, querying command is:

```shell
 ./bcc balance --accAddress="localHMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG" --tokenName="LOC" --chainid local

Return results:

OK
Response: [
  {
    "tokenAddress": "localAJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA",
    "tokenName": "LOC",
    "balance": "9977498750000"
  }
]
```

To set the `OpenURLs` for the side chain, we take the side chain name is `smartCity`, the side chain public URL is `["http://ip1:46657"]` as an example to show how to use bcc tool to set the `OpenURLs` for the side chain:

```shell
./bcc call --contract netgovernance --method SetOpenURLs --splitBy @ --params smartCity@"[\"http://ip1:46657\"]" --gasLimit 100000 --orgName genesis --name scowner --password SCOwner@2019 --chainid local

Return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 125000000,
  "txHash": "0xCE0E3359A967E60A73316E7AE7726D7890AFD05B70FDCA319BC5E50E8E161464",
  "height": 11503
}
```

The value of option `params` in the command line is the argument to set for the side chain OpenURLs.

```html
the first parameter: smartCity, the side chain name
the second parameter: ["http://ip1:46657"], the list of URL open to the public, it could be many, such as ["http://ip1:46657", "http://ip2:46657"]
```

After adjusting `openURLs` for the side chain, you can query whether the `openURLs` of the side chain is set successfully. Query command is:

```shell
./bcc query -k /sidechain/local[smartCity]/openurls

Return results:

OK
Response:
  Code: 200
  Key: /sidechain/local[smartCity]/openurls
  Value: ["ip1:46657"]
  
After querying, you can see the side chain URL is the above set URL.
```

If the querying result is not the URL set above, you can query the details of the transaction by the returned`txhash` when you set the URL:

```shell
./bcc tx --txhash 0xCE0E3359A967E60A73316E7AE7726D7890AFD05B70FDCA319BC5E50E8E161464
OK
Response: {
  "txHash": "0xCE0E3359A967E60A73316E7AE7726D7890AFD05B70FDCA319BC5E50E8E161464",
  "txTime": "2019-11-30 05:42:54.886886465 +0000 UTC",
  "code": 200,
  "log": "",
  "blockHash": "0x3aa75d9b3c08adf5d7140377b50ee02ffdb62abc",
  "blockHeight": 4102,
  "from": "localHMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG",
  "nonce": 2,
  "gasLimit": 100000,
  "fee": 125000000,
  "note": "",
  "messages": [
    {
      "smcAddress": "local4f5YLBNi336r1zUYZTga9PXVJifDqdg3U",
      "smcName": "netgovernance",
      "method": "SetOpenURLs(string,[]string)",
      "to": "",
      "value": ""
    }
  ],
  "tags": {
    "/0/0/std::fee": {
          ......
    },
    "/0/1/netgovernance.setOpenURL": {
      "Name": "netgovernance.setOpenURL",
      "ContractAddr": "",
      "ReceiptBytes": "eyJzaWRlQ2hhaW5JRCI6ImxvY2FsW3l5XSIsIm9wZW5VUkxzIjpbImh0dHA6Ly8xNzIuMTYuNDIuMTM2OjQ2NjU3IiwiaHR0cDovLzE3Mi4xNi40Mi4xMzU6NDY2NTciXX0=",
      "ReceiptHash": "0x45F4E7344F40ED8E27BCE4ED63B0D5678BF4B095970F6A3B901490E67DF60D3D",
      "Receipt": {
        "openURLs": [
          "http://ip1:46657"
        ],
        "sideChainID": "local[SmartCity]"
      }
    },
    "/1/0/totalFee": {
      ......
    },
    "/1/1/transferFee": {
      ......
    },
    "/1/2/transferFee": {
      ......
    },
    "/1/3/transferFee": {
      ......
    },
    "/1/4/transferFee": {
      ......
    }
  }
}
```

You can find the receipt for `netgovernance.setOpenURL` in the tag, and check if the `openURLs`and`sideChainID` in the `Receipt` field are correct.

### 1.2 Adjust the gas price ratio for the side chain

You can use the bcc tool to adjust the gas price ratio of the side chain, we take the side chain is `smartCity`, the gas price ratio is `2.000` as an example to show how to adjust the gas price ratio of the side chain:

```shell
./bcc call --contract netgovernance --method SetGasPriceRatio --splitBy @ --params SmartCity@"2.000" --gasLimit 100000 --orgName genesis --name scowner --password SCOwner@2019 --chainid local

Return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 127500000,
  "txHash": "0x5100A109C3FDEACED7B5E7B90A61C966E1A093D6409ACFD2045D3CC8CBAB679E",
  "height": 12831
}
```

The value of option `params` in the command line is the argument to set for the side chain genesis creation:

```html
the first parameter: SmartCity, the side chain name
the second parameter: "2.000", the gas price ratio, note that the format must be accurate to three decimal places.
```

If we want to query if the above operation is successful, you can use the following command:

```shell
Query on the main chain:
./bcc query -k /sidechain/local[SmartCity]/chaininfo

Return results:

OK
Response:
  Code: 200
  Key: /sidechain/local[SmartCity]/chaininfo
  Value: {"sideChainName":"SmartCity","chainID":"local[SmartCity]","NodeNames":["node1"],"orgName":"SmartCity","owner":"localHMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","height":748,"status":"ready","gasPriceRatio":"2.000"}
  
Query on the side chain:
  ./bcc query -k /genesis/gaspriceratio --chainid local[SmartCity]

Return results:

OK
Response:
  Code: 200
  Key: /genesis/gaspriceratio
  Value: "2.000"
```

Through querying, you can see the side chain gas price ratio is the above set `gaspriceratio`. If the query result is not as expected, you can query the receipt by the following command:

```shell
./bcc tx  --chainid local --txhash 0x5100A109C3FDEACED7B5E7B90A61C966E1A093D6409ACFD2045D3CC8CBAB679E
OK
Response: {
  "txHash": "0x5100A109C3FDEACED7B5E7B90A61C966E1A093D6409ACFD2045D3CC8CBAB679E",
  "txTime": "2019-11-30 05:58:31.242099551 +0000 UTC",
  "code": 200,
  "log": "",
  "blockHash": "0x00b041f365468cbd9f9d911e20e1f9ef643dd0c4",
  "blockHeight": 5014,
  "from": "localHMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG",
  "nonce": 3,
  "gasLimit": 100000,
  "fee": 127500000,
  "note": "",
  "messages": [
    {
      "smcAddress": "local4f5YLBNi336r1zUYZTga9PXVJifDqdg3U",
      "smcName": "netgovernance",
      "method": "SetGasPriceRatio(string,string)",
      "to": "",
      "value": ""
    }
  ],
  "tags": {
    "/0/0/std::fee": {
      ......
    },
    "/0/1/netgovernance.setGasPriceRatio": {
      "Name": "netgovernance.setGasPriceRatio",
      "ContractAddr": "",
      "ReceiptBytes": "eyJjaGFpbk5hbWUiOiJ5eSIsImNoYWluSUQiOiJsb2NhbFt5eV0iLCJnYXNQcmljZVJhdGlvIjoiMi4wMDAifQ==",
      "ReceiptHash": "0xA20E055CA12756C18D74A17052BA2FE1A505380086158F549EC78F605165790A",
      "Receipt": {
        "chainID": "local[SmartCity]",
        "chainName": "SmartCity",
        "gasPriceRatio": "2.000"
      }
    },
    "/0/2/std::fee": {
      ......
    },
    "/0/3/ibc::packet/local->local[SmartCity]": {
      "Name": "ibc::packet/local->local[SmartCity]",
      "ContractAddr": "",
      "ReceiptBytes": "eyJmcm9tQ2hhaW5JRCI6ImxvY2FsIiwidG9DaGFpbklEIjoibG9jYWxbeXldIiwicXVldWVJRCI6ImxvY2FsLT5sb2NhbFt5eV0iLCJzZXEiOjEsIm9yZ0lEIjoib3JnSmdhR0NvblV5SzgxemlibnRVQmpRMzNQS2N0cGsxSzFHIiwiY29udHJhY3ROYW1lIjoibmV0Z292ZXJuYW5jZSIsImliY0hhc2giOiI2QTE2QTM2M0E1NDIxNUY1QzBFMUY2MzJENjg5RkJENjBDNjE0RkYyNEQwMDUxNEFDMTVCMzYzQ0UyRDM2QTA1IiwidHlwZSI6Im5vdGlmeSIsInN0YXRlIjp7InN0YXR1cyI6Ik5vQWNrIiwidGFnIjoiTm90aWZ5UGVuZGluZyIsImxvZyI6IiJ9LCJyZWNlaXB0cyI6W3sia2V5IjoiTHpBdmJtVjBaMjkyWlhKdVlXNWpaUzV6WlhSSFlYTlFjbWxqWlZKaGRHbHYiLCJ2YWx1ZSI6ImV5SnVZVzFsSWpvaWJtVjBaMjkyWlhKdVlXNWpaUzV6WlhSSFlYTlFjbWxqWlZKaGRHbHZJaXdpWTI5dWRISmhZM1JCWkdSeVpYTnpJam9pYkc5allXdzBaalZaVEVKT2FUTXpObkl4ZWxWWldsUm5ZVGxRV0ZaS2FXWkVjV1JuTTFVaUxDSnlaV05sYVhCMFFubDBaWE1pT2lKbGVVcHFZVWRHY0dKck5XaGlWMVZwVDJsS05XVlRTWE5KYlU1dldWZHNkVk5WVVdsUGFVcHpZakpPYUdKR2REVmxWakJwVEVOS2JsbFlUbEZqYld4cVdsWkthR1JIYkhaSmFtOXBUV2swZDAxRVFXbG1VVDA5SWl3aWNtVmpaV2x3ZEVoaGMyZ2lPaUpCTWpCRk1EVTFRMEV4TWpjMU5rTXhPRVEzTkVFeE56QTFNa0pCTWtaRk1VRTFNRFV6T0RBd09EWXhOVGhHTlRRNVJVTTNPRVkyTURVeE5qVTNPVEJCSW4wPSJ9XX0=",
      "ReceiptHash": "0x4B9FF741906AABC2977AA366F048C00F77E6CDFCC44F00B1FB0A8222BB27C5F2",
      "Receipt": {
        "contractName": "netgovernance",
        "fromChainID": "local",
        "ibcHash": "6A16A363A54215F5C0E1F632D689FBD60C614FF24D00514AC15B363CE2D36A05",
        "orgID": "orgJgaGConUyK81zibntUBjQ33PKctpk1K1G",
        "queueID": "local->local[SmartCity]",
        "receipts": [
          {
            "key": "LzAvbmV0Z292ZXJuYW5jZS5zZXRHYXNQcmljZVJhdGlv",
            "value": "eyJuYW1lIjoibmV0Z292ZXJuYW5jZS5zZXRHYXNQcmljZVJhdGlvIiwiY29udHJhY3RBZGRyZXNzIjoibG9jYWw0ZjVZTEJOaTMzNnIxelVZWlRnYTlQWFZKaWZEcWRnM1UiLCJyZWNlaXB0Qnl0ZXMiOiJleUpqYUdGcGJrNWhiV1VpT2lKNWVTSXNJbU5vWVdsdVNVUWlPaUpzYjJOaGJGdDVlVjBpTENKbllYTlFjbWxqWlZKaGRHbHZJam9pTWk0d01EQWlmUT09IiwicmVjZWlwdEhhc2giOiJBMjBFMDU1Q0ExMjc1NkMxOEQ3NEExNzA1MkJBMkZFMUE1MDUzODAwODYxNThGNTQ5RUM3OEY2MDUxNjU3OTBBIn0="
          }
        ],
        "seq": 1,
        "state": {
          "log": "",
          "status": "NoAck",
          "tag": "NotifyPending"
        },
        "toChainID": "local[SmartCity]",
        "type": "notify"
      }
    },
    "/1/0/totalFee": {
      ......
    },
    "/1/1/transferFee": {
      ......
    },
    "/1/2/transferFee": {
      ......
    },
    "/1/3/transferFee": {
      ......
    },
    "/1/4/transferFee": {
      ......
    }
  }
}
```

You can find the receipt named `netgovernance.setGasPriceRatio`, and check if the `chainID` and `gasPriceRatio` in the `Receipt` field are correct.

## 2. Quick start for node governance

### 2.1 Node preparation

+ After the previous operation, you have built a side chain, but it only has one observer node, so next, you need to add the verifier node of this side chain for consensus.
+ You need to build a observer node for the side chain so that the side chain observer node can be converted into the side chain verifier node. Refer to [BCB Installation Section](../../01-BCBBasic/02-BCBNode.md).

### 2.2 Export node private key

Using the following command to export the public key on the machine of the side chain observer node prepared in section 2.1. The node public key is used when turning the side chain observer into a verifier. Refer to [Export Node Public Key](./02-SideChainCreation.md) for the export node public key.

### 2.3 Add verifier node

> Notice: When add the verifier node for the side chain(verifier node is less than four), you must confirm the added public key is correct, otherwise the side chain will not work.

If you want to add a verifier node, you need to use the following command to add by the node public key from above, we take the verifier node name is `node2`, node public key is `0x0d180d63841102960cd86d88cf1f79e6695891d85385b4abf25f97b94cfaf2c0`, reward address is `local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG`, node weight is `10` as an example to show how to add verifier node:

```shell
./bcc call --contract governance --method NewValidator --params node2@0x0d180d63841102960cd86d88cf1f79e6695891d85385b4abf25f97b94cfaf2c0@local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG@10 --gasLimit 1000000 --orgName genesis --name scowner --password SCOwner@2019 --chainid local[SmartCity]

Return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 255000000,
  "txHash": "0xC6619B5D446CB718E555FB51C7E7FDCA46EE57E28683C979413EBA1F0FDF6A64",
  "height": 3819
}
```

The value of option `params` in the command line is the argument to set for the side chain genesis creation.

```html
the first parameter: node2, the verifier node name you added
the second parameter: 0x0d180d63841102960cd86d88cf1f79e6695891d85385b4abf25f97b94cfaf2c0, the node public key you got above + 0x
the third parameter:local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG, reward address
the forth parameter: 10, the node weight
```

Check the side chain `SmartCity` successfully adds the node by the following command:

```shell
./bcc query -k /ibc/local[SmartCity] --chainid local[SmartCity]

Return results:

OK
Response:
  Code: 200
  Key: /ibc/local[SmartCity]
  Value: {"local[SmartCity]33KDwKPQrtwdgTejxeGspyR7u4fefXTb7":{"nodepubkey":"0D180D63841102960CD86D88CF1F79E6695891D85385B4ABF25F97B94CFAF2C0","power":10,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node2","nodeaddr":"local[SmartCity]33KDwKPQrtwdgTejxeGspyR7u4fefXTb7"},"local[SmartCity]91TcFC3vPqsS3DWh5TksV1xCKZLWEftpD":{"nodepubkey":"10366FE4D47A9EA4AD54C864143B7FBD3ECA247995C663BCC3C8835D29317A30","power":10,"rewardaddr":"local[SmartCity]2V6b1EW2cExW5UtuUX9XXQhJCaaxXzLV6","name":"node1","nodeaddr":"local[SmartCity]91TcFC3vPqsS3DWh5TksV1xCKZLWEftpD"}}
```

You can see the side chain has added the new node `node2` successfully.

> Notice: when the current total number of the node is less than 4, the new node weight must be equal to 10, otherwise the addation of the new node will fail.

### 2.4 Adjust verifier node weight

When adjusting the verifier node weight, the current node must be guranteed to be greater than or equal to 4, we take the node public key is `0x2113d7a30d47a08ca79c8ebbc32a9c73a65a488b3f93da3a1eb42c57b35f9c9f`, node weight is `12` as an example to show how to adjust the verifier node weight:

```shell
./bcc call --contract governance --method SetPower --params 0x2113d7a30d47a08ca79c8ebbc32a9c73a65a488b3f93da3a1eb42c57b35f9c9f@12 --gasLimit 1000000 --orgName genesis --name scowner --password SCOwner@2019 --chainid local[SmartCity]

Return result:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 175000000,
  "txHash": "0xB0BB34E92ED02745460D4C6FD98F0B70B9B199A7B11B54C64F0281FA48D520F6",
  "height": 830
}
```

The value of option `params` in the command line is the argument to set for the side chain genesis creation:

```html
the first parameter:0x2113d7a30d47a08ca79c8ebbc32a9c73a65a488b3f93da3a1eb42c57b35f9c9f,  the node public key + 0x
the second parameter:12, the node weight
```

If you want to query if the node weight be set successfully, you can verify by the following command:

```shell
./bcc query -k /ibc/local[SmartCity] --chainid local[SmartCity]

Return results:

OK
Response:
  Code: 200
  Key: /ibc/local[SmartCity]
  Value: {"local[SmartCity]CFCHxFV6z6djWJR5FH1uSrJ8eN7AYj6gE":{"nodepubkey":"E1464972D492C1FB916336658068F0B7A92B458A6D7D0D010BDE5F035BC32A90","power":10,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node2","nodeaddr":"local[SmartCity]CFCHxFV6z6djWJR5FH1uSrJ8eN7AYj6gE"},"local[SmartCity]F5GqPDn294pdydBfxSgPEspbU5RPpwnUS":{"nodepubkey":"F3D77C12669A83AF7E922A7190001A40304AF01AD545A464D786A332761FB494","power":10,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node4","nodeaddr":"local[SmartCity]F5GqPDn294pdydBfxSgPEspbU5RPpwnUS"},"local[SmartCity]Gbh2JuVFg6orPcpCpQvAdv5gYT5kFQV3Q":{"nodepubkey":"2113D7A30D47A08CA79C8EBBC32A9C73A65A488B3F93DA3A1EB42C57B35F9C9F","power":12,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node3","nodeaddr":"local[SmartCity]Gbh2JuVFg6orPcpCpQvAdv5gYT5kFQV3Q"},"local[SmartCity]MwKS9rCK2nBNsevTdBBeiqKCrqQRkAK18":{"nodepubkey":"D781A3CE164052F8E103D5F9DE216659438ABF2D2F956FF76483A7E6B9C93117","power":10,"rewardaddr":"local[SmartCity]8LtT8AonWgJ8nMCEdAR5UGrbRfUmuoeiz","name":"node1","nodeaddr":"local[SmartCity]MwKS9rCK2nBNsevTdBBeiqKCrqQRkAK18"}}
```

You can see the node weight of the node `node3` is set to 12 successfully.

> Notice: if current node number is less than 4, you are not allowed to modify the node weight.

### 2.5 Delete verifier node

Deleting a node means to set the node weight to 0.

Before delete a node, you can query the current node details:

```shell
./bcc query -k /ibc/local[SmartCity] --chainid local[SmartCity]

Return results:

OK
Response:
  Code: 200
  Key: /ibc/local[SmartCity]
  Value: {"local[SmartCity]33KDwKPQrtwdgTejxeGspyR7u4fefXTb7":{"nodepubkey":"0D180D63841102960CD86D88CF1F79E6695891D85385B4ABF25F97B94CFAF2C0","power":10,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node5","nodeaddr":"local[SmartCity]33KDwKPQrtwdgTejxeGspyR7u4fefXTb7"},"local[SmartCity]CFCHxFV6z6djWJR5FH1uSrJ8eN7AYj6gE":{"nodepubkey":"E1464972D492C1FB916336658068F0B7A92B458A6D7D0D010BDE5F035BC32A90","power":10,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node2","nodeaddr":"local[SmartCity]CFCHxFV6z6djWJR5FH1uSrJ8eN7AYj6gE"},"local[SmartCity]F5GqPDn294pdydBfxSgPEspbU5RPpwnUS":{"nodepubkey":"F3D77C12669A83AF7E922A7190001A40304AF01AD545A464D786A332761FB494","power":10,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node4","nodeaddr":"local[SmartCity]F5GqPDn294pdydBfxSgPEspbU5RPpwnUS"},"local[SmartCity]Gbh2JuVFg6orPcpCpQvAdv5gYT5kFQV3Q":{"nodepubkey":"2113D7A30D47A08CA79C8EBBC32A9C73A65A488B3F93DA3A1EB42C57B35F9C9F","power":12,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node3","nodeaddr":"local[SmartCity]Gbh2JuVFg6orPcpCpQvAdv5gYT5kFQV3Q"},"local[SmartCity]MwKS9rCK2nBNsevTdBBeiqKCrqQRkAK18":{"nodepubkey":"D781A3CE164052F8E103D5F9DE216659438ABF2D2F956FF76483A7E6B9C93117","power":10,"rewardaddr":"local[SmartCity]8LtT8AonWgJ8nMCEdAR5UGrbRfUmuoeiz","name":"node1","nodeaddr":"local[SmartCity]MwKS9rCK2nBNsevTdBBeiqKCrqQRkAK18"}}
```

We take the node `node5`(its node public key is `0d180d63841102960cd86d88cf1f79e6695891d85385b4abf25f97b94cfaf2c0`) as an example to delete a node:

```shell
./bcc call --contract governance --method SetPower --params 0x0d180d63841102960cd86d88cf1f79e6695891d85385b4abf25f97b94cfaf2c0@0 --gasLimit 1000000 --orgName genesis --name scowner --password SCOwner@2019 --chainid local[SmartCity]

Return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 175000000,
  "txHash": "0x2CA4F72EBA8D525E8AFF3B325024E1E87D673EF2FF6B8287AA87487657AF9AF5",
  "height": 1352
}
```

You can verify the removal of the node by the following command:

```shell
./bcc query -k /ibc/local[SmartCity] --chainid local[SmartCity]

Return results:

OK
Response:
  Code: 200
  Key: /ibc/local[SmartCity]
  Value: {"local[SmartCity]CFCHxFV6z6djWJR5FH1uSrJ8eN7AYj6gE":{"nodepubkey":"E1464972D492C1FB916336658068F0B7A92B458A6D7D0D010BDE5F035BC32A90","power":10,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node2","nodeaddr":"local[SmartCity]CFCHxFV6z6djWJR5FH1uSrJ8eN7AYj6gE"},"local[SmartCity]F5GqPDn294pdydBfxSgPEspbU5RPpwnUS":{"nodepubkey":"F3D77C12669A83AF7E922A7190001A40304AF01AD545A464D786A332761FB494","power":10,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node4","nodeaddr":"local[SmartCity]F5GqPDn294pdydBfxSgPEspbU5RPpwnUS"},"local[SmartCity]Gbh2JuVFg6orPcpCpQvAdv5gYT5kFQV3Q":{"nodepubkey":"2113D7A30D47A08CA79C8EBBC32A9C73A65A488B3F93DA3A1EB42C57B35F9C9F","power":12,"rewardaddr":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","name":"node3","nodeaddr":"local[SmartCity]Gbh2JuVFg6orPcpCpQvAdv5gYT5kFQV3Q"},"local[SmartCity]MwKS9rCK2nBNsevTdBBeiqKCrqQRkAK18":{"nodepubkey":"D781A3CE164052F8E103D5F9DE216659438ABF2D2F956FF76483A7E6B9C93117","power":10,"rewardaddr":"local[SmartCity]8LtT8AonWgJ8nMCEdAR5UGrbRfUmuoeiz","name":"node1","nodeaddr":"local[SmartCity]MwKS9rCK2nBNsevTdBBeiqKCrqQRkAK18"}}
```

You can see the node `node5` has been deleted successfully.

> Notice: if current node number is less than 4, you are not allowed to delete the node.
