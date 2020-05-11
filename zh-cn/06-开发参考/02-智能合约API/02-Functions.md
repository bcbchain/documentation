# Functions

## 1 func Require()

函数原型：

```
func Require(expr bool, errCode uint32, errInfo string)
```

断言表达式 `expr` 为 `true`，如果 `expr` 为 `false`，将触发智能合约 `panic` 一个类型为 `types.Error` 的对象，其中错误码为指定的 `errCode`，错误信息为指定的 `errInfo`。如果 `expr` 为 `true`，智能合约将被允许继续往下执行。



## 2 func RequireNotError()

函数原型：

```
func RequireNotError(err error, errCode uint32)
```

断言 `err` 不是错误，要求 `err` 对象必须为空，如果 `err` 对象不为空，将触发智能合约 `panic` 一个类型为 `types.Error` 的对象，其中错误码为指定的 `errCode`，错误信息为 `err` 对象中的错误描述信息。如果 `err` 为空，智能合约将被允许继续往下执行。



## 3 func RequireOwner()

函数原型：

```
func RequireOwner()
```

断言本次智能合约调用的调用者必须是合约的拥有者。如果不满足要求，将触发智能合约 `panic` 一个类型为 `types.Error` 的对象，其中错误码为 `types.ErrNoAuthorization`，错误信息为具体错误原因。如果满足要求，智能合约将被允许继续往下执行。



## 4 func RequireAddress()

函数原型：

```
func RequireAddress(addr types.Address)
```

断言 `addr` 是一个格式正确的地址，如果地址格式不正确，将触发智能合约 `panic` 一个类型为 `types.Error` 的对象，其中错误码为 `types.ErrInvalidAddress`，错误信息为具体错误原因。如果地址格式正确，智能合约将被允许继续往下执行。



## 5 func RequireAddressEx()

函数原型：

```
func RequireAddressEx(chainID string, addr types.Address)
```

断言 `addr` 是一个以 `chanID` 为前缀的格式正确的地址，如果地址格式不正确，将触发智能合约 `panic` 一个类型为 `types.Error` 的对象，其中错误码为 `types.ErrInvalidAddress`，错误信息为具体错误原因。如果地址格式正确，智能合约将被允许继续往下执行。



## 6 func RequireSideChain()

函数原型：

```
func RequireSideChain()
```

断言当前链为侧链，如果当前链不为侧链，将触发智能合约 `panic` 一个类型为 `types.Error` 的对象，其中错误码为 `types.ErrNoAuthorization`，错误信息为 `require side chain, now main chain`。如果当前链为侧链，智能合约将被允许继续往下执行。



## 7 func RequireMainChain()

函数原型：

```
func RequireMainChain()
```

断言当前链为主链，如果当前链不为主链，将触发智能合约 `panic` 一个类型为 `types.Error` 的对象，其中错误码为 `types.ErrNoAuthorization`，错误信息为 `require main chain, now side chain`。如果当前链为主链，智能合约将被允许继续往下执行。



## 8 func Array()

函数原型：

```
func Array(items ...interface{}) []interface{}
```

将多个对象转换成一个切片进行表示。
