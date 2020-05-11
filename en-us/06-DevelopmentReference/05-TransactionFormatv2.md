# Transaction Format v2

The following describes the transaction format of BCBChain (the version of transaction format is "V2"). This version of transaction format is supported from BCBChain 2.0.

This version of the transaction format supports multiple calls to different smart contract methods in a transaction. Each call to the smart contract method is called a message, and multiple calls in a transaction are called cascading messages.

The receipt of a message output in the cascade message is used as the input of the next message, and the output receipt of the previous message needs to be used in the smart contract method called by the latter message.

The typical application scenario 1 of cascaded messages is described as follows (using BCBChain token):

* Transfer x BCB to the smart contract address A in the first message;
* In the second message, call the function in the contract A. In this function, uses X BCB to purchase game props for users.

The typical application scenario 2 of cascade message is described as follows (using a token issued on BCBChain, such as "USDX"):

* In the first message, transfer y USDX to the smart contract address B
* In the second message, call the function in the contract B. In this function, uses y USDX to purchase game props for users.

Bcbchain v2.0 only supports two messages to be cascaded temporarily. In the future, more messages can be added for cascading calls according to business needs.

Bcbchain v2.1 adds a container selection option for running smart contracts to support relay programs to handle cross chain messages.

## 1.  Frame

The transaction format of BCBChain is defined as follows (two formats):

> **bcb\<tx\>.v2.**Payload.\<SignNumber>.Signature.….Signature

The transaction format is divided into multiple segments by "." and the meaning of each segment is described below (pay attention to case sensitivity)

| Parameter          |     type    | comment                                                   |
| :------------ | :-----------: | :----------------------------------------------------------- |
| **bcb\<tx>**  |    String     | uses the chain ID as the transaction prefix to identify the string, indicating that this is a transaction on which the smart contract is executed on the blockchain, and this transaction will modify the world state of the blockchain |
| **v2**        |    String     | transaction version. The current version is defined as "V2"               |
| Payload       | Base58 String | the payload of a transaction is defined as a base58 encoded string. Please refer to the subsequent sections of this chapter for specific definitions |
| \<SignNumber> |    \<Int>     | the number of signatures. Note that it is a decimal integer expressed as a string, which must be 1, which means that all transactions on BCBChain must be signed, for example: "<1>". According to the number of signatures, the last signature should be repeated the same number of times|
| Signature     | Base58 String | describes the signature of a signer. It is a base58 encoded string. Please refer to the subsequent sections of this chapter for specific definitions. According to the number of signatures, the last signature should be repeated the same number of times|

## 2. Payload

This section defines the transaction payload data format in detail. All the defined fields in the table are encoded with RLP. Then, the RLP codes of these fields are output and spliced together in recursive hierarchical order, and the payload length field of RLP code format is added at the top as the naked data of transaction payload. The signature is based on the naked data of payload.

Finally, the payload output to the transaction framework format package needs to be encoded as a base58 string based on the raw data.

### 2.1 Call smart contract

The smart contract call only appears in the type "bcb\<tx\>", this function is to call the methods provided by the smart contract to modify the status of the blockchain world. For example, calling the token transfer contract to transfer from account A to account B, the business logic of these methods is provided by the smart contract code independently.

The data structure of the smart contract call request is defined as follows:

