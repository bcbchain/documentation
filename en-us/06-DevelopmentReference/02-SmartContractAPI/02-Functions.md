# Functions

## 1 func Require()

Function prototype:

```go
func Require(expr bool, errCode uint32, errInfo string)
```

The assertion expression `expr` is`true`. If `expr` is `false`, an object of type `types.Error` of smart contract `panic` will be triggered. The error code is the specified `errCode`, and the error information is the specified `errInfo`. If `expr` is`true`, the smart contract will be allowed to continue to execute.

## 2 func RequireNotError()

Function prototype:

```go
func RequireNotError(err error, errCode uint32)
```

Asserting `err` is not an error, and it requires the `err` object to be empty. If the `err` object is not empty, an object of type `types.Error` of smart contract `panic` will be triggered, where the error code is the specified `errCode`, and the error information is the error description information in the `err` object. If `err` is empty, the smart contract will be allowed to continue to execute.

## 3 func RequireOwner()

Function prototype:

```go
func RequireOwner()
```

Assert that the caller of this smart contract call must be the owner of the contract. If the requirements are not met, an object of type `types.Error` of smart contract `panic` will be triggered, in which the error code is `types.ErrNoAuthorization`', and the error information is the specific error reason. If the requirements are met, the smart contract will be allowed to continue to execute.

## 4 func RequireAddress()

Function prototype:

```go
func RequireAddress(addr types.Address)
```

Assert that `addr` is a correctly formatted address. If the address format is not correct, an object of type `types.Error` of smart contract `panic` will be triggered, where the error code is `types.ErrInvalidAddress`, and the error information is the specific error reason. If the address format is correct, the smart contract will be allowed to continue.

## 5 func RequireAddressEx()

Function prototype:

```go
func RequireAddressEx(chainID string, addr types.Address)
```

Assert that `addr` is a correctly formatted address prefixed with `chanID`. If the address format is not correct, a smart contract `panic` object of type `types.Error` will be triggered, in which the error code is `types.ErrInvalidAddress`, and the error information is the specific error reason. If the address format is correct, the smart contract will be allowed to continue.

## 6 func RequireSideChain()

Function prototype:

```go
func RequireSideChain()
```

Assert that the current chain is a side chain. If the current chain is not a side chain, an object of type `types.Error` of smart contract `panic` will be triggered. The error code is `types.ErrNoAuthorization`, and the error message is `require side chain, now main chain`. If the current chain is a side chain, the smart contract will be allowed to continue to execute.

## 7 func RequireMainChain()

Function prototype:

```go
func RequireMainChain()
```

Assert that the current chain is the main chain. If the current chain is not the main chain, an object of type `types.Error` of smart contract `panic` will be triggered. The error code is `types.ErrNoAuthorization`, and the error message is `require main chain, now side chain`. If the current chain is the main chain, the smart contract will be allowed to continue to execute.

## 8 func Array()

Function prototype:

```go
func Array(items ...interface{}) []interface{}
```

Convert multiple objects to a slice for presentation.
