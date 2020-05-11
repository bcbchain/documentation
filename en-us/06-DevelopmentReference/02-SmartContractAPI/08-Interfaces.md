# Interfaces

## 1 sdk/ISmartContract

The interface ```sdk/ISmartContract``` encapsulates the path to smart contract context acquisition.

### 1.1 func Block()

Function Prototype:

```go
func (ISmartContract) Block() IBlock
```

Returns the block data when the blockchain of BCBChain is called.

### 1.2 func Tx()

Function Prototype:

```go
func (ISmartContract) Tx() ITx
```

Returns the transaction data called on the blockchain of BCBChain.

### 1.3 func Message()

Function Prototype:

```go
func (ISmartContract) Message() IMessage
```

Returns the message for this smart contract call.

### 1.4 func Helper()

Function Prototype:

```go
func (ISmartContract) Helper() IHelper
```

Returns a helper object that encapsulates all the support functions of the SDK.

## 2 sdk/IBlock

The interface `sdk/IBlock` encapsulates the block information obtained by the smart contract.

When a smart contract is invoked, the `IBlock` interface will have different block information depending on two different phases.

> In the checkTx phase, the current smart contract call has yet to reach a consensus, ISmartContract::Block() is called to obtain an simulated block (may be an empty block. In short, this block has nothing to do with the currently executed smart contract call) generated above the last block on the blockchain (block height plus 1).
> In the deliverTx phase, the transaction that invoked the smart contract has reached a consensus on the blockchain and is written to the latest block. At this point, ISmartContract::Block() is called to get the latest real-time information on the blockchain. (The block now cannot be an empty block, it contains at least one transaction information called for this smart contract).

### 2.1 func ChainID()

Function Prototype:

```go
func (IBlock) ChainID() string
```

Returns the chain ID of the current blockchain.

### 2.2 func BlockHash()

Function Prototype:

```go
func (IBlock) BlockHash() types.Hash
```

Returns the block hash of the current block.

### 2.3 func Height()

Function Prototype:

```go
func (IBlock) Height() int64
```

Returns the height of the current block.

### 2.4 func Time()

Function Prototype:

```go
func (IBlock) Time() int64
```

Returns the timestamp when the current block was created. The result is the number of seconds past the `1970-1-1 00:00:00`.

### 2.5 func Now()

Function Prototype:

```go
func (IBlock) Now() bn.Number
```

An alias for the `Time()` function. Returns the timestamp when the current block was created. The result is the number of seconds past the `1970-1-1 00:00:00`.

### 2.6 func NumTxs()

Function Prototype:

```go
func (IBlock) NumTxs() int32
```

Returns the number of transactions in the current block.

### 2.7 func DataHash()

Function Prototype:

```go
func (IBlock) DataHash() types.Hash
```

Returns the data hash of the current block.

### 2.8 func ProposerAddress()

Function Prototype:

```go
func (IBlock) ProposerAddress() types.Address
```

Returns the proposer address of the current block.

### 2.9 func RewardAddress()

Function Prototype:

```go
func (IBlock) RewardAddress() types.Address
```

Returns the reward address of the current block.

### 2.10 func RandomNumber()

Function Prototype:

```go
func (IBlock) RandomNumber() types.HexBytes
```

Returns the block random number of the current block.

### 2.11 func Version()

Function Prototype:

```go
func (IBlock) Version() string
```

Returns the software version when the current block proposer created the block.

### 2.12 func LastBlockHash()

Function Prototype:

```go
func (IBlock) LastBlockHash() types.Hash
```

Returns the block hash of the previous block.

### 2.13 func LastCommitHash()

Function Prototype:

```go
func (IBlock) LastCommitHash() types.Hash
```

Returns the commit hash of the previous block.

### 2.14 func LastAppHash()

Function Prototype:

```go
func (IBlock) LastAppHash() types.Hash
```

Returns the application hash of the previous block.

### 2.15 func LastFee()

Function Prototype:

```go
func (IBlock) LastFee() int64
```

Returns the handling fee (unit: `cong`) of the previous block.

## 3 sdk/ITx

The interface `sdk/ITx` encapsulates the transaction information that is called on the BCBChain blockchain.

### 3.1 func Note()

Function Prototype:

```go
func (ITx) Note() string
```

Returns the comment information of the current transaction.

### 3.2 func GasLimit()

Function Prototype:

```go
func (ITx) GasLimit() int64
```

Returns the max gas limit of the current transaction.

### 3.3 func GasLeft()

Function Prototype:

```go
func (ITx) GasLeft() int64
```

Returns the amount of gas remaining in the current transaction (the amount of gas required for the current smart contract call has been pre-deducted).

### 3.4 func Signer()

Function Prototype:

```go
func (ITx) Signer() IAccount
```

Returns the account object of the signer (initiator) for the current transaction.

### 3.5 func TxHash()

Function Prototype:

```go
func (ITx) TxHash() []byte
```

Returns a byte slice of the current transaction hash.

## 4 sdk/IMessage

The interface `sdk/IMessage` encapsulates all the information related to a single call to a smart contract method. In the same transaction, you can cascade multiple messages that are called for different smart contract methods.

### 4.1 func Contract()

Function Prototype:

```go
func (IMessage) Contract() types.Address
```

Returns the smart contract address called by the current message.

### 4.2 func MethodID()

Function Prototype:

```go
func (IMessage) MethodID() string
```

Returns the smart contract method ID (represented by a hex string) called by the current message.

### 4.3 func Items()

Function Prototype:

```go
func (IMessage) Items() []types.HexBytes
```

Returns the raw data of each parameter field called by the current message. When a cross-contract call occurs, the data obtained by `Items()` is `nil` inside the called contract.

### 4.4 func GasPrice()

Function Prototype:

```go
func (IMessage) GasPrice() int64
```

Returns the gas price (unit: `cong`) called by the current message.

### 4.5 func Sender()

Function Prototype:

```go
func (IMessage) Sender() IAccount
```

Returns the account object of the caller. If the call is made on the first level, the caller is the signer of the transaction. If the call is cross-contract, within the called contract, `Sender()` returns the contract account object that initiated the call.

### 4.6 func Payer()

Function Prototype:

```go
func (IMessage) Payer() IAccount
```

Returns the account object that pays the current message handling fee.

### 4.7 func Origins()

Function Prototype:

```go
func (IMessage) Origins() []types.Address
```

Returns the complete call chain of the message. If it is not a cross-contract call, `Origins()` returns an array containing the account address of the originator of the transaction. If it is a cross-contract call, `Origins()` returns the contract chain that represents the call. Within the called contract, the last address in the list of addresses returned by `Origins()` is the contract address of the contract that initiated the call.

### 4.8 func InputReceipts()

Function Prototype:

```go
func (IMessage) InputReceipts() []types.KVPair
```

When the cascading and cross-contract message is called, the receipt of the previous message call output will be used as the input of the next message call. This function returns the array of receipts entered into the current message call.

### 4.9 func GetTransferToMe()

Function Prototype:

