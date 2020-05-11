# Interfaces

## 1 sdk/ISmartContract

接口 `sdk/ISmartContract` 封装了智能合约上下文获取的途径。



### 1.1 func Block()

函数原型：

```
func (ISmartContract) Block() IBlock
```

返回对 BCBChain 区块链进行调用时的区块信息。



### 1.2 func Tx()

函数原型：

```
func (ISmartContract) Tx() ITx
```

返回对 BCBChain 区块链进行调用的交易信息。



### 1.3 func Message()

函数原型：

```
func (ISmartContract) Message() IMessage
```

返回针对本智能合约调用的消息信息。



### 1.4 func Helper()

函数原型：

```
func (ISmartContract) Helper() IHelper
```

返回封装了SDK所有辅助功能的对象。




## 2 sdk/IBlock

接口 `sdk/IBlock` 封装了智能合约获取到的区块信息。

在智能合约调用时，`IBlock` 接口在两个不同阶段对应的区块信息是有区别的。

> 在checkTx阶段，当前智能合约的调用还没有取得共识，此时调用 ISmartContract::Block() 获得的为区块链上最后一个区块之上（区块高度加1）生成的一个模拟区块的信息（可能是一个空区块，总之这个区块与当前所执行的智能合约调用没有任何关系）。

> 在deliverTx阶段，此次调用智能合约的交易已经在区块链上达成共识，并写入到最新一个区块中，此时调用ISmartContract::Block() 获得的为区块链上最新一个实时区块的信息（不可能是一个空区块，这个区块中至少包含一笔对本次智能合约调用的交易信息）。




### 2.1 func ChainID()

函数原型：

```
func (IBlock) ChainID() string
```
返回当前区块链的链标识。



### 2.2 func BlockHash()

函数原型：

```
func (IBlock) BlockHash() types.Hash
```
返回当前区块的区块哈希。



### 2.3 func Height()

函数原型：

```
func (IBlock) Height() int64
```
返回当前区块的高度。



### 2.4 func Time()

函数原型：

```
func (IBlock) Time() int64
```
返回当前区块生成时的时间戳信息，结果为相对于 `1970-1-1 00:00:00` 过去的秒数。



### 2.5 func Now()

函数原型：

```
func (IBlock) Now() bn.Number
```

对 `Time()` 函数的别称。返回当前区块生成时的时间戳信息，结果为相对于 `1970-1-1 00:00:00` 过去的秒数。



### 2.6 func NumTxs()

函数原型：

```
func (IBlock) NumTxs() int32
```
返回当前区块收录的交易笔数。



### 2.7 func DataHash()

函数原型：

```
func (IBlock) DataHash() types.Hash
```
返回当前区块的数据哈希。



### 2.8 func ProposerAddress()

函数原型：

```
func (IBlock) ProposerAddress() types.Address
```
返回当前区块的提案者地址。



### 2.9 func RewardAddress()

函数原型：

```
func (IBlock) RewardAddress() types.Address
```
返回当前区块的提案者接收出块奖励的地址。



### 2.10 func RandomNumber()

函数原型：

```
func (IBlock) RandomNumber() types.HexBytes
```
返回当前区块的区块随机数。



### 2.11 func Version()

函数原型：

```
func (IBlock) Version() string
```
返回当前区块提案者出块时的软件版本。



### 2.12 func LastBlockHash()

函数原型：

```
func (IBlock) LastBlockHash() types.Hash
```
返回上一区块的区块哈希。



### 2.13 func LastCommitHash()

函数原型：

```
func (IBlock) LastCommitHash() types.Hash
```
返回上一区块的确认哈希。



### 2.14 func LastAppHash()

函数原型：

```
func (IBlock) LastAppHash() types.Hash
```
返回上一区块的应用层哈希。



### 2.15 func LastFee()

函数原型：

```
func (IBlock) LastFee() int64
```
返回上一区块的手续费（单位：`cong`）。




## 3 sdk/ITx

接口 `sdk/ITx` 封装了对 BCBChain 区块链进行调用的交易信息。



### 3.1 func Note()

函数原型：

```
func (ITx) Note() string
```
返回当前交易的备注信息。



### 3.2 func GasLimit()

函数原型：

```
func (ITx) GasLimit() int64
```

返回当前交易的最大燃料限制数量。



### 3.3 func GasLeft()

函数原型：

```
func (ITx) GasLeft() int64
```

返回当前交易的剩余燃料数量（已经预扣除对当前智能合约调用需要的燃料数量）。



### 3.4 func Signer()

函数原型：

```
func (ITx) Signer() IAccount
```

返回当前交易签名人(发起人)的账户对象。



### 3.5 func TxHash()

函数原型：

```
func (ITx) TxHash() []byte
```

返回当前交易Hash的字节切片。




## 4 sdk/IMessage

接口 `sdk/IMessage` 封装了对某个智能合约方法的一次调用相关的所有信息。在同一笔交易当中可以级联多次对不同智能合约方法进行调用的消息。




### 4.1 func Contract()

函数原型：

```
func (IMessage) Contract() types.Address
```

返回当前消息调用的智能合约地址。



### 4.2 func MethodID()

函数原型：

```
func (IMessage) MethodID() string
```

返回当前消息调用的智能合约方法ID（采用十六进制字符串进行表示）。



### 4.3 func Items()

函数原型：

```
func (IMessage) Items() []types.HexBytes
```

返回当前消息调用的每个参数数据字段的原始信息。当发生跨智能合约调用时，在被调用合约内部，`Items()` 获得的数据为 `nil`。



### 4.4 func GasPrice()

函数原型：

```
func (IMessage) GasPrice() int64
```

返回当前消息调用的燃料价格（单位：`cong`）。



### 4.5 func Sender()

函数原型：

```
func (IMessage) Sender() IAccount
```

返回当前消息调用发起人的账户对象。第一层的消息调用，消息发起人就是交易的签名人；当发生跨合约调用时，在被调用合约内部，`Sender()` 返回的是发起合约的账户对象。



### 4.6 func Payer()

函数原型：

```
func (IMessage) Payer() IAccount
```

返回支付当前消息手续费的账户对象。



### 4.7 func Origins()

函数原型：

```
func (IMessage) Origins() []types.Address
```

返回消息完整的调用链。在不是进行跨合约调用时，`Origins()` 返回包含本次交易发起者的账户地址的切片。当发生跨智能合约调用时，`Origins()` 返回表达调用的合约链，在被调用合约内部，`Origins()` 返回的地址列表中最后一个为本次调用发起合约的合约地址。



### 4.8 func InputReceipts()

函数原型：

```
func (IMessage) InputReceipts() []types.KVPair
```

