# sdk/crypto/sha3

The code package `blockchain/smcsdk/sdk/crypto/sha3` encapsulates a simple application interface for hash algorithm `SHA-3`.

## 1. functions

### 1.1 func Sum224()

Function prototype:

```go
func Sum224(datas ...[]byte) []byte
```

Use the `SHA3-224` algorithm to calculate the 224 bit hash value of the input data table (multiple input parameters are calculated according to the input order) and return the calculation result.

### 1.2 func Sum256()

Function prototype:

```go
func Sum256(datas ...[]byte) []byte
```

Use the `SHA3-256` algorithm to calculate the 256 bit hash value of the input data table (multiple input parameters are calculated according to the input order) and return the calculation result.

### 1.3 func Sum384()

Function prototype:

```go
func Sum384(datas ...[]byte) []byte
```

Use the `SHA3-384` algorithm to calculate the 384 bit hash value of the input data table (multiple input parameters are calculated according to the input order) and return the calculation result.

### 1.4 func Sum512()

Function prototype:

```go
func Sum512(datas ...[]byte) []byte
```

Use the `SHA3-512` algorithm to calculate the 512 bit hash value of the input data table (multiple input parameters are calculated according to the input order) and return the calculation result.
