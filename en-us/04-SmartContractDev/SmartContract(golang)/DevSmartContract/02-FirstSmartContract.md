# First Smart Contract

## 1. Create a new contract

Let's start by creating the first smart contract.

Using ```GoLand``` open the ```GoLand Project``` you just created and create a new smart contract with the BCBChain plugin. The following is the execution path:

```text
GoLand left sidebar Project Explorer
    >> Right click on the src/contract directory to bring up the menu
        >> BCB Smart Contract
            >> New...
                >> Input  Name         #demo1
                >> Input  Type         #Demo1
                >> Input  Version       #1.0
                >> Input  Organization #orgE37w7wxhZwaox1fhndt5Czm8WnLBrh6db - DAO
                >> Input  Author       #alice
                >> OK
```

Successful creation of the smart contract will automatically generate the framework code. The file path is as follows:

```text
src/contract/mydonation/v1.0/mydonation/mydonation.go
```

The initial code for the smart contract is as follows:

```go
package mydonation

import (
    "blockchain/smcsdk/sdk"
)

//Mydonation This is struct of contract
//@:contract:mydonation
//@:version:1.0
//@:organization:orgE37w7wxhZwaox1fhndt5Czm8WnLBrh6db
//@:author:e5b95784049c3b8669aa58ba08abd9f54281df8905dd3af24bf795b0103f9ec7
type Mydonation struct {
    sdk sdk.ISmartContract

    //This is a sample field which is to store in db
    //@:public:store
    sampleStore string
}

//InitChain Constructor of this Mydonation
//@:constructor
func (m *Mydonation) InitChain() {
    //TODO
    //This method is automatically selected when the block height reaches
    //the contract effective block height.
}

//UpdateChain Constructor of this Mydonation
//@:constructor
func (m *Mydonation) UpdateChain() {
    //TODO
    //This method is automatically selected when the block height reaches
    //the new version contract effective block height.
}

//SampleMethod This is a sample method
//@:public:method:gas[500]
func (m *Mydonation) SampleMethod() {

}
```

## 2. Donation Contract

Let's modify the smart contract to make it more interesting. The following smart contract code contains a set of simple functions for charitable donations. The modified code is as follows:

