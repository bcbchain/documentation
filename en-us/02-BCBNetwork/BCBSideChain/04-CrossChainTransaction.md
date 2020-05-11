# Cross-Chain Transfer

> In this section, we will experience how to achieve cross-chain transfer based on the built side chain `SmartCity` and `EShop`.
>
> BCB chain supports three modes of cross-chain transfer, they are main chain to side chain, side chain to main chain, and side chain to side chain, respectively.

## 1. Preparation

### 1.1 Prepare account

Prepare a transfer account for the side chain, we assume that the account user name created is `scAccount`, the password is `Ab1@Cd3$`, an account address on the side chain `SmartCity` is `local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG`,another account address on the side chain `EShop` is `local[EShop]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG`.

> Learn how to create an account, please refer to [BCBTools-bcwTool](../../03-BCBTools\02-bcw.md)

## 2. Token cross-chain transfer

### 2.1 Transfer from the main chain to the side chain

As for the transfer of the main chain to the side chain, we use the owner account on the main chain to transfer to the account `local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG` on the side chain `SmartCity` which prepares in step one. Before transferring, we query the account balance on the side chain `SmartCity`, we take the token is `LOC` on the main chain as an example to show how to query the account balance:

```shell
./bcc balance --accAddress="local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG" --tokenName="LOC" --chainid local[SmartCity]

Expected return results:

OK
Response: [
  {
    "tokenAddress": "local[SmartCity]AJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA",
    "tokenName": "LOC",
    "balance": "0"
  }
]
```

We can see the token balance of the new account is 0.

We take the token is `LOC` as an example to show how to execute transfer operation from the account `owner` on the main chain to the account `scAccount` on the side chain:

```shell
./bcc transfer --name owner --password Ab1@Cd3$ --token LOC --gasLimit 100000  --to local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG --value 100 --chainid local

Expected return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 5000000,
  "txHash": "0x6C8C4A3324C87ECE2EC85F03D25D3994AB5BE31183AED6F7D8044CA2CCC0F25F",
  "height": 25974
}
```

The value of `to` is the account `scAccount` on the side chain, `value` is the transfer amount in `LOC`.

Waiting for abount 5s, we query the account balance of the account `local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG` on the side chain:

```shell
./bcc balance --accAddress="local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG" --tokenName="LOC" --chainid local[SmartCity]

Expected return results:

OK
Response: [
  {
    "tokenAddress": "local[SmartCity]AJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA",
    "tokenName": "LOC",
    "balance": "100000000000"
  }
]
```

Because the showing balance is in `cong`, so it needs to be multiplied by the 9th power of 10 on the basis on the value of `100`. If the account balance is not in the account(maybe transaction is still on pending), you can query this cross-chain transaction by getting `transaction Hash` on the target chain(refer to the section 2, Cross-Chain Creation). If the cross-chain transaction status is shown to have been completed, but the query balance is still not in the account, you can query the failure reason according to the section 2, Cross-Chain Creation.

### 2.2 Transfer from the side chain to the main chain

We transfer 100 `LOC` to the account `scAccount` on the side chain, now if we want to transfer the funds back to the main chain, we can do it by the transfer of the side chain to the main chain, at first, we query the balance of the account address `localHMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG` on the main chain:

```shell
./bcc balance --accAddress="localHMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG" --tokenName="LOC" --chainid local

Return results:

OK
Response: [
  {
    "tokenAddress": "localAJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA",
    "tokenName": "LOC",
    "balance": "0"
  }
]
```

Then use the following command to transfer:

```shell
./bcc transfer --name scAccount --password Ab1@Cd3$ --token LOC --gasLimit 100000  --to localHMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG --value 10 --chainid local[SmartCity]

Expected return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 10000000,
  "txHash": "0x20B5238E777BDA4D7F883C0698C608C30874A080DCB2FAAAFD1C8EF4FBD98098",
  "height": 6225
}
```

Check the account balance at the receipt address:

```shell
./bcc balance --accAddress="localHMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG" --tokenName="LOC" --chainid local
OK
Response: [
  {
    "tokenAddress": "localAJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA",
    "tokenName": "LOC",
    "balance": "10000000000"
  }
]
```

We can see the funds is transferred from the side chain to the main chain successfully, confirm the success of cross-chain transfer. If the account balance is not in the account(maybe transaction is still on pending), you can query this cross-chain transaction by getting `transaction Hash` on the target chain(refer to the section 2, Cross-Chain Creation). If the cross-chain transaction status is shown to have been completed, but the query balance is still not in the account, you can query the failure reason according to the section 2, Cross-Chain Creation.

### 2.3 Transfer from the side chain to the side chain

If we want to transfer from one side chain to the another side chain, what should we do?

At first, we prepare another side chain `EShop`, refer to [Side Chain Registration](01-SideChainRegistration.md) and [Side Chain Creation](02-SideChainCreation.md)

Then we query the balance of the account address `local[EShop]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG` on the side chain `EShop`:

```shell
./bcc balance --accAddress="local[EShop]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG" --tokenName="LOC" --chainid local[EShop]

Expected return results:

OK
Response: [
  {
    "tokenAddress": "local[EShop]AJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA",
    "tokenName": "LOC",
    "balance": "0"
  }
]
```

Next, we start to transfer from the side chain `SmartCity` to the side chain `EShop`:

