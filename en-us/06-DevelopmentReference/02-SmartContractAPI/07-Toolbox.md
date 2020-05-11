# Toolbox

## 1. sdk/forx

The package ```blockchain/smcsdk/sdk/mapx``` encapsulates the application interface that optimizes the for loop.

### 1.1 func Range()

Function prototype:

```go
func Range(args... interface{})
```

The keyword ```for``` is not allowed to be used in any part of the smart contract code.

To perform loops, use the ```Range()``` function instead.

There are six ways to use the ```Range()``` function, examples are as follows:

**Model one:**

```go
func Range( m map[keyType]valType, f func(key keyType, val valType) )
func Range( m map[keyType]valType, f func(key keyType, val valType) bool )
```

The traversal operation is performed on the mapping table object m, and the order of the traversal is based on the mapping table key. The operation function is f. If the return value of f is defined as void, the loop can be ended after the traversal is finished. If the return value of f is a boolean, false value will terminate the execution of the traversal operation and exit the loop, while true value will continue the traversal operation. The input parameters are required to meet the following conditions. If any one is not satisfied, an exception occurs. When an exception occurs, the SDK will automatically trigger a panic:

> - The type of the parameter m must be a mapping table;
> - The parameter f must be a function, and the return value of the function must be between void and boolean type;
> - Function f must have two arguments
> - The first parameter type of the function f must be the type corresponding to the key of the mapping table m;
> - The second parameter type of the function f must be the type corresponding to the value of the mapping table m.

The sample code is as follows:

```go
m := make(map[int]string)
m[93] = "23231"
m[13] = "23423423234324"
m[54] = "3432432423"
m[23] = "3434545345345"

forx.Range(m, func(k int, v string) {
    printf("key=%v value=%v\n", k, v)
})
```

**Model two:**

```go
func Range( s []valType, f func(i int, val valType) )
func Range( s []valType, f func(i int, val valType) bool )
```

The traversal operation is performed on the object array s. The traversal is performed in order of the array order from front to end. The operation function is f. If the return value of f is defined as void, the loop can be ended after the traversal is finished.  If the return value of f is a boolean, false value will terminate the execution of the traversal operation and exit the loop, while true value will continue the traversal operation. The input parameters are required to meet the following conditions. If any one is not satisfied, an exception occurs. When an exception occurs, the SDK will automatically trigger a panic:

> - The type of the parameter m must be an array;
> - The parameter f must be a function, and the return value of the function must be between void and boolean type;
> - Function f must have two arguments
> - The first argument type of function f must be of type int, indicating the index number of the element, starting at 0;
> - The second parameter type of function f must be the type corresponding to the element value of array s.

The sample code is as follows:

```go
s := make([]string)
s = append(s, "23231")
s = append(s, "423792234")
s = append(s, "23232")
s = append(s, "3243455454")

forx.Range(s, func(i int, v string) {
    printf("i=%v value=%v\n", i, v)
})
```

**Model three:**

```go
func Range( n intType, f func(i intType) )
func Range( n intType, f func(i intType) bool )
```

The loop executes for the specified number of times. The operation function is f. If the return value of f is defined as void, the loop can be ended after the specified number of times. If the return value of f is a boolean, false value will exit the loop, while true value will continue the loop. The input parameters are required to meet the following conditions. If any one is not satisfied, an exception occurs. When an exception occurs, the SDK will automatically trigger a panic:

> - The type of the parameter n must be a type that expresses an integer, such as: int, uint, int32, etc., and the value must be greater than or equal to 0;
> - The parameter f must be a function, and the return value of the function must be between void and boolean type;
> - Function f must have exactly one argument. The type must be the same type of argument n, indicating the index number of the execution loop, starting at 0.

The sample code is as follows:

```go
forx.Range(10, func(i int) {
    printf("i=%v\n", i)
})
```

**Model four:**

```go
func Range( m,n intType, f func(k intType) )
func Range( m,n intType, f func(k intType) bool )
```

