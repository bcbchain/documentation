# Deeper Understanding of Smart Contracts

## 1. Organization

The smart contracts developed for the BCBChain backbone are organized according to the organization's architecture, and all smart contracts developed for the same organization will be integrated into a contract process for users to call.

In a smart contract, you can call the interface that is implemented by other smart contracts. Through the interface in the called smart contract, you can call another smart contract interface. BCBChain supports up to 8 levels of such nested cross-contract calls, but they are not allowed to form a loop.

BCBChain has set up a base organization, and the smart contracts developed for this base organization will be integrated into the contract process of all organizations for users to call. The organization is mainly set up to provide some cross-contract calls that can be executed by any organization at any time, such as the basic validators for the BCBChain main chain and the token template contract.

## 2. BNF Paradigm

This section describes the contract specifications using the BNF paradigm.

The English abbreviation for the Backus paradigm is BNF, a formal grammatical representation of the American name Backus and the Danish name Naur, used to describe a formal system of grammar. A typical meta language. Also known as the Backus-Naur form. Not only does it strictly represent grammatical rules, but the described grammar is context-independent. It has the characteristics of simple syntax, clear definition, and easy parsing and compilation.

The way the BNF paradigm represents grammar rules is:

- Non-terminals are enclosed in angle brackets.
- The left part of each rule is a non-terminal character, and the right part is a symbol string consisting of non-terminal symbols and terminators. The middle is usually separated by ::=.
- Rules with the same left part can share one left part, with the right parts separated by a vertical line "|".

The meta-characters commonly used in the BNF paradigm and their meanings are as follows:

```text
1. Characters in double quotes (such as "word") represent the characters themselves.  
   Double_quote is used to represent double quotes themselves.
2. Words outside the double quotes (possibly underlined) represent the grammar part.
3. The angle brackets < > are mandatory.
4. The square brackets [ ] contain optional items.
5. The braces { } contain items that can be repeated from 0 to innumerable.
6. A set of all the items contained in parentheses ( ) is used to control the priority of
   the expression.
7. Vertical line | means that you can choose one of the left and right sides, which is
   equivalent to "OR".
8. ::= means "defined as".
9. Blank Characters The blank character spacing that appears in the BNF paradigm
   definition is only required for typesetting and is not part of the specification.
```

## 3. Contract Markups

The BCBChain smart contract code uses the notation to describe the contract's metadata in the contract code's comments.

Below is a detailed syntax description of the various tags used by the BCBChain Smart Contract.

### 3.1 contract

The markup ```contract``` is used to identify the contract name, which must be unique within the organization. Please ask the developer of the smart contract to design the contract names accordingly.

The markup ```contract```is mandatory, but can only appear once in the entire contract code.

The BNF paradigm for ```contract``` markup is defined as follows:

```go
<contract markup syntax> ::= "//@:contract:" <contract name>
<contract name> ::= <letter> | <contract name> <alphanumeric string>
<alphanumeric string> ::= <letter> |
                          <decimal number> |
                          <alphanumeric string> <letter> |
                          <alphanumeric string> <decimal number>
<let> ::= "_" | "-" | "." | <lowercase> | <uppercase>
<lowercase letter> ::= "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j" |
                       "k" | "l" | "m" | "n" | "o" | "p" | "q" | "r" | "s" | "t" |
                       "u" | "v" | "w" | "x" | "y" | "z"
<Capital letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J" |
                     "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T" |
                     "U" | "V" | "W" | "X" | "Y" | "Z"
<decimal number> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | 8 | "9"
```

The code after the ```contract```markup must be strictly followed by a contract class definition containing the ```sdk.ISmartContract``` member. This contract class follows the context of the smart contract. Each time there is a message call to a smart contract, an instance of the contract class will be automatically created, and its smart contract method will be called. The methods that it provide for the outside to call, must be a member function of its class. The first letter of the class name must be capitalized.

Example below：

```go
//@:contract:mycoin
type Mycoin struct {
    sdk sdk.ISmartContract

    //@:public:store:cache
    totalSupply bn.Number

    //@:public:store
    balanceOf map[types.Address]bn.Number
}
```

### 3.2 version

The markup```version```is used to identify the version of the contract and can only appear once in the entire contract code.

```version```is mandatory, but can only appear once in the entire contract code.

The BNF paradigm for ```version```is defined as follows:

```go
<version markup syntax> ::= "//@:version:" <contract version>
<Contract version> ::= <decimal number> |
              <decimal number> "." <decimal number> |
              <decimal number> "." <decimal number> "." <decimal number> |
              <decimal number> "." <decimal number> "." <decimal number> "." <decimal number>
<decimal number> ::= <decimal number> | <decimal number> <decimal number>
<decimal number> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | 8 | "9"
```

