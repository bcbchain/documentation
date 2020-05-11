# Toolbox

## 1. sdk/forx

代码包 `blockchain/smcsdk/sdk/mapx`封装了对 `for` 循环进行优化处理的应用接口。

### 1.1 func Range()

函数原型：

```
func Range(args... interface{})
```

智能合约规范中不允许智能合约代码中使用关键字 `for`。

智能合约中需要循环执行的指令必须采用 `Range()` 函数。

 `Range()` 函数存在六种模型。

**. 模型一**

```
func Range( m map[keyType]valType, f func(key keyType, val valType) )
func Range( m map[keyType]valType, f func(key keyType, val valType) bool )
```
对映射表对象 m 进行遍历操作，遍历按照映射表键的顺序执行，操作函数为 f，如果 f 的返回值定义为空，则遍历结束以后才可以结束循环，如果 f 的返回值定义为布尔类型，f 返回 false 表示终止执行遍历操作退出循环，f 返回 true 表示继续执行遍历操作。输入参数要求满足如下条件，如果任意一条不满足则发生异常，当发生异常时，将会自动触发SDK进行 panic：

> - 参数 m 的类型必须是一个映射表；
> - 参数 f 必须是一个函数，函数的返回值必须是在空与布尔类型之间二选一；
> - 函数 f 的参数必须是两个；
> - 函数 f 的第一个参数类型必须是映射表 m 的键对应的类型；
> - 函数 f 的第二个参数类型必须是映射表 m 的值对应的类型。

示例代码如下：

```
m := make(map[int]string)
m[93] = "23231"
m[13] = "23423423234324"
m[54] = "3432432423"
m[23] = "3434545345345"

forx.Range(m, func(k int, v string) {
	printf("key=%v value=%v\n", k, v)
}) 
```



**. 模型二**

```
func Range( s []valType, f func(i int, val valType) )
func Range( s []valType, f func(i int, val valType) bool )
```

对切片对象 s 进行遍历操作，遍历按照切片顺序从小到大顺序执行，操作函数为 f，如果 f 的返回值定义为空，则遍历结束以后才可以结束循环，如果 f 的返回值定义为布尔类型，f 返回 false 表示终止执行遍历操作结束循环，f 返回 true 表示继续执行遍历操作。输入参数要求满足如下条件，如果任意一条不满足则发生异常，当发生异常时，将会自动触发SDK进行 panic：

> - 参数 s 的类型必须是一个切片；
> - 参数 f 必须是一个函数，函数的返回值必须是在空与布尔类型之间二选一；
> - 函数 f 的参数必须是两个；
> - 函数 f 的第一个参数类型必须是 int 类型，表示元素的索引号，从 0 开始；
> - 函数 f 的第二个参数类型必须是切片 s 的元素值对应的类型。

示例代码如下：

```
s := make([]string)
s = append(s, "23231")
s = append(s, "423792234")
s = append(s, "23232")
s = append(s, "3243455454")

forx.Range(s, func(i int, v string) {
	printf("i=%v value=%v\n", i, v)
}) 
```

**. 模型三**

```
func Range( n intType, f func(i intType) )
func Range( n intType, f func(i intType) bool )
```

循环执行指定次数，操作函数为 f，如果 f 的返回值定义为空，则执行完指定次数以后才可以结束循环，f 返回 false 表示终止循环操作，f 返回 true 表示继续循环操作。输入参数要求满足如下条件，如果任意一条不满足则发生异常，当发生异常时，将会自动触发SDK进行 panic：

> - 参数 n 的类型必须为表达整数的类型，例如：int、uint、int32等, 值必须大于等于 0 的整数；
> - 参数 f 必须是一个函数，函数的返回值必须是在空与布尔类型之间二选一；
> - 函数 f 的参数必须是一个，类型必须于参数 n 的类型相同，表示执行循环的索引号，从 0 开始。

示例代码如下：

```
forx.Range(10, func(i int) {
	printf("i=%v\n", i)
}) 
```

**. 模型四**

```
func Range( m,n intType, f func(k intType) )
func Range( m,n intType, f func(k intType) bool )
```

根据输入参数遍历 m 到 n 之间(包含 m 和 n)的所有整数，从 m 开始执行，到 n 结束，操作函数为 f，如果 f 的返回值定义为空，则遍历结束以后才可以结束循环，f 返回 false 表示终止执行遍历操作退出循环，f 返回 true 表示继续执行遍历操作。输入参数要求满足如下条件，如果任意一条不满足则发生异常，当发生异常时，将会自动触发SDK进行 panic：