```go
func (IMessage) GetTransferToMe() []*std.Transfer
```

Queries and returns all receipts that are transferred to the current smart contract in the receipt of the previous message call output, or `nil` if not found. The transfer receipt is defined as follows:

```go
package std

type Transfer struct {
 Token types.Address `json:"token"` // token address
 From  types.Address `json:"from"`  // account address of fund transferor
 To    types.Address `json:"to"`    // account address of receiver of funds
 Value bn.Number     `json:"value"` // transfer amount (unit: cong)
}
```

## 5 sdk/IAccount

The interface `sdk/IAccount` encapsulates the access interface to an account address.

### 5.1 func Address()

Function Prototype:

```go
func (IAccount) Address() types.Address
```

Returns the account address of the account object.

### 5.2 func PubKey()

Function Prototype:

```go
func (IAccount) PubKey() types.PubKey
```

Returns the public key data of the account object (may be empty).

### 5.3 func Balance()

Function Prototype:

```go
func (IAccount) Balance() bn.Number
```

In a token-issuing contract, the fund balance of the token-issuing sub-account issued by the object of the account is returned (unit: `cong`). In a non-token-issuing contract, it is return `0`.

### 5.4 func BalanceOfToken()

Function Prototype:

```go
func (IAccount) BalanceOfToken(token types.Address) bn.Number
```

Given the token address, return the fund balance (unit: `cong`) of the account object in the specified token sub-account. If the specified token address is not a token, the return balance is `0`.

### 5.5 func BalanceOfName()

Function Prototype:

```go
func (IAccount) BalanceOfName(name string) bn.Number
```

Given the token name, return the fund balance (unit: `cong`) of the account object in the specified token sub-account. If the specified token name is not a token, the return balance is `0`.

### 5.6 func BalanceOfSymbol()

Function Prototype:

```go
func (IAccount) BalanceOfSymbol(symbol string) bn.Number
```

Given the token symbol, return the fund balance (unit: `cong`) of the account object in the specified token sub-account. If the specified token symbol is not a token, the return balance is `0`.

### 5.7 func Transfer()

Function Prototype:

```go
func (IAccount) Transfer(to types.Address, value bn.Number)
```

In a token-issuing contract, transfers the funds of account object from token sub-account to the account designated in the parameter `to` (unit: `cong`), whereby the account object includes the account that initiated the message or the current contract account.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - The parameter to is not an address;
> - The parameter to is the same as the account address;
> - The parameter value is less than or equal to 0;
> - The balance of the account is insufficient to pay the transfer;
> - The current contract has not issued tokens (because the parameters of the function do not specify which token to transfer);
> - The current contract has issued tokens, but the account is neither the one that initiated the message call nor the contract account of the current smart contract.

### 5.8 func TransferWithNote()

Function Prototype:

```go
func (IAccount) TransferWithNote(to types.Address, value bn.Number, note string)
```

In the token contract, transfer the funds of the token sub-account of the account object issued in this contract to the account (funding unit: `cong`) with the receiving address `to`, and return the `note` information in the receipt. Here the account object includes the originator of the message call or the current contract account.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - Parameter to is not an address;
> - The parameter to is the same as the account address;
> - Parameter value is less than or equal to 0;
> - The balance of the account is not enough to pay the value;
> - If no tokens have been issued in the current contract (because the function does not specify which token to transfer);
> - If the current contract has issued tokens, the account is neither the initiator of the message call nor the contract account of the current smart contract.

### 5.9 func TransferWithNoteEx()

Function Prototype:

```go
func (IAccount) TransferWithNoteEx(to types.Address, value bn.Number, note string) types.Error
```

In the token contract, transfer the funds of the token sub-account of the account object issued in this contract to the account (funding unit: `cong`) with the receiving address `to`, and return the `note` information in the receipt. Here the account object includes the originator of the message call or the current contract account.

An error occurs if any of the following is met. When an error occurs, the error code and information are returned in the return value:

> - Parameter to is not an address;
> - The parameter to is the same as the account address;
> - Parameter value is less than or equal to 0;
> - The balance of the account is not enough to pay the value;
> - If no tokens have been issued in the current contract (because the function does not specify which token to transfer);
> - If the current contract has issued tokens, the account is neither the initiator of the message call nor the contract account of the current smart contract.

### 5.10 func TransferByToken()

Function Prototype:

```go
func (IAccount) TransferByToken(token types.Address, to types.Address, value bn.Number)
```

If the specified token address is the token issued by the contract, transfers the funds of account object from token sub-account to the account designated in the parameter `to` (unit: `cong`), whereby the account object includes the account that initiated the message or the current contract account.

If the specified token address is not the token issued by this contract, transfers the funds of account object from the specified token address to the account designated as `to` (unit: `cong`), whereby the account object can only be the current contract account.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - The parameter token is not an address;
> - The parameter token is not a token;
> - The parameter to is not an address;
> - The parameter to is the same as the account address;
> - The parameter value is less than or equal to 0;
> - The balance of the account is insufficient to pay the transfer;
> - If the current contract does not issue tokens, and the account is not the account of the current smart contract;
> - The current contract has issued tokens, but the account is neither the one that initiated the message call nor the contract account of the current smart contract.

### 5.11 func TransferByTokenWithNote()

Function Prototype:

```go
func (IAccount) TransferByTokenWithNote(token types.Address, to types.Address, value bn.Number, note string)
```

If the specified token address is the token issued by this contract, transfer the funds of the account's token sub-account issued by this contract to the account with the receiving address `to` (funding unit:`cong`) and `Note` information is returned in the receipt, where the account object includes the originator of the message call or the current contract account.

If the specified token address is not a token issued by this contract, transfer the funds of the specified token sub-account of the account object to the account (funding unit: `cong`) with the receiving address `to` and return it in the receipt note` information, here the account object can only be the current contract account.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - Parameter token is not an address;
> - Parameter token is not a token;
> - Parameter to is not an address;
> - The parameter to is the same as the account address;
> - Parameter value is less than or equal to 0;
> - The balance of the account is not enough to pay the value;
> - If the current contract has not issued tokens, the account is not the contract account of the current smart contract;
> - If the current contract has issued tokens, the account is not the sender of the message or the contract account of the current smart contract.

### 5.12 func TransferByName()

Function Prototype:

```go
func (IAccount) TransferByName(name string, to types.Address, value bn.Number)
```

If the designated token name is the token issued by the contract, transfers the funds of account object from token sub-account to the account designated in the parameter `to` (unit: `cong`), whereby the account object includes the account that initiated the message or the current contract account.

If the specified token address is not the token issued by this contract, transfers the funds of account object from the specified token address to the account designated as `to` (unit: `cong`), whereby the account object can only be the current contract account. .

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - The parameter name is not the name of a token;
> - The parameter to is not an address;
> - The parameter to is the same as the account address;
> - The parameter value is less than or equal to 0;
> - The balance of the account is insufficient to pay the transfer;
> - If the current contract does not issue tokens, and the account is not the account of current smart contract;
> - The current contract has issued tokens, but the account is neither the one that initiated the message call nor the contract account of the current smart contract.

### 5.13 func TransferByNameWithNote()

Function Prototype:

```go
func (IAccount) TransferByNameWithNote(name string, to types.Address, value bn.Number, note string)
```

If the specified token name is the token issued by this contract, transfer the funds of the account's token sub-account issued by this contract to the account with the receiving address `to` (fund unit:`cong`) `Note` information is returned in the receipt, where the account object includes the originator of the message call or the current contract account.

If the specified token address is not a token issued by this contract, transfer the funds of the specified token sub-account of the account object to the account (funding unit: `cong`) with the receiving address`to` and return it in the receipt note` information, here the account object can only be the current contract account.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - Parameter name is not the name of a token;
> - Parameter to is not an address;
> - The parameter to is the same as the account address;
> - Parameter value is less than or equal to 0;
> - The balance of the account is not enough to pay the value;
> - If the current contract has not issued tokens, the account is not the contract account of the current smart contract;
> - If the current contract has issued tokens, the account is not the sender of the message or the contract account of the current smart contract.

