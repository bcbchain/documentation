# sdk/crypto/ed25519

代码包 `blockchain/smcsdk/sdk/crypto/ed25519`封装了对椭圆曲线 `ed25519` 的简便应用接口。



## 1. functions

### 1.1 func VerifySign()

函数原型：

```
func VerifySign(pubkey, data, sign []byte) bool
```

验证签名，成功返回 `true`。`pubkey` 为公钥，`data` 为被签名的数据， `sign` 为签名数据。
