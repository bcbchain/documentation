# sdk/crypto/ed25519

The package `blockchain/smcsdk/sdk/crypto/ed25519` encapsulates a simple application interface for elliptic curve `ed25519`.

## 1. functions

### 1.1 func VerifySign()

Function prototype:

```go
func VerifySign(pubkey, data, sign []byte) bool
```

Verify the signature and if succeeds, returns `true`. `pubkey` is the public key, `data` is the signed data, `sign` is the signed data.