在级联和跨合约消息调用时，前一个消息调用输出的收据将作为后一个消息调用的输入，本函数返回输入到本次消息调用的收据列表。



### 4.9 func GetTransferToMe()

函数原型：

```
func (IMessage) GetTransferToMe() []*std.Transfer
```

在前一个消息调用输出的收据中查询并返回向当前智能合约进行转账的所有收据，如果找不到则返回 `nil`。转账收据定义如下：

```
package std

type Transfer struct {
	Token types.Address `json:"token"` // 代币地址
	From  types.Address `json:"from"`  // 资金转出方账户地址
	To    types.Address `json:"to"`    // 资金接收方账户地址
	Value bn.Number     `json:"value"` // 转账金额（单位：`cong`）
}
```




## 5 sdk/IAccount

接口 `sdk/IAccount` 封装了对某个账户地址的访问接口。



### 5.1 func Address()

函数原型：

```
func (IAccount) Address() types.Address
```

返回账户对象的账户地址。



### 5.2 func PubKey()

函数原型：

```
func (IAccount) PubKey() types.PubKey
```

返回账户对象的公钥数据（可能为空）。



### 5.3 func Balance()

函数原型：

```
func (IAccount) Balance() bn.Number
```

在发行代币的合约中，返回账户对象在本合约所发行的代币子账户的资金余额（单位：`cong`）。在非代币合约中，返回 `0`。



### 5.4 func BalanceOfToken()

函数原型：

```
func (IAccount) BalanceOfToken(token types.Address) bn.Number
```

给定代币地址，返回账户对象在指定代币子账户的资金余额（单位：`cong`）。如果指定的代币地址不是一个代币，直接返回余额为 `0`。



### 5.5 func BalanceOfName()

函数原型：

```
func (IAccount) BalanceOfName(name string) bn.Number
```

给定代币名称，返回账户对象在指定代币子账户的资金余额（单位：`cong`）。如果指定的代币名称不是一个代币，直接返回余额为 `0`。



### 5.6 func BalanceOfSymbol()

函数原型：

```
func (IAccount) BalanceOfSymbol(symbol string) bn.Number
```

给定代币符号，返回账户对象在指定代币子账户的资金余额（单位：`cong`）。如果指定的代币符号不是一个代币，直接返回余额为 `0`。



### 5.7 func Transfer()

函数原型：

```
func (IAccount) Transfer(to types.Address, value bn.Number)
```

在代币合约中，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），在这里账户对象包括消息调用的发起人或当前合约账户。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 如果当前合约没有发行过代币（因为该函数的参数中没有指定转移哪种代币）；
> - 如果当前合约发行过代币，账户既不是消息调用的发起人也不是当前智能合约的合约账户。



### 5.8 func TransferWithNote()

函数原型：

```
func (IAccount) TransferWithNote(to types.Address, value bn.Number, note string)
```

在代币合约中，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），并在收据中返回 `note` 信息，在这里账户对象包括消息调用的发起人或当前合约账户。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 如果当前合约没有发行过代币（因为该函数的参数中没有指定转移哪种代币）；
> - 如果当前合约发行过代币，账户既不是消息调用的发起人也不是当前智能合约的合约账户。



### 5.9 func TransferWithNoteEx()

函数原型：

```
func (IAccount) TransferWithNoteEx(to types.Address, value bn.Number, note string) types.Error
```

在代币合约中，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），并在收据中返回 `note` 信息，在这里账户对象包括消息调用的发起人或当前合约账户。

满足如下任意一条则发生错误，当发生错误时，错误编码和信息在返回值中返回：

> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 如果当前合约没有发行过代币（因为该函数的参数中没有指定转移哪种代币）；
> - 如果当前合约发行过代币，账户既不是消息调用的发起人也不是当前智能合约的合约账户。



### 5.10 func TransferByToken()

函数原型：

```
func (IAccount) TransferByToken(token types.Address, to types.Address, value bn.Number)
```

如果指定的代币地址为本合约所发行的代币，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），在这里账户对象包括消息调用的发起人或当前合约账户。

如果指定的代币地址不是本合约所发行的代币，将账户对象的指定代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），在这里账户对象只能为当前合约账户。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 参数 token 不是一个地址；
> - 参数 token 不是一个代币；
> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 如果当前合约没有发行过代币，账户不是当前智能合约的合约账户；
> - 如果当前合约发行过代币，账户不是消息发送者或当前智能合约的合约账户者。



### 5.11 func TransferByTokenWithNote()

函数原型：

```
func (IAccount) TransferByTokenWithNote(token types.Address, to types.Address, value bn.Number, note string)
```

如果指定的代币地址为本合约所发行的代币，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），并在收据中返回 `note` 信息，在这里账户对象包括消息调用的发起人或当前合约账户。

如果指定的代币地址不是本合约所发行的代币，将账户对象的指定代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），并在收据中返回 `note` 信息，在这里账户对象只能为当前合约账户。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 参数 token 不是一个地址；
> - 参数 token 不是一个代币；
> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 如果当前合约没有发行过代币，账户不是当前智能合约的合约账户；
> - 如果当前合约发行过代币，账户不是消息发送者或当前智能合约的合约账户者。




### 5.12 func TransferByName()

函数原型：

```
func (IAccount) TransferByName(name string, to types.Address, value bn.Number)
```

如果指定的代币名称为本合约所发行的代币，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），在这里账户对象包括消息调用的发起人或当前合约账户。

如果指定的代币地址不是本合约所发行的代币，将账户对象的指定代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），在这里账户对象只能为当前合约账户。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 参数 name 不是一个代币的名称；
> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 如果当前合约没有发行过代币，账户不是当前智能合约的合约账户；
> - 如果当前合约发行过代币，账户不是消息发送者或当前智能合约的合约账户者。



### 5.13 func TransferByNameWithNote()

函数原型：

```
func (IAccount) TransferByNameWithNote(name string, to types.Address, value bn.Number, note string)
```

如果指定的代币名称为本合约所发行的代币，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），并在收据中返回 `note` 信息，在这里账户对象包括消息调用的发起人或当前合约账户。

如果指定的代币地址不是本合约所发行的代币，将账户对象的指定代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），并在收据中返回 `note` 信息，在这里账户对象只能为当前合约账户。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 参数 name 不是一个代币的名称；
> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 如果当前合约没有发行过代币，账户不是当前智能合约的合约账户；
> - 如果当前合约发行过代币，账户不是消息发送者或当前智能合约的合约账户者。




### 5.14 func TransferBySymbol()

函数原型：

```
func (IAccount) TransferBySymbol(symbol string, to types.Address, value bn.Number)
```

