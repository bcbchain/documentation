# Communication protocol

## 1. Overview

Bcbchain supports the following `RPC` protocol:

* `URI over HTTP or HTTPS`
* `JSONRPC over HTTP or HTTPS`

All `RPC` interfaces and their parameters supported by bcbchain can be obtained through `URL`： `http://ip:port`  or `https://ip:port`, or through the domain name of a well-known node, for example: <https://earth.bcbchain.io.>

bcb follower node（tendermint）the list of `RPC` interface is as follow(supports' HTTP 'or' HTTPS')

```html
Available endpoints:
//earth.bcbchain.io/abci_info
//earth.bcbchain.io/dump_consensus_state
//earth.bcbchain.io/genesis
//earth.bcbchain.io/genesis_pkg
//earth.bcbchain.io/health
//earth.bcbchain.io/net_info
//earth.bcbchain.io/num_unconfirmed_txs
//earth.bcbchain.io/status
//earth.bcbchain.io/unconfirmed_txs

Endpoints that require arguments:
//earth.bcbchain.io/abci_query?path=_&data=_&height=_&trusted=_
//earth.bcbchain.io/abci_query_ex?path=_
//earth.bcbchain.io/block?height=_
//earth.bcbchain.io/block_results?height=_
//earth.bcbchain.io/blockchain?minHeight=_&maxHeight=_
//earth.bcbchain.io/broadcast_tx_async?tx=_
//earth.bcbchain.io/broadcast_tx_commit?tx=_
//earth.bcbchain.io/broadcast_tx_sync?tx=_
//earth.bcbchain.io/commit?height=_
//earth.bcbchain.io/tx?hash=_&prove=_
//earth.bcbchain.io/validators?height=_
```

## 2. URI over HTTP

When use `GET` method of the `HTTP` protocol for `RPC` requests, the parameters must be `URI` encoded. For the `URL` format of all `RPC` calls, please refer to the above table. For specific business and parameter descriptions, please refer to the subsequent sections of this chapter.

## 3. JSONRPC over HTTP

When use `POST` method of the `HTTP` protocol for `RPC` requests, it will use the `JSONRPC` application protocol, the format of the `HTTP` data body of the request is as follows:

```json
Example：
{
  "jsonrpc": "2.0",
  "id": "dontcare/anything",
  "method": " broadcast_tx_commit",
  "params": {
    "tx": "bcb<tx>.v2.xxxxxx.<1>.xxxxxx"
  }
}
```

Please refer to the following chapters for specific communication interface services and parameter descriptions.

After successfully execute interface, the general data structure is defined as follows:

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    ...  //different APIs return different JSON structures, and they are customized.
  }
}
```

After unsuccessfully execute interface, the general data structure is defined as follows:(all interfaces return the same data structure when failed):

```json
{
  "jsonrpc": "2.0",
  "id": "",
  "error": {
    "code": -32603,
    "message": "Internal error",
    "data": "Error on broadcastTxCommit: Tx already exists in cache"
  }
}
```