```shell
./bcc transfer --name scAccount --password Aa1@Cd3$ --token LOC --gasLimit 100000  --to local[EShop]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG --value 10 --chainid local[SmartCity]

Expected return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 10000000,
  "txHash": "0x25FEA54305EDE927A7FDC47AE28FE3B2D29A8FB54A85080CBD7C738A7B0FB7C8",
  "height": 6559
}
```

Query the balance of the account address `local[EShop]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG` on the side chain `EShop` again:

```shell
./bcc balance --accAddress="local[EShop]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG" --tokenName="LOC" --chainid local[EShop]

Expected return results:

OK
Response: [
  {
    "tokenAddress": "local[EShop]AJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA",
    "tokenName": "LOC",
    "balance": "10000000000"
  }
]
```

we can confirm the success of cross-chain transfer from above infomation. If the account balance is not in the account(maybe transaction is still on pending), you can query this cross-chain transaction by getting `transaction Hash` on the target chain(refer to the section 2, Cross-Chain Creation). If the cross-chain transaction status is shown to have been completed, but the query balance is still not in the account, you can query the failure reason according to the section 2, Cross-Chain Creation.

### 2.4 Token activation

If we want our side chain to support some type of standard tokens, we can use token activation function; We take the activation of token `TST` on the side chain `SmartCity` as an example to show how to activate token on the side chain:

```shell
./bcc call --contract token-issue --method Activate --splitBy @ --params "TST"@"SmartCity" --gasLimit 100000 --orgName genesis --name scowner --password SCOwner@2019 --chainid local

Expected return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 131000000,
  "txHash": "0x177CE19688464BCCC35F78288B28E1D0E766ACF302A7A3E994D86100F7D2CAAE",
  "height": 47177
}
```

We can check on the side chain whether to generate the information corresponding to the token.

```shell
 ./bcc query -k "/token/name/TST" --chainid local[SmartCity]

Return results:

OK
Response:
  Code: 200
  Key: /token/name/TST
  Value: "local[SmartCity]8GPJL6ipTyYRNr5xTyGWWFayd2k1EoLYu"
```

We can get token address from above, we also can use following command to query the token information:

```shell
./bcc query -k "/token/local[SmartCity]8GPJL6ipTyYRNr5xTyGWWFayd2k1EoLYu" --chainid local[SmartCity]

Return results:

OK
Response:
  Code: 200
  Key: /token/local[SmartCity]8GPJL6ipTyYRNr5xTyGWWFayd2k1EoLYu
  Value: {"address":"local[SmartCity]8GPJL6ipTyYRNr5xTyGWWFayd2k1EoLYu","owner":"local[SmartCity]ETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL","name":"TST","symbol":"TST","totalSupply":0,"addSupplyEnabled":false,"burnEnabled":false,"gasprice":2500}
```

Now, we have finished the activation of the token `Diamond Coin`, so we can use the following command to try to transfer:

```shell
./bcc transfer --name owner --password Ab1@Cd3$ --token "TST" --gasLimit 100000  --to local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG --value 100 --chainid local

Return results:

OK
Response: {
  "code": 200,
  "log": "",
  "fee": 5250000,
  "txHash": "0xE1B35FF40EFA83A972C2E1260E2677937025842BCA87B5C61F515CEA2B1BFB40",
  "height": 48518
}
```

We can complete the cross-chain transfer of the token `Diamond Coin` by the above command, then we try to check if the transaction is successful:

```shell
./bcc balance --accAddress="local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG" --tokenName="Diamond Coin" --chainid local[SmartCity]

Return results:

OK
Response: [
  {
    "tokenAddress": "local[SmartCity]8GPJL6ipTyYRNr5xTyGWWFayd2k1EoLYu",
    "tokenName": "TST",
    "balance": "100000000000"
  }
]
```

we can confirm the token `TST` successful to account. If the account balance is not in the account, you can query this cross-chain transaction by getting `transaction Hash` on the target chain(refer to the section 2, Cross-Chain Creation).

## 3. Cross-Chain Transaction

### 3.1 Cross-Chain Transaction Hash

Cross-Chain Transaction Hash, that is `ibcHash`, we can get the status and information of cross-chain transaction throught it.

We take the transfer from main chain to side chain in 2.1 as an example, we get the transaction height is 25974, we get `ibcHash` by the following command:

```shell
./bcc block -t 25974
OK
Response: {
  "blockHeight": 25974,
  "blockHash": "0xf8f381cd2c5bae781aebd8524edad20af4654158",
  "parentHash": "0xf838ca7c49b12e8cd3839fe7ce3d0f8d2ee72bd8",
  "chainID": "local",
  "validatorHash": "0xf2c0a2f00f78c4b8cef2c7e56dd62e191ab7d0b7",
  "consensusHash": "0xf66ef1df8ba6dac7a1ecce40cc84e54a1cebc6a5",
  "blockTime": "2019-11-28 07:27:33.528200078 +0000 UTC",
  "blockSize": 1039,
  "proposerAddress": "localMp5Xi3o2rnXjzbCuzo5R4m6qv7fbfNgkW",
  "txs": [
    {
      "txHash": "0x6c8c4a3324c87ece2ec85f03d25d3994ab5be31183aed6f7d8044ca2ccc0f25f",
      "txTime": "2019-11-28 07:27:33.528200078 +0000 UTC",
      "code": 200,
      "log": "",
      "blockHash": "0xf8f381cd2c5bae781aebd8524edad20af4654158",
      "blockHeight": 25974,
      "from": "localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL",
      "nonce": 61,
      "gasLimit": 100000,
      "fee": 5000000,
      "note": "",
      "messages": [
        ......
      ],
      "tags": {
        ......,
        "/0/4/ibc::packet/local->local[SmartCity]": {
          "Name": "ibc::packet/local->local[SmartCity]",
          "ContractAddr": "",
          "ReceiptBytes": "eyJmcm9tQ2hhaW5JRCI6ImxvY2FsIiwidG9DaGFpbklEIjoibG9jYWxbeXldIiwicXVldWVJRCI6ImxvY2FsLT5sb2NhbFt5eV0iLCJzZXEiOjUsIm9yZ0lEIjoib3JnSmdhR0NvblV5SzgxemlibnRVQmpRMzNQS2N0cGsxSzFHIiwiY29udHJhY3ROYW1lIjoidG9rZW4tYmFzaWMiLCJpYmNIYXNoIjoiMUJBMTNCOTU1OUVGQzlBMkI2RTBGRDU4OUVENThBNUREODI5QkFEOTY5MDk4NkYzMzE5RDYwRUE3MENGMTM5NyIsInR5cGUiOiJ0Y2N0eCIsInN0YXRlIjp7InN0YXR1cyI6Ik5vQWNrV2FudGVkIiwidGFnIjoiUmVjYXN0UGVuZGluZyIsImxvZyI6IiJ9LCJyZWNlaXB0cyI6W3sia2V5IjoiTHpBdmMzUmtPanAwY21GdWMyWmxjZz09IiwidmFsdWUiOiJleUp1WVcxbElqb2ljM1JrT2pwMGNtRnVjMlpsY2lJc0ltTnZiblJ5WVdOMFFXUmtjbVZ6Y3lJNklteHZZMkZzU0V4RWFIRjViMG94ZGxKMWJ6aHlaVGxIZUVaQlJsVXlRbXR6ZHpKclRuVndJaXdpY21WalpXbHdkRUo1ZEdWeklqb2laWGxLTUdJeWRHeGlhVWsyU1cxNGRsa3lSbk5SVlhCNVdXMXpNbFl5VW0xT01WSkVXVzVXZFdOc2FGbFZlbFp5VXpOYWFWWXhXbnBsYldoRVRWWlNRa2xwZDJsYWJrcDJZbE5KTmtsdGVIWlpNa1p6VWxaU1RFNHhjRzlQVjJoUFZURkNlVkpWZEd0aVZVNXVZbXRvUldSRldsRlpXRkpxWTNwc1dHUXhXazFKYVhkcFpFYzRhVTlwU25OaU1rNW9Za1JOZWsxclNubFBSWFJNWTFSV2JrNUVaR2hoTTA1aFpHMHhNVkV3VGpOT2Frb3hZakJOZWxOR1RtbE9hVWx6U1c1YWFHSklWbXhKYW05NFRVUkJkMDFFUVhkTlJFRjNUVVJCYzBsdE5YWmtSMVZwVDJsS2MySXlUbkpQYVVvNUlpd2ljbVZqWldsd2RFaGhjMmdpT2lJeVFUSkdNREpCTXpVNE56UkJNRGN5UVVZNFJqQTVNakpFTlRjNE5qUTVSVFJCT0VSRFFqa3pRalEwUlVVNE9EUkdOMFU1T1VSQ01qUTFPREV6TVRNNEluMD0ifSx7ImtleSI6Ikx6RXZkRzlyWlc1aVlYTnBZeTVCYzNObGRFTm9ZVzVuWlE9PSIsInZhbHVlIjoiZXlKdVlXMWxJam9pZEc5clpXNWlZWE5wWXk1QmMzTmxkRU5vWVc1blpTSXNJbU52Ym5SeVlXTjBRV1JrY21WemN5STZJbXh2WTJGc1NFeEVhSEY1YjBveGRsSjFiemh5WlRsSGVFWkJSbFV5UW10emR6SnJUblZ3SWl3aWNtVmpaV2x3ZEVKNWRHVnpJam9pWlhsS01scFlTbnBoVnpsMVNXcHZhVTFwTkhoSmFYZHBaRWhzZDFwVFNUWkpiWGgyV1RKemFVeERTakJpTW5Sc1ltbEpOa2x0ZUhaWk1rWnpVVlZ3ZVZsdGN6SldNbEp0VGpGU1JGbHVWblZqYkdoWlZYcFdjbE16V21sV01WcDZaVzFvUkUxV1VrSkphWGRwV201S2RtSlRTVFpKYlhoMldUSkdjMUpXVWt4T01YQnZUMWRvVDFVeFFubFNWWFJyWWxWT2JtSnJhRVZrUlZwUldWaFNhbU42YkZoa01WcE5TV2wzYVdSSE9HbFBhVXB6WWpKT2FHSkdkRFZsVmpGSlZGaENWR1ZZVVhsVGJYTXhVVzFzUjJGV1NYbGhhbEV4WW10a1NHRnNVblpTYW14MFlWWldWMWxWWTJsTVEwb3lXVmQ0TVZwVFNUWk5WRUYzVFVSQmQwMUVRWGROUkVGM1RFTktjRmx0VGtsWldFNXZTV3B2YVUxVlNrSk5WRTVEVDFSVk1VOVZWa2RSZW14Q1RXdEpNbEpVUWtkU1JGVTBUMVZXUlU1VWFFSk9WVkpGVDBSSk5WRnJSa1ZQVkZrMVRVUnJORTVyV1hwTmVrVTFVa1JaZDFKVlJUTk5SVTVIVFZSTk5VNTVTWE5KYlU1dldWYzFibHBWYkRCYVZ6RjZTV3B3WW1WNVNrUmhSMFp3WW10c1JVbHFiMmxpUnpscVdWZDNhVXhEU2tKYVIxSjVXbGhPZWtscWIybGlSemxxV1ZkM2VrMTZTa05qYW1oTVV6TkZNVnA2VVROWlYzUjZWMjVhZEdSVlRrUmtlbGw1WkZjNVJFMHdhRlJaYWxscFRFTktVVnBYVm5sUk1taG9ZVmMxU2xKRFNUWkpiWGgyV1RKR2MxY3piRFZZVTBselNXeENiRnBZU2tSaFIwWndZbXRLYUdKSFJuVlpNbFZwVDJwSmQwMUVRWGROUkVGM1RVUkJkMlpXTVRraUxDSnlaV05sYVhCMFNHRnphQ0k2SWtWR09UazRRalZDUmpSQ1JEUTNPVEl4UXpnMVF6QXhORU5FTlVNNE56UXlOelUzT0VNeE9FUXpNMEUzTlVRNVFqazRSa1kwTmtaQk5qWTBSVVpETjBNaWZRPT0ifV19",
          "ReceiptHash": "0x075860DF0B94E3A2D346150DD1E17F99D4B171F1B689A87C39CA0977AFBA8D40",
          "Receipt": {
            "contractName": "token-basic",
            "fromChainID": "local",
            "ibcHash": "1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397",
            "orgID": "orgJgaGConUyK81zibntUBjQ33PKctpk1K1G",
            "queueID": "local->local[SmartCity]",
            "receipts": [
              {
                "key": "LzAvc3RkOjp0cmFuc2Zlcg==",
                "value": "eyJuYW1lIjoic3RkOjp0cmFuc2ZlciIsImNvbnRyYWN0QWRkcmVzcyI6ImxvY2FsSExEaHF5b0oxdlJ1bzhyZTlHeEZBRlUyQmtzdzJrTnVwIiwicmVjZWlwdEJ5dGVzIjoiZXlKMGIydGxiaUk2SW14dlkyRnNRVXB5WW1zMlYyUm1OMVJEWW5WdWNsaFlVelZyUzNaaVYxWnplbWhETVZSQklpd2labkp2YlNJNklteHZZMkZzUlZSTE4xcG9PV2hPVTFCeVJVdGtiVU5uYmtoRWRFWlFZWFJqY3psWGQxWk1JaXdpZEc4aU9pSnNiMk5oYkRNek1rSnlPRXRMY1RWbk5EZGhhM05hZG0xMVEwTjNOakoxYjBNelNGTmlOaUlzSW5aaGJIVmxJam94TURBd01EQXdNREF3TURBc0ltNXZkR1VpT2lKc2IyTnJPaUo5IiwicmVjZWlwdEhhc2giOiIyQTJGMDJBMzU4NzRBMDcyQUY4RjA5MjJENTc4NjQ5RTRBOERDQjkzQjQ0RUU4ODRGN0U5OURCMjQ1ODEzMTM4In0="
              },
              {
                "key": "LzEvdG9rZW5iYXNpYy5Bc3NldENoYW5nZQ==",
                "value": "eyJuYW1lIjoidG9rZW5iYXNpYy5Bc3NldENoYW5nZSIsImNvbnRyYWN0QWRkcmVzcyI6ImxvY2FsSExEaHF5b0oxdlJ1bzhyZTlHeEZBRlUyQmtzdzJrTnVwIiwicmVjZWlwdEJ5dGVzIjoiZXlKMlpYSnphVzl1SWpvaU1pNHhJaXdpZEhsd1pTSTZJbXh2WTJzaUxDSjBiMnRsYmlJNklteHZZMkZzUVVweVltczJWMlJtTjFSRFluVnVjbGhZVXpWclMzWmlWMVp6ZW1oRE1WUkJJaXdpWm5KdmJTSTZJbXh2WTJGc1JWUkxOMXBvT1doT1UxQnlSVXRrYlVObmJraEVkRVpRWVhSamN6bFhkMVpNSWl3aWRHOGlPaUpzYjJOaGJGdDVlVjFJVFhCVGVYUXlTbXMxUW1sR2FWSXlhalExYmtkSGFsUnZSamx0YVZWV1lVY2lMQ0oyWVd4MVpTSTZNVEF3TURBd01EQXdNREF3TENKcFltTklZWE5vSWpvaU1VSkJNVE5DT1RVMU9VVkdRemxCTWtJMlJUQkdSRFU0T1VWRU5UaEJOVVJFT0RJNVFrRkVPVFk1TURrNE5rWXpNekU1UkRZd1JVRTNNRU5HTVRNNU55SXNJbU5vWVc1blpVbDBaVzF6SWpwYmV5SkRhR0ZwYmtsRUlqb2liRzlqWVd3aUxDSkJaR1J5WlhOeklqb2liRzlqWVd3ek16SkNjamhMUzNFMVp6UTNZV3R6V25adGRVTkRkell5ZFc5RE0waFRZallpTENKUVpXVnlRMmhoYVc1SlJDSTZJbXh2WTJGc1czbDVYU0lzSWxCbFpYSkRhR0ZwYmtKaGJHRnVZMlVpT2pJd01EQXdNREF3TURBd2ZWMTkiLCJyZWNlaXB0SGFzaCI6IkVGOTk4QjVCRjRCRDQ3OTIxQzg1QzAxNENENUM4NzQyNzU3OEMxOEQzM0E3NUQ5Qjk4RkY0NkZBNjY0RUZDN0MifQ=="
              }
            ],
            "seq": 5,
            "state": {
              "log": "",
              "status": "NoAckWanted",
              "tag": "RecastPending"
            },
            "toChainID": "local[SmartCity]",
            "type": "tcctx"
          }
        },
        ......
                 }
    }
  ]
}
```