如果指定的代币符号为本合约所发行的代币，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），在这里账户对象包括消息调用的发起人或当前合约账户。

如果指定的代币地址不是本合约所发行的代币，将账户对象的指定代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），在这里账户对象只能为当前合约账户。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 参数 symbol 不是一个代币的符号；
> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 当前合约没有发行过代币，账户不是当前智能合约的合约账户；
> - 如果当前合约发行过代币，账户不是消息发送者或当前智能合约的合约账户者。



### 5.15 func TransferBySymbolWithNote()

函数原型：

```
func (IAccount) TransferBySymbolWithNote(symbol string, to types.Address, value bn.Number, note string)
```

如果指定的代币符号为本合约所发行的代币，将账户对象在本合约所发行的代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），并在收据中返回 `note` 信息，在这里账户对象包括消息调用的发起人或当前合约账户。

如果指定的代币地址不是本合约所发行的代币，将账户对象的指定代币子账户资金转给接收地址为 `to` 的账户（资金单位：`cong`），并在收据中返回 `note` 信息，在这里账户对象只能为当前合约账户。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 参数 symbol 不是一个代币的符号；
> - 参数 to 不是一个地址；
> - 参数 to 与账户地址相同；
> - 参数 value 小于 0；
> - 账户的余额不够支付 value 的值；
> - 当前合约没有发行过代币，账户不是当前智能合约的合约账户；
> - 如果当前合约发行过代币，账户不是消息发送者或当前智能合约的合约账户者。




## 6 sdk/IContract

接口 `sdk/IContract` 封装了某个智能合约的所有信息以及操作智能合约的接口。



### 6.1 func Address()

函数原型：

```
func (IContract) Address() types.Address
```

返回智能合约的地址。



### 6.2 func Account()

函数原型：

```
func (IContract) Account() IAccount
```

返回智能合约的账户对象。

智能合约的账户地址可用于接收转给合约的资金，智能合约账户地址的计算只与合约名称和组织ID相关，合约升级后合约地址发生变化但不会影响合约的账户地址，合约的账户地址没有私钥与之对应，合约账户上的资金只能通过合约进行操纵。



### 6.3 func Owner()

函数原型：

```
func (IContract) Owner() IAccount
```

返回智能合约的拥有者的外部账户对象（外部账户地址有私钥与之对应）。



### 6.4 func Name()

函数原型：

```
func (IContract) Name() string
```

返回智能合约名称。



### 6.5 func Version()

函数原型：

```
func (IContract) Version() string
```

返回智能合约版本号。



### 6.6 func CodeHash()

函数原型：

```
func (IContract) CodeHash() types.Hash
```

返回智能合约代码所对应的哈希。



### 6.7 func EffectHeigt()

函数原型：

```
func (IContract) EffectHeight() int64
```

返回智能合约开始生效时的区块高度。



### 6.8 func LoseHeight()

函数原型：

```
func (IContract) LoseHeight() int64
```

返回智能合约开始失效时的区块高度，0表示没有失效。



### 6.9 func KeyPrefix()

函数原型：

```
func (IContract) KeyPrefix() string
```

返回智能合约内所能访问的状态数据库KEY值的前缀（格式为`/xxx/yyy`），可用于进行智能合约之间数据的隔离保护。



### 6.10 func Methods()

函数原型：

```
func (IContract) Methods() []std.Method
```

返回智能合约所有公开方法的详细信息（可被用于级联消息调用合约）。`std.Method` 结构定义如下：

```
package std

type Method struct {
    MethodID    string    // 方法ID
    Gas         int64     // 方法在调用时需要消耗的燃料
    ProtoType   string    // 方法原型
}
```



### 6.11 func Interfaces()

函数原型：

```
func (IContract) Interfaces() []std.Method
```

返回智能合约所有公开接口（可被用于跨合约调用）的详细信息。



### 6.12 func IBCs()

函数原型：

```
func (IContract) IBCs() []std.Method
```

返回智能合约所有公开跨链方法（可被用于执行跨链业务）的详细信息。



### 6.13 func Mine()

函数原型：

```
func (IContract) Mine() []std.Method
```

返回智能合约公开的挖矿接口的详细信息。



### 6.14 func Token()

函数原型：

```
func (IContract) Token() types.Address
```

返回智能合约所注册的代币地址，如果合约没有注册过代币，返回空地址。



### 6.15 func OrgID()

函数原型：

```
func (IContract) OrgID() string
```

返回智能合约所属的组织标识。



### 6.16 func ChainVersion()

函数原型：

```
func (IContract) ChainVersion() string
```

返回智能合约的链版本。



### 6.17 func SetOwner()

函数原型：

```
func (IContract) SetOwner( newOwner types.Address)
```

设置智能合约新的拥有者。`newOwner` 为智能合约新的拥有者的外部账户地址。函数 `SetOwner()` 只能由智能合约的原拥有者调用。如果智能合约发行了代币，该操作同时会将代币的拥有者设置给新的拥有者。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 消息调用者不是合约的原拥有者；
> - 参数 newOwner 不是一个地址；
> - 参数 newOwner 是合约的原拥有者；
> - 参数 newOwner 是合约的地址；
> - 参数 newOwner 是合约的账户地址。




## 7 sdk/IToken

接口 `sdk/IToken` 封装了某个代币的所有信息以及操作代币的接口。



### 7.1 func Address()

函数原型：

```
func (IToken) Address() types.Address
```

返回代币的地址。



### 7.2 func Owner()

函数原型：

```
func (IToken) Owner() IAccount
```

返回代币拥有者的外部账户对象。



### 7.3 func Name()

函数原型：

```
func (IToken) Name() string
```

返回代币的名称。



### 7.4 func Symbol()

函数原型：

```
func (IToken) Symbol() string
```

返回代币的符号。



### 7.5 func TotalSupply()

函数原型：

```
func (IToken) TotalSupply() Number
```

返回代币的总供应量（单位：`cong`）。



### 7.6 func AddSupplyEnabled()

函数原型：

```
func (IToken) AddSupplyEnabled() bool
```

返回代币是否允许增发。



### 7.7 func BurnEnabled()

函数原型：

```
func (IToken) BurnEnabled() bool
```

返回代币是否允许燃烧。



### 7.8 func GasPrice()

函数原型：

```
func (IToken) GasPrice() int64
```

返回代币的燃料价格（单位：`cong`）。



### 7.9 func SetTotalSupply()

函数原型：