```go
package mydonation

import (
    "blockchain/smcsdk/sdk"
    "blockchain/smcsdk/sdk/bn"
    "blockchain/smcsdk/sdk/forx"
    "blockchain/smcsdk/sdk/std"
    "blockchain/smcsdk/sdk/types"
)

//Mydonation This is struct of contract
//@:contract:mydonation
//@:version:1.0
//@:organization:orgE37w7wxhZwaox1fhndt5Czm8WnLBrh6db
//@:author:e5b95784049c3b8669aa58ba08abd9f54281df8905dd3af24bf795b0103f9ec7
type Mydonation struct {
    sdk sdk.ISmartContract

    //Total donations received by donees
    //@:public:store
    donations map[types.Address]bn.Number // key=address of donee
}

const (
    errDoneeCannotBeOwner = 55000 + iota,
    errDoneeCannotBeSmc,
    errDoneeAlreadyExist,
    errDoneeNotExist,
    errDonationExist,
    errDonationNotEnough
)

//@:public:receipt
type receipt interface {
    emitAddDonee(donee types.Address)
    emitDelDonee(donee types.Address)
    emitDonate(from, donee types.Address, value, balance bn.Number)
    emitTransferDonation(donee types.Address, value, balance bn.Number)
}

//InitChain Constructor of this Mydonation
//@:constructor
func (m *Mydonation) InitChain() {
    //TODO
    //This method is automatically selected when the block height reaches
    //the contract effective block height.
}

//UpdateChain Constructor of this Mydonation
//@:constructor
func (m *Mydonation) UpdateChain() {
    //TODO
    //This method is automatically selected when the block height reaches
    //the new version contract effective block height.
}

//AddDonee Add a new donee
//@:public:method:gas[500]
func (d *Mydonation) AddDonee(donee types.Address) {
    sdk.RequireOwner()
    sdk.RequireAddress(donee)
    sdk.Require(donee != d.sdk.Message().Sender().Address(),
        errDoneeCannotBeOwner, "Donee can not be owner")
    sdk.Require(donee != d.sdk.Message().Contract().Address(),
        errDoneeCannotBeSmc, "Donee can not be this smart contract")
    sdk.Require(donee != d.sdk.Message().Contract().Account().Address(),
        errDoneeCannotBeSmc, "Donee can not be account of this smart contract")
    sdk.Require(!d._chkDonations(donee),
        errDoneeAlreadyExist, "Donee already exists")

    d._setDonations(donee, bn.N(0))

    //emit receipt
    d.emitAddDonee(donee)
}

//Donate delete a donee
//@:public:method:gas[500]
func (d *Mydonation) DelDonee(donee types.Address) {
    sdk.RequireOwner()
    sdk.RequireAddress(donee)
    sdk.Require(d._chkDonations(donee),
        errDoneeNotExist, "Donee does not exist")
    sdk.Require(d._donations(donee).IsEqualI(0),
        errDonationExist, "Donation exists")

    d._delDonations(donee)

    //emit receipt
    d.emitDelDonee(donee)
}

//Donate Charitable donors donate money to smart contract
//@:public:method:gas[500]
func (d *Mydonation) Donate(donee types.Address) {
    sdk.RequireAddress(donee)
    sdk.Require(d._chkDonations(donee),
        errDoneeNotExist, "Donee does not exist")

    var valTome *std.Transfer
    token := d.sdk.Helper().GenesisHelper().Token()
    forx.Range(d.sdk.Message().GetTransferToMe(), func(i int, receipt *std.Transfer) {
        sdk.Require(receipt.Token == token.Address(),
            types.ErrInvalidParameter, "Accept donations in genesis token only")
        sdk.Require(valTome == nil,
            types.ErrInvalidParameter, "Accept only one donation at a time")
        valTome = receipt
    })
    sdk.Require(valTome != nil,
        types.ErrInvalidParameter, "Please transfer token to me first")

    balance := d._donations(donee).Add(valTome.Value)
    d._setDonations(donee, balance)

    //emit receipt
    d.emitDonate(
        d.sdk.Message().Sender().Address(),
        donee,
        valTome.Value,
        balance,
    )
}

//Withdraw To transfer donations to donee
//@:public:method:gas[500]
func (d *Mydonation) Transfer(donee types.Address, value bn.Number) {
    sdk.RequireOwner()
    sdk.RequireAddress(donee)
    sdk.Require(d._chkDonations(donee),
        errDoneeNotExist, "Donee does not exist")
    sdk.Require(value.IsGreaterThanI(0),
        types.ErrInvalidParameter, "Parameter \"value\" must be greater than 0")
    sdk.Require(d._donations(donee).IsGE(value),
        errDonationNotEnough, "Donation is not enough")

    token := d.sdk.Helper().GenesisHelper().Token()
    account := d.sdk.Message().Contract().Account()
    account.TransferByToken(token.Address(), donee, value)
    balance := d._donations(donee).Sub(value)
    d._setDonations(donee, balance)

    //emit receipt
    d.emitTransferDonation(
        donee,
        value,
        balance,
    )
}
```

Let's briefly describe the methods provided by this contract.

### 2.1 AddDonee

The ```AddDonee``` method adds an account address for accepting donations to the smart contract.

Constraint is as follows:

> * Only the contract owner can call;
> * The input parameter  ```donee``` must be a legal address;
> * The input parameter  ```donee``` cannot be the contract owner;
> * The input parameter  ```donee``` cannot be the contract address;
> * The input parameter  ```donee``` cannot be the contract account address;
> * The input parameter  ```donee``` cannot be an existing account address for receiving donations.

Execution results:

> * State Database:
>
>   Creates a new KEY: ```/orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer/mydonation/xxx```,where ```xxx```is the address corresponding to the input parameter ```donee```,Value：```0```；
>
> * BCBChain：
>
>   Results of successful transaction execution can be scanned, which includes receipts ```addDonee```:
>
>   ```go
>    type addDonee struct {
>        Donee types.Address `json:"donee"`
>    }
>    ```

### 2.2 DelDonee

The ```DelDonee``` method deletes an account address that receives donations from the smart contract.

Constraint is as follows:

> - Only the contract owner can call;
> - The input parameter ```donee``` must be a legal address;
> - The input parameter ```donee``` must be an existing account address for receiving donations;
> - The input parameter ```donee```'s all donations received have been withdrawn or no donations have been received.

Results of execution:

> - State Database:
>
>   Deletes the KEY:```/orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer/mydonation/xxx```,where  ```xxx``` is the address corresponding to the input parameter ```donee```；
>
> - BCBChain：
>
>   Results of successful transaction execution can be scanned, which includes receipts:
>
>   ```go
>   type delDonee struct {
>       Donee types.Address `json:"donee"`
>   }
>   ```

