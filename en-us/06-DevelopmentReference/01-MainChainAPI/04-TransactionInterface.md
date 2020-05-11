# Transaction Interface

## 1. broadcast\_tx\_commit

Submit a transaction to the node of bcbchain, which calls the method of smart contract. The message type must be "bcb\<tx>", the transaction contained in the message allows the smart contract to modify the **bcchain** world state, and the interface will block until it fails or the delivertx execution is completed and the execution result has been written to the latest block.

**. Request URI over HTTP/HTTPS**

```html
http://earth.bcbchain.io/broadcast_tx_commit?tx="bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
or
https://earth.bcbchain.io/broadcast_tx_commit?tx="bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "broadcast_tx_commit",
  "params": {
    "tx": "bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
  }
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | :------: | ------------------------------------------------------------ |
| tx       |  String  | A string that follows the message format defined in Chapter 5 of this article, with the message type limited to "bcb\<tx>"  |

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "check_tx": {
      "code": 200,
      "log": "Check tx succeed",
      "tx_hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7"
    },
    "deliver_tx": {
      "code": 200,
      "log": "Deliver tx succeed",
      "gas_limit": 2500,
      "gas_used": 500,
      "fee": 1250000,
      "tx_hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7",
      "height": 1881
    },
    "hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7",
    "height": 1882
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter** |   **type**    | **comment** |
| ----------------------------- | :-----------: | ------------------------------------------------------------ |
| check\_tx: {  | Object    | The execution result of the transaction in the verification / endorsement phase.    |
| &nbsp;&nbsp;code        | Int       | Transaction verification / endorsement result code. 200 indicates success.   |
| &nbsp;&nbsp;log          | String    | The description of the transaction verification / endorsement result. When the code is not equal to 200, it will describe a specific error information  |
| &nbsp;&nbsp;tx\_hash     | HexString | Transaction hash                                              |
| }                 |           |                                                              |
| deliver\_tx: { |           | The execution result of the transaction in the confirmation stage.        |
| &nbsp;&nbsp;code        | Int       | Transaction execution result code, 200 indicates success.                          |
| &nbsp;&nbsp;log          | String    | For the description of the transaction execution result, when the code is not equal to 200, it will describe a specific error information |
| &nbsp;&nbsp;gas\_limit | Int64     |The gas limit specified by the transaction sponsor.            |
| &nbsp;&nbsp;gas\_used   | Int64     | The gas limit at which the transaction is executed actually.                        |
| &nbsp;&nbsp;fee     | Int64     | Transaction fee(uint: **cong**)                     |
| &nbsp;&nbsp;tx\_hash     | HexString | Transaction hash                                              |
| &nbsp;&nbsp;height     | Uint64    | At what height is the transaction confirmed.                         |
| }                 |           |                                                              |
| hash         | HexString | Transaction hash                                              |
| height     | Uint64    | At what height is the transaction confirmed.                         |

## 2. broadcast\_tx\_sync

Submit a transaction to the node of bcbchain, which calls the method of smart contract. The message type must be "bcb\<tx>", the transaction contained in the message allows the smart contract to modify the **bcchain** world state, and the interface will not return until the failure or the completion of the node verification / endorsement stage of the received transaction (the completion of a single node checktx). After that, the client can use the hash of the returned transaction to query the final execution result of the transaction.

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/broadcast_tx_sync?tx="bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
or
https://earth.bcbchain.io/broadcast_tx_sync?tx="bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "broadcast_tx_sync",
  "params": {
    "tx": "bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
  }
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | :------: | ------------------------------------------------------------ |
| tx       |  String  | A string that follows the message format defined in Chapter 5 of this article, with the message type limited to "bcb\<tx>"  |

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "code": 200,
    "data": "",
    "log": "Check tx succeed",
    "hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7"
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**                      |   **type**    | **comment** |
| ----------------------------- | :-----------: | ------------------------------------------------------------ |
| code | Int | Transaction verification / endorsement result code. 200 indicates success. |
| data |  String | Reserver                                |
| log |  String | The description of the transaction result, when the code is not equal to 200, it will describe a specific error information. |
| hash | HexString | Transaction hash |

## 3. broadcast\_tx\_async

Submit a transaction to the node of bcbchain, which calls the method of smart contract. The message type must be "bcb\<tx>", the transaction contained in the message allows the smart contract to modify the **bcchain** world state. After the blockchain receives the request from the interface and checks the request URL parameter, it calculates the transaction hash and returns it to the client immediately. After that, the client can use the returned transaction hash to query the final execution result of the transaction.

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/broadcast_tx_async?tx="bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
or
https://earth.bcbchain.io/broadcast_tx_async?tx="bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "broadcast_tx_async",
  "params": {
    "tx": "bcb<tx>.v1.CZxGwH5UgYK1nv2kJKvZ7WVsNzHSGfHmLg94csSZ8365oReLrf2cuqYEjUaHBSmYc1UK79S6crDJpKXJXhyKdvowUCRonTKHC9hUzznKEJVCtB55of43P8zT2Zo1TcoSGuVbyhZxZy2WS25nS1XAoisqH9izsnZnNcSPKps.<1>.YTgiA1gdDGi2L8hyCkL2y6X6icLSZu1eA1yTLZ8RCqRvuApMm58t4BGrJdm4wpUNyqA7khGhhMU7BDQ7qXrBYGV2etAUxGg4AMCDtG5PX9zRXNwepoWzTgu51gPMUHCsKb9TkM3AFxceNoCecHnEp"
  }
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | :------: | ------------------------------------------------------------ |
| tx       |  String  | A string that follows the message format defined in Chapter 5 of this article, with the message type limited to "bcb\<tx>"  |



**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "code": 200,
    "data": "",
    "log": "",
    "hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7"
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**                      |   **type**    | **comment** |
| ----------------------------- | :-----------: | ------------------------------------------------------------ |
| code | Int | Execute transaction result, 200 indicates success |
| data |  String | Reserver                                |
| log |  String | The description of the transaction result, when the code is not equal to 200, it will describe a specific error information. |
| hash | HexString | Transaction hash |

## 4. tx

Submit the execution result of query specified transaction to BCBChain's node.

**. Request URI over HTTP/HTTPS**

```text
http://earth.bcbchain.io/tx?hash="8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7"
or
https://earth.bcbchain.io/tx?hash="8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7"
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "tx",
  "params": {
    "hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7"
  }
}
```

**. Request Parameters**

| **Parameter** | **type**  | **comment** |
| -------- | :-------: | ------------------------------------------------------------ |
| hash     | HexString | Transaction hash                                              |

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7",
    "height": 1882,
    "index": 0,
    "deliver_tx": {
      "code": 200,
      "log": "Deliver tx succeed",
      "gas_limit": 2500,
      "gas_used": 500,
      "fee": 1250000,
      "tx_hash": "8F928C4F932D8D7938E3EC186082D9FB002969785C1131B722F2F7123ED267A7",
      "height": 1882
    },
    "check_tx": {},
    "tx": null,
    "state_code": 3
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**                      |   **type**    | **comment** |
| ----------------------------- | :-----------: | ------------------------------------------------------------ |
| hash         | String    | Transaction hash                                              |
| height    | Uint64    | The block height of the exchange in the block is 0 when the transaction has not yet fallen into the block.   |
| index         | Uint32    | Index of the transaction in the block (encoded from 0).              |
| deliver\_tx: {  | Object    | Confirm the execution result of the transaction.                   |
| &nbsp;&nbsp;code        | Int       | Transaction execution result code, 200 indicates success.                          |
| &nbsp;&nbsp;log          | String    | The description of the transaction result, when the code is not equal to 200, it will describe a specific error information. |
| &nbsp;&nbsp;gas\_limit | Int64     |The gas limit specified by the transaction sponsor.                    |
| &nbsp;&nbsp;gas\_used   | Int64     | The gas limit at which the transaction is executed actually.                        |
| &nbsp;&nbsp;fee     | Int64     | Transaction fee(uint: **cong**)                     |
| &nbsp;&nbsp;tx\_hash     | HexString | Transaction hash                                              |
| &nbsp;&nbsp;height    | Uint64    | Block height of the transaction in the block.                                |
| }                 |           |                                                              |
| check\_tx | Object    | The structure of the verification/endorsement execution result of the transaction is the same as "deliver\_tx"         |
| tx        | Object    | Reserver                                                       |
| state\_code | Uint32    | Status code:   <br>&nbsp;&nbsp;1:  checking;   <br>&nbsp;&nbsp;2: Check completed(the result of checking may be success or failure);   <br>&nbsp;&nbsp;3: deliver completed(the result of deliver may be success or failure);   <br>&nbsp;&nbsp;4:  Check and deliver both query (transactions are submitted and queried at the same node, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; and query before timeout) |