### 5.14 func TransferBySymbol()

Function Prototype:

```go
func (IAccount) TransferBySymbol(symbol string, to types.Address, value bn.Number)
```

If the designated token symbol is the token issued by the contract, transfers the funds of account object from token sub-account to the account designated in the parameter `to` (unit: `cong`), whereby the account object includes the account that initiated the message or the current contract account.

If the specified token symbol is not the token issued by this contract, transfers the funds of account object from the specified token address to the account designated as `to` (unit: `cong`), whereby the account object can only be the current contract account.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - The parameter symbol is not the symbol of a token;
> - The parameter to is not an address;
> - The parameter to is the same as the account address;
> - The parameter value is less than or equal to 0;
> - The balance of the account is insufficient to pay the transfer;
> - If the current contract does not issue tokens, and the account is not the account of current smart contract;
> - The current contract has issued tokens, but the account is neither the one that initiated the message call nor the contract account of the current smart contract.

### 5.15 func TransferBySymbolWithNote()

Function Prototype:

```go
func (IAccount) TransferBySymbolWithNote(symbol string, to types.Address, value bn.Number, note string)
```

If the designated token symbol is the token issued by this contract, transfer the funds of the account object's token sub-account issued in this contract to the account with the receiving address `to` (funding unit:`cong`) and `Note` information is returned in the receipt, where the account object includes the originator of the message call or the current contract account.

If the specified token address is not a token issued by this contract, transfer the funds of the specified token sub-account of the account object to the account (funding unit: `cong`) with the receiving address `to` and return it in the receipt note` information, here the account object can only be the current contract account.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - Parameter symbol is not a token symbol;
> - Parameter to is not an address
> - The parameter to is the same as the account address;
> - Parameter value is less than or equal to 0
> - The balance of the account is not enough to pay the value;
> - The current contract has not issued tokens, and the account is not the contract account of the current smart contract;
> - If the current contract has issued tokens, the account is not the sender of the message or the contract account of the current smart contract.

## 6 sdk/IContract

The interface `sdk/IContract` encapsulates all the information about a smart contract and the interface to operate it.

### 6.1 func Address()

Function Prototype:

```go
func (IContract) Address() types.Address
```

Returns the address of the smart contract.

### 6.2 func Account()

Function Prototype:

```go
func (IContract) Account() IAccount
```

Returns the account object of the smart contract.

The account address of the smart contract can be used to receive funds transferred to the contract. The calculation of the smart contract account address only requires the contract name and organization ID. The change in the address after the contract upgrades will not affect the address of the account. The contract account address does not contain a corresponding private key, so the funds in the contract account can only be changed through the contract.

### 6.3 func Owner()

Function Prototype:

```go
func (IContract) Owner() IAccount
```

Returns the external account object of the owner of the smart contract (the external account address has a corresponding private key).

### 6.4 func Name()

Function Prototype:

```go
func (IContract) Name() string
```

Returns the smart contract name.

### 6.5 func Version()

Function Prototype:

```go
func (IContract) Version() string
```

Returns the smart contract version number.

### 6.6 func CodeHash()

Function Prototype:

```go
func (IContract) CodeHash() types.Hash
```

Returns the hash corresponding to the smart contract code.

### 6.7 func EffectHeight()

Function Prototype:

```go
func (IContract) EffectHeight() int64
```

Returns the block height at which the smart contract begins to take effect.

### 6.8 func LoseHeight()

Function Prototype:

```go
func (IContract) LoseHeight() int64
```

Returns the block height at which the smart contract begins to fail, with 0 indicating no failure.

### 6.9 func KeyPrefix()

Function Prototype:

```go
func (IContract) KeyPrefix() string
```

Returns the prefix of the state database KEY value (in the format `/xxx/yyy`) that can be accessed in the smart contract, which can be used to separate the data between smart contracts.

### 6.10 func Methods()

Function Prototype:

```go
func (IContract) Methods() []std.Method
```

Returns the details of all public methods of the smart contract (can be used to call the contract for cascading messages). The `std.Method` structure is defined as follows:

```go
package std