### 2.3 Donate

The ```Donate``` method makes a donation to an account address in the smart contract that accepts donations.

Constraint is as follows:

> - Anyone can call;
> - The input parameter ```donee``` must be a legal address;
> - The input parameter ```donee``` must be an existing account address for receiving donations;
> - The call to the ```Donate``` method must be preceded by a transfer message that passes the transfer receipt to the ```Donate``` method;
> - The destination address of the received transfer receipt must be the account address of ```mydonation``` contract；
> - The donation received must be the ```BCB``` token on BCBChain；
> - Only one donation (transfer receipt) meeting the above conditions can be received.

Results of execution:

> - State Database:
>
>   Updates the KEY: ```/orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer/mydonation/xxx```,where  ```xxx``` is the address corresponding to the input parameter ```donee``` , Value: increase the value corresponding to the transfer amount;
>
> - BCBChain：
>
>   Results of successful transaction execution can be scanned, which includes receipts:
>
>   ```go
>   type donate struct {
>       From    types.Address `json:"from"`
>       Donee   types.Address `json:"donee"`
>       Value   bn.Number     `json:"value"`
>       Balance bn.Number     `json:"balance"`
>   }
>   ```

### 2.4 Transfer

The ```Transfer``` method transfers the donation received from the smart contract to the account address receiving the donation.

Constraint is as follows:

> - Only the contract owner can call;
> - The input parameter ```donee``` must be a legal address;
> - The input parameter ```donee``` must be an existing account address for receiving donations;
> - The input parameter ```value``` must be greater than or equal to ```0```;
> - The accepted donation balance at the address corresponding to the input parameter ```donee``` must be greater than or equal to the input parameter ```value```.

Results of execution:

> - State Database:
>
>   Updates the KEY: ```/orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer/mydonation/xxx```,where ```xxx``` is the address corresponding to the input parameter ```donee```, Value: subtract the value corresponding to the input parameter ```value```;
>
>   Updates the KEY: ```/account/ex/xxx/token/yyy```, where ```xxx``` is the address corresponding to the input parameter donee, ```yyy``` is the BCB token address on ```BCBChain```, Value: add the value corresponding to the input parameter ```value``` to the account balance.
>
> - BCBChain：
>
>   Results of successful transaction execution can be scanned, which includes receipts:
>
>   ```go
>   type transferDonation struct {
>       Donee   types.Address `json:"donee"`
>       Value   bn.Number     `json:"value"`
>       Balance bn.Number     `json:"balance"`
>   }
>
>   type std.Transfer struct {
>       Token types.Address `json:"token"` // Token types.Address
>       From  types.Address `json:"from"`  // Account address of Sender
>       To    types.Address `json:"to"`    // Account address of Receiver
>       Value bn.Number     `json:"value"` // Transfer value
>   }
>   ```

## 3. Contract specification check

The following execution path can check whether the charitable donation contract completed above conforms to the BCBChain smart contract specification:

```text
GoLand left sidebar Project Explorer
    >> Right click on the src/contract/mydonation/v1.0/mydonation directory to bring up
       the menu
            >> BCB Smart Contract
                >> Check
```

## 4. Contract code completion

So far, we have completed the contract code which will be uploaded to the ```BCBChain```, but this contract code cannot be directly run in ```Goland IDE```, and can only be run locally after completing the code using the code generation function provided by the plugin, the following is the execution path of the completion code:

```text
GoLand left sidebar Project Explorer
    >> Right click on the src/contract/mydonation/v1.0/mydonation directory to bring up
       the menu
            >> BCB Smart Contract
                >> Generate Code
```

After the completion code is executed, the following code files will be automatically generated in the contract code directory:

```text
//The following files will overwrite the original contents every time the code is
//automatically generated. Please do not modify these code files.
mydonation_autogen_store.go            //Auto-completed code for state database accessing
mydonation_autogen_receipt.go        //Auto-completed code for receipts
mydonation_autogen_sdk.go            //Auto-completed code for miscellaneous
mydonation_wrap_test.go                //Auto-completed code for unit test

//The following files are codes for unit testing, which require programmers to complete
//the unit tests for each method. The contents of these files will not be automatically
//modified the next time the code is automatically generated.
mydonation_case_adddonee_test.go    //Auto-completed unit test code -  for AddDonee
mydonation_case_deldonee_test.go    //Auto-completed unit test code -  for DelDonee
mydonation_case_donate_test.go        //Auto-completed unit test code -  for Donate
mydonation_case_transfer_test.go    //Auto-completed unit test code -  for Transfer
```

