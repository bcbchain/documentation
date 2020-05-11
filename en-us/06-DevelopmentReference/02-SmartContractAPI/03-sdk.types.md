# sdk/types

The package `blockchain/smcsdk/sdk/types` encapsulates some basic data types needed to develop smart contracts.

## 1 struct Error

SDK provides the standard type to describe the error.

### 1.1 definition

```go
//Error define type for error of sdk
type Error struct {
    ErrorCode uint32 // Error code
    ErrorDesc string // Error description
}
```

### 1.2 func Error()

Function prototype:

```go
func (err *Error) Error() string
```

Returns the error message text.

### 1.3 error code

```shell
CodeOK = 200                      ErrorDesc = ""

//for stub
ErrStubDefined = 51000            ErrorDesc = "Error stub defined"
ErrGasNotEnough = 51001           ErrorDesc = "Gas limit is not enough"
ErrFeeNotEnough = 51002           ErrorDesc = "Insufficient balance to pay fee"

//for sdk
ErrAddSupplyNotEnabled = 52000    ErrorDesc = "Add supply is not enabled"
ErrBurnNotEnabled = 52001         ErrorDesc = "Burn supply is not enabled"
ErrInvalidAddress = 52002         ErrorDesc = "Invalid address"

//for contract
ErrNoAuthorization = 53000        ErrorDesc = "No authorization to execute contract"
ErrInvalidParameter = 53001       ErrorDesc = "Invalid parameter"
ErrInsufficientBalance = 53002    ErrorDesc = "Insufficient balance"

//for user defined
ErrUserDefined = 55000            ErrorDesc = "Error user defined"
```

## 2 type HexBytes

SDK provides the type of byte array/slice, and encapsulates some commonly used serialization interfaces.

### 2.1 definition

```go
type HexBytes []byte
```

### 2.2 func Marshal()

Function prototype:

```go
func (bz HexBytes) Marshal() ([]byte, error)
```

Implement the standard binary serialization interface.

### 2.3 func Unmarshal()

Function prototype:

```go
func (bz *HexBytes) Unmarshal(data []byte) error
```

Implement the standard binary deserialization interface, and set the value of `bz` to the value of `data`.

### 2.4 func MarshalJSON()

Function prototype:

```go
func (bz HexBytes) MarshalJSON() ([]byte, error)
```

Implement the standard JSON serialization interface.

### 2.5 func UnmarshalJSON()

Function prototype:

```go
func (bz *HexBytes) UnmarshalJSON(data []byte) error
```

Implement the standard JSON deserialization interface, and set the value of `bz` to the value of JSON string `data`.

### 2.6 func Bytes()

Function prototype:

```go
func (bz HexBytes) Bytes() []byte
```

Implement the standard get byte slice interface.

### 2.7 func String()

Function prototype:

```go
func (bz HexBytes) String() string
```

Implement the standard string expression interface to convert `bz` to all uppercase hexadecimal strings.

## 3 type Address

SDK provides the standard type to describe the account address.

### 3.1 definition

```go
type Address = string
```

## 4 type Hash

SDK provides the standard type to describe the hash data.

### 4.1 definition

```go
type Hash = HexBytes
```

## 5 type PubKey

SDK provides the standard type to describe public key data.

### 5.1 definition

```go
type PubKey = HexBytes
```

## 6 type KVPair

SDK provides the standard type to describe key/value pairs.

### 6.1 definition

```go
type KVPair struct {
    Key   []byte `protobuf:"bytes,1,opt,name=key,proto3" json:"key,omitempty"`
    Value []byte `protobuf:"bytes,2,opt,name=value,proto3" json:"value,omitempty"`
}
```
