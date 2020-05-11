# Protocol

## 1. Protocol Overview

bcbXwallet_rpc server supports the the following PRC communication protocols:

- URI over HTTPS

- JSONRPC over HTTPS

  All RPC interfaces supported by the bcbXwallet_rpc server and their parameters can be obtained at: <https://ip:port>

  The list of RPC interfaces provided by the bcbXwallet_rpc server is as follows (supports HTTPS, default port 37657):
  
  ```html
  Available endpoints:
  //localhost:37657/bcb_blockHeight
  //localhost:37657/bcb_version
  
  Endpoints that require arguments:
  //localhost:37657/bcb_allBalance?address=_
  //localhost:37657/bcb_balance?address=_
  //localhost:37657/bcb_balanceOfToken?address=_&tokenAddress=_&tokenName=_
  //localhost:37657/bcb_block?height=_
  //localhost:37657/bcb_commitTx?tx=_
  //localhost:37657/bcb_nonce?address=_
  //localhost:37657/bcb_transaction?txHash=_
  //localhost:37657/bcb_transfer?name=_&accessKey=_&walletParams=_
  //localhost:37657/bcb_transferOffline?name=_&accessKey=_&walletParams=_
  //localhost:37657/bcb_walletCreate?name=_&password=_
  //localhost:37657/bcb_walletExport?name=_&password=_&accessKey=_&plainText=_
  //localhost:37657/bcb_walletImport?name=_&privateKey=_&password=_&accessKey=_&plainText=_
  //localhost:37657/bcb_walletList?pageNum=_
  ```

## 2. URI over HTTP

When using the HTTP GET method for RPC requests, the parameters must be URI-encoded. For the URL format of all RPC calls, see the list above. For details about each service and its parameters, refer to the following parts of this section.

## 3. JSONRPC over HTTP

When using HTTP POST and JSONRPC application protocol for requests, data body format is as follows:

```json
Example：
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": "bcb_block",
  "params": {
    "height": 2500
  }
}
```

Refer to the following parts of the section for in-depth information on the services and their parameters.

General format of the return data of a successful request is as below:

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    …  //JSON format varies depending on the api called
  }
}
```

General format of the return data of a failed request is as below (same for all failed requests):

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "error": {
    "code": -32603,
    "message": "Invalid parameters.",
    "data": ""
  }
}
```