The following is the content of  ```mydonation_autogen_store.go```:

```go
package mydonation

import (
    "fmt"
    "blockchain/smcsdk/sdk/types"
    "blockchain/smcsdk/sdk/bn"
)

//_setDonations This is a method of Mydonation
func (m *Mydonation) _setDonations(k types.Address, v bn.Number) {
    m.sdk.Helper().StateHelper().Set(fmt.Sprintf("/donations/%v", k), &v)
}

//_donations This is a method of Mydonation
func (m *Mydonation) _donations(k types.Address) bn.Number {
    temp := bn.N(0)
    return *m.sdk.Helper().StateHelper().GetEx(fmt.Sprintf("/donations/%v", k), &temp).(*bn.Number)
}

//_chkDonations This is a method of Mydonation
func (m *Mydonation) _chkDonations(k types.Address) bool {
    return m.sdk.Helper().StateHelper().Check(fmt.Sprintf("/donations/%v", k))
}

//_delDonations This is a method of Mydonation
func (m *Mydonation) _delDonations(k types.Address) {
    m.sdk.Helper().StateHelper().Delete(fmt.Sprintf("/donations/%v", k))
}
```

The following is the content of ```mydonation_autogen_receipt.go```: 

```go
package mydonation

import (
    "blockchain/smcsdk/sdk/types"
    "blockchain/smcsdk/sdk/bn"
)

var _ receipt = (*Mydonation)(nil)

//emitAddDonee This is a method of Mydonation
func (m *Mydonation) emitAddDonee(donee types.Address) {
    type addDonee struct {
        Donee types.Address `json:"donee"`
    }

    m.sdk.Helper().ReceiptHelper().Emit(
        addDonee{
            Donee: donee,
        },
    )
}

//emitDelDonee This is a method of Mydonation
func (m *Mydonation) emitDelDonee(donee types.Address) {
    type delDonee struct {
        Donee types.Address `json:"donee"`
    }

    m.sdk.Helper().ReceiptHelper().Emit(
        delDonee{
            Donee: donee,
        },
    )
}

//emitDonate This is a method of Mydonation
func (m *Mydonation) emitDonate(from, donee types.Address, value, balance bn.Number) {
    type donate struct {
        From    types.Address `json:"from"`
        Donee   types.Address `json:"donee"`
        Value   bn.Number     `json:"value"`
        Balance bn.Number     `json:"balance"`
    }

    m.sdk.Helper().ReceiptHelper().Emit(
        donate{
            From:    from,
            Donee:   donee,
            Value:   value,
            Balance: balance,
        },
    )
}

//emitTransferDonation This is a method of Mydonation
func (m *Mydonation) emitTransferDonation(donee types.Address, value, balance bn.Number) {
    type transferDonation struct {
        Donee   types.Address `json:"donee"`
        Value   bn.Number     `json:"value"`
        Balance bn.Number     `json:"balance"`
    }

    m.sdk.Helper().ReceiptHelper().Emit(
        transferDonation{
            Donee:   donee,
            Value:   value,
            Balance: balance,
        },
    )
}
```

The following is the initial content of unit test code, take ```mydonation_case_adddonee_test.go``` file as an example:

```go
package mydonation

import (
    "blockchain/smcsdk/sdk"
)

func (mysuit *MySuite) test_Donate(owner sdk.IAccount, test *TestObject) {
    //TODO
}
```

## 5. Contract unit test

Let's complete the unit test code of the charitable donation contract.

Source code：```mydonation_case_AddDonee_test.go```:

```go
package mydonation

import (
    "blockchain/smcsdk/common/gls"
    "blockchain/smcsdk/sdk"
    "blockchain/smcsdk/sdk/bn"
    "blockchain/smcsdk/sdk/types"
    "blockchain/smcsdk/utest"
    "fmt"

    "gopkg.in/check.v1"
)

func keyOfDonation(addr types.Address) string {
    return fmt.Sprintf("/donations/%v", addr)
}

//AddDonee This is a method of MySuite
func (mysuit *MySuite) TestDemo_AddDonee(c *check.C) {
    utest.Init(orgID)
    contractOwner := utest.DeployContract(c, contractName, orgID, contractMethods, contractInterfaces)

    gls.Mgr.SetValues(gls.Values{gls.SDKKey: utest.UTP.ISmartContract}, func() {
        test := NewTestObject(contractOwner)
        test.setSender(contractOwner).InitChain()
        mysuit.test_AddDonee(contractOwner, test)
    })
}

func (mysuit *MySuite) test_AddDonee(owner sdk.IAccount, test *TestObject) {
    fmt.Println("=== Run  UnitTest case: AddDonee(donee types.Address)")

    fmt.Println("=== prepare for test")
    zero := bn.N(0)
    oneCoin := bn.N(1000000000)
    a1 := utest.NewAccount("TSC", oneCoin)
    a2 := utest.NewAccount("TSC", oneCoin)
    fmt.Println("=== pass")

    fmt.Println("=== test for authorization")
    test.run(types.ErrNoAuthorization, func(t *TestObject) types.Error {
        return t.setSender(a1).AddDonee(a2.Address())
    })
    fmt.Println("=== pass")

    fmt.Println("=== test for parameters")
    //prepare
    var cases = []struct {
        sender     sdk.IAccount
        addr       types.Address
        codeExpect uint32
    }{
        {owner, "", types.ErrInvalidAddress},
        {owner, "local", types.ErrInvalidAddress},
        {owner, "localhshskhjkshfsswtsysyst6t76ddsg7s7w", types.ErrInvalidAddress},
        {owner, owner.Address(), errDoneeCannotBeOwner},
        {owner, utest.GetContract().Address(), errDoneeCannotBeSmc},
        {owner, utest.GetContract().Account().Address(), errDoneeCannotBeSmc},
    }
    //run
    for _, c := range cases {
        test.run(c.codeExpect, func(t *TestObject) types.Error {
            return t.setSender(c.sender).AddDonee(c.addr)
        })
    }
    fmt.Println("=== pass")

    fmt.Println("=== test for business logic")
    //prepare
    utest.AssertSDB(keyOfDonation(a1.Address()), nil)
    //run
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        return t.setSender(owner).AddDonee(a1.Address())
    })
    test.run(errDoneeAlreadyExist, func(t *TestObject) types.Error {
        return t.setSender(owner).AddDonee(a1.Address())
    })
    //check
    utest.AssertSDB(keyOfDonation(a1.Address()), &zero)
    utest.AssertSDB(keyOfDonation(a2.Address()), nil)
    fmt.Println("=== pass")
}
```

Source code：```mydonation_case_DelDonee_test.go```