type Method struct {
    MethodID    string    // method id
    Gas         int64     // gas required to call the method
    ProtoType   string    // method prototype
}
```

### 6.11 func Interfaces()

Function Prototype:

```go
func (IContract) Interfaces() []std.Method
```

Returns the details of all public interfaces of the smart contract that can be used to make cross-contract calls.

### 6.12 func IBCs()

Function Prototype:

```go
func (IContract) IBCs() []std.Method
```

Returns all public cross-chain methods of smart contracts (Can be used to perform cross-chain business) details.

### 6.13 func Mine()

Function Prototype:

```go
func (IContract) Mine() []std.Method
```

Returns the details of the mining interface exposed by the smart contract.

### 6.14 func Token()

Function Prototype:

```go
func (IContract) Token() types.Address
```

Returns the token address registered by the smart contract. If the contract has not registered a token, it returns an empty address.

### 6.15 func OrgID()

Function Prototype:

```go
func (IContract) OrgID() string
```

Returns the organization ID of the smart contract.

### 6.16 func ChainVersion()

Function Prototype:

```go
func (IContract) ChainVersion() string
```

Returns the chain version of the smart contract.

### 6.17 func SetOwner()

Function Prototype:

```go
func (IContract) SetOwner( newOwner types.Address)
```

Sets the new owner of the smart contract. `newOwner` is the external account address of the new owner of the smart contract. The function `SetOwner()` can only be called by the original owner of the smart contract. If the smart contract issues a token, the operation will also set the token owner to the new owner.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - The message caller is not the original owner of the contract;
> - The parameter newOwner is not an address;
> - The parameter newOwner is the original owner of the contract;
> - The parameter newOwner is the address of the contract;
> - The parameter newOwner is the account address of the contract.

## 7 sdk/IToken

The interface `sdk/IToken` encapsulates all the information of a token and the interface for operating the token.

### 7.1 func Address()

Function Prototype:

```go
func (IToken) Address() types.Address
```

Returns the address of the token.

### 7.2 func Owner()

Function Prototype:

```go
func (IToken) Owner() IAccount
```

Returns the external account object of the token owner.

### 7.3 func Name()

Function Prototype:

```go
func (IToken) Name() string
```

Returns the name of the token.

### 7.4 func Symbol()

Function Prototype:

```go
func (IToken) Symbol() string
```

Returns the symbol of the token.

### 7.5 func TotalSupply()

Function Prototype:

```go
func (IToken) TotalSupply() Number
```

Returns the total supply of the token (unit: `cong`).

### 7.6 func AddSupplyEnabled()

Function Prototype:

```go
func (IToken) AddSupplyEnabled() bool
```

Return whether additional issuance of tokens is allowed.

### 7.7 func BurnEnabled()

Function Prototype:

```go
func (IToken) BurnEnabled() bool
```

Return whether burned of tokens is allowed.

### 7.8 func GasPrice()

Function Prototype:

```go
func (IToken) GasPrice() int64
```

Returns the gas price of the token (unit: `cong`).

### 7.9 func SetTotalSupply()

Function Prototype:

```go
func (IToken) SetTotalSupply(newTotalSupply bn.Number)
```

Sets the new total supply of tokens. `newTotalSupply` is the new total supply of tokens (unit: `cong`), and updates the balance of the contract owner on the token sub-account.

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - The message caller is not the owner of the contract;
> - The parameter newTotalSupply is less than 1000000000(cong);
> - The parameter newTotalSupply is greater than the original supply, but additional issuance of tokens is not allowed;
> - The parameter newTotalSupply is less than the original supply, but the tokens are not allowed to burn;
> - The balance of the contract owner on the token sub-account will be less than 0 after the update.

### 7.10 func SetGasPrice()

Function Prototype:

```go
func (IToken) SetGasPrice(newGasPrice int64)
```

Sets the gas price of the token. `newGasPrice` is the new gas price for the token (unit: `cong`).

An exception occurs when any of the following is satisfied. When an exception occurs, the SDK will automatically triggered a `panic`:

> - The message caller is not the owner of the contract;
> - The parameter newGasPrice is greater than 1000000000(cong);
> - The parameter newGasPrice is less than the base gas price.

## 8 sdk/IHelper

The interface `sdk/IHelper` encapsulates all the help objects of the SDK.

### 8.1 func AccountHelper()

Function Prototype:

```go
func (IHelper) AccountHelper() IAccountHelper
```

Returns the account helper object of the account.

### 8.2 func BlockchainHelper()

Function Prototype:

```go
func (IHelper) BlockChainHelper() IBlockChainHelper
```

Returns the helper object related to the blockchain.

### 8.3 func BuildHelper()

Function Prototype:

```go
func (IHelper) BuildHelper() IBuildHelper
```

Returns the helper object related to the contract building.

### 8.4 func ContractHelper()

Function Prototype:

```go
func (IHelper) ContractHelper() IContractHelper
```

Returns the helper object related to the smart contract.

### 8.5 func GenesisHelper()

Function Prototype:

```go
func (IHelper) GenesisHelper() IGenesisHelper
```

Return to the helper object related to genesis of blockchain.

### 8.6 func ReceiptHelper()

Function Prototype:

```go
func (IHelper) ReceiptHelper() IReceiptHelper
```

Returns the helper object related to the receipt.

### 8.7 func TokenHelper()

Function Prototype:

```go
func (IHelper) TokenHelper() ITokenHelper
```

Returns the helper object related to the token.

### 8.8 func StateHelper()

Function Prototype:

```go
func (IHelper) StateHelper() IStateHelper
```

Returns the helper object related to the state storage.

### 8.9 func IBCHelper()

Function Prototype:

```go
func (IHelper) IBCHelper() IIBCHelper
```

Returns the help object related to initiating cross-chain.

### 8.10 func IBCStubHelper()

Function Prototype:

```go
func (IHelper) IBCStubHelper() IIBCStubHelper
```

Returns help objects related to handling cross-chain transactions.

## 9 sdk/IAccountHelper

The interface `sdk/IAccountHelper` encapsulates help objects for accessing accounts on blockchain .

### 9.1 func AccountOf()

Function Prototype:

```go
func (IAccountHelper) AccountOf(addr types.Address) IAccount
```

Uses the address of the account to generate an account object, for the purpose of performing some operations on the account. `Addr` is the account address. Returns the created account object.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - The parameter addr is not an address.

### 9.2 func AccountOfPubKey()

Function Prototype:

```go
func (IAccountHelper) AccountOfPubKey(pubkey types.PubKey) IAccount
```

Uses the public key of the account to generate an account object, for the purpose of performing some operations on the account. `pubkey` is the account’s public key. Returns the created account object.

An error occurs when any of the following is satisfied, and `nil` will returned:

> - The parameter pubkey is not a public key (the length is not equal to 32 bytes).

## 10 sdk/IBlockChainHelper

The interface `sdk/IBlockChainHelper` encapsulates help objects for accessing the blockchain.

### 10.1 func IsPeerChainAddress()

Function Prototype:

```go
func (IBlockchainHelper) IsPeerChainAddress(address types.Address) bool
```

Determines whether the given address `address` is an external link address. If yes, it returns true, if not, returns false.

If any of the following conditions is met, an exception occurs. When an exception occurs, the SDK will automatically trigger the `panic`:

> The parameter address is not a valid address format.

### 10.2 func IsSideChain()

Function Prototype:

```go
func (IBlockchainHelper) IsSideChain() bool
```

Determine whether the current chain is a side chain. It returns true if it is not, otherwise it returns false.

### 10.3 func CalcSideChainID()

Function Prototype:

```go
func (IBlockchainHelper) CalcSideChainID(chainName string) string
```

Calculate the chain ID based on the chain name. `chainName` is the name of the chain. Returns the calculated chain ID.

If any of the following conditions is met, an exception occurs. When an exception occurs, the SDK will automatically trigger the `panic`:

> - The parameter chainName is not a valid chain name format.

### 10.4 func CalcAccountFromPubkey()

Function Prototype:

```go
func (IBlockchainHelper) CalcAccountFromPubkey(pubkey types.PubKey) types.Address
```

Calculates and returns the account address using the public key. `pubkey` is the public key.

An error occurs if any of the following is satisfied, and an empty address will be returned:

> The parameter pubkey is not a public key (the length is not equal to 32 bytes).

### 10.5 func CalcAccountFromName()

Function Prototype:

```go
func (IBlockchainHelper) CalcAccountFromName(name string, orgID string) types.Address
```

Calculates and returns account address of the contract using the contract name and its organization ID. `name` is the contract name and `orgID` is the organization ID.

### 10.6 func CalcContractAddress()

Function Prototype:

```go
func (IBlockchainHelper) CalcContractAddress(
    name string,
    version string,
    orgID string) types.Address
