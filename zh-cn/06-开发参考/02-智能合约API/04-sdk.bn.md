# sdk/bn

代码包 `blockchain/smcsdk/sdk/bn`封装了一个处理大数的类 `Number`，进行加减乘除操作时不必考虑溢出的问题。

## 1 functions

本章描述程序包 `sdk/bn` 提供的关于类 `Number` 简便构造函数。

### 1.1 func N()

函数原型：

```
func N(x int64) Number
```

将 `int64` 类型的 `x` 转换成 `Number` 类型对象并返回。



### 1.2 func N1()

函数原型：

```
func N1(b int64, d int64) Number
```

根据传入的 `b` 和 `d`，计算 `b * d` 的结果并返回 `Number` 类型对象。



### 1.3 func N2()

函数原型：

```
func N2(b int64, d1, d2 int64) Number
```

根据传入的 `b`，`d1`，`d2`，计算 `b * d1 * d2` 的结果并返回 `Number` 类型对象。



### 1.4 func NB()

函数原型：

```
func NB(x *big.Int) Number
```

将 `big.Int` 类型的大整数 `x` 转换成 `Number` 类型对象并返回。



### 1.5 func NBS()

函数原型：

```
func NBS(x []byte) Number
```

将按大端表示无符号大整数的字节切片 `x` 转换成 `Number` 类型对象并返回。



### 1.6 func NSBS()

函数原型：

```
func NSBS(x []byte) Number
```

将按大端表示带符号大整数的字节切片 `x` 转换成 `Number` 类型对象并返回。



### 1.7 func NBytes()

函数原型：

```
func NBytes(x []byte) Number
```

将按大端表示无符号大整数的字节切片 `x` 转换成 `Number` 类型对象并返回。



### 1.8 func NSBytes()

函数原型：

```
func NSBytes(x []byte) Number
```

将按大端表示带符号大整数的字节切片 `x` 转换成 `Number` 类型对象并返回。



### 1.9 func NString()

函数原型：

```
func NS(s string) Number
```

将按十进制字符串表示的大整数 `s` 转换成 `Number` 类型对象并返回，如果解析失败将返回 `0`。



### 1.10 func NStringHex()

函数原型：

```
func NS(s string) Number
```

将以 `0x` 或 `0X` 开头的十六进制字符串表示的无符号大整数 `s` 转换成 `Number` 类型对象并返回，如果解析失败将返回 `0`。



### 1.11 func NewNumber()

函数原型：

```
func NewNumber(x int64) Number
```

将 `int64` 类型的大整数 `x` 转换成 `Number` 类型对象并返回。



### 1.12 func NewNumberStringBase()

函数原型：

```
func NewNumberStringBase(s string, base int) Number
```

将字符串表示的大整数 `s` 转换成 `Number` 类型对象并返回，字符串按给定的基数 `base` 进行解析，如果解析失败将返回 `0`。

基数 `base` 必须是 `0` 或者 `2` 到 `MaxBase` 之间的整数。如果 `base` 为 `0`，字符串 `s` 的前缀决定实际的转换基数：前缀为 `"0x"`、`"0X"` 表示十六进制；前缀 `"0b"`、`"0B"` 表示二进制；前缀 `"0"` 表示八进制；其它都自动采用十进制作为基数。

针对 `<= 36` 的基数，大写和小写字母表达相同的数，字母 `'a'` 到 `'z'` 和 `'A'` 到 `'Z'` 都表达数值 `10` 到 `35`。

针对 `> 36` 的基数，大写字母 `'A'` 到 `'Z'` 表达数值 `36` 到 `61`。



### 1.13 func NewNumberBigInt()

函数原型：

```
func NewNumberBigInt(x *big.Int) Number
```

将 `big.Int` 类型的大整数 `x` 转换成 `Number` 类型对象并返回。



### 1.14 func NewNumberLong()

函数原型：

```
func NewNumberLong(b int64, d int64) Number
```

根据传入的 `b` 和 `d`，计算 `b * d` 的结果并返回 `Number` 类型对象。