```
func (IToken) SetTotalSupply(newTotalSupply bn.Number)
```
设置代币新的总供应量。`newTotalSupply` 为代币新的总供应量（单位：`cong`），同时更新合约拥有者在该代币子账户上的余额。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 消息调用者不是合约的拥有者；
> - 参数 newTotalSupply 小于 1000000000(cong)；
> - 参数 newTotalSupply 大于原供应量，但代币不允许增发；
> - 参数 newTotalSupply 小于原供应量，但代币不允许燃烧；
> - 合约拥有者在该代币子账户上的余额在更新后小于0。



### 7.10 func SetGasPrice()

函数原型：

```
func (IToken) SetGasPrice(newGasPrice int64)
```

设置代币的燃料价格。`newGasPrice` 为代币新的燃料价格（单位：`cong`）。

满足如下任意一条则发生异常，当发生异常时，将会自动触发SDK进行 `panic`：

> - 消息调用者不是合约拥有者；
> - 参数 newGasPrice 大于 1000000000(cong)；
> - 参数 newGasPrice 小于基础燃料价格。




## 8 sdk/IHelper

接口 `sdk/IHelper` 封装了SDK所有的帮助对象。



### 8.1 func AccountHelper()

函数原型：

```
func (IHelper) AccountHelper() IAccountHelper
```

返回账户相关的帮助对象。



### 8.2 func BlockchainHelper()

函数原型：

```
func (IHelper) BlockChainHelper() IBlockChainHelper
```

返回区块链相关的帮助对象。



### 8.3 func BuildHelper()

函数原型：

```
func (IHelper) BuildHelper() IBuildHelper
```
返回合约构建相关的帮助对象。



### 8.4 func ContractHelper()

函数原型：

```
func (IHelper) ContractHelper() IContractHelper
```

返回智能合约相关的帮助对象。



### 8.5 func GenesisHelper()

函数原型：

```
func (IHelper) GenesisHelper() IGenesisHelper
```

返回创世相关的帮助对象。



### 8.6 func ReceiptHelper()

函数原型：

```
func (IHelper) ReceiptHelper() IReceiptHelper
```

返回收据相关的帮助对象。



### 8.7 func TokenHelper()

函数原型：

```
func (IHelper) TokenHelper() ITokenHelper
```

返回代币相关的帮助对象。



### 8.8 func StateHelper()

函数原型：

```
func (IHelper) StateHelper() IStateHelper
```

返回状态存储相关的帮助对象。



### 8.9 func IBCHelper()

函数原型：

```
func (IHelper) IBCHelper() IIBCHelper
```

返回发起跨链相关的帮助对象。



### 8.10 func IBCStubHelper()

函数原型：

```
func (IHelper) IBCStubHelper() IIBCStubHelper
```

返回处理跨链事务相关的帮助对象。




## 9 sdk/IAccountHelper

接口 `sdk/IAccountHelper` 封装了对区块链账户进行访问的帮助对象。



### 9.1 func AccountOf()

函数原型：

```
func (IAccountHelper) AccountOf(addr types.Address) IAccount
```

根据账户地址构造一个账户对象，用来对账户进行一些操作。`addr` 为账户地址。返回账户对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 参数 addr 不是地址。



### 9.2 func AccountOfPubKey()

函数原型：

```
func (IAccountHelper) AccountOfPubKey(pubkey types.PubKey) IAccount
```

根据账户公钥构造一个账户对象，用来对账户进行一些操作。pubkey 为账户公钥。返回账户对象。

满足如下任意一条则发生错误，当错误时，返回 nil：

> - 参数 pubkey 不是公钥（长度不等于32字节）。




## 10 sdk/IBlockChainHelper

接口 `sdk/IBlockChainHelper` 封装了对区块链进行访问的帮助对象。



### 10.1 func IsPeerChainAddress()

函数原型：

```
func (IBlockchainHelper) IsPeerChainAddress(address types.Address) bool
```

判断给定的地址 `address` 是否是外链地址，是则返回true，不是返回false。

满足如下任意一条则发生异常，当异常时，将会自动触发SDK进行 `panic`：

> 参数address不是合法的地址格式。



### 10.2 func IsSideChain()

函数原型：

```
func (IBlockchainHelper) IsSideChain() bool
```

判断当前链是否为侧链。是则返回true，不是返回false。



### 10.3 func CalcSideChainID()

函数原型：

```
func (IBlockchainHelper) CalcSideChainID(chainName string) string
```

根据链名称计算链ID。`chainName` 为链名称。返回计算得出的链ID。

满足如下任意一条则发生异常，当异常时，将会自动触发SDK进行 `panic`：

> 参数 chainName 不是合法的链名称格式。



### 10.4 func CalcAccountFromPubkey()

函数原型：

```
func (IBlockchainHelper) CalcAccountFromPubkey(pubkey types.PubKey) types.Address
```

根据公钥计算账户地址。`pubkey` 为公钥。返回计算得出的地址。

满足如下任意一条则发生错误，当错误时，返回空地址：

> 参数 pubkey 不是公钥（长度不等于32字节）。
>



### 10.5 func CalcAccountFromName()

函数原型：

```
func (IBlockchainHelper) CalcAccountFromName(name string, orgID string) types.Address
```

根据合约名称及其所属组织ID计算出合约的账户地址。`name` 为合约名称，`orgID` 为组织ID。返回计算得出的合约账户地址。



### 10.6 func CalcContractAddress()

函数原型：

```
func (IBlockchainHelper) CalcContractAddress(
                                name string, 
                                version string,
                                orgID string) types.Address
```

根据给定的合约参数计算合约地址。`name` 为合约名称。`version` 为合约版本。`orgID` 为合约所属组织的地址。返回计算得出的地址。



### 10.7 func RecalcAddress()

函数原型：

```
func (IBlockchainHelper) RecalcAddress(
								address types.Address, 
								chainID string) types.Address
```

根据给定的地址参数计算新地址。`address` 为新地址需要派生的旧地址。`chainID` 为新地址的前缀链ID。返回计算得出的地址。

满足如下任意一条则发生异常，当异常时，将会自动触发SDK进行 `panic`：

> 参数 address 不是合法的地址格式。



### 10.8 func CalcOrgID()

函数原型：

```
func CalcOrgID(name string) string
```

根据组织名称计算出组织标识。`name` 为组织名称。返回计算得出的组织标识。



### 10.9 func CheckAddress()

函数原型：

```
func (IBlockchainHelper) CheckAddress(addr types.Address) error
```

校验地址格式的合法性。`addr` 为地址。成功返回 `nil`。



### 10.10 func CheckAddressEx()

函数原型：

```
func (IBlockchainHelper) CheckAddressEx(chainID string, addr types.Address) error
```

校验地址格式的合法性。`chainID` 为链ID，地址必须以该链ID为前缀。`addr` 为地址。成功返回 `nil`。