```

Calculates and returns the contract address based on the given contract parameters. `name` is the contract name. `version` is the contract version. `orgID` is the organization ID to which the contract belongs.

### 10.7 func RecalcAddress()

Function Prototype:

```go
func (IBlockchainHelper) RecalcAddress(
    address types.Address,
    chainID string) types.Address
```

Calculates a new address based on the given address parameters. `address` is the old address to be derived for the new address. `chainID` is the prefix chain ID of the new address. Returns the calculated address.

If any of the following conditions is met, an exception occurs. When an exception occurs, the SDK will automatically trigger the `panic`:

> The parameter address is not a valid address format.

### 10.8 func CalcOrgID()

Function Prototype:

```go
func CalcOrgID(name string) string
```

Calculates and returns the organization ID is calculated based on the organization name. `name` is the organization name.

### 10.9 func CheckAddress()

Function Prototype:

```go
func (IBlockchainHelper) CheckAddress(addr types.Address) error
```

Validates the address format. `addr` is the address. Returns `nil` if the validation is successful.

### 10.10 func CheckAddressEx()

Function Prototype:

```go
func (IBlockchainHelper) CheckAddressEx(chainID string, addr types.Address) error
```

Check the validity of the address format. `chainID` is the chain ID, and the address must be prefixed with the chain ID. `addr` is the address. Successfully returns `nil`.

### 10.11 func GetBlock()

Function Prototype:

```go
func (IBlockChainHelper) GetBlock(height int64) IBlock
```

Returns the block information of the `height` specified. height is the specified block height. If the input height is less than or equal to 0, `nil` is returned. If there is no block information for the specified height, or the block information is abnormal, a generic block information object with all other parameters as null is returned.

### 10.12 func GetChainID()

Function Prototype:

```go
func (IBlockChainHelper) GetChainID(address types.Address) string
```

Extract the chain ID from the address information and return.

If any of the following conditions is met, an exception occurs. When an exception occurs, the SDK will automatically trigger the `panic`:

> The parameter address is not a valid address format.

### 10.12 func GetMainChainID()

Function Prototype:

```go
func (IBlockChainHelper) GetMainChainID() string
```

Get the main chain ID from the current chain ID and return.

### 10.13 func FormatTime()

Function Prototype:

```go
func (IBlockChainHelper) FormatTime(seconds int64, layout string) string
```

Formats the output time string based on the time in seconds. `seconds` is the time in seconds. `layout` is a formatted string. Returns the formatted time.

### 10.14 func ParseTime()

Function Prototype:

```go
func (IBlockChainHelper) ParseTime(layout, value string) (int64, error)
```

Formats a string according to time, and performs format parsing on a given time value. `layout` is a formatted string. `value` is the time value. Returns the number of seconds or error message corresponding to the time value.

If any of the following conditions is met, an error occurs. When an error occurs, an empty address is returned:

> Parameter value is not in the format specified by layout.

## 11 sdk/IBuildHelper

The interface `sdk/IBuildHelper` encapsulates help objects for building smart contracts.

### 11.1 func Build()

Function Prototype:

```go
func (IBuildHelper) Build(meta std.ContractMeta) std.BuildResult
```

Build a contract.
`meta` is the contract metadata entered, and the `std.ContractMeta` structure is defined as follows:

```go
package std

type ContractMeta struct {
      Name         string           //Contract name
      ContractAddr types.Address    //Contract address
      OrgID        string           //The organization ID to which the contract belongs
      Version      string           //Contract version
      EffectHeight int64            //Block height when the contract begins to take effect
      LoseHeight   int64            //Height at which the block fails (Fixed at 0)
      CodeData     []byte           //Contract code compression package data
      CodeHash     []byte           //Contract code hash
      CodeDevSig   []byte           //Contract developer's signature data for the contract
                                    //code compression package
      CodeOrgSig   []byte           //The signature data of the organization's signature on
                                    //the contract developer
}
```

Returns the details of the build results. The `std.BuildResult` structure is defined as follows:

```go
package std

type Method struct {
    MethodID     string        //Method ID, method ID calculation is based on method prototype
    Gas          int64         //Gas to be burnt when calling the method
    ProtoType    string        //Method prototype
}

type BuildResult struct {
    Code         uint32
    Error        string
    Methods      []Method      //Public method list
    Interfaces   []Method      //Public interface list
    Mine         []Method      //Public mining interface
    OrgCodeHash  []byte        //All valid contract codes in the organization (program names after compilation)
}
```

Any of the below will cause a failure and return `BuildResult.Code != types.CodeOK (200)`:

> - The current contract is not a contract management contract;
> - The organization to which the current contract belongs is not a genesis organization;
> - The contract compilation process failed.

## 12 sdk/IContractHelper

The interface sdk/IContractHelper encapsulates help objects for accessing smart contracts.

### 12.1 func ContractOfAddress()

Function Prototype:

```go
func (IContractHelper) ContractOfAddress(addr types.Address) IContract
```

Constructs a contract object based on the contract address and reads in the contract information, with the purpose of performing some operations on the contract. `addr` is the contract address. Returns the contract object.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - The parameter addr is not an address;
> - The parameter addr is not a contract.

### 12.2 func ContractOfToken()

Function Prototype:

```go
func (IContractHelper) ContractOfToken(tokenAddr types.Address) IContract
```

Constructs a contract object based on the token address and reads in the current effective version of the contract information, with the purpose of performing some operations on the contract. `tokenAddr` is the token address. Returns the contract object.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - The parameter tokenAddr is not an address;
> - The parameter tokenAddr is not a token.

### 12.3 func ContractOfName()

Function Prototype:

```go
func (IContractHelper) ContractOfName(name string) IContract
```

Constructs a contract object based on the contract name and reads in the contract information with the purpose of performing some operations on the contract. name is the contract `name`. Returns the contract object.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - The parameter name is an empty string;
> - The parameter name is not a contract.

## 13 sdk/IReceiptHelper

The interface `sdk/IReceiptHelper` encapsulates help objects for processing receipts.

### 13.1 func Emit()

Function Prototype:

```go
func (IReceiptHelper) Emit(interface Interface{})
```

Sends a receipt. The underlying implementation of the SDK will automatically serialize the incoming receipt object as a member of the output receipt that is set for this call contract. `interface` is the receipt object.

The SDK helper will automatically call the `Emit()` function with the relevant code generated by the smart contract definition, so it need not be called manually. An example is as follows:

```go
//@:public:receipt
type receipt interface {
    emitTransferMyCoin(token, from, to types.Address, value bn.Number)
}

func (mc *Mycoin) Transfer(to types.Address, value bn.Number) {
    .
    .
    .
    mc.emitTransferMyCoin(
        mc.sdk.Message().Contract().Address(),
        sender,
        receiver,
        value,
    )
}
```

## 14 sdk/IGenesisHelper

The interface `sdk/IGenesisHelper` encapsulates helper objects for accessing information at the time of creation.

### 14.1 func ChainID()

Function Prototype:

```go
func (IGenesisHelper) ChainID() string
```

Return to the block chain ID specified at the time of genesis.

### 14.2 func OrgID()

Function Prototype:

```go
func (IGenesisHelper) OrgID() string

