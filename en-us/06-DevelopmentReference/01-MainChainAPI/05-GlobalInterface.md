# Global Interface

## 1. abci\_query

Query **bcchain** world status from BCBChain node.

**. Request URI over HTTP/HTTPS**

```html
http://earth.bcbchain.io/abci_query?path="/genesis/token"
or
https://earth.bcbchain.io/abci_query?path="/genesis/token"
```

**. Request JSONRPC over HTTP/HTTPS**

```json
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "abci_query",
  "params": {
    "path": "/genesis/token "
  }
}
```

**. Request Parameters**

| **Parameter** | **type** | **comment** |
| -------- | :------: | ------------------------------------------------------------ |
| path     |  String  | The key value to query.                                         |

**. Response SUCCESS Example**

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "response": {
      "code": 200,
      "key": "L2dlbmVzaXMvdG9rZW4=",
      "value": "eyJhZGRyZXNzIjoiYmNiTFZnYjNvZFRmS0M5WTlHZUZuTldMOXdtUjRwd1dpcXdlIiwib3duZXIiOiJiY2I4eU5lcUFpeFo3RERReDFmSFN2UWRBM2tLRFE0OGdjaTciLCJ2ZXJzaW9uIjoiIiwibmFtZSI6IkJDQiIsInN5bWJvbCI6IkJDQiIsInRvdGFsU3VwcGx5Ijo1MDAwMDAwMDAwMDAwMDAwMDAwLCJhZGRTdXBwbHlFbmFibGVkIjpmYWxzZSwiYnVybkVuYWJsZWQiOmZhbHNlLCJnYXNwcmljZSI6MjUwMH0="
    }
  }
}
```

**. Response SUCCESS Parameters**

| **Parameter**         |   **type**    | **comment** |
| ---------------- | :-----------: | ------------------------------------------------------------ |
| response: {   |         |        |
| &nbsp;&nbsp;code |    Int  | bcbchain program execution result of this operation, 200 indicates success. |
| &nbsp;&nbsp;log  | String | The description of the execution result, when the code is not equal to 200, it will describe a specific error information. |
| &nbsp;&nbsp;key  | Base64 String | The key value of the request query is a Base64 encoded string. |
| &nbsp;&nbsp;value      | Base64 String | After the query is successful, the value of the corresponding key value in the blockchain status database is returned <br/> The output string is encoded according to Base64, and the encoded original data is JSON format <br/> string. When the key value does not exist, there is no "value" field in the returned result. |
| }                |               |                                                              |

## 2. abci_query_ex

Query multiple **bcbchain** world states from BCBChain nodes at a time.

- **Request URI over HTTP/HTTPS**

  ```text
  http://earth.bcbchain.io/abci_query_ex?path="/token/[bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe,bcbMLpC7HFd8JCm6RXQiu1t7aX4GaiW5c4Cm]"
  or
  https://earth.bcbchain.io/abci_query_ex?path="/token/[bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe,bcbMLpC7HFd8JCm6RXQiu1t7aX4GaiW5c4Cm]"
  ```

- **Request JSONRPC over HTTP/HTTPS**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "dontcare/anything",
    "method": "abci_query_ex",
    "params": {
      "path": "/token/[bcbLVgb3odTfKC9Y9GeFnNWL9wmR4pwWiqwe,bcbMLpC7HFd8JCm6RXQiu1t7aX4GaiW5c4Cm]"
    }
  }
  ```

- **Request Parameters**

  | **Parameter** | **type** | **comment** |
  | -------- | :------: | ------------------------------------------------------------ |
  | path     |  String  |  As for the **KEY** value to query, multiple **KEY** values are enclosed in square brackets **[ ]**, separated by **,**, for example: <br>&nbsp;&nbsp;&nbsp;&nbsp;**/token[token address1, token address2, token address3]**|

- **Response SUCCESS Example【参见：[abci_query.json](./json20/abci_query.json)】**

  ```json
  {
    "jsonrpc": "2.0",
    "id": "",
    "result": {
      "response": {
        "code": 200,
        "KeyValues": [
          {
            "key": "L3Rva2VuL2JjYkxWZ2Izb2RUZktDOVk5R2VGbk5XTDl3bVI0cHdXaXF3ZQ==",
            "value": "eyJhZGRyZXNzIjoiYmNiTFZnYjNvZFRmS0M5WTlHZUZuTldMOXdtUjRwd1dpcXdlIiwib3duZXIiOiJiY2I4eU5lcUFpeFo3RERReDFmSFN2UWRBM2tLRFE0OGdjaTciLCJ2ZXJzaW9uIjoiIiwibmFtZSI6IkJDQiIsInN5bWJvbCI6IkJDQiIsInRvdGFsU3VwcGx5Ijo2NjAwMDAwMDAwMDAwMDAwMCwiYWRkU3VwcGx5RW5hYmxlZCI6ZmFsc2UsImJ1cm5FbmFibGVkIjpmYWxzZSwiZ2FzcHJpY2UiOjI1MDB9"
          },
          {
            "key": "L3Rva2VuL2JjYk1McEM3SEZkOEpDbTZSWFFpdTF0N2FYNEdhaVc1YzRDbQ==",
            "value": "eyJhZGRyZXNzIjoiYmNiTUxwQzdIRmQ4SkNtNlJYUWl1MXQ3YVg0R2FpVzVjNENtIiwib3duZXIiOiJiY2I4eU5lcUFpeFo3RERReDFmSFN2UWRBM2tLRFE0OGdjaTciLCJ2ZXJzaW9uIjoiIiwibmFtZSI6IlVTRFgiLCJzeW1ib2wiOiJVU0RYIiwidG90YWxTdXBwbHkiOjIwMDAwMDAwMDAwMDAwMDAwMCwiYWRkU3VwcGx5RW5hYmxlZCI6dHJ1ZSwiYnVybkVuYWJsZWQiOnRydWUsImdhc3ByaWNlIjoyNTAwfQ=="
          }
        ]
      }
    }
  }
  ```

- **Response SUCCESS Parameters**

  | **Parameter**          |   **type**    | **comment** |
  | ----------------- | :-----------: | ------------------------------------------------------------ |
  | response: {       |               |                                                              |
  | &nbsp;&nbsp;code  |      Int      | bcbchain program execution result of this operation, 200 indicates success.                |
  | &nbsp;&nbsp;log   |    String     | The description of the execution result, when the code is not equal to 200, it will describe a specific error information. |
  | &nbsp;&nbsp;KeyValues: [{|               |                                                              |
  | &nbsp;&nbsp;&nbsp;&nbsp;key   | Base64 String | The key value of the request query is a Base64 encoded string.                        |
  | &nbsp;&nbsp;&nbsp;&nbsp;value | Base64 String | After the query is successful, the value of the corresponding key value in the blockchain status database is returned <br/> The output string is encoded according to Base64, and the encoded original data is JSON format <br/> string. When the key value does not exist, there is no "value" field in the returned result. |
  | &nbsp;&nbsp;}] |               |                                                              |
  | }                 |               |                                                              |
