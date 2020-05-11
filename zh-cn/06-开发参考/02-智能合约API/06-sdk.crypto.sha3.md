# sdk/crypto/sha3

代码包 `blockchain/smcsdk/sdk/crypto/sha3`封装了对散列算法 `SHA-3` 的简便应用接口。



## 1. functions

### 1.1 func Sum224()

函数原型：

```
func Sum224(datas ...[]byte) []byte
```

使用 `SHA3-224` 算法计算输入的数据表（多项输入参数按输入顺序进行计算）的 224 位散列值并返回计算结果。



### 1.2 func Sum256()

函数原型：

```
func Sum256(datas ...[]byte) []byte
```

使用 `SHA3-256` 算法计算输入的数据表（多项输入参数按输入顺序进行计算）的 256 位散列值并返回计算结果。



### 1.3 func Sum384()

函数原型：

```
func Sum384(datas ...[]byte) []byte
```

使用 `SHA3-384` 算法计算输入的数据表（多项输入参数按输入顺序进行计算）的 384 位散列值并返回计算结果。



### 1.4 func Sum512()

函数原型：

```
func Sum512(datas ...[]byte) []byte
```

使用 `SHA3-512` 算法计算输入的数据表（多项输入参数按输入顺序进行计算）的 512 位散列值并返回计算结果。