```

Returns the genesis organization ID specified at the time of genesis.

### 14.3 func Contracts()

Function Prototype:

```go
func (IGenesisHelper) Contracts() []IContract
```

Return to the list of smart contract objects deployed at the time of genesis.

### 14.4 func Token()

Function Prototype:

```go
func (IGenesisHelper) Token() IToken
```

Returns the genesis Token object specified at the time of genesis.

### 14.5 func GasPriceRatio()

Function Prototype:

```go
func (IGenesisHelper) GasPriceRatio() uint64
```

Returns the fuel price ratio value specified at the time of creation. The default value is 1000 (unit: ‰).

## 15 sdk/ITokenHelper

The interface `sdk/ITokenHelper` encapsulates helper objects for accessing BRC20 standard tokens.

### 15.1 func RegisterToken()

Function Prototype:

```go
func (ITokenHelper) RegisterToken(name string,
                                  symbol string,
                                  totalSupply Number,
                                  addSupplyEnabled bool,
                                  burnEnabled bool) IToken
```

Registers a BRC20 standard token on the BCBChain blockchain. `name` is the token name, `symbol` is the token symbol, totalSupply is the total supply (unit: `cong`), `addSupplyEnabled` is whether the additional supply is allowed, and `burnEnabled` is whether the burn is allowed. The registration successfully returns the corresponding token object.

If any of the following is satisfied, the registration fails and returns `nil`:

> - The initiator of the message call is not the owner of the contract;
> - The length of the parameter name is not in the range of [3,40];
> - The token corresponding to the parameter name already exists;
> - The length of the parameter symbol is not in the range of [3,20];
> - The token corresponding to the parameter symbol already exists;
> - The parameter totalSupply is less than 1000000000(cong);
> - The contract has previously registered a BRC20 standard token;
> - The current contract does not define a standard transfer method or standard transfer interface.

### 15.2 func Token()

Function Prototype:

```go
func (ITokenHelper) Token() IToken
```

Returns the token information object that is registered in the current contract, for the purpose of performing some operations on the token.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - There is no registered token in the current contract

### 15.3 func TokenOfAddress()

Function Prototype:

```go
func (ITokenHelper) TokenOfAddress(tokenAddr types.Address) IToken
```

Returns the token object that is fetched based on the token address provided, for the purpose of performing some operations on the token. `tokenAddr` is the token address.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - The parameter tokenAddr is not an address;
> - The parameter tokenAddr is not a token.

### 15.4 func TokenOfName()

Function Prototype:

```go
func (ITokenHelper) TokenOfName(name string) IToken
```

Returns the token object that is fetched based on the token name provided, for the purpose of performing some operations on the token. name is the `name` of the token.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - The parameter name is not the name of a token.

### 15.5 func TokenOfSymbol()

Function Prototype:

```go
func (ITokenHelper) TokenOfSymbol(symbol string) IToken
```

Returns the token object that is fetched based on the token symbol provided, for the purpose of performing some operations on the token. `symbol` is the token symbol.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - The parameter symbol is not a token of a token.

### 15.6 func TokenOfContract()

Function Prototype:

```go
func (ITokenHelper) TokenOfContract(contractAddr types.Address) IToken
```

Returns the token object that is fetched based on the contract address provided, for the purpose of performing some operations on the token. `contractAddr` is the contract address.

An error occurs when any of the following is satisfied, and `nil` will be returned:

> - The parameter contractAddr is not an address;
> - The parameter contractAddr is not a contract;
> - The contract corresponding to the contractAddr has no registered tokens.

### 15.7 func BaseGasPrice()

Function Prototype:

```go
func (ITokenHelper) BaseGasPrice() int64
```

Returns the base gas price (unit: `cong`).

### 15.7 func CheckActivate()

Function Prototype:

```go
func (ITokenHelper) CheckActivate(address types.Address) error
```

Determine whether the side chain corresponding to the specified address has activated the current contract token. `address` is a general account address. Activated to return `nil`.

If any of the following conditions is met, an exception occurs. When an exception occurs, the SDK will automatically trigger the `panic`:

> The parameter address is not a valid address format.

If any of the following conditions is met, an error occurs. When an error occurs, the corresponding error object is returned:

> - The current contract does not issue tokens, and an error message is returned: this contract not exist token;
> - Corresponding side chain has not activated the token corresponding to the current contract, and returns an error message: chain: *chainName* never activate current token;

## 16 sdk/IStateHelper

The interface `sdk/IStateHelper` encapsulates help objects that access the state storage.

### 16.1 func Check()

Function Prototype:

```go
func (IStateHelper) Check(key string) bool
```

Validates if the provided KEY value exists within the permissible scope of the smart contract. `key` is the KEY value.

### 16.2 func Get()

Function Prototype:

```go
func (IStateHelper) Get(key string, defaultData Interface{}) Interface{}
func (IStateHelper) GetEx(key string, defaultData Interface{}) Interface{}
```

Fetches data from the permissible scope of the smart contract using the provided KEY value and returns it. `key` is the KEY value, and `defaultData` is a template or default for the data type of the storage object. If the data does not exist, `Get()` returns `nil`, and `GetEx()` returns the default value.

Here are some simple read functions for the underlying type package:

```go
func (IStateHelper) GetInt(key string) int
func (IStateHelper) GetInt8(key string) int8
func (IStateHelper) GetInt16(key string) int16
func (IStateHelper) GetInt32(key string) int32
func (IStateHelper) GetInt64(key string) int64
func (IStateHelper) GetUint(key string) uint
func (IStateHelper) GetUint8(key string) uint8
func (IStateHelper) GetUint16(key string) uint16
func (IStateHelper) GetUint32(key string) uint32
func (IStateHelper) GetUint64(key string) uint64
func (IStateHelper) GetByte(key string) byte
func (IStateHelper) GetBool(key string) bool
func (IStateHelper) GetString(key string) string

func (IStateHelper) GetInts(key string) []int
func (IStateHelper) GetInt8s(key string) []int8
func (IStateHelper) GetInt16s(key string) []int16
func (IStateHelper) GetInt32s(key string) []int32
func (IStateHelper) GetInt64s(key string) []int64
func (IStateHelper) GetUints(key string) []uint
func (IStateHelper) GetUint8s(key string) []uint8
func (IStateHelper) GetUint16s(key string) []uint16
func (IStateHelper) GetUint32s(key string) []uint32
func (IStateHelper) GetUint64s(key string) []uint64
func (IStateHelper) GetBytes(key string) []byte
func (IStateHelper) GetBools(key string) []bool
func (IStateHelper) GetStrings(key string) []string
```

If the above function does not read the data from the state database, it directly returns the default value of the corresponding type.

### 16.3 func Set()

Function Prototype:

```go
func (IStateHelper) Set(key string, data Interface{})
```

Sets the data object based on the KEY value allowed by the state database in the smart contract. `key` is the KEY value and data is the data object to be saved.

Here are some easy setup functions for the underlying type package:

```go
func (IStateHelper) SetInt(key string, v int)
func (IStateHelper) SetInt8(key string, v int8)
func (IStateHelper) SetInt16(key string, v int16)
func (IStateHelper) SetInt32(key string, v int32)
func (IStateHelper) SetInt64(key string, v int64)
func (IStateHelper) SetUint(key string, v uint)
func (IStateHelper) SetUint8(key string, v uint8)
func (IStateHelper) SetUint16(key string, v uint16)
func (IStateHelper) SetUint32(key string, v uint32)
func (IStateHelper) SetUint64(key string, v uint64)
func (IStateHelper) SetByte(key string, v byte)
func (IStateHelper) SetBool(key string, v bool)
func (IStateHelper) SetString(key string, v string)