```go
package mydonation

import (
    "blockchain/smcsdk/common/gls"
    "blockchain/smcsdk/sdk"
    "blockchain/smcsdk/sdk/bn"
    "blockchain/smcsdk/sdk/types"
    "blockchain/smcsdk/utest"
    "fmt"

    "gopkg.in/check.v1"
)

//DelDonee This is a method of MySuite
func (mysuit *MySuite) TestDemo_DelDonee(c *check.C) {
    utest.Init(orgID)
    contractOwner := utest.DeployContract(c, contractName, orgID, contractMethods, contractInterfaces)

    gls.Mgr.SetValues(gls.Values{gls.SDKKey: utest.UTP.ISmartContract}, func() {
        test := NewTestObject(contractOwner)
        test.setSender(contractOwner).InitChain()
        mysuit.test_DelDonee(contractOwner, test)
    })
}

func (mysuit *MySuite) test_DelDonee(owner sdk.IAccount, test *TestObject) {
    fmt.Println("=== Run  UnitTest case: DelDonee(donee types.Address)")

    fmt.Println("=== prepare for test")
    zero := bn.N(0)
    oneCoin := bn.N(1000000000)
    halfCoin := bn.N(500000000)
    a1 := utest.NewAccount("TSC", oneCoin)
    a2 := utest.NewAccount("TSC", oneCoin)
    a3 := utest.NewAccount("TSC", oneCoin)
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        return t.setSender(owner).AddDonee(a1.Address())
    })
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        return t.setSender(owner).AddDonee(a2.Address())
    })
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        t.setSender(a1)
        utest.Assert(t.transfer(halfCoin) != nil)
        return t.Donate(a2.Address())
    })
    fmt.Println("=== pass")

    fmt.Println("=== test for authorization")
    test.run(types.ErrNoAuthorization, func(t *TestObject) types.Error {
        return t.setSender(a2).DelDonee(a1.Address())
    })
    fmt.Println("=== pass")

    fmt.Println("=== test for parameters")
    //prepare
    var cases = []struct {
        sender     sdk.IAccount
        addr       types.Address
        codeExpect uint32
    }{
        {owner, "", types.ErrInvalidAddress},
        {owner, "local", types.ErrInvalidAddress},
        {owner, "localhshskhjkshfsswtsysyst6t76ddsg7s7w", types.ErrInvalidAddress},
        {owner, owner.Address(), errDoneeNotExist},
        {owner, utest.GetContract().Address(), errDoneeNotExist},
        {owner, utest.GetContract().Account().Address(), errDoneeNotExist},
        {owner, a3.Address(), errDoneeNotExist},
    }
    //run
    for _, c := range cases {
        test.run(c.codeExpect, func(t *TestObject) types.Error {
            return t.setSender(c.sender).DelDonee(c.addr)
        })
    }
    fmt.Println("=== pass")

    fmt.Println("=== test for business logic 1")
    //prepare
    utest.AssertSDB(keyOfDonation(a1.Address()), &zero)
    //run
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        return t.setSender(owner).DelDonee(a1.Address())
    })
    //check
    utest.AssertSDB(keyOfDonation(a1.Address()), nil)
    //run
    test.run(errDoneeNotExist, func(t *TestObject) types.Error {
        t.setSender(owner)
        return t.DelDonee(a1.Address())
    })
    //check
    utest.AssertSDB(keyOfDonation(a1.Address()), nil)
    fmt.Println("=== pass")

    fmt.Println("=== test for business logic 2")
    //prepare
    utest.AssertSDB(keyOfDonation(a2.Address()), &halfCoin)
    //run
    test.run(errDonationExist, func(t *TestObject) types.Error {
        return t.setSender(owner).DelDonee(a2.Address())
    })
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        t.setSender(owner)
        return t.Transfer(a2.Address(), halfCoin)
    })

    utest.AssertSDB(keyOfDonation(a2.Address()), &zero)
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        t.setSender(owner)
        return t.DelDonee(a2.Address())
    })
    //check
    utest.AssertSDB(keyOfDonation(a2.Address()), nil)
    //run
    test.run(errDoneeNotExist, func(t *TestObject) types.Error {
        t.setSender(owner)
        return t.DelDonee(a2.Address())
    })
    //check
    utest.AssertBalance(a2, "TSC", oneCoin.Add(halfCoin))
    fmt.Println("=== pass")
}
```

Source code：```mydonation_case_Donate_test.go```