According to the input parameters, all integers between m and n (including m and n) are traversed, starting from m and ending at n, the operation function is f. If the return value of f is defined as void, the loop can be ended after the traversal is over. If the return value of f is a boolean, false value will terminate the execution of the traversal operation and exit the loop, while true value will continue the traversal operation. The input parameters are required to meet the following conditions. If any one is not satisfied, an exception occurs. When an exception occurs, the SDK will automatically trigger a panic:

> - The parameters m and n must be of the same type that express an integer, for example: int, uint, int32, etc. If m is less than n, then the loop will be in ascending order. If m is greater than n, the order will be descending;
> - The parameter f must be a function, and the return value of the function must be between void and boolean type;
> - Function f must have exactly one argument. The type must be the same type as the arguments m and n, representing the integer value traversed, starting at m.

The sample code is as follows:

```go
forx.Range(1,100, func(k int) {
    printf("k=%v\n", k)
})
```

**Model five:**

```go
func Range( c func() bool, f func(i int) )
func Range( c func() bool, f func(i int) bool )
```

The loop executes the function f. When the control function c returns true, the loop is terminated. This controls when the loop ends. If the return value of f is a boolean, false value will exit the loop, while true value will continue the loop. The input parameters are required to meet the following conditions. If any one is not satisfied, an exception occurs. When an exception occurs, the SDK will automatically trigger a panic:

> - The parameter c must be a function, and the return value of the function must be a boolean type;
> - The parameter f must be a function, and the return value of the function must be between void and boolean type;
> - Function f must have exactly one argument. The type must be int, indicating the index of the number of execution loops, starting at 0.

The sample code is as follows:

```go
toVoter := ballot._voters(to)
forx.range( func() bool {
              return toVoter.delegate != ""
            },
            func(i int) {
              to = toVoter.delegate
              toVoter = ballot._voters(to)
            })
```

**Model six**

```go
func Range( f func(i int) bool )
```

The loop will execute function f in each iteration. Since the return value of f is a boolean, false value will exit the loop, while true value will continue the loop. The input parameters are required to meet the following conditions. If any one is not satisfied, an exception occurs. When an exception occurs, the SDK will automatically trigger a panic:

> - The argument f must be a function, and the return value of the function must be a boolean type;
> - Function f must have exactly one argument. The type must be int, which represents the index of the number of execution loops, starting at 0.

The sample code is as follows:

```go
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

Function prototype:

```go
func RangeReverse(args... interface{})
```

RangeReverse provides a for loop that traverses slices in reverse.
There is a model for the `RangeReverse ()` function.

**Model one:**

```go
func RangeReverse( s []valType, f func(i int, val valType) )
func RangeReverse( s []valType, f func(i int, val valType) bool )
```

The traversal operation is performed on the slice object s. The traversal is performed in the order of the slice from large to small. The operation function is f. If the return value of f is defined as empty, the loop can be ended after the traversal is completed. Type, f returns false to terminate the traversal operation and end the loop, and f returns true to continue the traversal operation. The input parameters are required to meet the following conditions. If any one is not satisfied, an exception occurs. When an exception occurs, the SDK will automatically trigger a panic:

> - The type of parameter s must be a slice;
> - The parameter f must be a function, and the return value of the function must be one of null and Boolean;
> - Function f must have two arguments;
> - The first parameter type of function f must be of type int, which represents the index number of the element, starting from len (s) -1 and decreasing;
> - The second argument type of function f must be the type corresponding to the element value of slice s.

The sample code is as follows:

```go
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

The package ```blockchain/smcsdk/sdk/jsoniter``` encapsulates a simple application interface to ```jsoniter```, a third-party package that quickly processes JSON data.

### 2.1 func Marshal()

Function prototype:

```go
func Marshal(v interface{}) ([]byte, error)
```

Serializes the input object ```v``` into a JSON-formatted string and returns it.

### 2.2 func Unmarshal()

Function prototype:

```go
func Unmarshal(bz []byte, v interface{}) error
```

Deserializes the input JSON string to the object pointed to by ```v```.

## 3. sdk/rlp

The package ```blockchain/smcsdk/sdk/rlp``` encapsulates the BCBChain RLP encoding of the transaction. The source code is based on the open source version of ```geth```. Due to BCBChain requirements, codec support for ```bn.Number``` large numbers is added, as well as support for mapping tables.
