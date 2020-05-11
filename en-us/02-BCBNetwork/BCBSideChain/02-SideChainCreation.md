# Side Chain Creation

## 1. Prepare for the creation

### 1.1 Build observer node for the main chain

+ The side chain creation needs to build the observer node of the main chain at first, and then use this observer node for side chain creation.

+ Building the main chain observer node refers to:[Installation of the BCB node](../../01-BCBBasic/02-BCBNode.md)

### 1.2 Export node public key

After building the observer node of the main chain, we need to derive the public key of the observer node, which will be used when sending the side chain creation transaction.

execute the following commands on the observer node of the main chain to export the public key of the node:

```shell
export TMHOME=/etc/tmcore
/usr/local/tmcore/bin/tendermint show_validator

Return results:

{"type":"AC26791624DE60","value":"dfkOn9m4x8wqxOz7i+hlpBo3dNey0TJ+mluT3IoYopo="}
75f90e9fd9b8c7cc2ac4ecfb8be865a41a3774d7b2d1327e9a5b93dc8a18a29a

75f90e9fd9b8c7cc2ac4ecfb8be865a41a3774d7b2d1327e9a5b93dc8a18a29a即为节点公钥
```

> Notice: When you try to export the public key, you must set the environment variable `export TMHOME=/etc/tmcore`, otherwise the data exported will be incorrect.

## 2. Genesis transaction

### 2.1 execute transaction

After the node public key is exported, the side chain genesis transactioncan be sent to the main chain, using the owner account prepared in `Side chain registration 1.3` for genesis transaction. we take the side chain name is `smartCity`, the side chain node name is `node1`, the side chain reward address is `0x75f90e9fd9b8c7cc2ac4ecfb8be865a41a3774d7b2d1327e9a5b93dc8a18a29a`, the side chain open access path OpenURLs is `http://side chain ip:46657`, and the gas price ratio is `1.000` as an example to show how to send the side chain genesis transaction.

```shell
./bcc call --contract netgovernance --method GenesisSideChain --splitBy @ --params smartCity@node1@0x75f90e9fd9b8c7cc2ac4ecfb8be865a41a3774d7b2d1327e9a5b93dc8a18a29a@local[smartCity]LvP9ForVPgagpSuH23MTp9jfW3GVxWfDK@http:// side chain ip:46657@"1.000" --gasLimit 10000000 --orgName genesis --name scowner --password SCOwner@2019

Return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 12500000000,
  "txHash": "0xB6107AAAA7527523153A69EE2CE87EA0C27A02A10131502950A444A28C436AD9",
  "height": 1934
}
```

The value of option `params` in the command line is the argument to set for the side chain genesis transaction:

```html
the first parameter：smartCity is side chain name, after genesis creation, the side chain id is the same as the main chain id.
the second parameter: node1 is the side chain genesis node name.
the third parameter: 0x75f90e9fd9b8c7cc2ac4ecfb8be865a41a3774d7b2d1327e9a5b93dc8a18a29a is the public key of the side chain genesis node(that is the public key derived from the section 1.2, and it is preceded by 0x).
the fourth parameter：local[smartCity]LvP9ForVPgagpSuH23MTp9jfW3GVxWfDK is the side chain reward address
the fifth parameter：http://side chain ip:46657 is the side chain open access path OpenURLs
the sixth parameter："1.000" is gas rrice ratio that keeps three decimals places.
```

You can query the receipt to confirm the genesis information, the query command is:

```shell
./bcc tx --txhash 0xB6107AAAA7527523153A69EE2CE87EA0C27A02A10131502950A444A28C436AD9 --chainid local

Return results:

OK
  Response: {
  .....
  "tags": {
  .....
    "/0/1/netgovernance.genesisSideChain": {
      "Name": "netgovernance.genesisSideChain",
      "ContractAddr": "",
  .....
        "genesisInfo": "{\"chain_id\":\"local[smartCity]\",\"chain_version\":\"2\",\"genesis_time\":\"2019-11-30T11:09:56Z\",\"app_hash\":\"\",\"app_state\":{\"organization\":\"genesis\",\"gas_price_ratio\":\"1.000\",\"token\":{\"address\":\"local[smartCity]AJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA\",\"owner\":\"local[smartCity]ETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL\",\"name\":\"LOC\",\"symbol\":\"LOC\",\"totalSupply\":0,\"addSupplyEnabled\":false,\"burnEnabled\":false,\"gasprice\":2500},\"rewardStrategy\":[{\"name\":\"validators\",\"rewardPercent\":\"100.00\",\"address\":\"\"}],\"contracts\":[{\"name\":\"token-basic\",\"version\":\"2.1\",\"code\":\"token-basic-2.1.tar.gz\",\"codeHash\":\"ff66c796d153764491a3dfdbf95cd4dcb2bb9af6be683adc4825816dfcbe8372\",\"codeDevSig\":{\"pubkey\":\"5e8339cb1a5cce65602fd4f57e115905348f7e83bcbe38dd77694dbe1f8903c9\",\"signature\":\"59EA39CEB1AAA03FB25A1E5B1E9947548FAD9EACCA87AFDF2BA9BE784A929F18B21FCFF31419889951BBA79655D3CF7BABB95546CEC9E8621B4B4FB177EA5707\"},\"codeOrgSig\":{\"pubkey\":\"0c27b3396bdc1b486af51e84accbdd23a0d55a49c34fa51cf0ed6aedccf984d4\",\"signature\":\"CF23FDCFD92408F43634D3BA7C89919D41416F269B3FB07025E148D6458B9E36772F5C473A279F17845B068AD23B983ECF8DE8326431192DFACA0691BB812B07\"}},{\"name\":\"token-issue\",\"version\":\"2.1\",\"code\":\"token-issue-2.1.tar.gz\",\"codeHash\":\"05cbacf200ad36c084efa13f372583615c3ae1dd12dbcec3c7e778889da256ea\",\"codeDevSig\":{\"pubkey\":\"5e8339cb1a5cce65602fd4f57e115905348f7e83bcbe38dd77694dbe1f8903c9\",\"signature\":\"9DAA25E40414F1F07E3D0798627465E36CF1DE7367AEECD820D5ABB95D2E2560F5056C2B86FBBF692C89FC3AB3179FAC8D5C273B28B5E54C6022CE5DD8EAF90C\"},\"codeOrgSig\":{\"pubkey\":\"0c27b3396bdc1b486af51e84accbdd23a0d55a49c34fa51cf0ed6aedccf984d4\",\"signature\":\"3C73104013C634AC888E1E5063247C0778274B01B3F833A49B29E8518D4D059E7AAD13AFDB230DE28DF015CDDDE19033FF2C1785F273F74DC00C907A585CD20B\"}},{\"name\":\"governance\",\"version\":\"2.1\",\"owner\":\"local[smartCity]LvP9ForVPgagpSuH23MTp9jfW3GVxWfDK\",\"code\":\"governance-2.1.tar.gz\",\"codeHash\":\"32faaea316ee5f385b673c2f8d60637e4aa9c8166fca998cb5080bff7fceeacf\",\"codeDevSig\":{\"pubkey\":\"5e8339cb1a5cce65602fd4f57e115905348f7e83bcbe38dd77694dbe1f8903c9\",\"signature\":\"084631935319C2B7F0BADAD04103D0628BC79F606523907D76951A0056066DF79E5B0CC7094C46027B20C3299E257B8D47B173153C69B11B80F8E5DEBC289204\"},\"codeOrgSig\":{\"pubkey\":\"0c27b3396bdc1b486af51e84accbdd23a0d55a49c34fa51cf0ed6aedccf984d4\",\"signature\":\"69ABDF8F61C5D96A169F5B2B2D853662D3CF279125AFD31DA4BD4FE883005F79CE716DC8816714B9584D2DEA6CEBCCDA6158856B731D26EFE9146817D891340D\"}},{\"name\":\"organization\",\"version\":\"2.1\",\"code\":\"organization-2.1.tar.gz\",\"codeHash\":\"b8f55cbb984553d68dfebbd608727db13162ff1b0aae36345aefeabd4951bb6d\",\"codeDevSig\":{\"pubkey\":\"5e8339cb1a5cce65602fd4f57e115905348f7e83bcbe38dd77694dbe1f8903c9\",\"signature\":\"3F66F5F4A25E1F67C53F2D36D216E299475F65AAD92A5F90D47E2B77B32B716787ADA9D9CCDCB2CD6EF31071E171063C57496F13D008518DBE1A6C5AE71A5107\"},\"codeOrgSig\":{\"pubkey\":\"0c27b3396bdc1b486af51e84accbdd23a0d55a49c34fa51cf0ed6aedccf984d4\",\"signature\":\"0AC47FE7FB20BF9A66415CDD6BB52CC3A595E32FA2BEBF907C693BD054B674F5A9E4D1727D243B5F75298993122231734DE75E04764DABC86D2EF4B43694A900\"}},{\"name\":\"smartcontract\",\"version\":\"2.1\",\"code\":\"smartcontract-2.1.tar.gz\",\"codeHash\":\"41836992a6eb8cf3787323393841a89959d050fbe7ca5a18349f8d308e3b9dcf\",\"codeDevSig\":{\"pubkey\":\"5e8339cb1a5cce65602fd4f57e115905348f7e83bcbe38dd77694dbe1f8903c9\",\"signature\":\"AB18C8E319C2F844E780C9D4D6AEC2AD0874A2FD0CFD2CC719679A87407CE0FA23226304362F3C4D2500CBD06E1D84DBB6BA7AADE0B63F73FB3D83122D4E340B\"},\"codeOrgSig\":{\"pubkey\":\"0c27b3396bdc1b486af51e84accbdd23a0d55a49c34fa51cf0ed6aedccf984d4\",\"signature\":\"96B0C8EEB55341060D1CDCC2F84A250F0C5EC9B1AFE232235E0D5F29EBE46F8FEF070AD3EE2AE3C5FD804AFF82170CA4917AB15921C23D453AFBA6D10E46440D\"}},{\"name\":\"ibc\",\"version\":\"2.1\",\"code\":\"ibc-2.1.tar.gz\",\"codeHash\":\"a684f89185e6f98f83dc78f10340ca5899e8fd2eb601ff3f8db4b0b038152747\",\"codeDevSig\":{\"pubkey\":\"5e8339cb1a5cce65602fd4f57e115905348f7e83bcbe38dd77694dbe1f8903c9\",\"signature\":\"64BD0994180A3EBCE404105772F74197A3EE5CAE35436D1E6DFB5EF67CB88F2E7B6ADC2FB23858AAF39455FC238D93B328863EE7D46D29756219F0640AEA340E\"},\"codeOrgSig\":{\"pubkey\":\"0c27b3396bdc1b486af51e84accbdd23a0d55a49c34fa51cf0ed6aedccf984d4\",\"signature\":\"2034DB17354A8F8604F659947A087BBE8D864EAF40CFF2EA19C2614219BDE01A15F84A5ACE31B1206F8B9DCB809B909753B6D7233F61C2B3C2421CCBF1F9D709\"}}],\"orgBind\":{\"orgName\":\"smartCity\",\"owner\":\"local[smartCity]LvP9ForVPgagpSuH23MTp9jfW3GVxWfDK\"},\"mainChain\":{\"openUrls\":[\"http://192.170.41.72:46657\"],\"validators\":{\"local582JbHcuDcQMdMVdzdwKJTy4ekhZk9MFb\":{\"nodepubkey\":\"6C549B3002D1E699732DFF1B78F011065BBA3BF95FC327AA896A1132D4BDB7E9\",\"power\":10,\"name\":\"local\",\"nodeaddr\":\"local582JbHcuDcQMdMVdzdwKJTy4ekhZk9MFb\"}}}},\"validators\":[{\"nodepubkey\":\"75F90E9FD9B8C7CC2AC4ECFB8BE865A41A3774D7B2D1327E9A5B93DC8A18A29A\",\"power\":10,\"reward_addr\":\"local[smartCity]LvP9ForVPgagpSuH23MTp9jfW3GVxWfDK\",\"name\":\"node1\",\"nodeaddr\":\"local[smartCity]AKHbp57Sqfv8G39KHmsntWodxAfPDPTrd\"}]}",
        "openURLs": [
          "http://side chain ip:46657"
        ],
        "sideChainID": "local[smartCity]"
      }
    },
  .....

The side chain information can be seen from the above genesisInfo, the "nodepubkey" in the
"validators\":[{\"nodepubkey\":\"75F90E9FD9B8C7CC2AC4ECFB8BE865A41A3774D7B2D1327E9A5B93DC8A18A29A\",\"power\":10,\"reward_addr\":\"local[smartCity]LvP9ForVPgagpSuH23MTp9jfW3GVxWfDK\",\"name\":\"node1\",\"nodeaddr\":\"local[smartCity]AKHbp57Sqfv8G39KHmsntWodxAfPDPTrd\"}]}" should be the same as the node public key derived from section 1.2 converted to uppercase letters, "openURLs" is the side chain addrress set at the genesis creation.
```

## 3. Confirm results

In order to confirm whether the genesis creation of the side chain is successful, you need to confirm on the main chain and the side chain respectively, querying commands are:

Confirm on the main chain:

```shell
Query commands on the main chain: the state becomes to ready
./bcc query -k /sidechain/local[smartCity]/chaininfo

Return results:

OK
Response:
  Code: 200
  Key: /sidechain/local[smartCity]/chaininfo
  Value: {"sideChainName":"smartCity","chainID":"local[smartCity]","NodeNames":["node1"],"orgName":"smartCity","owner":"localLvP9ForVPgagpSuH23MTp9jfW3GVxWfDK","height":1934,"status":"ready","gasPriceRatio":"1.000"}
```

Confirm on the side chain:

```shell
Query commands on the side chain:
./bcc query -k /genesis/chainid

Return results:

OK
Response:
  Code: 200
  Key: /genesis/chainid
  Value: "local[smartCity]"

You can see the chain id of the original main chain observer has become the chain id of the new side chain.
```