Example below:

```go
//@:version:1.0
```

Note: The BCBChain chain does not require specific rules for smart contract versions, ie the contract version can be either a one-segment (eg 1, 2, 3) or a two-segment (1.0, 1.1, 1.2), three-segment (1.0. 1, 1.0.2, 1.0.3), four-segment (1.0.1.102, 1.0.1.103), but different versions of the same smart contract need to maintain the consistency of the number of version format segments.

### 3.3 organization

The markup```organization```is used to identify the ID of the organization to which the contract belongs.

```organization```is mandatory, but can only appear once in the entire contract code.

The BNF paradigm for ```organization```is defined as follows:

```go
<organization markup syntax> ::= "//@:organization:" <organization ID>
<Organization ID> ::= <prefix code> <Base58 string>
<prefix code> ::= "org"
<Base58 string> ::= <Base58 character> | <Base58 string> <Base58 character>
<Base58 characters> ::= <decimal numbers> | <uppercase letters> | <lowercase letters>
<decimal number> ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | 8 | "9"
<Capital Letters> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "J" | "K" |
                      "L" | "M" | "N" | "P" | "Q" | "R" | "S" | "T" | "U" | "V" |
                      "W" | "X" | "Y" | "Z"
<lowercase letter> ::= "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j" |
                       "k" | "m" | "n" | "o" | "p" | "q" | "r" | "s" | "t" | "u" |
                       "v" | "w" | "x" | "y" | "z"
```

An example is as follows:

```go
//@:organization:orgBtjfCSPCAJ84uQWcpNr74NLMWYm5SXzer
```

### 3.4 author

The markup```author```is used to identify the account public key of the contract author.

```author```is a mandatory markup, but can only appear once in the entire contract code.

The BNF paradigm for```author```is defined as follows:

```go
<author markup syntax> ::= "//@:author:" <account public key>
<account public key> ::= <hex string>
<hexadecimal string> ::= <hexadecimal number> | <hexadecimal string> <hexadecimal number>
<hexadecimal number> ::= "0" | 1" | "2" | "3" | "4" | "5" | "6" | "7" | 8 | "9" |
                           "A" | "B" | "C" | "D" | "E" | "F" |
                           "a" | "b" | "c" | "d" | "e" | "f"
```

Example below:

```go
//@:author:b37e7627431feb18123b81bcf1f41ffd37efdb90513d48ff2c7f8a0c27a9d06c
```

Note: The hexadecimal public key string length must be equal to 64.

### 3.5 constructor

The markup ```constructor```is used to identify the chain's initialization function.

The valid code that follows the ```constructor``` must be a no-argument function called ```InitChain```or ```UpdateChain``` , which will automatically make the only call when the first created (```InitChain```) or upgrade (```UpdateChain```) of the contract on the BCBChain chain, in order to complete its initialization work in the block, such as initializing the initial values of some global state data.

```constructor```is optional, but can only appear up to two times in the entire contract code, once for the ```InitChain```function, and once for the ```UpdateChain```function.

The BNF paradigm for```constructor``` is defined as follows:

```go
<author markup syntax> ::= "//@:constructor"
```

Example below:

```go
//@:constructor
func (mc *Mycoin) InitChain() {
    ...
}

//@:constructor
func (mc *Mycoin) UpdateChain() {
    ...
}
```

### 3.6 public:store

The markup ```public:store``` is used to identify a state variable, which must be a valid member variable of the contract class (one with the ```contract``` markup).

The valid code that follows```public:store``` must be the definition of a member variable.

```public:store```is an optional markup that can appear multiple times in the contract class definition, each time identifying a different state variable.

The BNF paradigm for ```public:store```is defined as follows:

```go
<public:store markup syntax> ::= "//@:public:store"
```

Example below:

```go
//@:contract:mycoin
type Mycoin struct {
    sdk sdk.ISmartContract
    ...
    //@:public:store
    balanceOf map[types.Address]bn.Number
}
```

The state variable with the ```public:store``` markup cannot be directly accessed in the contract code. According to the BCBChain contract specification, the SDK matching tool provided by BCBChain automatically generates a read/write function for the state variable. Example below:

```go
//Read the function of balanceOf
func (mc *Mycoin) _balanceOf(k types.Address) bn.Number {
    return *mc.sdk.Helper().StateHelper().GetEx(
        fmt.Sprintf("/balanceOf/%v", k), &bn.Number{V: big.NewInt(0)}).(*bn.Number)
}

//A function that detects whether balanceOf exists
func (mc *Mycoin) _chkBalanceOf(k types.Address) bool {
    return mc.sdk.Helper().StateHelper().Check(fmt.Sprintf("/balanceOf/%v", k))
}

//Configures the function of balanceOf
func (mc *Mycoin) _setBalanceOf(k types.Address, v bn.Number) {
    mc.sdk.Helper().StateHelper().Set(fmt.Sprintf("/balanceOf/%v", k), &v)
}

//Function to remove the key value of balanceOf from the state database
func (mc *Mycoin) _delBalanceOf(k types.Address) {
    mc.sdk.Helper().StateHelper().Delete(fmt.Sprintf("/balanceOf/%v", k))
}
```