func (IStateHelper) SetInts( key string, v []int )
func (IStateHelper) SetInt8s( key string, v []int8 )
func (IStateHelper) SetInt16s( key string, v []int16 )
func (IStateHelper) SetInt32s( key string, v []int32 )
func (IStateHelper) SetInt64s( key string, v []int64 )
func (IStateHelper) SetUints( key string, v []uint )
func (IStateHelper) SetUint8s( key string, v []uint8 )
func (IStateHelper) SetUint16s( key string, v []uint16 )
func (IStateHelper) SetUint32s( key string, v []uint32 )
func (IStateHelper) SetUint64s( key string, v []uint64 )
func (IStateHelper) SetBytes(key string, v []byte)
func (IStateHelper) SetBools( key string, v []bool )
func (IStateHelper) SetStrings( key string, v []string )
```

Sets the data object based on the KEY value allowed by the state database in the smart contract. `key` is the KEY value and `v` is the base type data value.

### 16.4 func Delete()

Function Prototype:

```go
func (IStateHelper) Delete(key string)
```

Delete the data corresponding to the `key` value in the state database.

### 16.5 func Flush()

Function Prototype:

```go
func (IStateHelper) Flush()
```

The update to the state database is flushed to the database layer without committing the transaction.

### 16.6 func McCheck()

Function Prototype:

```go
func (sh *StateHelper) McCheck(key string) bool
```

Checks if there is data specified by the KEY value within the permissible scope of the smart contract, including the cache and the database. `key` is the KEY, and value will be automatically loaded into the cache if it exists.

### 16.7 func McGet()

Function Prototype:

```go
func (IStateHelper) McGet(key string, defaultData Interface{}) Interface{}
func (IStateHelper) McGetEx(key string, defaultData Interface{}) Interface{}
```

Given the KEY value, the data is read within the permissible scope of the smart contract, and cached in the memory. This makes it possible to directly read from the memory in the call message of the subsequent smart contract without accessing the database. `key` is the KEY value, and `defaultData` is a template or default for the data type of the storage object. If the data does not exist, `McGet()` returns `nil`, and `McGetEx()` returns the default value.

Here are some simple read functions for the underlying type package:

```go
func (IStateHelper) McGetInt(key string) int
func (IStateHelper) McGetInt8(key string) int8
func (IStateHelper) McGetInt16(key string) int16
func (IStateHelper) McGetInt32(key string) int32
func (IStateHelper) McGetInt64(key string) int64
func (IStateHelper) McGetUint(key string) uint
func (IStateHelper) McGetUint8(key string) uint8
func (IStateHelper) McGetUint16(key string) uint16
func (IStateHelper) McGetUint32(key string) uint32
func (IStateHelper) McGetUint64(key string) uint64
func (IStateHelper) McGetByte(key string) byte
func (IStateHelper) McGetBool(key string) bool
func (IStateHelper) McGetString(key string) string

func (IStateHelper) McGetInts(key string) []int
func (IStateHelper) McGetInt8s(key string) []int8
func (IStateHelper) McGetInt16s(key string) []int16
func (IStateHelper) McGetInt32s(key string) []int32
func (IStateHelper) McGetInt64s(key string) []int64
func (IStateHelper) McGetUints(key string) []uint
func (IStateHelper) McGetUint8s(key string) []uint8
func (IStateHelper) McGetUint16s(key string) []uint16
func (IStateHelper) McGetUint32s(key string) []uint32
func (IStateHelper) McGetUint64s(key string) []uint64
func (IStateHelper) McGetBytes(key string) []byte
func (IStateHelper) McGetBools(key string) []bool
func (IStateHelper) McGetStrings(key string) []string
```

If the above function does not read the data from the state database, it directly returns the default value of the corresponding type.

### 16.8 func McSet()

Function Prototype:

```go
func (IStateHelper) McSet(key string, data Interface{})
```

Sets the data object based on the KEY value allowed by the state database smart contract, and updates it in the memory cache. This makes it possible to read directly from the memory in the call message of the subsequent smart contract without having to access the database. `key` is the KEY value and `data` is the data object to be saved.

Here are some easy setup functions for the underlying type package:

```go
func (IStateHelper) McSetInt(key string, v int)
func (IStateHelper) McSetInt8(key string, v int8)
func (IStateHelper) McSetInt16(key string, v int16)
func (IStateHelper) McSetInt32(key string, v int32)
func (IStateHelper) McSetInt64(key string, v int64)
func (IStateHelper) McSetUint(key string, v uint)
func (IStateHelper) McSetUint8(key string, v uint8)
func (IStateHelper) McSetUint16(key string, v uint16)
func (IStateHelper) McSetUint32(key string, v uint32)
func (IStateHelper) McSetUint64(key string, v uint64)
func (IStateHelper) McSetByte(key string, v byte)
func (IStateHelper) McSetBool(key string, v bool)
func (IStateHelper) McSetString(key string, v string)