> - 参数 m 和 n 的类型必须为表达整数的同一类型，例如：int、uint、int32等，如果 m 小于 n，则执行顺序为增序，如果 m 大于 n，则执行顺序为降序；
> - 参数 f 必须是一个函数，函数的返回值必须是在空与布尔类型之间二选一；
> - 函数 f 的参数必须是一个，类型必须与参数 m 和 n 的类型相同，表示遍历的整数值，从 m 开始。


示例代码如下：

```
forx.Range(1,100, func(k int) {
	printf("k=%v\n", k)
}) 
```

**. 模型五**

```
func Range( c func() bool, f func(i int) )
func Range( c func() bool, f func(i int) bool )
```

循环执行函数 f，当控制函数 c 满足返回值为 true 时立即终止循环操作，它控制循环结束的时间，如果 f 的返回值定义为布尔类型，则除了函数 c 可以控制循环结束以外，f 返回 false 表示终止执行循环操作，f 返回 true 表示继续执行循环操作，输入参数要求满足如下条件，如果任意一条不满足则发生异常，当发生异常时，将会自动触发SDK进行 panic：

> - 参数 c 必须是一个函数，函数的返回值必须是布尔类型；
> - 参数 f 必须是一个函数，函数的返回值必须是在空与布尔类型之间二选一；
> - 函数 f 的参数必须是一个，类型必须是 int，表示执行循环次数的索引，从 0 开始。

示例代码如下：

```
toVoter := ballot._voters(to)
forx.range( func() bool {
              return toVoter.delegate != "" 
            },
            func(i int) {                
              to = toVoter.delegate
              toVoter = ballot._voters(to)
            })
```

**. 模型六**

```
func Range( f func(i int) bool )
```

循环执行函数 f，f 返回 false 表示终止执行循环操作，f 返回 true 表示继续执行循环操作。输入参数要求满足如下条件，如果任意一条不满足则发生异常，当发生异常时，将会自动触发SDK进行 panic：

> - 参数 f 必须是一个函数，函数的返回值必须是布尔类型；
> - 函数 f 的参数必须是一个，类型必须是 int，表示执行循环次数的索引，从 0 开始。

示例代码如下：

```
toVoter := ballot._voters(to)
forx.Range( func(i int) bool {                
              to = toVoter.delegate
              toVoter = ballot._voters(to)
              
              if toVoter.delegate != "" {
                return forx.Break
              } else {
                return forx.Continue
              }
            })
```



### 1.2 func RangeReverse()

函数原型：

```
func RangeReverse(args... interface{})
```

RangeReverse提供反向遍历切片的for循环。

 `RangeReverse()` 函数存在一种模型。

**. 模型一**

```
func RangeReverse( s []valType, f func(i int, val valType) )
func RangeReverse( s []valType, f func(i int, val valType) bool )
```

对切片对象 s 进行遍历操作，遍历按照切片顺序从大到小顺序执行，操作函数为 f，如果 f 的返回值定义为空，则遍历结束以后才可以结束循环，如果 f 的返回值定义为布尔类型，f 返回 false 表示终止执行遍历操作结束循环，f 返回 true 表示继续执行遍历操作。输入参数要求满足如下条件，如果任意一条不满足则发生异常，当发生异常时，将会自动触发SDK进行 panic：

> - 参数 s 的类型必须是一个切片；
> - 参数 f 必须是一个函数，函数的返回值必须是在空与布尔类型之间二选一；
> - 函数 f 的参数必须是两个；
> - 函数 f 的第一个参数类型必须是 int 类型，表示元素的索引号，从 len(s)-1 开始递减；
> - 函数 f 的第二个参数类型必须是切片 s 的元素值对应的类型。

示例代码如下：

```
s := make([]string)
s = append(s, "23231")
s = append(s, "423792234")
s = append(s, "23232")
s = append(s, "3243455454")

forx.Range(s, func(i int, v string) {
	printf("i=%v value=%v\n", i, v)
}) 
```

## 2. sdk/jsoniter

代码包 `blockchain/smcsdk/sdk/jsoniter`封装了对快速处理 JSON 数据的第三方包 `jsoniter` 的简便应用接口。

### 2.1 func Marshal()

函数原型：

```
func Marshal(v interface{}) ([]byte, error)
```

将输入的对象 `v` 序列化成 JSON 格式的字符串并返回。



### 2.2 func Unmarshal()

函数原型：

```
func Unmarshal(bz []byte, v interface{}) error
```

对输入的 JSON 字符串进行解析，并将解析结果存入 `v` 指向的对象。

## 3. sdk/rlp

代码包 `blockchain/smcsdk/sdk/rlp` 封装了 BCBChain 对交易进行 RLP 编码的操作。源码是基于 `geth` 的开源版本，根据 BCBChain 的需要，添加了对 `bn.Number` 大数的编解码支持，同时添加了对映射表的支持。