### 1.15 func NewNumberLongLong()

函数原型：

```
func NewNumberLongLong(b int64, d1, d2 int64) Number
```

根据传入的 `b`，`d1`，`d2`，计算 `b * d1 * d2` 的结果并返回 `Number` 类型对象。



## 2 class Number

本章描述类 `Number` 的成员函数。

### 2.1 func String()

函数原型：

```
func (x Number) String() string
```

实现标准的获取字符串表达接口，将 `x` 转换为十进制字符串。`x` 未设定初始大数值，返回 `nil`。



### 2.2 func Value()

函数原型：

```
func (x Number) Value() *big.Int
```

获取 `x` 的 `big.Int` 的值。`x` 未设定初始大数值，返回 `nil`。



### 2.3 func CmpI()

函数原型：

```
func (x Number) CmpI(y int64) int
```

将 `x` 与 `y` 进行比较，返回 `-1` 代表 `x < y`，`0` 代表 `x == y`，`+1` 代表 `x > y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.4 func Cmp()

函数原型：

```
func (x Number) Cmp(y Number) int
```

将 `x` 与 `y` 进行比较，返回 `-1` 代表 `x < y`，`0` 代表 `x == y`，`+1` 代表 `x > y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.5 func IsZero()

函数原型：

```
func (x Number) IsZero() bool
```

判断 `x` 是否为 `0`。`x` 等于 `0` 返回 `true`。`x` 未设定初始大数值将触发 `panic`。



### 2.6 func IsPositive()

函数原型：

```
func (x Number) IsPositive() bool
```

判断 `x` 是否为正整数(不包含 `0`)。`x` 为正数返回 `true`。`x` 未设定初始大数值将触发 `panic`。



### 2.7 func IsNegative()

函数原型：

```
func (x Number) IsNegative() bool
```

判断 `x` 是否为负整数。`x` 为负数返回 `true`。`x` 未设定初始大数值将触发 `panic`。



### 2.8 func IsEqualI()

函数原型：

```
func (x Number) IsEqualI(y int64) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x == y`，`false` 代表 `x != y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.9 func IsEqual()

函数原型：

```
func (x Number) IsEqual(y Number) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x == y`，`false` 代表 `x != y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.10 func IsGreaterThanI()

函数原型：

```
func (x Number) IsGreaterThanI(y int64) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x > y`，`false` 代表 `x <= y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.11 func IsGreaterThan()

函数原型：

```
func (x Number) IsGreaterThan(y Number) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x > y`，`false` 代表 `x <= y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.12 func IsLessThanI()

函数原型：

```
func (x Number) IsLessThanI(y int64) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x < y`，`false` 代表 `x >= y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.13 func IsLessThan()

函数原型：

```
func (x Number) IsLessThan(y Number) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x < y`，`false` 代表 `x >= y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.14 func IsGEI()

函数原型：

```
func (x Number) IsGEI()(y int64) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x >= y`，`false` 代表 `x < y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.15 func IsGE()

函数原型：

```
func (x Number) IsGE(y Number) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x >= y`，`false` 代表 `x < y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.16 func IsLEI()

函数原型：

```
func (x Number) IsLEI(y int64) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x <= y`，`false` 代表 `x > y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.17 func IsLE()

函数原型：

```
func (x Number) IsLE(y Number) bool
```

将 `x` 与 `y` 进行比较，返回 `true` 代表 `x <= y`，`false` 代表 `x > y`。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.18 func AddI()

函数原型：

```
func (x Number) AddI(y int64) Number
```

计算 `x + y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.19 func Add()

函数原型：

```
func (x Number) Add(y Number) Number
```

计算 `x + y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.20 func SubI()

函数原型：

```
func (x Number) SubI(y int64) Number
```

计算 `x - y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.21 func Sub()

函数原型：

```
func (x Number) Sub(y Number) Number
```

计算 `x - y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.22 func MulI()

函数原型：

```
func (x Number) MulI(y int64) Number
```

计算 `x * y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.23 func Mul()

函数原型：

```
func (x Number) Mul(y Number) Number
```