### 3.7 public:store:cache

The markup ```public:store:cache```is used to identify a state variable that can be cached in memory, which must be a valid member variable of the contract class (one with the ```contract``` markup).

The valid code that follows```public:store:cache``` must be the definition of a member variable.

```public:store:cache``` is an optional markup that can appear multiple times in the contract class definition, each time identifying a state variable.

The BNF paradigm for ```public:store:cache```is defined as follows:

```go
<public:store:cache markup syntax> ::= "//@:public:store:cache"
```

Example below:

```go
//@:contract:mycoin
type Mycoin struct {
    sdk sdk.ISmartContract
    ...
    //@:public:store:cache
    totalSupply bn.Number
}
```

The cacheable state variable cannot be directly accessed in the contract code. According to the BCBChain contract specification, the SDK matching tool provided by BCBChain automatically generates a read/write function for the state variable. Example below:

```go
//Read the function of the state variable totalSupply
func (mc *Mycoin) _totalSupply() bn.Number {
    return *mc.sdk.Helper().StateHelper().McGetEx(
        "/totalSupply", &bn.Number{V: big.NewInt(0)}).(*bn.Number)
}

//A function that detects whether totalSupply exists
func (mc *Mycoin) _chkTotalSupply() bool {
    return mc.sdk.Helper().StateHelper().McCheck("/totalSupply")
}

//Sets the function of totalSupply
func (mc *Mycoin) _setTotalSupply(v bn.Number) {
    mc.sdk.Helper().StateHelper().McSet("/totalSupply", &v)
}

//Clears the function of totalSupply
func (mc *Mycoin) _clrTotalSupply() {
    mc.sdk.Helper().StateHelper().McClear("/totalSupply")
}

//Remove totalSupply from the state database
func (m *Mycoin) _delTotalSupply() {
    m.sdk.Helper().StateHelper().McDelete("/totalSupply")
}
```

### 3.8 public:receipt

The markup```public:receipt``` is used to identify the definition of all receipts in the contract.

The valid code following ```public:receipt``` must be an interface definition called ```receipt```.

```public:receipt```is optional and can only appear at most once in the entire contract code.

The BNF paradigm for ```public:receipt```is defined as follows:

```go
<public:receipt markup syntax> ::= "//@:public:receipt"
```

Example below:

```go
//@:public:receipt
type receipt interface {
    emitTransferMyCoin(token, from, to types.Address, value bn.Number)
}
```

Every method that sends a ```receipt```must start with the word "```emit```", as defined in the Receipt interface. The first word after the word "```emit```" is converted to lowercase and must be the name of the receipt struct, which can be used to retrieve from the BCBChain chain. Based on BCBChain contract specification, the SDK supporting tool provided by BCBChain will automatically generate the implementation code for the sending receipt function. Example below:

```go
//The following functions are automatically generated by the BCBChain tool.
func (mc *Mycoin) emitTransferMyCoin(token, from, to types.Address, value bn.Number) {
    type transferMyCoin struct {
        Token types.Address `json:"token"`
        From types.Address `json:"from"`
        To types.Address `json:"to"`
        Value bn.Number `json:"value"`
    }
    mc.sdk.Helper().ReceiptHelper().Emit(
        transferMycoin{
            Token:   token,
            From:    from,
            To:      to,
            Value:   value,
        })
}

//The following is a sample code for sending a receipt, located in the implementation of the Transfer function.
func (mc *Mycoin) Transfer(to types.Address, value bn.Number) {

    //Business logic code that implements the transfer
    ...

    //Send a transfer receipt
    mc.emitTransferMyCoin(
        mc.sdk.Message().Contract().Address(),
        sender,
        to,
        value)
}
```

### 3.9 public:method

The markup```public:method``` is used to identify a public method of the contract.

The valid code following ```public:method``` must be a member function definition of the contract class (one with the ```contract```markup) The function name must start with an uppercase letter, and it can be executed from BCBChain transaction broadcasts.

```public:method```is optional and can appear zero, one or more times throughout the contract code.

The BNF paradigm for ```public:method``` is defined as follows:

```go
<public:method markup syntax> ::= "//@:public:method:gas[" <gas quantity> "]"
<number of gas> ::= ["-"] <decimal number>
<decimal number> ::= <decimal number> | <decimal number> <decimal number>
<decimal number> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | 8 | "9"
```