func (IStateHelper) McSetInts( key string, v []int )
func (IStateHelper) McSetInt8s( key string, v []int8 )
func (IStateHelper) McSetInt16s( key string, v []int16 )
func (IStateHelper) McSetInt32s( key string, v []int32 )
func (IStateHelper) McSetInt64s( key string, v []int64 )
func (IStateHelper) McSetUints( key string, v []uint )
func (IStateHelper) McSetUint8s( key string, v []uint8 )
func (IStateHelper) McSetUint16s( key string, v []uint16 )
func (IStateHelper) McSetUint32s( key string, v []uint32 )
func (IStateHelper) McSetUint64s( key string, v []uint64 )
func (IStateHelper) McSetBytes(key string, v []byte)
func (IStateHelper) McSetBools( key string, v []bool )
func (IStateHelper) McSetStrings( key string, v []string )
```

Sets the data object based on the KEY value allowed by the state database smart contract, and updates it in the memory cache. This makes it possible to read directly from the memory in the call message of the subsequent smart contract without having to access the database. `key` is the KEY value and `v` is the base type data value.

### 16.9 func McClear()

Function Prototype:

```go
func (IStateHelper) McClear(key string)
```

Clears the data specified in the in-memory cache (retain the data in the state database). `key` is the KEY value.

### 16.10 func McDelete()

Function Prototype:

```go
func (IStateHelper) McDelete(key string)
```

The data corresponding to the `key` value is deleted in the state database, and the data corresponding to the `key` value is cleared from the cache.

## 17 sdk/IIBCHelper

The interface `sdk / IIBCHelper` encapsulates a helper object that initiates cross-chain transactions or notifications.

### 17.1 func IbcHash()

Function Prototype:

```go
func (IIBCHelper) IbcHash(toChainID string) types.Hash
```

Calculate the cross-chain transaction hash based on the target chain ID, the current chain ID, and the current transaction hash. `toChainID` is the target chain ID.

### 17.2 func Run()

Function Prototype:

```go
func (IIBCHelper) Run(f func()) IIBCHelper
```

Execute the code snippet that needs to generate a cross-chain receipt, and return the current object. `f` is a function that encapsulates a code segment.

### 17.3 func Register()

Function Prototype:

```go
func (IIBCHelper) Register(toChainID string)
```

Register for cross-chain transactions. `toChainID` is the target chain ID value.

An exception is generated when any of the following conditions is met. When an exception occurs, the SDK will automatically trigger a `panic`:

> - The contract interface that called the interface was called across contracts.
> - The chain has not deployed an IBC contract or the IBC contract has not taken effect.
> - IBC contract transaction registration interface processing produced an error.

### 17.4 func Notify()

Function Prototype:

```go
func (IIBCHelper) Notify(toChainIDs []string)
```

Initiate cross-chain notification. `toChainIDs` is the value of the target chain ID list.

An exception is generated when any of the following conditions is met. When an exception occurs, the SDK will automatically trigger a `panic`:

> - The contract interface that called the interface was called across contracts.
> - All elements in the target chain ID list are invalid chain IDs.
> - The chain has not deployed an IBC contract or the IBC contract has not taken effect.
> - IBC contract transaction registration interface processing produced an error.

### 17.5 func Broadcast()

Function Prototype:

```go
func (IIBCHelper) Broadcast() types.Hash
```

Initiate cross-chain broadcasting.

An exception is generated when any of the following conditions is met. When an exception occurs, the SDK will automatically trigger a `panic`:

> - The contract interface that called the interface was called across contracts.
> - The chain has not deployed an IBC contract or the IBC contract has not taken effect.
> - IBC contract transaction registration interface processing produced an error.

### 17.6 func CalcBlockHash()

Function Prototype:

```go
func (IIBCHelper) CalcBlockHash(h *ibc.Header) types.Hash
```

Calculate block hash based on block header. `h` is the block header object.

An exception is generated when any of the following conditions is met. When an exception occurs, the SDK will automatically trigger a `panic`:

> - The block header object is nil.
> - The time string in the block header is not in the correct format.

### 17.7 func CalcQueueHash()

Function Prototype:

```go
func (IIBCHelper) CalcQueueHash(packet ibc.Packet, lastQueueHash types.Hash) types.Hash
```

Calculate the current node hash of the queue based on the message data and the previous queue hash. `packet` is the current message value. `lastQueueHash` is the last Hash queue node.

### 17.8 func VerifyPrecommit()

Function Prototype:

```go
func (IIBCHelper) VerifyPrecommit(
    pubKey types.PubKey,
    precommit ibc.Precommit,
    chainID string,
    height int64) bool
```

Verify block proof data. `pubKey` is the public key value of the initiating chain verifier node. `precommit` Voting data for the initiating chain validator node. `chainID` is the originating chain ID. `height` The block height of the initiation chain to initiate cross-chain transaction proof data.

An exception is generated when any of the following conditions is met. When an exception occurs, the SDK will automatically trigger a `panic`:

> - The time string in the voting information is not in the correct format.

## 18 sdk/IIBCStubHelper

The interface `sdk / IIBCStubHelper` encapsulates a helper object that handles cross-chain transactions. In theory, this object is not needed in the contract.

### 18.1 func Recast()

Function Prototype:

```go
func Recast(ibcHash types.HexBytes,
    orgID, contractName string,
    receipts []types.KVPair) (bool, []types.KVPair, types.Error)
```

Asset recast interface. `ibcHash` is the hash value of the cross-chain transaction. `orgID` is the organization to which the application contract belongs. `contractName` is the application contract name. `receipts` is the cross-chain receipt information.

### 18.2 func Confirm()

Function Prototype:

```go
func Confirm(ibcHash types.HexBytes,
    orgID, contractName string,
    receipts []types.KVPair) ([]types.KVPair, types.Error)
```

Cross-chain transaction confirmation interface. `ibcHash` is the hash value of the cross-chain transaction. `orgID` is the organization to which the application contract belongs. `contractName` is the application contract name. `receipts` is the cross-chain receipt information.

### 18.3 func Cancel()

Function Prototype:

```go
func Cancel(ibcHash types.HexBytes,
    orgID, contractName string,
    receipts []types.KVPair) ([]types.KVPair, types.Error)
```

Cross-chain transaction cancellation interface. `ibcHash` is the hash value of the cross-chain transaction. `orgID` is the organization to which the application contract belongs. `contractName` is the application contract name. `receipts` is the cross-chain receipt information.

### 18.4 func TryRecast()

Function Prototype:

```go
func TryRecast(ibcHash types.HexBytes,
    orgID, contractName string,
    receipts []types.KVPair) (bool, []types.KVPair, types.Error)
```

Cross-chain asset pre-recast interface. `ibcHash` is the hash value of the cross-chain transaction. `orgID` is the organization to which the application contract belongs. `contractName` is the application contract name. `receipts` is the cross-chain receipt information.

### 18.5 func ConfirmRecast()

Function Prototype:

```go
func ConfirmRecast(ibcHash types.HexBytes,
    orgID, contractName string,
    receipts []types.KVPair) ([]types.KVPair, types.Error)
```

Cross-chain transaction transfer confirmation interface. `ibcHash` is the hash value of the cross-chain transaction. `orgID` is the organization to which the application contract belongs. `contractName` is the application contract name. `receipts` is the cross-chain receipt information.

### 18.6 func CancelRecast()

Function Prototype:

```go
func CancelRecast(ibcHash types.HexBytes,
    orgID, contractName string,
    receipts []types.KVPair) ([]types.KVPair, types.Error)
```

Cross-chain transaction transfer cancels the interface. `ibcHash` is the hash value of the cross-chain transaction. `orgID` is the organization to which the application contract belongs. `contractName` is the application contract name. `receipts` is the cross-chain receipt information.

### 18.7 func Notify()

Function Prototype:

```go
func Notify(ibcHash types.HexBytes,
    orgID, contractName string,
    receipts []types.KVPair) ([]types.KVPair, types.Error)
```

Cross-chain notification interface. `ibcHash` is the hash value of the cross-chain transaction. `orgID` is the organization to which the application contract belongs. `contractName` is the application contract name. `receipts` for cross-chain receipt information.