```go
package mydonation

import (
    "blockchain/smcsdk/common/gls"
    "blockchain/smcsdk/sdk"
    "blockchain/smcsdk/sdk/bn"
    "blockchain/smcsdk/sdk/types"
    "blockchain/smcsdk/utest"
    "fmt"

    "gopkg.in/check.v1"
)

//Donate This is a method of MySuite
func (mysuit *MySuite) TestDemo_Donate(c *check.C) {
    utest.Init(orgID)
    contractOwner := utest.DeployContract(c, contractName, orgID, contractMethods, contractInterfaces)

    gls.Mgr.SetValues(gls.Values{gls.SDKKey: utest.UTP.ISmartContract}, func() {
        test := NewTestObject(contractOwner)
        test.setSender(contractOwner).InitChain()
        mysuit.test_Donate(contractOwner, test)
    })
}

func (mysuit *MySuite) test_Donate(owner sdk.IAccount, test *TestObject) {
    fmt.Println("=== Run  UnitTest case: Donate(donee types.Address)")

    fmt.Println("=== prepare for test")
    halfCoin := bn.N(500000000)
    oneCoin := bn.N(1000000000)
    oneHalfCoin := bn.N(1500000000)
    twoCoin := bn.N(2000000000)
    utest.Transfer(nil, owner.Address(), "TSC", twoCoin)
    utest.Transfer(nil, owner.Address(), "BTC", twoCoin)
    a1 := utest.NewAccount("TSC", oneCoin)
    a2 := utest.NewAccount("TSC", oneCoin)
    a3 := utest.NewAccount("TSC", oneCoin)
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        return t.setSender(owner).AddDonee(a1.Address())
    })
    fmt.Println("=== pass")

    fmt.Println("=== test for parameters")
    //prepare
    var cases = []struct {
        sender     sdk.IAccount
        addr       types.Address
        codeExpect uint32
    }{
        {owner, "", types.ErrInvalidAddress},
        {owner, "local", types.ErrInvalidAddress},
        {owner, "localhshskhjkshfsswtsysyst6t76ddsg7s7w", types.ErrInvalidAddress},
        {owner, a2.Address(), errDoneeNotExist},
        {owner, a3.Address(), errDoneeNotExist},
    }
    //run
    for _, c := range cases {
        test.run(c.codeExpect, func(t *TestObject) types.Error {
            return t.setSender(c.sender).Donate(c.addr)
        })
    }
    fmt.Println("=== pass")

    fmt.Println("=== test for receipt of transfer")
    //run
    test.run(types.ErrInvalidParameter, func(t *TestObject) types.Error {
        return t.setSender(owner).Donate(a1.Address())
    })
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        t.setSender(owner)
        utest.Assert(t.transfer("TSC", halfCoin) != nil)
        return t.Donate(a1.Address())
    })
    test.run(types.ErrInvalidParameter, func(t *TestObject) types.Error {
        t.setSender(owner)
        utest.Assert(test.transfer("TSC", halfCoin) != nil)
        utest.Assert(test.transfer("TSC", halfCoin) != nil)
        return t.Donate(a1.Address())
    })
    test.run(types.ErrInvalidParameter, func(t *TestObject) types.Error {
        t.setSender(owner)
        utest.Assert(t.transfer("BTC", halfCoin) != nil)
        return t.Donate(a1.Address())
    })
    fmt.Println("=== pass")

    fmt.Println("=== test for business logic")
    //prepare
    utest.AssertSDB(keyOfDonation(a1.Address()), &halfCoin)
    //run
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        t.setSender(a2)
        utest.Assert(t.transfer(halfCoin) != nil)
        return t.Donate(a1.Address())
    })
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        t.setSender(a3)
        utest.Assert(t.transfer(halfCoin) != nil)
        return t.Donate(a1.Address())
    })
    //check
    utest.AssertSDB(keyOfDonation(a1.Address()), &oneHalfCoin)
    fmt.Println("=== pass")
}
```

Source code：```mydonation_case_Transfer_test.go```

```go
package mydonation

import (
    "blockchain/smcsdk/common/gls"
    "blockchain/smcsdk/sdk"
    "blockchain/smcsdk/sdk/bn"
    "blockchain/smcsdk/sdk/types"
    "blockchain/smcsdk/utest"
    "fmt"

    "gopkg.in/check.v1"
)

//Transfer This is a method of MySuite
func (mysuit *MySuite) TestDemo_Transfer(c *check.C) {
    utest.Init(orgID)
    contractOwner := utest.DeployContract(c, contractName, orgID, contractMethods, contractInterfaces)

    gls.Mgr.SetValues(gls.Values{gls.SDKKey: utest.UTP.ISmartContract}, func() {
        test := NewTestObject(contractOwner)
        test.setSender(contractOwner).InitChain()
        mysuit.test_Transfer(contractOwner, test)
    })
}

func (mysuit *MySuite) test_Transfer(owner sdk.IAccount, test *TestObject) {
    fmt.Println("=== Run  UnitTest case: Transfer(donee types.Address, value bn.Number)")

    fmt.Println("=== prepare for test")
    zero := bn.N(0)
    oneCoin := bn.N(1000000000)
    halfCoin := bn.N(500000000)
    utest.Transfer(nil, owner.Address(), bn.N(2).Mul(oneCoin))
    a1 := utest.NewAccount("TSC", oneCoin)
    a2 := utest.NewAccount("TSC", oneCoin)
    a3 := utest.NewAccount("TSC", oneCoin)
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        return t.setSender(owner).AddDonee(a1.Address())
    })
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        t.setSender(owner)
        utest.Assert(test.transfer(oneCoin) != nil)
        return t.Donate(a1.Address())
    })
    utest.AssertOK(test.AddDonee(a2.Address()))
    fmt.Println("=== pass")

    fmt.Println("=== test for authorization")
    //run
    test.run(types.ErrNoAuthorization, func(t *TestObject) types.Error {
        t.setSender(a2)
        utest.Assert(test.transfer(oneCoin) != nil)
        return t.Transfer(a1.Address(), halfCoin)
    })
    fmt.Println("=== pass")

    fmt.Println("=== test for parameters")
    //prepare
    var cases = []struct {
        sender     sdk.IAccount
        addr       types.Address
        amount     bn.Number
        codeExpect uint32
    }{
        {owner, "", halfCoin, types.ErrInvalidAddress},
        {owner, "local", halfCoin, types.ErrInvalidAddress},
        {owner, "localhshskhjkshfsswtsysyst6t76ddsg7s7w", halfCoin, types.ErrInvalidAddress},
        {owner, owner.Address(), halfCoin, errDoneeNotExist},
        {owner, utest.GetContract().Address(), halfCoin, errDoneeNotExist},
        {owner, utest.GetContract().Account().Address(), halfCoin, errDoneeNotExist},
        {owner, a3.Address(), halfCoin, errDoneeNotExist},
        {owner, a1.Address(), bn.N(-1), types.ErrInvalidParameter},
        {owner, a1.Address(), bn.N(0), types.ErrInvalidParameter},
        {owner, a1.Address(), bn.N(1), types.CodeOK},
        {owner, a1.Address(), oneCoin, errDonationNotEnough},
    }
    //run
    for _, c := range cases {
        test.run(c.codeExpect, func(t *TestObject) types.Error {
            return t.setSender(c.sender).Transfer(c.addr, c.amount)
        })
    }
    fmt.Println("=== pass")

    fmt.Println("=== test for business logic")
    //prepare
    x := oneCoin.SubI(1)
    utest.AssertSDB(keyOfDonation(a1.Address()), &x)
    //run
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        t.setSender(owner)
        utest.Assert(test.transfer(bn.N(1)) != nil)
        return t.Donate(a1.Address())
    })
    //check
    utest.AssertSDB(keyOfDonation(a1.Address()), &oneCoin)
    //run
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        return t.setSender(owner).Transfer(a1.Address(), halfCoin)
    })
    test.run(types.CodeOK, func(t *TestObject) types.Error {
        return t.setSender(owner).Transfer(a1.Address(), halfCoin)
    })
    //check
    utest.AssertSDB(keyOfDonation(a1.Address()), &zero)
    utest.AssertBalance(a1, "TSC", bn.N(2).Mul(oneCoin).AddI(1))
    fmt.Println("=== pass")
}
```