计算 `x * y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.24 func DivI()

函数原型：

```
func (x Number) DivI(y int64) Number
```

计算 `x / y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.25 func Div()

函数原型：

```
func (x Number) Div(y Number) Number
```

计算 `x / y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.26 func ModI()

函数原型：

```
func (x Number) ModI(y int64) Number
```

计算 `x % y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.27 func Mod()

函数原型：

```
func (x Number) Mod(y Number) Number
```

计算 `x % y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.28 func Sq()

函数原型：

```
func (x Number) Sq() Number
```

计算 `x ** 2` ，并返回计算结果。`x` 未设定初始大数值将触发 `panic`。



### 2.29 func Sqrt()

函数原型：

```
func (x Number) Sqrt() Number
```

计算 `x` 平方根，并返回计算结果。`x` 未设定初始大数值将触发 `panic`。



### 2.30 func Exp()

函数原型：

```
func (x Number) Exp(y Number) Number
```

计算 `x ** y` ，并返回计算结果。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.31 func Lsh()

函数原型：

```
func (x Number) Lsh(n uint) Number
```

将 `x` 向左移 `n` 位，并返回移位结果。`x` 未设定初始大数值将触发 `panic`。



### 2.32 func Rsh()

函数原型：

```
func (x Number) Rsh(n uint) Number
```

将 `x` 向右移 `n` 位，并返回移位结果。`x` 未设定初始大数值将触发 `panic`。



### 2.33 func And()

函数原型：

```
func (x Number) And(y Number) Number
```

按位计算 `x & y` ，并返回计算结果（需要注意这里`x`、`y`有可能为负数，采用二进制补码形式进行按位与）。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.34 func Or()

函数原型：

```
func (x Number) Or(y Number) Number
```

按位计算 `x | y` ，并返回计算结果（需要注意这里`x`、`y`有可能为负数，采用二进制补码形式进行按位或）。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.35 func Xor()

函数原型：

```
func (x Number) Xor(y Number) Number
```

按位计算 `x ^ y` ，并返回计算结果（需要注意这里`x`、`y`有可能为负数，采用二进制补码形式进行按位异或）。`x` 或 `y` 未设定初始大数值将触发 `panic`。



### 2.36 func Not()

函数原型：

```
func (x Number) Not() Number
```

按位计算 `^ x` ，并返回计算结果（需要注意这里`x`有可能为负数，采用二进制补码形式进行取反）。`x` 未设定初始大数值将触发 `panic`。



### 2.37 func Bytes()

函数原型：

```
func (x Number) Bytes() []byte
```

实现标准的获取字节切片接口，将 `x` 转换为大端顺序的字节切片（第一字节解为表示符号，负数为`0xFF`，非负数为 `0x00`），并返回转换结果。例如：`380`将被转换为`0x00017C`；`-380`将被转换为`0xFF017C`。`x` 未设定初始大数值将触发 `panic`。



### 2.37 func SetBytes()

函数原型：

```
func (x *Number) SetBytes(buf []byte) Number
```

将 `x` 的值设置为一个大端顺序的字节切片（第一字节为 `0xFF` 表示是一个负数，其绝对值从第二字节开始编码，否则整个字节切片表示一个非负整数），并将 `x` 的值返回。例如：`0x00017C`和`0x017C` 都将被转换为`380`；`0xFF017C`将被转换为`-380`。



### 2.38 func MarshalJSON()

函数原型：

```
func (x Number) MarshalJSON() (data []byte, err error)
```

实现标准的 JSON 序列化接口。将 `x` 转成简化版的 JSON 字符串，例如字符串`380`。`x` 未设定初始大数值将触发 `panic`。



### 2.39 func UnmarshalJSON()

函数原型：

```
func (x *Number) UnmarshalJSON(data []byte) error
```

实现标准的 JSON 反序列化接口。将 `x` 的值设为输入的 JSON 字符串对应的大数。支持简化版的 JSON 字符串（例如：字符串`380`）与结构版的 JSON 字符串（例如：字符串`{"v":380}`）。