### 10.11 func GetBlock()

函数原型：

```
func (IBlockChainHelper) GetBlock(height int64) IBlock
```

根据高度读取区块信息。`height` 为指定的区块高度。返回区块信息对象。如果输入的高度小于等于 `0`，则返回 `nil`，如果输入的高度没有保存区块信息或区块数据不正常，则返回一个该高度的区块信息对象，其它参数全部为空值。



### 10.12 func GetTx()

函数原型：

```
func (IBlockChainHelper) GetTx(txHash string) *std.TxResult
```

根据交易哈希读取交易信息。`txHash` 为指定的交易哈希。返回交易结果对象指针。如果输入的交易哈希为空或者没有对应的交易信息，则返回 `nil`。



### 10.13 func GetChainID()

函数原型：

```
func (IBlockChainHelper) GetChainID(address types.Address) string
```

从地址信息中提取链ID并返回。

满足如下任意一条则发生异常，当异常时，将会自动触发SDK进行 `panic`：

> 参数 address 不是合法的地址格式。



### 10.14 func GetMainChainID()

函数原型：

```
func (IBlockChainHelper) GetMainChainID() string
```

从当前链ID中获取主链ID并返回。



### 10.15 func FormatTime()

函数原型：

```
func (IBlockChainHelper) FormatTime(seconds int64, layout string) string
```

根据时间秒数格式化输出时间字符串。`seconds` 为时间秒数。`layout` 为格式化字符串。返回格式化后的时间。



### 10.16 func ParseTime()

函数原型：

```
func (IBlockChainHelper) ParseTime(layout, value string) (int64, error)
```

根据时间格式化字符串，进行格式化解析给定的时间值。`layout` 为格式化字符串。`value` 为时间值。返回时间值对应的秒数或者错误信息。

满足如下任意一条则发生错误，当错误时，返回空地址：

> 参数 value 不是 layout 指定的格式。




## 11 sdk/IBuildHelper

接口 `sdk/IBuildHelper` 封装了对智能合约进行构建的帮助对象。



### 11.1 func Build()

函数原型：

```
func (IBuildHelper) Build(meta std.ContractMeta) std.BuildResult
```

构建合约。
`meta` 为输入的合约元数据，`std.ContractMeta` 结构定义如下：

```
package std

type ContractMeta struct {
  	Name         string		   //合约名称
  	ContractAddr types.Address //合约地址
  	OrgID        string		   //合约所属组织ID
  	Version      string        //合约的版本
  	EffectHeight int64		   //合约生效高度
  	LoseHeight   int64		   //合约失效高度（固定为0）
  	CodeData     []byte		   //合约代码压缩包数据
  	CodeHash     []byte		   //合约代码的哈希
  	CodeDevSig   []byte		   //合约开发者对合约代码压缩包的签名数据
  	CodeOrgSig   []byte		   //组织对合约开发者的签名进行的签名数据
}
```

返回构建结果的详细信息。`std.BuildResult` 结构定义如下：

```
package std

type Method struct {
    MethodID     string        // 方法ID，方法ID的计算与方法原型相关
    Gas          int64         // 方法在调用时消耗的燃料
    ProtoType    string        // 方法原型
}

type BuildResult struct {
    Code         uint32		
    Error        string
    Methods      []Method      // 公开的方法列表
    Interfaces   []Method      // 公开的接口列表
    Mine         []Method      // 公开的挖矿接口
    OrgCodeHash  []byte        // 组织所有有效合约代码的哈希（编译以后的程序名称）
}
```
满足如下任意一条则导致失败，当失败时，返回 `BuildResult.Code != types.CodeOK (200)`：

> - 当前合约不是合约管理合约；
> - 当前合约所属组织不是创世组织；
> - 合约编译过程失败。




## 12 sdk/IContractHelper

接口 `sdk/IContractHelper` 封装了对智能合约进行访问的帮助对象。



### 12.1 func ContractOfAddress()

函数原型：

```
func (IContractHelper) ContractOfAddress(addr types.Address) IContract
```

根据合约地址构造一个合约对象并读取合约信息，用来对合约进行一些操作。`addr` 为合约地址。返回合约对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 参数 addr 不是地址；
> - 参数 addr 不是合约。



### 12.2 func ContractOfToken()

函数原型：

```
func (IContractHelper) ContractOfToken(tokenAddr types.Address) IContract
```

根据代币地址构造一个针对该代币的合约对象并读取当前有效版本的合约信息，用来对合约进行一些操作。`tokenAddr` 为代币地址。返回合约对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 参数 tokenAddr 不是地址；
> - 参数 tokenAddr 不是代币。



### 12.3 func ContractOfName()

函数原型：

```
func (IContractHelper) ContractOfName(name string) IContract
```

根据合约名称构造一个合约对象并读取合约信息，用来对合约进行一些操作。`name` 为合约名称。返回合约对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 参数 name 为空串；
> - 参数 name 不是合约。




## 13 sdk/IReceiptHelper

接口 `sdk/IReceiptHelper` 封装了对收据进行处理的帮助对象。



### 13.1 func Emit()

函数原型：

```
func (IReceiptHelper) Emit(interface Interface{})
```

发送一个收据，SDK底层实现会自动将传入的收据对象进行序列化作为本次调用合约的输出收据集中的一员。`interface` 为收据对象。

SDK辅助工具会自动将智能合约定义的收据生成相关代码调用 `Emit()` 函数，合约代码中可以不用直接使用这个函数。示例如下：

```
//@:public:receipt
type receipt interface {
	emitTransferMyCoin(token, from, to types.Address, value bn.Number)
}

func (mc *Mycoin) Transfer(to types.Address, value bn.Number) {
    .
    .
    .
    mc.emitTransferMyCoin(
	  mc.sdk.Message().Contract().Address(),
	  sender,
	  receiver,
	  value,
	)
}
```




## 14 sdk/IGenesisHelper

接口 `sdk/IGenesisHelper` 封装了对创世信息进行访问的帮助对象。



### 14.1 func ChainID()

函数原型：

```
func (IGenesisHelper) ChainID() string
```

返回创世时指定的区块链ID。



### 14.2 func OrgID()

函数原型：

```
func (IGenesisHelper) OrgID() string

```

返回创世时指定的创世组织ID。



### 14.3 func Contracts()

函数原型：

```
func (IGenesisHelper) Contracts() []IContract
```

返回创世时部署的智能合约对象列表。



### 14.4 func Token()

函数原型：

```
func (IGenesisHelper) Token() IToken
```

返回创世时指定的创世通证对象。



### 14.5 func GasPriceRatio()

函数原型：

```
func (IGenesisHelper) GasPriceRatio() uint64
```