After the unit test code is completed, you can use the following execution path to perform unit tests:

```text
GoLand left sidebar Project Explorer
    >> Right click on the src/contract/mydonation/v1.0/mydonation directory to bring up
       the menu
            >> Run
                >> go test mydonation
```

After the unit test is completed, the test results are output as follows:

```shell
GOROOT=C:\Go #gosetup
=== RUN   Test
=== Run  UnitTest case: AddDonee(donee types.Address)
=== prepare for test
=== pass
=== test for authorization
only contract owner just can do it
=== pass
=== test for parameters
Address chainID is error!
Address chainID is error!
Address chainID is error!
Donee can not be owner
Donee can not be this smart contract
Donee can not be account of this smart contract
=== pass
=== test for business logic
Donee already exists
=== pass
=== Run  UnitTest case: DelDonee(donee types.Address)
=== prepare for test
=== pass
=== test for authorization
only contract owner just can do it
=== pass
=== test for parameters
Address chainID is error!
Address chainID is error!
Address chainID is error!
Donee does not exist
Donee does not exist
Donee does not exist
Donee does not exist
=== pass
=== test for business logic 1
Donee does not exist
=== pass
=== test for business logic 2
Donation exists
Donee does not exist
=== pass
=== Run  UnitTest case: Donate(donee types.Address)
=== prepare for test
=== pass
=== test for parameters
Address chainID is error!
Address chainID is error!
Address chainID is error!
Donee does not exist
Donee does not exist
=== pass
=== test for receipt of transfer
Please transfer token to me first
Accept only one donation at a time
Accept donations in genesis token only
=== pass
=== test for business logic
=== pass
=== Run  UnitTest case: Transfer(donee types.Address, value bn.Number)
=== prepare for test
=== pass
=== test for authorization
only contract owner just can do it
=== pass
=== test for parameters
Address chainID is error!
Address chainID is error!
Address chainID is error!
Donee does not exist
Donee does not exist
Donee does not exist
Donee does not exist
Parameter "value" must be greater than 0
Parameter "value" must be greater than 0
Donation is not enough
=== pass
=== test for business logic
=== pass
OK: 4 passed
--- PASS: Test (0.14s)
PASS
ok      contract/orgexample/code/mydonation/v1.0/mydonation    (cached)

Process finished with exit code 0
```
