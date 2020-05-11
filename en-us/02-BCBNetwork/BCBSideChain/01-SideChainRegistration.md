# Side Chain Registration

> Notice 1：All contents of this sequence document are based on the `Build Private Chain`, if you have not built a private chain, please refer to [Build For Private Chain](../02-BuildForPrivateChain.md)
> Notice 2: All operation examples of this sequence document are based on the `BCB Tool`, if you want ot learn BCC Tool, please refer to [BCB Tools - BCB Tool](../../03-BCBTools\03-bcc.md)

## 1. Preparation

### 1.1 Registered Organizations

- Before registering the side chain, it is necessary to register an organization, you can define its name by yourself. When registering the side chain, it is necessary to specify an organization which the side chain belongs, and the side chain can not belong to the creation organization.

- Organization registration Refer to [Organization Development](../../04-SmartContractDev\SmartContract(golang)\DevSmartContract\01-DevelopmentEnvironment.md)

### 1.2 Set the list of public access paths for the main chain

After registering organizations, you need to set a list of public access paths for the main chain, that is OpenURLs, such as: `["http://localhost:46657"]`, the communication between the side chain and the main chain depends on the OpenURLs, if do not set it will cause the transaction sending from the side chain to the main chain can not be completed. We take the main chain id is `local`, OpenURLs is `["http://localhost:46657"]` as the example to show how to use bcc tools to complete the OpenURLs settings of the main chain.

```shell
./bcc call --contract netgovernance --method SetOpenURLs --splitBy @ --params  private chain chainID@[\"http://localhost:46657\"] --gasLimit 10000000 --orgName genesis --name owner --password Ab1@Cd3$

If the result is returned, the setting is successful, otherwise the setting fails.

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 250000000,
  "txHash": "0x48D9F66AFDC562936AAA2694D35CB94931997DABA74671106382E99C0937C604",
  "height": 1060
}
```

The value of option `params` in the command line is the argument to set for the main chain OpenURLs.

```html
first argument：local is the main chain ChainID
second argument：[\"http://localhost:46657\"] is the list of public access paths for the main chain to be set.
```

### 1.3 Prepare the side chain owner account on

The side chain owner account specified when registering the side chain will determine which account to operate for the subsequent series of operations, which can be the same account as the account of the registered organization. In this document we use the account name `scowner` generated in the main chain as the owner account for the side chain.

### 1.4 Prepare for a side cahin name

- Each side chain needs to have a clear name, and it is globally unique.
- The side chain name will be used to generate the side chain id, the generation rule is: the main chain id + `[` + the side chain name + `]`.
- The side chain name can be the same as the organization name to which it belongs.

## 2. Side chain registration

### 2.1 Implementation of registration

After finishing preparation work, you can register on the side chain. The following example takes the organization name `smartCity`, the side chain name `smartCity`, and the side chain owner account `localLvP9ForVPgagpSuH23MTp9jfW3GVxWfDK` as an example to show how to register the side chain using bcc tool:

```shell
./bcc call --contract netgovernance --method RegisterSideChain --splitBy @ --params smartCity@smartCity@localLvP9ForVPgagpSuH23MTp9jfW3GVxWfDK --gasLimit 100000 --orgName genesis --name owner --password Ab1@Cd3$

The following return results indicate success of the operation.

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 125000000,
  "txHash": "0x1861879BD4D0C8631806948454586DCA2C5B94850BA44CAE12DB4908084F6121",
  "height": 1436
}
```

The value of option `params` in the command line is the argument to set for the side chain.

```html
first argument：smartCity the side chain name
second argument：smartCity the organization name which the side chain belongs
third argument：localLvP9ForVPgagpSuH23MTp9jfW3GVxWfDK  the side chain owner account
```

### 2.2 Query data on chain

After the above opration is completed, you can query the registration information of the side chain from the chain to confirm the data is correct. The query command is:

```shell
./bcc query -k /sidechain/local[smartCity]/chaininfo

Return results:

OK
Response:
  Code: 200
  Key: /sidechain/local[smartCity]/chaininfo
  Value: {"sideChainName":"smartCity","chainID":"local[smartCity]","NodeNames":null,"orgName":"smartCity","owner":"localLvP9ForVPgagpSuH23MTp9jfW3GVxWfDK","height":0,"status":"init","gasPriceRatio":""}
```

We can see the side chain name is `smartCity`, chain id is `local[smartCity]`, state is `init` indicates that the side chain is in the initialization state waiting for creation form the query result.