返回创世时指定的燃料价格比例值，默认返回1000（单位为：‰）。




## 15 sdk/ITokenHelper

接口 `sdk/ITokenHelper` 封装了对 BRC20 标准代币进行访问的帮助对象。



### 15.1 func RegisterToken()

函数原型：

```
func (ITokenHelper) RegisterToken(name string, 
                                  symbol string, 
                                  totalSupply Number,
                                  addSupplyEnabled bool,
                                  burnEnabled bool) IToken
```

向 BCBChain 区块链注册一个 `BRC20` 标准代币。`name` 为代币名称，`symbol` 为代币符号，`totalSupply`  为总的供应量（单位：`cong`），`addSupplyEnabled` 为是否允许增发，`burnEnabled` 为是否允许燃烧。注册成功返回对应的代币对象。

满足如下任意一条则注册失败，返回 `nil`：

> - 消息调用的发起人不是合约的拥有者；
> - 参数 name 的长度不在 [3,40] 的范围内；
> - 参数 name 对应的代币已经存在；
> - 参数 symbol 的长度不在 [3,20] 的范围内；
> - 参数 symbol 对应的代币已经存在；
> - 参数 totalSupply 小于 1000000000(cong)；
> - 合约以前已经注册过一个 BRC20 标准代币；
> - 当前合约未定义标准转账方法或标准转账接口。



### 15.2 func Token()

函数原型：

```
func (ITokenHelper) Token() IToken
```

返回当前合约所注册的代币信息，用来对代币进行一些操作。返回代币对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 当前合约没有注册代币。



### 15.3 func TokenOfAddress()

函数原型：

```
func (ITokenHelper) TokenOfAddress(tokenAddr types.Address) IToken
```

根据代币地址获取代币的信息，用来对代币进行一些操作。`tokenAddr` 为代币地址。返回代币对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 参数 tokenAddr 不是地址；
> - 参数 tokenAddr 不是代币。



### 15.4 func TokenOfName()

函数原型：

```
func (ITokenHelper) TokenOfName(name string) IToken
```

按代币名称获取代币的信息，用来对代币进行一些操作。`name` 为代币名称。返回代币对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 参数 name 不是一个代币的名称。



### 15.5 func TokenOfSymbol()

函数原型：

```
func (ITokenHelper) TokenOfSymbol(symbol string) IToken
```

按代币符号获取代币的信息，用来对代币进行一些操作。`symbol` 为代币符号。返回代币对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 参数 symbol 不是一个代币的符号。



### 15.6 func TokenOfContract()

函数原型：

```
func (ITokenHelper) TokenOfContract(contractAddr types.Address) IToken
```

根据合约地址获取该合约所注册的代币的信息，用来对代币进行一些操作。`contractAddr` 为合约地址。返回代币对象。

满足如下任意一条则发生错误，当错误时，返回 `nil`：

> - 参数 contractAddr 不是地址；
> - 参数 contractAddr 不是一个合约；
> - 参数 contractAddr 对应的合约没有注册代币。



### 15.7 func BaseGasPrice()

函数原型：

```
func (ITokenHelper) BaseGasPrice() int64
```

返回基础燃料价格（单位：`cong`）。



### 15.7 func CheckActivate()

函数原型：

```
func (ITokenHelper) CheckActivate(address types.Address) error
```

判断指定地址对应的侧链是否已经激活当前合约代币。`address` 为普通账户地址。已激活返回nil。

满足如下任意一条则发生异常，当异常时，将会自动触发SDK进行 `panic`：

> 参数 address 不是合法的地址格式。

满足如下任意一条则发生错误，当错误时，返回 对应的错误对象：

> - 当前合约没有发行代币，返回错误信息： this contract not exist token；
> - 对应侧链未激活当前合约对应的代币，返回错误信息：chain: *chainName* never activate current token；




## 16 sdk/IStateHelper

接口 `sdk/IStateHelper` 封装了对存储状态进行访问的帮助对象。



### 16.1 func Check()

函数原型：

```
func (IStateHelper) Check(key string) bool
```

根据给定的KEY值，检测在智能合约被许可的范围内是否存在KEY值指定的数据。`key` 为KEY值。



### 16.2 func Get()

函数原型：

```
func (IStateHelper) Get(key string, defaultData Interface{}) Interface{}
func (IStateHelper) GetEx(key string, defaultData Interface{}) Interface{}
```

根据给定的KEY值，在智能合约被许可的范围内读取数据。`key` 为KEY值，`defaultData` 为Value对应存储对象类型的模板或默认值。如果数据不存在则 `Get()` 返回 `nil`， `GetEx()` s返回默认值。

下面是一些对基础类型封装的简便读取函数：

```
func (IStateHelper) GetInt(key string) int
func (IStateHelper) GetInt8(key string) int8
func (IStateHelper) GetInt16(key string) int16
func (IStateHelper) GetInt32(key string) int32
func (IStateHelper) GetInt64(key string) int64
func (IStateHelper) GetUint(key string) uint
func (IStateHelper) GetUint8(key string) uint8
func (IStateHelper) GetUint16(key string) uint16
func (IStateHelper) GetUint32(key string) uint32
func (IStateHelper) GetUint64(key string) uint64
func (IStateHelper) GetByte(key string) byte
func (IStateHelper) GetBool(key string) bool
func (IStateHelper) GetString(key string) string

func (IStateHelper) GetInts(key string) []int
func (IStateHelper) GetInt8s(key string) []int8
func (IStateHelper) GetInt16s(key string) []int16
func (IStateHelper) GetInt32s(key string) []int32
func (IStateHelper) GetInt64s(key string) []int64
func (IStateHelper) GetUints(key string) []uint
func (IStateHelper) GetUint8s(key string) []uint8
func (IStateHelper) GetUint16s(key string) []uint16
func (IStateHelper) GetUint32s(key string) []uint32
func (IStateHelper) GetUint64s(key string) []uint64
func (IStateHelper) GetBytes(key string) []byte
func (IStateHelper) GetBools(key string) []bool
func (IStateHelper) GetStrings(key string) []string
```

以上函数如果从状态数据库中读不到数据，直接返回对应基础类型的默认值。



### 16.3 func Set()

函数原型：

```
func (IStateHelper) Set(key string, data Interface{})
```

将输入的数据保存到状态数据库智能合约被允许的KEY值下。`key` 为KEY值，`data` 为要保存的数据对象。

下面是一些对基础类型封装的简便设置函数：

