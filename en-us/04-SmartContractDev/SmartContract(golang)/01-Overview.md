# Smart Contract Overview

Since ```V2.0```, BCBChain supports independent development and deployment of smart contracts, developed using ```golang```.

## 1. Simple smart contract

### 1.1 Storage

Let us first take a look at the simplest form of a smart contract

```go
package mystorage

import (
    "blockchain/smcsdk/sdk"
)

//MyStorage a demo contract
//@:contract:mystorage
//@:version:1.0
//@:organization:orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer
//@:author:b37e7627431feb18123b81bcf1f41ffd37efdb90513d48ff2c7f8a0c27a9d06c
type MyStorage struct {
    sdk sdk.ISmartContract

    //@:public:store
    storedData uint64
}

//InitChain init when deployed on the blockchain first time
//@:constructor
func (ms *MyStorage) InitChain() {
}

//Set set a data to the stored data
//@:public:method:gas[100]
func (ms *MyStorage) Set(data uint64) {
    ms._setStoredData(data)
}

//Get get the stored data
//@:public:method:gas[100]
func (ms *MyStorage) Get() uint64 {
    return ms._storedData()
}
```

BCBChain's smart contract is a combination of code (functions of the contract) and data (data types in the contract) and a set of tags (metadata of the contract), and is located at a specific address of the BCBChain.

Code line:

```go
package mystorage
```

Declare the name of the smart contract code package, this can be set by the developer, so long it conforms to ```golang``` standards.

Code segment:

```go
import (
    "blockchain/smcsdk/sdk"
)
```

Declaration of the library to import, it is a smart contract ```SDK``` released by BCBChain. When creating the smart contract, you will need to configure the ```SDK``` path in ```GOPATH```.

Code segment:

```go
//MyStorage a demo contract
//@:contract:mystorage
//@:version:1.0
//@:organization:orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer
//@:author:b37e7627431feb18123b81bcf1f41ffd37efdb90513d48ff2c7f8a0c27a9d06c
type MyStorage struct {
    sdk sdk.ISmartContract

    //@:public:store
    storedData uint64
}
```

Declare the metadata and status of the smart contract.

* Comment line ```//MyStorage a demo contract``` A comment defining the smart contract below.
* Markup ```//@:contract:mystorage``` Declares the struct ```MyStorage``` that will be defined below represents a smart contract, and also declares the name of the smart contract as mystorage. This is the contract name to be sent to the BCBChain main chain during deployment. As an organization may develop multiple different smart contracts, the names of each smart contract will need to be unique, so the authors have to plan around this restriction.
* Markup ```//@:version:1.0``` Declares the code version of the smart contract.
* Markup ```//@:organization:orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer``` Identifies the organization to which the smart contract belongs. The organization name in this example is: example.
* Markup ```//@:author:b37e7627431feb18123b81bcf1f41ffd37efdb90513d48ff2c7f8a0c27a9d06c``` Author’s public key. The code line ```type MyStorage struct {``` declares the opening of the smart contract data structure, its members and its data type. The code line ```sdk sdk.ISmartContract``` indicates that the data structure is a BCBChain Smart Contract SDK and will automatically possess the smart contract access context provided by the SDK (variable names must be defined as sdk).
* Markup ```//@:public:store``` indicates that the next line of code will declare a data type.
* Code line ```storedData uint64``` Declares a state data variable of type```uint64``` with the name ```storedData```. You can view it as a member in the state database, and access or mutate its values by calling the database management functions, as well as access its KEY value (```/orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer/mystorage/storedData```) externally. The helper tools provided by BCBChain will automatically encapsulate the state variables and generate access functions```_storeData() uint64```, ```_setStoreData(uint64)```,```_chkStoreData() bool``` and ```_delStoreData() bool```.
* Code line ```}``` marks the end of this data structure’s declaration.

Code segment:

```go
//InitChain init when deployed on the blockchain first time
//@:constructor
func (ms *MyStorage) InitChain() {
}
```

Declares the initialization code for the smart contract when it first joins the chain (executed only on the first time,another initialization code ```UpdateChain```will be executed when the contract is upgraded, this does not need to be defined in this contract).

* Markup ```//@:constructor``` indicates that the function ```InitChain()``` defined below is an initialization function that is to be used once, when a smart contract is first deployed to BCBChain in order to complete the initialization of the smart contract on the blockchain. A part of the initialization, for example, includes the initialization of certain values in the global state variables.
* Code line ```func (ms *MyStorage) InitChain() {``` A function prototype that declares the initialization of a smart contract. The function name must be ```InitChain```, which has no input parameters.
* The code line ```}``` completes the function.

