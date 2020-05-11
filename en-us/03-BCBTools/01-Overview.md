# Overview

BCBChain ToolBox is the auxiliary toolbox of the BCB chain, which is convenient for the user to interact with BCB main chain, The main command is as follow:

* bcw

  Use to create, import, export wallets and sign files.

* bcc

  Deploy smart contracts, call smart contracts, query block information and other operations.

* smcpack

  Package the contracts, specify the contract directory, and package it into `*.tar.gz` file. But only package the contract code, not the test file.

  Contract signature, input `.tar.gz` to output the signature file (to sign codehash).

* smc2rpc

  Input the contract compression package, output the source code, including RPC services and command-line command, just package the function that the contract calls, and output the signed transaction package.

* sigorg

  Input file name with `.tar.gz` and developer signature file name, verify and output organization signature file (sign developer signature data).

* addr

  Input the chain ID and wallet name, then export the address.

* orgid

  Calculation tool for organization ID.

* genesis

  The genesis creation tool, it generates the genesis file _genesis.json.

* txparse

  Tools for analyzing transactions.