Find the receipt name containing `ibc::packet` and get `ibcHash` in the structure of `Receipt`.

### 3.2 Cross-Chain Transaction Data

You can query to get `ibcHash`: `1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397` from above, and then we use following command to get cross-chain transaction data:

```shell
./bcc query -k /ibc/1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397/packets

Return results:

OK
Response:
  Code: 200
  Key: /ibc/1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397/packets
 Value: [
 ......,{
  "fromChainID": "local",
  "toChainID": "local[SmartCity]",
  "queueID": "",
  "seq": 0,
  "orgID": "orgJgaGConUyK81zibntUBjQ33PKctpk1K1G",
  "contractName": "token-basic",
  "ibcHash": "1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397",
  "type": "tcctx",
  "state": {
    "status": "NoAck",
    "tag": "Confirmed",
    "log": ""},
  "receipts": [{
    "key": "LzAvc3RkOjp0cmFuc2Zlcg==",
    "value": "eyJuYW1lIjoic3RkOjp0cmFuc2ZlciIsImNvbnRyYWN0QWRkcmVzcyI6ImxvY2FsSExEaHF5b0oxdlJ1bzhyZTlHeEZBRlUyQmtzdzJrTnVwIiwicmVjZWlwdEJ5dGVzIjoiZXlKMGIydGxiaUk2SW14dlkyRnNRVXB5WW1zMlYyUm1OMVJEWW5WdWNsaFlVelZyUzNaaVYxWnplbWhETVZSQklpd2labkp2YlNJNklteHZZMkZzUlZSTE4xcG9PV2hPVTFCeVJVdGtiVU5uYmtoRWRFWlFZWFJqY3psWGQxWk1JaXdpZEc4aU9pSnNiMk5oYkRNek1rSnlPRXRMY1RWbk5EZGhhM05hZG0xMVEwTjNOakoxYjBNelNGTmlOaUlzSW5aaGJIVmxJam94TURBd01EQXdNREF3TURBc0ltNXZkR1VpT2lKc2IyTnJPaUo5IiwicmVjZWlwdEhhc2giOiIyQTJGMDJBMzU4NzRBMDcyQUY4RjA5MjJENTc4NjQ5RTRBOERDQjkzQjQ0RUU4ODRGN0U5OURCMjQ1ODEzMTM4In0="
    }, {
    "key": "LzEvdG9rZW5iYXNpYy5Bc3NldENoYW5nZQ==",
    "value": "eyJuYW1lIjoidG9rZW5iYXNpYy5Bc3NldENoYW5nZSIsImNvbnRyYWN0QWRkcmVzcyI6ImxvY2FsSExEaHF5b0oxdlJ1bzhyZTlHeEZBRlUyQmtzdzJrTnVwIiwicmVjZWlwdEJ5dGVzIjoiZXlKMlpYSnphVzl1SWpvaU1pNHhJaXdpZEhsd1pTSTZJbXh2WTJzaUxDSjBiMnRsYmlJNklteHZZMkZzUVVweVltczJWMlJtTjFSRFluVnVjbGhZVXpWclMzWmlWMVp6ZW1oRE1WUkJJaXdpWm5KdmJTSTZJbXh2WTJGc1JWUkxOMXBvT1doT1UxQnlSVXRrYlVObmJraEVkRVpRWVhSamN6bFhkMVpNSWl3aWRHOGlPaUpzYjJOaGJGdDVlVjFJVFhCVGVYUXlTbXMxUW1sR2FWSXlhalExYmtkSGFsUnZSamx0YVZWV1lVY2lMQ0oyWVd4MVpTSTZNVEF3TURBd01EQXdNREF3TENKcFltTklZWE5vSWpvaU1VSkJNVE5DT1RVMU9VVkdRemxCTWtJMlJUQkdSRFU0T1VWRU5UaEJOVVJFT0RJNVFrRkVPVFk1TURrNE5rWXpNekU1UkRZd1JVRTNNRU5HTVRNNU55SXNJbU5vWVc1blpVbDBaVzF6SWpwYmV5SkRhR0ZwYmtsRUlqb2liRzlqWVd3aUxDSkJaR1J5WlhOeklqb2liRzlqWVd3ek16SkNjamhMUzNFMVp6UTNZV3R6V25adGRVTkRkell5ZFc5RE0waFRZallpTENKUVpXVnlRMmhoYVc1SlJDSTZJbXh2WTJGc1czbDVYU0lzSWxCbFpYSkRhR0ZwYmtKaGJHRnVZMlVpT2pJd01EQXdNREF3TURBd2ZWMTkiLCJyZWNlaXB0SGFzaCI6IkVGOTk4QjVCRjRCRDQ3OTIxQzg1QzAxNENENUM4NzQyNzU3OEMxOEQzM0E3NUQ5Qjk4RkY0NkZBNjY0RUZDN0MifQ=="
    }, {
    "key": "LzEvc3RkOjp0cmFuc2Zlcg==",
    "value": "eyJuYW1lIjoic3RkOjp0cmFuc2ZlciIsImNvbnRyYWN0QWRkcmVzcyI6ImxvY2FsW3l5XUFKcmJrNldkZjdUQ2J1bnJYWFM1a0t2YldWc3poQzFUQSIsInJlY2VpcHRCeXRlcyI6ImV5SjBiMnRsYmlJNklteHZZMkZzVzNsNVhVRktjbUpyTmxka1pqZFVRMkoxYm5KWVdGTTFhMHQyWWxkV2MzcG9RekZVUVNJc0ltWnliMjBpT2lKc2IyTmhiRnQ1ZVYwek16SkNjamhMUzNFMVp6UTNZV3R6V25adGRVTkRkell5ZFc5RE0waFRZallpTENKMGJ5STZJbXh2WTJGc1czbDVYVWhOY0ZONWRESkthelZDYVVacFVqSnFORFZ1UjBkcVZHOUdPVzFwVlZaaFJ5SXNJblpoYkhWbElqb3hNREF3TURBd01EQXdNREI5IiwicmVjZWlwdEhhc2giOiIzMDJENDc0OTFCNDIyNDQzQUFBODFCRkFBQjA4MzQwOTJCMDY4OTYwOEFCQjUyMzhERTM5RjI2NzlGNjQ4Q0QyIn0="
    }, {
    "key": "LzIvdG9rZW5iYXNpYy5Bc3NldENoYW5nZQ==",
    "value": "eyJuYW1lIjoidG9rZW5iYXNpYy5Bc3NldENoYW5nZSIsImNvbnRyYWN0QWRkcmVzcyI6ImxvY2FsW3l5XUFKcmJrNldkZjdUQ2J1bnJYWFM1a0t2YldWc3poQzFUQSIsInJlY2VpcHRCeXRlcyI6ImV5SjJaWEp6YVc5dUlqb2lNaTR4SWl3aWRIbHdaU0k2SW5KbFkyRnpkQ0lzSW5SdmEyVnVJam9pYkc5allXeGJlWGxkUVVweVltczJWMlJtTjFSRFluVnVjbGhZVXpWclMzWmlWMVp6ZW1oRE1WUkJJaXdpWm5KdmJTSTZJbXh2WTJGc1JWUkxOMXBvT1doT1UxQnlSVXRrYlVObmJraEVkRVpRWVhSamN6bFhkMVpNSWl3aWRHOGlPaUpzYjJOaGJGdDVlVjFJVFhCVGVYUXlTbXMxUW1sR2FWSXlhalExYmtkSGFsUnZSamx0YVZWV1lVY2lMQ0oyWVd4MVpTSTZNVEF3TURBd01EQXdNREF3TENKcFltTklZWE5vSWpvaU1VSkJNVE5DT1RVMU9VVkdRemxCTWtJMlJUQkdSRFU0T1VWRU5UaEJOVVJFT0RJNVFrRkVPVFk1TURrNE5rWXpNekU1UkRZd1JVRTNNRU5HTVRNNU55SXNJbU5vWVc1blpVbDBaVzF6SWpwYmV5SkRhR0ZwYmtsRUlqb2liRzlqWVd4YmVYbGRJaXdpUVdSa2NtVnpjeUk2SW14dlkyRnNXM2w1WFRNek1rSnlPRXRMY1RWbk5EZGhhM05hZG0xMVEwTjNOakoxYjBNelNGTmlOaUlzSWxCbFpYSkRhR0ZwYmtsRUlqb2liRzlqWVd3aUxDSlFaV1Z5UTJoaGFXNUNZV3hoYm1ObElqb3RNVEl3TURBd01EQXdNREF3ZlYxOSIsInJlY2VpcHRIYXNoIjoiREU3MTRCRjJFOTQ1Rjg1MTFDNzA5RUUzNUE2MzYyOUMzQzczRDkyQkQyNzU0QjdCNTJBQkY0QzkzOTBCODQyRiJ9"
    }, {
    "key": "LzEvdG9rZW5iYXNpYy5Bc3NldENoYW5nZQ==",
    "value": "eyJuYW1lIjoidG9rZW5iYXNpYy5Bc3NldENoYW5nZSIsImNvbnRyYWN0QWRkcmVzcyI6ImxvY2FsSExEaHF5b0oxdlJ1bzhyZTlHeEZBRlUyQmtzdzJrTnVwIiwicmVjZWlwdEJ5dGVzIjoiZXlKMlpYSnphVzl1SWpvaU1pNHhJaXdpZEhsd1pTSTZJbVJsYzNSeWIza2lMQ0owYjJ0bGJpSTZJbXh2WTJGc1FVcHlZbXMyVjJSbU4xUkRZblZ1Y2xoWVV6VnJTM1ppVjFaemVtaERNVlJCSWl3aVpuSnZiU0k2SW14dlkyRnNSVlJMTjFwb09XaE9VMUJ5UlV0a2JVTm5ia2hFZEVaUVlYUmpjemxYZDFaTUlpd2lkRzhpT2lKc2IyTmhiRnQ1ZVYxSVRYQlRlWFF5U21zMVFtbEdhVkl5YWpRMWJrZEhhbFJ2UmpsdGFWVldZVWNpTENKMllXeDFaU0k2TVRBd01EQXdNREF3TURBd0xDSnBZbU5JWVhOb0lqb2lNVUpCTVROQ09UVTFPVVZHUXpsQk1rSTJSVEJHUkRVNE9VVkVOVGhCTlVSRU9ESTVRa0ZFT1RZNU1EazROa1l6TXpFNVJEWXdSVUUzTUVOR01UTTVOeUlzSW1Ob1lXNW5aVWwwWlcxeklqcGJleUpEYUdGcGJrbEVJam9pYkc5allXd2lMQ0pCWkdSeVpYTnpJam9pYkc5allXd3pNekpDY2poTFMzRTFaelEzWVd0elduWnRkVU5EZHpZeWRXOURNMGhUWWpZaUxDSlFaV1Z5UTJoaGFXNUpSQ0k2SW14dlkyRnNXM2w1WFNJc0lsQmxaWEpEYUdGcGJrSmhiR0Z1WTJVaU9qRXlNREF3TURBd01EQXdNSDFkZlE9PSIsInJlY2VpcHRIYXNoIjoiQ0ZGQ0RCNjUzQjk5NDRDNDUwOERBRDc1M0VCMTk1ODU3RUE0NjE5RTA4MDk0RUYzNDcwRDQ3OTBBNkY3Q0U0MCJ9"
    }]
}
]
```