Code segment:

```go
//Set set a data to the stored data
//@:public:method:gas[100]
func (ms *MyStorage) Set(data uint64) {
    ms._setStoredData(data)
}
```

Declares the code for the smart contract

* Markup ```//@:public:method:gas[100]``` declares that the function ```Set()``` defined below is a public function of a smart contract, which can be called by BCBChain transaction broadcast, whereby the call information and result will be recorded in the blockchain. In doing so, the calling function will consume 100 gas.
* Code line ```func (ms *MyStorage) Set(data uint64) {``` Declares a function for a smart contract. The line```ms._setStoredData(data)``` is the implementation code for the function, which means that the input parameters are saved to the state variable ```storedData```.
* The code line ```}``` completes the smart contract function.

Code segment:

```go
//Get get the stored data
//@:public:method:gas[100]
func (ms *MyStorage) Get() uint64 {
    return ms._storedData()
}
```

Declares the code for the smart contract

* Markup ```//@:public:method:gas[100]``` declares that the function ```Get()``` defined below is a public function of a smart contract, which can be called by BCBChain transaction broadcast, whereby the call information and result will be recorded in the blockchain. In doing so, the calling function will consume 100 gas.
* Code line ```func (ms *MyStorage) Get() uint64 {``` Declare a function prototype for a smart contract. The code line ```return ms._storedData()``` is the implementation code for the function, indicating that the value of the state variable ```storedData```will be read and returned to the caller.
* The code line ```}``` completes the smart contract function.

There aren't many things that can be done with this contract: it allows anyone to store a single number in the contract, and that number can be accessed by anyone in the world, and there is no viable way to prevent you from publishing this number. Of course, anyone can call the ```Set()``` function again, passing in different values, overwriting your number, but this number will still be stored in the history of the blockchain. Later, we will see how to impose access restrictions to ensure that only you can change this number.

Note:

* All identifiers (contract name, function name, and variable name) of the smart contract code can only use the ```ASCII``` character set.
* Smart contract codes require storage in the form of ```ASCII``` or ```UTF-8``` encoding.

### 1.2 Token

The following contract implements one of the simplest encryption tokens. Here, the token can indeed be produced out of nothing, but only the owner of the contract can do it, and anyone can transfer the currency to others without registering the username and password - all that is required is a BCBChain-compliant encrypted key pair.

```go
package mycoin

import (
    "blockchain/smcsdk/sdk"
    "blockchain/smcsdk/sdk/bn"
    "blockchain/smcsdk/sdk/types"
)

//Mycoin a demo contract for digital coin
//@:contract:mycoin
//@:version:1.0
//@:organization:orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer
//@:author:b37e7627431feb18123b81bcf1f41ffd37efdb90513d48ff2c7f8a0c27a9d06c
type Mycoin struct {
    sdk sdk.ISmartContract

    //@:public:store:cache
    totalSupply bn.Number

    //@:public:store
    balanceOf map[types.Address]bn.Number
}

const oneToken int64 = 1000000000

//InitChain init when deployed on the blockchain first time
//@:constructor
func (mc *Mycoin) InitChain() {
  thisContract := mc.sdk.Helper().ContractHelper().ContractOfName("mycoin")
  totalSupply := bn.N1(1000000, oneToken)
  mc._setTotalSupply(totalSupply)
  mc._setBalanceOf(thisContract.Owner().Address(), totalSupply)
}

//@:public:receipt
type receipt interface {
    emitTransferMyCoin(token, from, to types.Address, value bn.Number)
}

//Transfer transfer coins from sender to another
//@:public:method:gas[500]
//@:public:interface:gas[450]
func (mc *Mycoin) Transfer(to types.Address, value bn.Number) {
    sdk.Require(value.IsPositive(),
        types.ErrInvalidParameter, "value must be positive")

    sender := mc.sdk.Message().Sender().Address()
    newBalanceOfSender := mc._balanceOf(sender).Sub(value)
    sdk.Require(newBalanceOfSender.IsGEI(0),
        types.ErrInsufficientBalance, "")

    receiver := to
    newBalanceOfReceiver := mc._balanceOf(receiver).Add(value)

    mc._setBalanceOf(sender, newBalanceOfSender)
    mc._setBalanceOf(receiver, newBalanceOfReceiver)

    mc.emitTransferMyCoin(
        mc.sdk.Message().Contract().Address(),
        sender,
        receiver,
        value)
}
```

This contract introduces some new concepts, which will be explained one-by-one in detail below

Code segment:

```go
    //@:public:store:cache
    totalSupply bn.Number
```

Declare state data for smart contracts.

* Markup ```//@:public:store:cache``` means that the next line of code will declare a state data that will be cached in memory.
* Code line ```totalSupply bn.Number``` declares a state variable of type  ```bn.Number```. The variable name is ```totalSupply```. The ```bn.Number``` type represents a signed large number. The addition, subtraction, multiplication, and division operations do not need to consider the overflow problem. The KEY value of this variable in the database is ```/orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer/mycoin/totalSupply```. The helper tool provided by BCBChain will automatically encapsulate the variable and generate access functions ```_totalSupply() bn.Number```,```_setTotalSupply(bn.Number)```, ```_chkTotalSupply() bool``` and```_delTotalSupply()```, which will also be generated due to the influence of the tag ```cache```. A function to clear the memory cache ```_clrTotalSupply()```.

Code segment:

```go
    //@:public:store
    balanceOf map[types.Address]bn.Number
```

A public state variable is also declared, but it is a more complex data type. This type maps the address to a large number and is used to store the balance corresponding to the account address that owns the token. The KEY value of this variable from the external access state database is ```/orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer/mycoin/balanceOf/address```, where ```address``` is the actual account address to be queried. The helper tool provided by BCBChain will automatically encapsulate and generate access functions for this variable```_balanceOf(types.Address) bn.Number```,```_setBalanceOf(types.Address, bn.Number)```,```_chkBalanceOf(types.Address) bool```and ```_delBalanceOf(types.Address)```.

Code segment:

```go
//@:public:receipt
type receipt interface {
    emitTransferMyCoin(token, from, to types.Address, value bn.Number)
}
```

Declares the receipt of the smart contract transaction, which be stored in the BCBChain chain for later access

* Markup ```//@:public:receipt``` declares the next line of code as the receipt interface.
* Code line ```type receipt interface {``` declares the start of the receipt type, with the type name as ```receipt```.
* Code line ```emitTransferMyCoin(token, from, to types.Address, value bn.Number)```declares a so-called receipt (receipt) that will be emitted on the last line of the Transfer function. The user interface (including the server application) can listen for the receipt being sent on the BCBChain chain at no cost. Once it is sent, the receipt ```listener``` will will be notified to facilitate tracking of the transaction.
* Code line ```}``` marks the end of the interface definition.

Code segment:

```go
//Transfer transfer coins from sender to another
//@:public:method:gas[500]
//@:public:interface:gas[450]
func (mc *Mycoin) Transfer(to types.Address, value bn.Number) {
    .
    .
    .
}
```

Declares the code for the smart contract

* Markup ```//@:public:interface:gas[450]``` declares that the function```Transfer()``` defined below is a public interface of a smart contract, which can be called between multiple smart contracts, and its use and results will be written into the BCBChain chain. The smart contracts from the same organization can call each other on the BCBChain. The public interface provided by BCBChain-based organization’s smart contracts can be called by any smart contract.

Code segment:

```go
  sdk.RequireAddress(to)
  sdk.Require(value.IsPositive(),
        types.ErrInvalidParameter, "value must be positive")
```

Declares a part of the code logic in the contract. The function ```sdk.RequireAddress()``` is provided by the SDK to validate if input parameter ```to```is an account address. If not, it will terminate the contract execution and return an error message in the response. The function```sdk.Require()``` is provided by the SDK to detect that a certain condition must be met (in this case, the input parameter ```value```must be greater than 0), otherwise, it will terminate the contract execution and return an error message in the response.

Code segment:

```go
  sender := mc.sdk.Message().Sender().Address()
  newBalanceOfSender := mc._balanceOf(sender).Sub(value)
  sdk.Require(newBalanceOfSender.IsGEI(0),
        types.ErrInsufficientBalance, "")
```

Declares a part of the code logic in the contract. The function ```mc.sdk.Message().Sender().Address()``` is provided by the SDK to retrieve the account address of the sender ```mc._balanceOf(sender).Sub(value)``` is used to obtain the balance of the tokens in the sender's account address after subtracting the transfer amount. The function ```_balanceOf()```is automatically generated by a support tool in BCBChain. The function ```sdk.Require()``` is provided by the SDK to detect that a certain condition must be met (in this case, the balance of the sender is must be sufficient for the transfer), otherwise, it will terminate the contract execution and return an error message in the response.

Code segment:

```go
  receiver := to
  newBalanceOfReceiver := mc._balanceOf(receiver).Add(value)
```