Note:

- A positive integer number indicates that the gas cost consumed by the method call is paid by the original sender of the transaction;
- A gas quantity of 0 means no payment is required;
- A negative integer number indicates that the gas cost consumed by the method call is paid by the current smart contract account.
  
Example below:

```go
//@:public:method:gas[500]
func (mc *Mycoin) Transfer(to types.Address, value bn.Number) {
    ...
}
```

### 3.10 public:interface

The markup```public:interface``` is used to identify the public interface of the contract.

The valid code following ```public:interface``` must be a member function definition for the contract class (one with the ```contract``` markup). The function name must start with an uppercase letter, and can be cross-called from other contracts.

```public:interface``` is optional and can appear zero, one or more times throughout the contract code.

The BNF paradigm for```public:interface``` is defined as follows:

```go
<public:interface markup syntax> ::= "//@:public:interface:gas[" <gas quantity> "]"
<number of gas> ::= <decimal number>
<decimal number> ::= <decimal number> | <decimal number> <decimal number>
<decimal number> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | 8 | "9"
```

Example below:

```go
//@:public:interface:gas[450]
func (mc *Mycoin) Transfer(to types.Address, value bn.Number) {
    ...
}
```

Note:

- The amount of gas must be greater than or equal to zero.

Markups ```public:interface```and ```public:method```can be used simultaneously on same member function of the contract class. The example above can be written as below:

```go
//@:public:method:gas[500]
//@:public:interface:gas[450]
func (mc *Mycoin) Transfer(to types.Address, value bn.Number) {
    ...
}
```

### 3.11 public:mine

The markup ```public:mine``` is used to identify the mining interface exposed by the contract.

The valid code following ```public:mine```must be a member function definition for the contract class (one with the ```contract``` markup). The mining function prototype must be:```func Mine() int64```, and it will automatically execute after BCBChain block reaches a consensus.

```public:mine``` is optional and can appear zero or one time throughout the contract code. Only the smart contract of the underlying organization of BCBChain is allowed to use this mining interface.

The BNF paradigm for ```public:mine``` is defined as follows:

```go
<public:interface tag syntax> ::= "//@:public:mine"
```

Example below:

```go
//@:public:mine
func (mc *Mycoin) Mine() int64 {
        ...
}
```

Note:

- The mining function ```Mine()``` can only be used with the markup```public:mine```.

### 3.12 import

The markup ```import``` is used to import an interface prototype for an external contract, making it easy to call external contracts from the current contract.

```import```is optional, and can appear multiple times in the entire contract code. Each time you import a cross-contract call interface of an external contract, the external contract can only be imported once.

The BNF paradigm for ```import``` is defined as follows:

```go
<import tag syntax> ::= "//@:import:" <contract name>
<contract name> ::= <letter> | <contract name> <alphanumeric string>
<alphanumeric string> ::= <letter> | <decimal number> | <alphanumeric string> <letter> | <alphanumeric string> <decimal number>
<let> ::= "_" | "-" | "." | <lowercase> | <uppercase>
<lowercase letter> ::= "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j" |
                       "k" | "l" | "m" | "n" | "o" | "p" | "q" | "r" | "s" | "t" |
                       "u" | "v" | "w" | "x" | "y" | "z"
<Capital letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J" |
                     "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T" |
                     "U" | "V" | "W" | "X" | "Y" | "Z"
<decimal number> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | 8 | "9"
```

Using the previous ```mycoin```token contract as an example, if you need to call the contract from other contracts, you need to write the following code:

```go
//This code is in the contract mycontract

//@:import:mycoin
type mycoin interface {
    Transfer(to types.Address, value bn.Number)
}
```

The interface name of the external contract is customizable, so long it follows the ```golang``` syntax specification.

The interface of the external contract cannot be directly accessed from the contract. According to the BCBChain contract specification, the ```SDK``` supporting tool provided by BCBChain will automatically generate an implementation function to access the external contract interface. The generated code example is as follows:

```go
// This code is automatically generated by the SDK supporting tools

//mycoin This is method of MyContract
func (m *MyContract) mycoin() *InterfacemycoinStub {
    return &InterfacemycoinStub{}
}

//Transfer This is a method of InterfacemycoinStub
func (is *InterfacemycoinStub) Transfer(to types.Address, value bn.Number) {
    return
}

//run Transfer some receipts to destination contract
func (is *InterfacemycoinStub) run(f func()) (*InterfacemycoinStub) {
    ...
    f()
    ...
    return is
}

//contract Wrap the destination contract information
func (is *InterfacemycoinStub) contract() IContract {
    ...
    return contract
}
```

Below is a sample code that calls an external contract in the contract code:

```go
//This code is in the contract mycontract

func (m *MyContract)TransferTest(to types.Address, value bn.Number) {
    m.mycoin().Transfer(to, value)
}
```

cross-contract calling support transmit receipts to contract that it's called, example code in below(from ```contract2``` to call ```contract1```'s interface):

> contract1, supply cross-contract interface service:
>
> ```go
> //@:contract:contract1
> type C1 struct {
>   sdk sdk.ISmartContract
>   ...
> }
>
> //@:public:interface:gas[450]
> func (c *C1) Register() {
>
>   //I need receipt from caller
>   transfers := dw.sdk.Message().GetTransferToMe()
>   sdk.Require(transfers!=nil && len(transfers)==1,
>     types.ErrInvalidParameter, "Please transfer to me first")
>
>   token := transfers[0].Token
>   value := transfers[0].Value
>
>   ...
> }
> ```
>
> contract2, cross-contract invoker:
>
> ```go
> //@:contract:contract2
> type C2 struct {
>   sdk sdk.ISmartContract
>   ...
> }
>
> //@:import:contract1
> type mycoin interface {
>   Register()
> }
>
> //@:public:method:gas[450]
> func (c *C2) Register() {
>   ...
>   c.contract1().run(func(){
>     c.sdk.Message().Contract().Account.TransferByName(
>       "bcb",
>       c.contract1().contract().Account().Address(),
>       bn.N(1000000000),
>     )
>   }).Register()
>   ...
> }
> ```

## 4. Contract Specification

### 4.1 BNF Paradigm Definition

Combining the above description of the contract mark, the following defines the ```BNF``` paradigm of the contract specification:

```go
<BCBChain Smart Contract> ::= <Contract Definition Code File> {<Contract Implementation Code File>} {<Contract Test Code File>}

<Contract Definition Code File> ::= <Code Package Definition> <Contract Definition Code>
<contract implementation code file> ::= <code package definition> <contract implementation code>
<Contract Test Code File> ::= <Code Package Definition> <Contract Test Code>
<code package definition> ::= "package" <contract package name>
<contract package name> ::= follows the glang syntax specification
<contract definition code> ::= "import ("
                     <Contract SDK root path>
                     {[package alias] <contract support code package path>}
                 ")"
 <contract class definition>
                 [<Contracting chain initialization function definition>]
                 [<mining definition>]
                 [<Contract Receipt Definition>]
                 {<Cross-contract call interface definition>}
                 {<Contract public function definition>}
                 {<contract implementation code>}
<contract SDK root path> ::= double_quote "blockchain/smcsdk/sdk" double_quote
<Contract Support Code Package Path> ::= Follow the golang code package path specification, follow the whitelist and graylist specifications of the BCBChain contract specification
<package alias> ::= Code package alias that follows the golang code specification, cannot use '.'
<contract implementation code> ::= Contract implementation code that follows the golang code specification (code that does not require BCBChain contract tags), including type definitions,
                 Constant definition, function definition (Note: can not contain global variable definition, do not allow the use of the for keyword, does not allow recursion
                 transfer)
<contract test code> ::= Test code that follows the golang unit test specification

<contract class definition> ::= "//@:contract:" <contract name>
               "//@:version:" <contract version>
               "//@:organization:" <organization ID>
               "//@:author:" <account public key>
               "type" <contract class name> " struct {"
               " sdk sdk.ISmartContract"
                   {<state variable definition>}
   {<golang variable definition>}
               "}"
<contract name> ::= See <contract mark: contract>
<contract version> ::= See <contract mark: version>
<Organization ID> ::= See <Contract Mark: organization>
<account public key> ::= See <contract mark: author>
<contract class name> ::= <identifier at the beginning of uppercase letter>
<golang variable definition> ::= Standard variable definition code that follows the golang code specification
<state variable definition> ::= <basic state variable definition> | <state variable definition with cache>
<Basic state variable definition> ::= "//@:public:store"
                        <variable name> ["*"] <variable type>
<state variable definition with cache> ::= "//@:public:store:cache"
                           <variable name> ["*"] <variable type>
<variable name> ::= <identifier>
<variable type> ::= <metadata type> | <array type> | <map table type>

<Contracting chain initialization function definition> ::= <deployment function> | <upgrade function>
<deployment function> ::= "//@:constructor"
              "func (" <contract object definition> ") InitChain() {"
                <winding code>
              "}"
<upgrade function> ::= "//@:constructor"
              "func (" <contract object definition> ") UpdateChain() {"
                <winding code>
              "}"
< Mining definition> ::= "//@:public:mine"
              "func (" <contract object definition> ") Mine() {"
                <mining code>
              "}"
<contract object definition> ::= <variable name> "*" <contract class name>
<winding code> ::= <golang function body>
              Note 1: Only access to state variables is allowed
              Note 2: Access to Message() and Tx() is not allowed in sdk
<mining code> ::= <golang function body>
              Note 1: Access to Message() and Tx() is not allowed in sdk
<golang function body> ::= Following the implementation of the body of the golang code specification, see the definition of <contract implementation code>

<Contract Receipt Definition> ::= "//@:public:receipt"
                 "type receipt interface {"
                     <receipt function name> <function entry parameter definition>
                 "}"
<receipt function name> ::= "emit" <identifier at the beginning of uppercase letters>
<function entry parameter definition> ::= "(" <parameter table> ")"
<Parameter Table> ::= <Parameter Definition> | <Parameter Table> "," <Parameter Definition>
<parameter definition> ::= <variable name> ["*"] <variable type>

<Cross-contract call interface definition> ::= "//@:import:" <contract name>
                      "type "<interface class name>" interface {"
                             <interface function name> <function entry parameter definition> <function return definition>
                      "}"
<interface class name> ::= <identifier at the beginning of uppercase letters>
<interface function name> ::= <identifier at the beginning of uppercase letter>
<function return definition> ::= <empty> | ["*"] <variable type> | "(" <return table> ")"
<empty> ::= blank
<back to table> ::= <return definition> | <return table> "," <return definition>
<return definition> ::= [<variable name>] ["*"] <variable type>

<Contract public function definition> ::=[<contract public method tag>]
                   [<Contract Public Interface Tag>]
                "func (" <contract object definition> ")" <public function name> <function entry parameter definition> <function return definition> "{"
                     <golang function body>
                "}"
<Contract public method tag> ::= "//@:public:method:gas[ "<gas quantity> "]"
<Contract public interface tag> ::= "//@:public:interface:gas[ "<gas quantity> "]"
<number of gas> ::= See <contract mark: public:method>
<public function name> ::= <identifier at the beginning of uppercase letter>

<identifier> ::= <letter> | <identifier> <alphanumeric string>
<identifier at the beginning of uppercase letters> ::= <capital letter> | <identifier at the beginning of uppercase letter> <alphanumeric string>
<alphanumeric string> ::= <letter> | <decimal number> | <alphanumeric string> <letter> | <alphanumeric string> <decimal number>
<letter> ::= "_" | <lowercase> | <uppercase letter>
<lowercase letter> ::= "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" |
              "m" | "n" | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x" |
              "y" | "z"
<Capital letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J" | "K" | "L" |
              "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T" | "U" | "V" | "W" | "X" |
              "Y" | "Z"
<decimal number> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | 8 | "9"
<decimal number> ::= <decimal number> | <decimal number> <decimal number>

<metadata type> := <golang built-in type> | <SDK built-in type> | <custom data structure>
<golang built-in type> ::= "int" | "int8" | "int16" | "int32" | "int64" |
                    "uint" | "uint8" | "uint16" | "uint32" | "uint64" |
                    "bool" | "string" | "byte"
<SDK built-in type> ::= <Address> | <HexBytes> | <Hash> | <PubKey> | <Number>
<Address> ::= "types.Address"
<HexBytes> ::= "types.HexBytes"
<Hash> ::= "types.Hash"
<PubKey> ::= "types.PubKey"
<Number> ::= "bn.Number"
<custom data structure> ::= "type" <identifier> " struct {"
                      {<variable name> ["*"] <variable type>}
                  "}"
<array type> ::= <array dimension definition> [<array dimension definition>] <metadata type>
<array dimension definition> ::= "[" [<decimal number>] "]"
<map table type> ::= <map table type 1> | <map table type 2>
<map table type 1> ::= <map table definition> [<map table definition>] <metadata type>
<map table type 2> ::= <map table definition> [<map table definition>] <array type>
<map table definition> ::= "map[" <metadata type> "]"
```

### 4.2 Package Specification

The BNF paradigm for defining the contract package structure is as follows:

```go
<Smart Contract Package Structure> ::= <Contract Definition Code File> {<Contract Implementation Code File>} {<Contract Test Code File>}
<Contract Definition Code File> ::= <Contract Code Directory> "/" <golang Implementation Code File Name>
<contract implementation code file> ::= <contract code directory> "/" <golang implementation code file name>
<Contract Test Code File> ::= <Contract Code Directory> "/" <golang test code file name>
<contract code directory> ::= <GOPATH> "/" <contract root directory> "/" <contract name> "/v" <contract version> "/" <contract name>
<GOPATH> ::= golang standard environment variable GOPATH points to the directory
<contract root directory> ::= "src/contract/" <organization ID> "/code"
<Organization ID> ::= See <Contract Mark: organization>
<golang implementation code file name> ::= <legal file name> ".go"
<golang test code file name> ::= <legal file name> "_test.go"
<arbitrary file name> ::= <legal file name>|<illegal file name>
<Illegal file name> ::= [<legal file name>] "autogen" [<legal file name>] | <arbitrary file name> "_test"
<legal file name> ::= Exclude <illegal file name> after all operating systems recognize the string as the file name
```