| **Parameter**                       | **type** | **comment**                                                     |
| ------------------------------ | :------: | :----------------------------------------------------------- |
| nonce                          |  Uint64  | Number  used once or Number once. The number of transactions initiated by the transaction initiator is less than br / > value. Starting from 1, it must grow monotonously with a growth step of 1|
| gasLimit                       |  Uint64  | the maximum amount of gas that the transaction originator is willing to pay to execute the transaction |
| note                           |  String  | UTF-8 encoded note information, up to 256 characters |
| msgs: [                        |  Array   | concatenated message list                                   |
| &nbsp;{                        |          | a message                                                |
| &nbsp;&nbsp;to                 | Address  | the location method of the called smart contract address (note, not the account address of the contract), There are two formats: <br/>&nbsp;&nbsp;&nbsp;&nbsp;**contract address**<br/>&nbsp;&nbsp;&nbsp;&nbsp;**organization ID. contract address**<br/> note: for the smart contract developed by **golang**, the organization ID is here for the system to choose the appropriate contract about running container, suitable for handling cross chain messages with relay program|
| &nbsp;&nbsp;MethodID           |  Uint32  | function id of the calling contract[require]                |
| &nbsp;&nbsp;items:   [         |          |                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;item-0 | RlpBytes | Parameter 0 of the smart contract method is the sequence of bytes encoded by RLP                   |
| &nbsp;&nbsp;&nbsp;&nbsp;item-1 | RlpBytes | Parameter 1 of the smart contract method is the sequence of bytes encoded by RLP          |
| &nbsp;&nbsp;&nbsp;&nbsp;…      |    …     | …                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;item-n | RlpBytes | Parameter n of the smart contract method is the sequence of bytes encoded by RLP      |
| &nbsp;&nbsp;]                  |          |                                                              |
| &nbsp;}                        |          |                                                              |
| ]                              |          |                                                              |

## 3. Signature

This section defines the signature data format in detail. All the defined fields in the table are encoded with RLP. Then, the RLP codes of these fields are output and spliced together in order, and the signature length field of RLP code format is added at the front as the raw data of signature.

Finally, the signature output to the transaction framework format package needs to be encoded as a base58 string based on the raw data.

The data definition of signature in transaction framework layer is as follows:

| **Parameter**  | **type** | **comment**                                                     |
| --------- | -------- | ------------------------------------------------------------ |
| type      | String   | signature type, currently only ed25519 is supported          |
| pubkey    | [32]byte | signer's 32-byte public key        |
| signature | [64]byte | 64 byte signature result. The data to be signed is the raw data of the transaction payload before the base58 encoding |

## 4. Transaction structure

This chapter takes BCBChain transfer as an example to describe the structure of transaction format-v2 in detail.

The following is the transaction construction process of calling a token transfer to the nickname of the specified contract registration game:

```shell
<==== sender ===========================================================>
privKey: 4a2c14697282e658b3ed7dd5324de1a102d216d6fa50d5937ffe89f35cbc12aa
         68eb9a09813bdf7c0869bf34a244cc545711509fe70f978d121afd3a4ae610e6
pubKey:  68EB9A09813BDF7C0869BF34A244CC545711509FE70F978D121AFD3A4AE610E6
address: bcb6qsUWWVeGgdqqM43XV9bWnVhTjCD5Wa3p

<==== raw params ========================================================>
nonce:               1
gasLimit:            500
note:                Example for cascade invoke smart contract.
msgs: [
  {
    toContract:      bcbMWedWqzzW8jkt5tntTomQQEN7fSwWFhw6
    MethodID:        0x44d8ca60
    items{
      toAccount:     bcbCpeczqoSoxLxx1x3UyuKsaS4J8yamzWzz
      value:         1000000000
    }
  }
  {
    toContract:      bcbCpeczqoSoxLxx1x3UyuKsaS4J8yamzWzz
    MethodID:        0x6457e648
    items{
      nickName:      mmmmhhhh
      referee:       bcb5rzgE1tSJbJuegEj4vbAkotmwRkxwiSyV
    }
  }
]

Each parameter of the calling method in raw data is encoded separately by RLP.
<==== raw params ========================================================>
nonce:               1
gasLimit:            500
note:                Example for cascade invoke smart contract.
msgs: [
  {
    toContract:      bcbMWedWqzzW8jkt5tntTomQQEN7fSwWFhw6
    MethodID:        0x44d8ca60
    items{
      toAccount(RLP):0xa4626362437065637a716f536f784c78783178335579754b736
                       153344a3879616d7a577a7a
      value(RLP):    0x843b9aca00
    }
  }
  {
    toContract:      bcbCpeczqoSoxLxx1x3UyuKsaS4J8yamzWzz
    MethodID:        0x6457e648
    items{
      nickName(RLP): 0x886d6d6d6d68686868
      referee(RLP):  0xa462636235727a67453174534a624a756567456a347662416b6
                       f746d77526b787769537956
    }
  }
]

Use the RLP to encode the parameter table calling the contract method in the original data.
<==== raw params (partial rlp encoded) ==================================>
nonce:               1
gasLimit:            500
note:                Example for cascade invoke smart contract.
msgs: [
  {
    toContract(RLP): 0xa46263624d57656457717a7a57386a6b7435746e74546f6d515
                       1454e376653775746687736
    MethodID(RLP):   0x8444d8ca60
    items(RLP):      0xeca5a4626362437065637a716f536f784c78783178335579754
                       b736153344a3879616d7a577a7a85843b9aca00
  },
  {
    toContract(RLP): 0xa4626362437065637a716f536f784c78783178335579754b736
                       153344a3879616d7a577a7a
    MethodID(RLP):   0x846457e648
    items(RLP):      0xf089886d6d6d6d68686868a5a462636235727a67453174534a6
                       24a756567456a347662416b6f746d77526b787769537956
  }
]

Use RLP to encode the single message calling the contract method in the original data:
<==== raw params (partial rlp encoded) ==================================>
nonce:               1
gasLimit:            500
note:                Example for cascade invoke smart contract.
msgs: [
  message1(RLP):     0xf857a46263624d57656457717a7a57386a6b7435746e74546f6
                       d5151454e3766537757466877368444d8ca60eca5a462636243
                       7065637a716f536f784c78783178335579754b736153344a387
                       9616d7a577a7a85843b9aca00
  message2(RLP):     0xf85ba4626362437065637a716f536f784c78783178335579754
                       b736153344a3879616d7a577a7a846457e648f089886d6d6d6d
                       68686868a5a462636235727a67453174534a624a756567456a3
                       47662416b6f746d77526b787769537956
]

Use RLP to encode the message table calling the contract method in the original data.
<==== raw params (partial rlp encoded) ==================================>
nonce:               1
gasLimit:            500
note:                Example for cascade invoke smart contract.
msgs:                0xf8b6f857a46263624d57656457717a7a57386a6b7435746e745
                       46f6d5151454e3766537757466877368444d8ca60eca5a46263
                       62437065637a716f536f784c78783178335579754b736153344
                       a3879616d7a577a7a85843b9aca00f85ba4626362437065637a
                       716f536f784c78783178335579754b736153344a3879616d7a5
                       77a7a846457e648f089886d6d6d6d68686868a5a46263623572
                       7a67453174534a624a756567456a347662416b6f746d77526b7
                       87769537956

Use RLP to encode the transaction data: get the payload data to be signed
<==== rlp for tx data (payload for sign) ================================>
payload:             0xf8e7018201f4aa4578616d706c6520666f72206361736361646
                       520696e766f6b6520736d61727420636f6e74726163742ef8b6
                       f857a46263624d57656457717a7a57386a6b7435746e74546f6
                       d5151454e3766537757466877368444d8ca60eca5a462636243
                       7065637a716f536f784c78783178335579754b736153344a387
                       9616d7a577a7a85843b9aca00f85ba4626362437065637a716f
                       536f784c78783178335579754b736153344a3879616d7a577a7
                       a846457e648f089886d6d6d6d68686868a5a462636235727a67
                       453174534a624a756567456a347662416b6f746d77526b78776
                       9537956

Sign the payload data:
<==== raw sign data for payload =========================================>
sig:type:            ed25519
sig:pubkey:          0x68eb9a09813bdf7c0869bf34a244cc545711509fe70f978d121
afd3a4ae610e6
sig:signdata:        0x52adbea8b118cd0f62b286beaee37cdf2912f0a86ddbb398f27
                       bf3d468a4f764d981c0143427560322c75c3da1b3f4749501cb
                       d78a0341448742b4d41d3ab30f

Use RLP to encode each field of signature data:
<==== rlp for raw sign data =============================================>
sig:type:            0x8765643235353139
sig:pubkey:          0xa068eb9a09813bdf7c0869bf34a244cc545711509fe70f978d1
                       21afd3a4ae610e6
sig:signdata:        0xb84052adbea8b118cd0f62b286beaee37cdf2912f0a86ddbb39
                       8f27bf3d468a4f764d981c0143427560322c75c3da1b3f47495
                       01cbd78a0341448742b4d41d3ab30f

The above RLP encoded signature data are combined in order:
<==== merged sign data list =============================================>
sig:signdata:        0x8765643235353139a068eb9a09813bdf7c0869bf34a244cc545
                       711509fe70f978d121afd3a4ae610e6b84052adbea8b118cd0f
                       62b286beaee37cdf2912f0a86ddbb398f27bf3d468a4f764d98
                       1c0143427560322c75c3da1b3f4749501cbd78a0341448742b4
                       d41d3ab30f

Use RLP to encode combined signature data again: get the final signature data
<==== rlp for merged sign data list =====================================>
rlp:signdata:        0xf86b8765643235353139a068eb9a09813bdf7c0869bf34a244c
                       c545711509fe70f978d121afd3a4ae610e6b84052adbea8b118
                       cd0f62b286beaee37cdf2912f0a86ddbb398f27bf3d468a4f76
                       4d981c0143427560322c75c3da1b3f4749501cbd78a03414487
                       42b4d41d3ab30f

Use base58 to encode the payload data:
<==== Base58 for payload ================================================>
data:  3BC4C8dK8GJbcqLqBdyQTiFvnjoDjMZ82FrjiNkcTteF8Lfwy5goNCzwStbhP5QkBUv
       nqWwtQnF3Dyh6E33aBg3B5hsFvT2ukvehnycqfrG2jFQr3LqaSXu9odXGmKjMwgaejQ
       os7DZ4nDF1MF5F7f1vF4r2SzB9zugJf1LQApZvkiXv9mGKrhsALXXDvhJ9z2sC4wHt7
       PmeZVMjURW3Bfc6JM6bnUtmsA3hXTfZS4FWbyc3bCreRcJvjvq6tiNbhNi4BAfuV25F
       Guf3C2cjzRuF7mjt95pr3PJ5EuxhgWY8xzJArpHMGLeZ4yEB5fB

Use base58 to encode the signature data:
<==== Base58 for sign data ==============================================>
data:  YTgiA1gdDGi2L8hvDHobGcmYj6sXf1qQ8qdiHsHnZsaS4DDHcgvJj7rJvDkqvWrEMgA
       JRAttrc9YKyNWVH8tZ9gnTsFPiLLBBMp5hEsiFzEWBCny1NnFpt4TAwRNuV7r7YtLJQ
       euc4sJsRo9aLGia

The payload encoded by base58 and signature data are used to construct the final transaction data according to the specification:
<==== final tx data =====================================================>
bcb<tx>.v2.3BC4C8dK8GJbcqLqBdyQTiFvnjoDjMZ82FrjiNkcTteF8Lfwy5goNCzwStbhP5Q
kBUvnqWwtQnF3Dyh6E33aBg3B5hsFvT2ukvehnycqfrG2jFQr3LqaSXu9odXGmKjMwgaejQos7
DZ4nDF1MF5F7f1vF4r2SzB9zugJf1LQApZvkiXv9mGKrhsALXXDvhJ9z2sC4wHt7PmeZVMjURW
3Bfc6JM6bnUtmsA3hXTfZS4FWbyc3bCreRcJvjvq6tiNbhNi4BAfuV25FGuf3C2cjzRuF7mjt9
5pr3PJ5EuxhgWY8xzJArpHMGLeZ4yEB5fB.<1>.YTgiA1gdDGi2L8hvDHobGcmYj6sXf1qQ8qd
iHsHnZsaS4DDHcgvJj7rJvDkqvWrEMgAJRAttrc9YKyNWVH8tZ9gnTsFPiLLBBMp5hEsiFzEWB
Cny1NnFpt4TAwRNuV7r7YtLJQeuc4sJsRo9aLGia

Calculate hash of transaction data:
<==== final tx hash =====================================================>
366E331B53A92A64EFE2CD877B43F291EE56E8C710F0DC544599A2B875D55E01
```