#### 3.2.1 Cross-Chain Transaction Data Analysis

We got a cross-chain transaction data successfully from above, and now let's analyze the cross-chain transaction data.

```go
type Packet struct {
  FromChainID  string           // From chain id（A）
  ToChainID    string           // To chain id（B）
  QueueID      string           // Cross-chain communications queue（A->B）
  Seq          uint64           // (A->B)The serial number on this queue, starting at 0.
  OrgID        string           // Organization ID
  ContractName string           // Smart contract name
  IbcHash      types.Hash       // Cross-chain transaction hash, it determines the final result from the blockchain
  Type         string           // Type of cross-chain communication："tcctx", "notify"
  State        State            // State
  Receipts     []types.KVPair   // Data to be transmitted
}

type State struct {
  Status string     // State："NoAckWanted", "NoAck"
  Tag    string     // status identification for the business layer：
  Log    string     // Abnormal log
}

Notice:
Type is the type of cross-chain communication："tcctx" means transaction, "notify" means notification

Status, the status of cross-chain transaction：
"NoAckWanted": the state of the cross-chain communication protocol, requiring the receipt to return a reply.
"NoAck": the state of the cross-chain communication protocol, does not require the receipt to return a reply

Tag: status identification for the business layer
"NotifyPending": the status of the cross-chain notification at the initiator side, indicating that the next step requires the execution of the business notification on the target side.

"Success": the cross-chain notification at the target side, indicating the business layer has completed the notification.
"Failure": the cross-chain notification at the target side, indicating the business layer has not completed the notification. Probably because the contract version is inconsistent.

"RecastPending": the status of the cross-chain transaction at the initiator side, indicating the next step is to execute the recast business on the target side, or to be transited by the hub chain.
"ConfirmPending": the state of the cross-chain transaction at the hub chain and the target chain, indicating the next step is to execute the confirmation transit business on the hub chain, or to execute the final confirmation business on the initiator side
"Confirmed": the state of the cross-chain notification at the initiator side, indicating the cross-chain operation has been completed.
"CancelPending": the state of the cross-chain transaction at the hub chain and the target chain, indicating the next step is to execute the cancellation service on the hub chain, or to execute the final cancellation service on the initiator side.
"Canceled": the state of the cross-chain transaction at the initiator side, indicating the cross-chain operation has been cancelled successfully.
```