Note: The white space interval that appears in the specification definition is only required for typesetting and is not part of the specification.

### 4.3 Whitelist

For security reasons, the BCBChain Smart Contract is limited to allow only packages that follow explicit import behaviour and do not produce inconsistent results for different nodes. Such packages are included in the whitelist.

The code packages supported in the whitelist are safe to use in smart contracts.

The specific contents of the whitelist and graylist will be different with the upgrade of the smart contract ```SDK``` and the matching BCBChain plugin version. For details, please refer to the related documents of the smart contract ```SDK``` and the matching BCBChain plugin.

Below is the first version of the whitelist:

```go
//The following are available golang ID packages
bytes
container/heap
container/list
container/ring
crypto
crypto/aes
crypto/cipher
crypto/des
crypto/hmac
crypto/md5
crypto/rc4
crypto/sha1
crypto/sha256
crypto/sha512
encoding
encoding/ascii85
encoding/asn1
encoding/base32
encoding/base64
encoding/binary
encoding/csv
encoding/gob
encoding/hex
encoding/json
encoding/pem
encoding/xml
errors
fmt
hash
hash/adler32
hash/crc32
hash/crc64
hash/fnv
index/suffixarray
math
math/big
math/bits
math/cmplx
reflect
regexp
regexp/syntax
sort
strconv
strings
unicode
unicode/utf16
unicode/utf8

//Below is standard package for the SDK
blockchain/smcsdk/sdk
```

## 5. BRC20 Token

The smart contract "Token" issued in Section 2.1.2 of this guide is a sample token contract, not a ```BRC20``` token that complies with the BCBChain standard.

Users of BCBChain can write their own smart contracts to issue tokens that comply with the ```BRC20``` token specification. This section defines smart contracts that comply with the ```BRC20``` token specification.

The specification is described as follows:

- The contract must explicitly call the interface provided by the Smart Contract SDK ```ITokenHelper::RegisterToken(...)``` to register a new token with BCBChain (each smart contract can only register one token);

- The contract registration token will automatically record a standard token generation receipt on BCBChain. The receipt is defined as follows:

  ```go
  import (
      "blockchain/smcsdk/sdk/bn"
      "blockchain/smcsdk/sdk/types"
  )
  
  // Name of receipt: std::newToken
  type NewToken struct {
      TokenAddress     types.Address `json:"tokenAddr"`     // Token Address
      ContractAddress  types.Address `json:"contractAddr"`  // Coin Contract Address
      Owner            types.Address `json:"owner"`         // Token Owner’s external account address
      Name             string      `json:"name"`            // Token Name
      Symbol           string      `json:"symbol"`          // Token Symbol
      TotalSupply      bn.Number   `json:"totalSupply"`     // Total Token Supply
      AddSupplyEnabled bool        `json:"addSupplyEnabled"`// Whether additional issuance is supported
      BurnEnabled      bool        `json:"burnEnabled"`     // Whether burn is enabled
      GasPrice         int64       `json:"gasPrice"`        // Gas Price
  }
  ```

- The contract must implement the methods and interfaces defined in this section

### 5.1 Transfer

**Method prototype**

```go
import (
    "blockchain/smcsdk/sdk/bn"
    "blockchain/smcsdk/sdk/types"
)

//@:public:method:gas[500]
//@:public:interface:gas[450]
Transfer(types.Address,bn.Number)
```

**Function Description**

- Execute the token transfer

**Implementation note**

- Must be implemented
- Must be marked with markup ```public:method```；
- Must be marked with markup ```public:interface```.

**Usage note**

- Allows calls from transaction broadcasts;
- Allows cross-contract calls with other smart contracts of the organization;
- Allows other smart contracts with the organization to be called directly via the interface provided by the SDK,```IAccount::Transfer``` (the underlying ```SDK``` automatically performs cross-contract calls).

**Input Parameters**

- _to types.Address Token recipient address (can be external account address, contract account address, contract address)
- _value bn.Number Token transfer amount (Unit: Cong)

Note: If the recipient address is a contract address, the received token will be automatically transferred to the account address of the contract.

**Receipt Output**