```
func (IStateHelper) SetInt(key string, v int)
func (IStateHelper) SetInt8(key string, v int8)
func (IStateHelper) SetInt16(key string, v int16)
func (IStateHelper) SetInt32(key string, v int32)
func (IStateHelper) SetInt64(key string, v int64)
func (IStateHelper) SetUint(key string, v uint)
func (IStateHelper) SetUint8(key string, v uint8)
func (IStateHelper) SetUint16(key string, v uint16)
func (IStateHelper) SetUint32(key string, v uint32)
func (IStateHelper) SetUint64(key string, v uint64)
func (IStateHelper) SetByte(key string, v byte)
func (IStateHelper) SetBool(key string, v bool)
func (IStateHelper) SetString(key string, v string)

func (IStateHelper) SetInts( key string, v []int )
func (IStateHelper) SetInt8s( key string, v []int8 )
func (IStateHelper) SetInt16s( key string, v []int16 )
func (IStateHelper) SetInt32s( key string, v []int32 )
func (IStateHelper) SetInt64s( key string, v []int64 )
func (IStateHelper) SetUints( key string, v []uint )
func (IStateHelper) SetUint8s( key string, v []uint8 )
func (IStateHelper) SetUint16s( key string, v []uint16 )
func (IStateHelper) SetUint32s( key string, v []uint32 )
func (IStateHelper) SetUint64s( key string, v []uint64 )
func (IStateHelper) SetBytes(key string, v []byte)
func (IStateHelper) SetBools( key string, v []bool )
func (IStateHelper) SetStrings( key string, v []string )
```

将输入的数据保存到状态数据库智能合约被允许的KEY值下。`key` 为KEY值， `v` 为基础类型数据值。



### 16.4 func Delete()

函数原型：

```
func (IStateHelper) Delete(key string)
```

在状态数据库中删除 `key` 值对应的数据。



### 16.5 func Flush()

函数原型：

```
func (IStateHelper) Flush()
```

将对状态数据库的更新刷新到数据库层，不关闭事务。



### 16.6 func McCheck()

函数原型：

```
func (sh *StateHelper) McCheck(key string) bool
```

根据给定的KEY值，检测在智能合约被许可的范围内是否存在KEY值指定的数据，包括缓存与数据库。`key` 为KEY值，如果存在将被自动加载到缓存中来。



### 16.7 func McGet()

函数原型：

```
func (IStateHelper) McGet(key string, defaultData Interface{}) Interface{}
func (IStateHelper) McGetEx(key string, defaultData Interface{}) Interface{}
```

根据给定的KEY值，在智能合约被许可的范围内读取数据，并将数据缓存在内存中，在后续智能合约的调用消息中可以直接从内存中读取，而不需要再次访问数据库。`key` 为KEY值，`defaultData` 为Value对应存储对象类型的模板或默认值。如果数据不存在则 `McGet()`返回 `nil`， `McGetEx()`返回默认值。

下面是一些对基础类型封装的简便读取函数：

```
func (IStateHelper) McGetInt(key string) int
func (IStateHelper) McGetInt8(key string) int8
func (IStateHelper) McGetInt16(key string) int16
func (IStateHelper) McGetInt32(key string) int32
func (IStateHelper) McGetInt64(key string) int64
func (IStateHelper) McGetUint(key string) uint
func (IStateHelper) McGetUint8(key string) uint8
func (IStateHelper) McGetUint16(key string) uint16
func (IStateHelper) McGetUint32(key string) uint32
func (IStateHelper) McGetUint64(key string) uint64
func (IStateHelper) McGetByte(key string) byte
func (IStateHelper) McGetBool(key string) bool
func (IStateHelper) McGetString(key string) string

func (IStateHelper) McGetInts(key string) []int
func (IStateHelper) McGetInt8s(key string) []int8
func (IStateHelper) McGetInt16s(key string) []int16
func (IStateHelper) McGetInt32s(key string) []int32
func (IStateHelper) McGetInt64s(key string) []int64
func (IStateHelper) McGetUints(key string) []uint
func (IStateHelper) McGetUint8s(key string) []uint8
func (IStateHelper) McGetUint16s(key string) []uint16
func (IStateHelper) McGetUint32s(key string) []uint32
func (IStateHelper) McGetUint64s(key string) []uint64
func (IStateHelper) McGetBytes(key string) []byte
func (IStateHelper) McGetBools(key string) []bool
func (IStateHelper) McGetStrings(key string) []string
```

以上函数如果从状态数据库中读不到数据，直接返回对应基础类型的默认值。



### 16.8 func McSet()

函数原型：

```
func (IStateHelper) McSet(key string, data Interface{})
```

将输入的数据保存到状态数据库智能合约被允许的KEY值下，同时更新内存缓存，在后续智能合约的调用消息中可以直接从内存中读取，而不需要再次访问数据库。`key` 为KEY值，`data` 为要保存的数据对象。

下面是一些对基础类型封装的简便设置函数：

```
func (IStateHelper) McSetInt(key string, v int)
func (IStateHelper) McSetInt8(key string, v int8)
func (IStateHelper) McSetInt16(key string, v int16)
func (IStateHelper) McSetInt32(key string, v int32)
func (IStateHelper) McSetInt64(key string, v int64)
func (IStateHelper) McSetUint(key string, v uint)
func (IStateHelper) McSetUint8(key string, v uint8)
func (IStateHelper) McSetUint16(key string, v uint16)
func (IStateHelper) McSetUint32(key string, v uint32)
func (IStateHelper) McSetUint64(key string, v uint64)
func (IStateHelper) McSetByte(key string, v byte)
func (IStateHelper) McSetBool(key string, v bool)
func (IStateHelper) McSetString(key string, v string)

func (IStateHelper) McSetInts( key string, v []int )
func (IStateHelper) McSetInt8s( key string, v []int8 )
func (IStateHelper) McSetInt16s( key string, v []int16 )
func (IStateHelper) McSetInt32s( key string, v []int32 )
func (IStateHelper) McSetInt64s( key string, v []int64 )
func (IStateHelper) McSetUints( key string, v []uint )
func (IStateHelper) McSetUint8s( key string, v []uint8 )
func (IStateHelper) McSetUint16s( key string, v []uint16 )
func (IStateHelper) McSetUint32s( key string, v []uint32 )
func (IStateHelper) McSetUint64s( key string, v []uint64 )
func (IStateHelper) McSetBytes(key string, v []byte)
func (IStateHelper) McSetBools( key string, v []bool )
func (IStateHelper) McSetStrings( key string, v []string )
```

将输入的数据保存到状态数据库智能合约被允许的KEY值下，同时更新内存缓存，在后续智能合约的调用消息中可以直接从内存中读取，而不需要再次访问数据库。`key` 为KEY值，`v` 为基础类型数据值。



### 16.9 func McClear()

函数原型：