The cross-chain transaction data is composed of slices of packet structure (as shown in the figure). A packet structure represents a transaction, and a complete cross-chain transaction is generally composed of one or more such transactions (generally, there is only one such transaction in the notification initiation chain and two in the notification receiving chain; there are three such transactions in the transaction initiation chain and two in the target chain.

#### 3.2.2 Cross-Chain Receipt Analysis

We have got a cross-chain transaction data from the above, there is a slice of the field `receipts`, and the data stored in it is the receipt of cross-chain transactions. In addition to the receipt of cross-chain transactions, there is receipt of handling fees, we only analyze the receipt of cross-chain transactions:

```go
{
  "key": "LzEvdG9rZW5iYXNpYy5Bc3NldENoYW5nZQ==",
  "value": "eyJuYW1lIjoidG9rZW5iYXNpYy5Bc3NldENoYW5nZSIsImNvbnRyYWN0QWRkcmVzcyI6ImxvY2FsSExEaHF5b0oxdlJ1bzhyZTlHeEZBRlUyQmtzdzJrTnVwIiwicmVjZWlwdEJ5dGVzIjoiZXlKMlpYSnphVzl1SWpvaU1pNHhJaXdpZEhsd1pTSTZJbVJsYzNSeWIza2lMQ0owYjJ0bGJpSTZJbXh2WTJGc1FVcHlZbXMyVjJSbU4xUkRZblZ1Y2xoWVV6VnJTM1ppVjFaemVtaERNVlJCSWl3aVpuSnZiU0k2SW14dlkyRnNSVlJMTjFwb09XaE9VMUJ5UlV0a2JVTm5ia2hFZEVaUVlYUmpjemxYZDFaTUlpd2lkRzhpT2lKc2IyTmhiRnQ1ZVYxSVRYQlRlWFF5U21zMVFtbEdhVkl5YWpRMWJrZEhhbFJ2UmpsdGFWVldZVWNpTENKMllXeDFaU0k2TVRBd01EQXdNREF3TURBd0xDSnBZbU5JWVhOb0lqb2lNVUpCTVROQ09UVTFPVVZHUXpsQk1rSTJSVEJHUkRVNE9VVkVOVGhCTlVSRU9ESTVRa0ZFT1RZNU1EazROa1l6TXpFNVJEWXdSVUUzTUVOR01UTTVOeUlzSW1Ob1lXNW5aVWwwWlcxeklqcGJleUpEYUdGcGJrbEVJam9pYkc5allXd2lMQ0pCWkdSeVpYTnpJam9pYkc5allXd3pNekpDY2poTFMzRTFaelEzWVd0elduWnRkVU5EZHpZeWRXOURNMGhUWWpZaUxDSlFaV1Z5UTJoaGFXNUpSQ0k2SW14dlkyRnNXM2w1WFNJc0lsQmxaWEpEYUdGcGJrSmhiR0Z1WTJVaU9qRXlNREF3TURBd01EQXdNSDFkZlE9PSIsInJlY2VpcHRIYXNoIjoiQ0ZGQ0RCNjUzQjk5NDRDNDUwOERBRDc1M0VCMTk1ODU3RUE0NjE5RTA4MDk0RUYzNDcwRDQ3OTBBNkY3Q0U0MCJ9"
}
```

The above receipt is a receipt obtained from the receipts field. We can know this is a receipt for asset change by `base64 decode`, that is the receipt name is `tokenbasic.AssetChange`, we decode the value through `base64 decode` to get the receipt information:

```go
{"name":"tokenbasic.AssetChange","contractAddress":"localHLDhqyoJ1vRuo8re9GxFAFU2Bksw2kNup","receiptBytes":"eyJ2ZXJzaW9uIjoiMi4xIiwidHlwZSI6ImRlc3Ryb3kiLCJ0b2tlbiI6ImxvY2FsQUpyYms2V2RmN1RDYnVuclhYUzVrS3ZiV1ZzemhDMVRBIiwiZnJvbSI6ImxvY2FsRVRLN1poOWhOU1ByRUtkbUNnbkhEdEZQYXRjczlXd1ZMIiwidG8iOiJsb2NhbFt5eV1ITXBTeXQySms1QmlGaVIyajQ1bkdHalRvRjltaVVWYUciLCJ2YWx1ZSI6MTAwMDAwMDAwMDAwLCJpYmNIYXNoIjoiMUJBMTNCOTU1OUVGQzlBMkI2RTBGRDU4OUVENThBNUREODI5QkFEOTY5MDk4NkYzMzE5RDYwRUE3MENGMTM5NyIsImNoYW5nZUl0ZW1zIjpbeyJDaGFpbklEIjoibG9jYWwiLCJBZGRyZXNzIjoibG9jYWwzMzJCcjhLS3E1ZzQ3YWtzWnZtdUNDdzYydW9DM0hTYjYiLCJQZWVyQ2hhaW5JRCI6ImxvY2FsW3l5XSIsIlBlZXJDaGFpbkJhbGFuY2UiOjEyMDAwMDAwMDAwMH1dfQ==","receiptHash":"CFFCDB653B9944C4508DAD753EB195857EA4619E08094EF3470D4790A6F7CE40"}
```

Then we decode the value of the field `receiptbytes` through `base64 decode` to get the receipt:

```go
{"version":"2.1","type":"destroy","token":"localAJrbk6Wdf7TCbunrXXS5kKvbWVszhC1TA","from":"localETK7Zh9hNSPrEKdmCgnHDtFPatcs9WwVL","to":"local[SmartCity]HMpSyt2Jk5BiFiR2j45nGGjToF9miUVaG","value":100000000000,"ibcHash":"1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397","changeItems":[{"ChainID":"local","Address":"local332Br8KKq5g47aksZvmuCCw62uoC3HSb6","PeerChainID":"local[SmartCity]","PeerChainBalance":120000000000}]}

Notice:
Type is the type of asset change:
"Lock" means that the funds has been locked in the initiator side
"Recast" means that the funds has been recast in the target chain
"Destroy" means that the funds has been destroyed in the initiator side

PeerChainID is the chain ID of the opposite chain

PeerChainBalance is the total balance of the token in the opposite chain (this is the total balance of the whole chain, and the token is the token corresponding to the token field)

```

Notice: there are multiple receipts for asset change in the field `receipts`, because it saves the receipt sent to it by the previous chain (that is, the receipt in the second packet contains the receipt in the first packet, and the receipt in the third packet contains the receipt in the second packet). In general, if you want to see the final receipt of this cross-chain transaction, You should see the last receipt of the asset change.

## 4. Query result

You can query to get `ibcHash`: `1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397` from above, and then we use following command to get the state of the cross-chain transaction:

```shell
./bcc query -k /ibc/1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397/state

Return results:

OK
Response:
  Code: 200
  Key: /ibc/1BA13B9559EFC9A2B6E0FD589ED58A5DD829BAD9690986F3319D60EA70CF1397/state
  Value: {"status":"NoAck","tag":"Confirmed","log":""}
```