- The BRC20 Token ```Transfer()``` method automatically records a standard token transfer receipt on BCBChain. The receipt is defined as follows：

  ```go
  import (
      "blockchain/smcsdk/sdk/bn"
      "blockchain/smcsdk/sdk/types"
  )
  
  // Name of receipt: std::transfer
  type Transfer struct {
      Token      smc.Address  `json:"token"`      // Token address
      From       smc.Address  `json:"from"`       // From address
      To         smc.Address  `json:"to"`         // Token recipient address
      Value      bn.Number    `json:"value"`      // The amount of token transferred
  }
  ```

### 5.2 AddSupply

**Method Prototype**

```go
import (
    "blockchain/smcsdk/sdk/bn"
)

//@:public:method:gas[2400]
AddSupply(bn.Number)
```

**Function Description**

- Increase supply of tokens.

**Implementation Note**

- Optional;
- If implemented, requires markup ```public:method```.

**Usage note**

- Only token owners can make calls through transaction broadcasts

**Input Parameters**

- _value bn.Number Newly added supply

**Receipt Output**

- The BRC20 Token ```AddSupply()``` method automatically records a standard token extension receipt on BCBChain. The receipt is defined as follows:

  ```go
  import (
      "blockchain/smcsdk/sdk/bn"
      "blockchain/smcsdk/sdk/types"
  )
  
  // Name of receipt: std::addSupply
  type AddSupply struct {
      Token       types.Address `json:"token"`       // Token address
      Value       bn.Number     `json:"value"`       // Additional supply（单位：cong）
      TotalSupply bn.Number     `json:"totalSupply"` // New total supply（单位：cong）
  }
  ```

- The BRC20 Token ```AddSupply()``` method also automatically records a standard ```std::transfer```receipt on BCBChain

### 5.3 Burn

**Method Prototype**

```go
import (
    "blockchain/smcsdk/sdk/bn"
)

//@:public:method:gas[2400]
Burn(bn.Number)
```

**Function Description**

- Burns the amount supplied.

**Implementation Note**

- Optional;
- If implemented, requires markup```public:method```.

**Usage note**

- Only token owners can make calls through transaction broadcasts.

**Input Parameters**

- _value bn.Number Burn the amount supplied (Unit: Cong)

**Receipt Output**

- The BRC20 Token ```Burn()``` method automatically records a standard token burning receipt on BCBChain. The receipt is defined as follows:

  ```go
  import (
      "blockchain/smcsdk/sdk/bn"
      "blockchain/smcsdk/sdk/types"
  )
  
  // Name of receipt: std::burn
  type Burn struct {
      Token       types.Address `json:"token"`       // Token address
      Value       bn.Number     `json:"value"`       // 燃烧的供应量（单位：cong）
      TotalSupply bn.Number     `json:"totalSupply"` // 新的总供应量（单位：cong）
  }
  ```
  
- The BRC20 Token ```Burn()``` method also automatically records a standard ```std::transfer``` receipt on BCBChain.

### 5.4 SetGasPrice

**Method Prototype**

```go
//@:public:method:gas[2400]
SetGasPrice(int64)
```

**Function Description**

- Sets the price for Gas.

**Implementation Note**

- Optional;
- If implemented, requires markup public:method.

**Usage note**

- Only token owners can make calls through transaction broadcasts

**Input Parameters**

- _value int64 New gas price (Unit: Cong)

**Receipt Output**

- The BRC20 Token ```SetGasPrice()``` method automatically records a standard set gas price receipt on BCBChain. The receipt is defined as follows:

  ```go
  import (
      "blockchain/smcsdk/sdk/types"
  )
  
  // Name of receipt: std::setGasPrice
  type SetGasPrice struct {
      Token    types.Address `json:"token"`    // Token address
      GasPrice int64         `json:"gasPrice"` // Gas Price (Unit: Cong)
  }
  ```

### 5.5 SetOwner

**Method Prototype**

```go
import (
    "blockchain/smcsdk/sdk/types"
)

//@:public:method:gas[2400]
SetOwner(types.Address)
```

**Function Description**

- Transfer ownership of smart contracts and tokens.

**Implementation Note**

- Optional;
- If implemented, requires markup ```public:method```.

**Usage note**

- Only token owners can make calls through transaction broadcasts

**Input Parameters**

- _newOwner types.Address Address of the new owner of the contract.

**Receipt Output**

- The BRC20 Token ```SetOwner()``` method automatically records a standard transfer ownership receipt on BCBChain. The receipt is defined as follows:

  ```go
  import (
      "blockchain/smcsdk/sdk/types"
  )
  
  // Name of receipt: std::setOwner
  type SetOwner struct {
      ContractAddr types.Address `json:"contractAddr"` // Address of the smart contract
      NewOwner     types.Address `json:"newOwner"`     // The external account address of the new owner
  }
  ```

- The BRC20 Token ```SetOwner()``` method also automatically records a standard ```std::transfer``` receipt on BCBChain.
