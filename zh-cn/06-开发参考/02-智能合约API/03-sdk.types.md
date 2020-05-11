# sdk/types

代码包 `blockchain/smcsdk/sdk/types` 封装了一些开发智能合约所需要的基础数据类型。



## 1 struct Error

SDK提供的描述错误的标准类型。

### 1.1 definition

```
//Error define type for error of sdk
type Error struct {
	ErrorCode uint32 // Error code
	ErrorDesc string // Error description
}
```



### 1.2 func Error()

函数原型：

```
func (err *Error) Error() string
```

返回错误信息文本。



### 1.3 error code

```
CodeOK = 200                      ErrorDesc = ""

//for stub
ErrStubDefined = 51000            ErrorDesc = "Error stub defined"
ErrGasNotEnough = 51001			  ErrorDesc = "Gas limit is not enough"
ErrFeeNotEnough = 51002			  ErrorDesc = "Insufficient balance to pay fee"

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

SDK提供的字节数组/切片类型，封装了一些常用的序列化接口。

### 2.1 definition

```
type HexBytes []byte
```



### 2.2 func Marshal()

函数原型：

```
func (bz HexBytes) Marshal() ([]byte, error)
```

实现标准的二进制序列化接口。



### 2.3 func Unmarshal()

函数原型：

```
func (bz *HexBytes) Unmarshal(data []byte) error
```

实现标准的二进制反序列化接口，将 `bz` 的值设置为 `data` 的值。



### 2.4 func MarshalJSON()

函数原型：

```
func (bz HexBytes) MarshalJSON() ([]byte, error)
```

实现标准的 JSON 序列化接口。



### 2.5 func UnmarshalJSON()

函数原型：

```
func (bz *HexBytes) UnmarshalJSON(data []byte) error
```

实现标准的 JSON 反序列化接口，将 `bz` 的值设置为 JSON字符串 `data` 的值。



### 2.6 func Bytes()

函数原型：

```
func (bz HexBytes) Bytes() []byte
```

实现标准的获取字节切片接口。



### 2.7 func String()

函数原型：

```
func (bz HexBytes) String() string
```

实现标准的获取字符串表达接口，将 `bz` 转换成全部大写的十六进制字符串。



## 3 type Address

SDK提供的描述账户地址的标准类型。

### 3.1 definition

```
type Address = string
```



## 4 type Hash

SDK提供的描述哈希数据的标准类型。

### 4.1 definition

```
type Hash = HexBytes
```



## 5 type PubKey

SDK提供的描述公钥数据的标准类型。

### 5.1 definition

```
type PubKey = HexBytes
```



## 6 type KVPair

SDK提供的描述键/值对的标准类型。

### 6.1 definition

```
type KVPair struct {
	Key   []byte `protobuf:"bytes,1,opt,name=key,proto3" json:"key,omitempty"`
	Value []byte `protobuf:"bytes,2,opt,name=value,proto3" json:"value,omitempty"`
}
```