```
func (IStateHelper) McClear(key string)
```

清除内存缓存中指定的数据（保留状态数据库中的数据）。`key` 为KEY值。



### 16.10 func McDelete()

函数原型：

```
func (IStateHelper) McDelete(key string)
```

在状态数据库中删除 `key` 值对应的数据，同时从缓存中清除 `key` 值对应的数据。



## 17 sdk/IIBCHelper

接口 `sdk/IIBCHelper` 封装了发起跨链交易或通知的帮助对象。



### 17.1 func IbcHash()

函数原型：

```
func (IIBCHelper) IbcHash(toChainID string) types.Hash
```

根据目标链ID、当前链ID和当前交易Hash计算跨链事务Hash。`toChainID` 为目标链ID。



### 17.2 func Run()

函数原型：

```
func (IIBCHelper) Run(f func()) IIBCHelper
```

执行需要产生跨链收据的代码段，返回当前对象。`f` 为封装代码段的函数。



### 17.3 func Register()

函数原型：

```
func (IIBCHelper) Register(toChainID string)
```

注册跨链事务。`toChainID` 为目标链ID值。

当满足如下任一条件时产生异常，当异常时，将会自动触发SDK进行 `panic`：

> - 调用该接口的合约接口被跨合约调用。
> - 链未部署IBC合约或IBC合约未生效。
> - IBC合约的事务注册接口处理产生错误。



### 17.4 func Notify()

函数原型：

```
func (IIBCHelper) Notify(toChainIDs []string)
```

发起跨链通知。`toChainIDs` 为目标链ID列表值。

当满足如下任一条件时产生异常，当异常时，将会自动触发SDK进行 `panic`：

> - 调用该接口的合约接口被跨合约调用。
> - 目标链ID列表中的所有元素都为无效链ID。
> - 链未部署IBC合约或IBC合约未生效。
> - IBC合约的事务注册接口处理产生错误。



### 17.5 func Broadcast()

函数原型：

```
func (IIBCHelper) Broadcast() types.Hash
```

发起跨链广播。

当满足如下任一条件时产生异常，当异常时，将会自动触发SDK进行 `panic`：

> - 调用该接口的合约接口被跨合约调用。
> - 链未部署IBC合约或IBC合约未生效。
> - IBC合约的事务注册接口处理产生错误。



### 17.6 func CalcBlockHash()

函数原型：

```
func (IIBCHelper) CalcBlockHash(h *ibc.Header) types.Hash
```

根据区块头计算区块Hash。`h` 为区块头对象。

当满足如下任一条件时产生异常，当异常时，将会自动触发SDK进行 `panic`：

> - 区块头对象为nil。
> - 区块头中的时间字符串不是正确的格式。



### 17.7 func CalcQueueHash()

函数原型：

```
func (IIBCHelper) CalcQueueHash(packet ibc.Packet, lastQueueHash types.Hash) types.Hash
```

根据消息数据及上一个队列Hash计算队列当前节点Hash。`packet` 为当前消息值。`lastQueueHash` 为上一个Hash队列节点。



### 17.8 func VerifyPrecommit()

函数原型：

```
func (IIBCHelper) VerifyPrecommit(
							pubKey types.PubKey, 
							precommit ibc.Precommit, 
							chainID string, 
							height int64) bool
```

校验区块证明数据。`pubKey` 为发起链验证者节点公钥值。`precommit` 为发起链验证者节点投票数据。`chainID` 为发起链ID。`height` 为发起链发起跨链事务证明数据的区块高度。

当满足如下任一条件时产生异常，当异常时，将会自动触发SDK进行 `panic`：

> - 投票信息中的时间字符串不是正确的格式。



## 18 sdk/IIBCStubHelper

接口 `sdk/IIBCStubHelper` 封装了处理跨链事务的帮助对象，理论上合约中并不需要使用该对象。



### 18.1 func Recast()

函数原型：

```
func Recast(ibcHash types.HexBytes, 
			orgID, contractName string, 
			receipts []types.KVPair) (bool, []types.KVPair, types.Error)
```

资产重铸接口。`ibcHash` 为跨链事务Hash值。`orgID` 为应用合约所属组织。`contractName` 为应用合约名称。 `receipts` 为跨链收据信息。



### 18.2 func Confirm()

函数原型：

```
func Confirm(	ibcHash types.HexBytes, 
				orgID, contractName string, 
				receipts []types.KVPair) ([]types.KVPair, types.Error)
```

跨链事务确认接口。`ibcHash` 为跨链事务Hash值。`orgID` 为应用合约所属组织。`contractName` 为应用合约名称。 `receipts` 为跨链收据信息。



### 18.3 func Cancel()

函数原型：

```
func Cancel(ibcHash types.HexBytes, 
			orgID, contractName string, 
			receipts []types.KVPair) ([]types.KVPair, types.Error)
```

跨链事务取消接口。`ibcHash` 为跨链事务Hash值。`orgID` 为应用合约所属组织。`contractName` 为应用合约名称。 `receipts` 为跨链收据信息。



### 18.4 func TryRecast()

函数原型：

```
func TryRecast(	ibcHash types.HexBytes, 
				orgID, contractName string, 
				receipts []types.KVPair) (bool, []types.KVPair, types.Error)
```

跨链资产预重铸接口。`ibcHash` 为跨链事务Hash值。`orgID` 为应用合约所属组织。`contractName` 为应用合约名称。 `receipts` 为跨链收据信息。



### 18.5 func ConfirmRecast()

函数原型：

```
func ConfirmRecast(	ibcHash types.HexBytes, 
					orgID, contractName string, 
					receipts []types.KVPair) ([]types.KVPair, types.Error)
```

跨链事务中转确认接口。`ibcHash` 为跨链事务Hash值。`orgID` 为应用合约所属组织。`contractName` 为应用合约名称。 `receipts` 为跨链收据信息。



### 18.6 func CancelRecast()

函数原型：

```
func CancelRecast(	ibcHash types.HexBytes, 
					orgID, contractName string, 
					receipts []types.KVPair) ([]types.KVPair, types.Error)
```

跨链事务中转取消接口。`ibcHash` 为跨链事务Hash值。`orgID` 为应用合约所属组织。`contractName` 为应用合约名称。 `receipts` 为跨链收据信息。



### 18.7 func Notify()

函数原型：

```
func Notify(ibcHash types.HexBytes, 
			orgID, contractName string, 
			receipts []types.KVPair) ([]types.KVPair, types.Error)
```

跨链通知接口。`ibcHash` 为跨链事务Hash值。`orgID` 为应用合约所属组织。`contractName` 为应用合约名称。 `receipts` 为跨链收据信息。