Declares a part of the code logic in the contract. ```mc._balanceOf(receiver).Add(value)``` calculates the new account balance of the transfer recipient’s account address.

Code segment:

```go
  mc._setBalanceOf(sender, newBalanceOfSender)
  mc._setBalanceOf(receiver, newBalanceOfReceiver)
```

Declares a part of the code logic in the contract. Used to write the calculated new account balance to the state database, the function```_setBalanceOf()```is automatically generated by the supporting tool provided by BCBChain

Code segment:

```go
  mc.emitTransferMyCoin(
        mc.sdk.Message().Contract().Address(),
        sender,
        receiver,
        value)
```

Declares a part of the code logic in the contract. It is to be used for updating the receipt of the current transfer transaction into the blockchain. The function ```emitTransferMyCoin()``` is automatically generated by the support tool provided by BCBChain.

This contract provides two functions. The function ```InitChain()``` is automatically called once by the BCBChain chain after contract creation to initialize the contract. The function for actual use by the user or other contract, and for completing the contract, is ```Transfer()```. This function can be used by anyone to send tokens to others (provided, of course, that the sender owns these tokens). Remember, if you use a contract to send tokens to an address, you will not see any relevant information when you view the address on the BCBChain chain browser. This is because the detailed information of the transfer and changes in balances is only stored in the data store of this contract (requires special means to query from the state database). By using receipts, you can easily create a “blockchain browser” for your new token to track transactions and balances.

## 2. Blockchain basics

programmers should not find the concept of blockchain difficult to understand, because most of the complex algorithms and protocols (hash, elliptic curve cryptography, peer-to-peer networking (P2P), etc.) are only used to fulfill special-case functionality and promise. Smart contract development programmers only need to accept these existing features and functions, and not care about the implementation of the underlying technology.

### 2.1 Transactions

A blockchain is a globally shared transactional database, which means that everyone can join the network to read the records in the database. If you want to change something in the database, you must create a transaction that is accepted by everyone else (also known as a transaction in the blockchain world). The word “transaction” means that for whatever that you want to do (assuming you want to change two values at the same time), it either occurs all at once, or not at all. In addition, when your transaction is saved to the database, it cannot be modified.

For example, imagine a table listing the balances of all accounts in an digital currency. If you send a request to transfer from one account to another, the transactional nature of the database ensures that if the amount is deducted from one account, it is always added to another account. If for some reason it is not possible to add an amount to the target account, the source account will not change.

In addition, the transaction is always signed by the sender (creator). This makes it very easy to add access protection mechanisms for specific modifications to the database. In the case of digital tokens, a simple check ensures that only the person holding the account key can transfer money from it.

### 2.2 States

BCBChain referenced Ethereum、Fabric、Tendermint、Cosmos and other open source blockchain solutions, drawing on some of these excellent ideas.

BCBChain is essentially a transaction-based state machine. In computer science, a state machine is a calculation model that contains a set of states, a start state, a set of input symbols (alphabet), and a A conversion function that maps the input symbol from current state to the next state (transition function).

In BCBChain, the state set is expressed by the state database. The initial state is called the genesis state. The input symbol set is the transaction (transaction, tx for short) in the blockchain field. The state transition function is the Smart contract.

![state machine](./p/statemachine.png)

According to the state machine of BCBChain, we start with the genesis state. This is almost similar to a blank slate, and there is no state of any transaction in the network. When the transaction is executed, the Genesis status will be transformed into the final state. At any time, this final state represents the current state of BCBChain.

### 2.3 Blocks

The state of BCBChain is composed of thousands of transactions. These transactions are "grouped" into blocks. A block contains a series of transactions, each block is linked to its previous block, and each block causes the state machine to reach a new state.

![blockchain](./p/blockchain.png)

For the state transition to happen, the transaction must be valid (i.e, to promote the non-repudiation characteristics of the blockchain technique). For a transaction to be considered valid, it must go through a verification process. Each transaction must be signed by the sender using its own private key, and the BCBChain's smart contract must be verified to meet certain conditions. Only then can the validation be successful.

### 2.4 Message Calls

Smart contracts can communicate with each other via message calls.

Each transaction can contain multiple top-level message calls that are executed in sequence. The receipt generated from the previous message call can be used as input for the next top-level message call for some logical processing.

Each top-level message called, will in turn generate more message calls across multiple contracts.

The number of message call layers is limited to 8. In order to prevent infinite loops, each layer of message calls are prohibited from forming a loop.

### 2.5 Receipt

On top of transaction result, message calls can also return the log data of the transaction execution process. Here, we call it the receipt, which is stored on the block and very easy to retrieve.
