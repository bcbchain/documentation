# Model Introduction

## 1. Overview

BCBChain has referred to Ethereum, Fabric, Tendermint, Cosmos and other open-source blockchain schemes, and some of the outstanding ideas.

BCBChain is essentially a transaction based state machine. In computer science, state machine is a calculation model which includes a set of states, a start state, a set of input symbols, a mapping input symbol and the transition function from the current state to the next state.

In BCBChain, the state set is expressed by the state database, and the initial state is called genesis state, the input symbol set is the transaction (TX) commonly used in the blockchain field, and the state transition function is the smart contract.

![State Machine](./p/statemachine.png)

According to BCBChain's state machine, we start with genesis state. This is almost like a blank slate, in the network there is no transaction generated state. When the transaction is executed, the state of creation will be transformed into the final state. At any time, this final state represents the current state of BCBChain.

BCBChain's status is reached by thousands of transactions. These transactions are "grouped" into blocks. A block contains a series of transactions, each block is linked with its previous block, and each block will lead the state machine to reach a new state.

![Blockchain](./p/blockchain.png)

In order to change one state to the next, the transaction must be effective (that is, the non repudiation feature requirements that promote the adoption of blockchain technology). In order to make a transaction been considered effective, it must go through a verification process. Each transaction must be signed by the transaction initiator through its own private key, and verified to meet certain conditions in BCBChain's smart contract before it can be considered effective.

## 2. Account description

BCBChain's global "shared state" is composed of many small objects (accounts), which can interact with each other through the messaging architecture. BCBChain's account concept refers to Ethereum's account concept. Each account has a state and an address associated with it. BCBChain has two types of accounts:

* **External Account**, which is controlled by private key and has no code associated with it

* **Contract Account**, which is controlled by their contract code and has a code associated with it. The contract account is only related to the name of the contract and has nothing to do with the version and owner of the contract. After upgrading the contract, the new version of the contract will have the new contract address, but the account address of the contract will remain the same.

## 3. BCBChain pass

BCBChain defined the basic token when it was created, and implemented the business logic based on the basic token in the built-in basic contract. We named it BCB.

The unit of measurement of BCB refers to the concept of bitcoin and is defined as follows:

| **uint**  | **Cong value**           |
| --------- | -------------------- |
| **cong**  | 1 cong               |
| **Kcong** | 1,000   cong         |
| **Mcong** | 1,000,000   cong     |
| **BCB**   | 1,000,000,000   cong |

## 4. BCBChain chain id

Bcbchain defined the chain ID when it was created, its name is "BCB". The chain ID of the test chain corresponding to bcbchain (used to test bug correction, new features, etc.) is "bcbtest".

After opening the source code of the BCBChain, if you want to deploy the private chain or test chain, the chain ID can be arbitrarily selected except "bcb" and "bcbtest".

## 5. BCB side chain ID

The side chain based on BCB ecology can freely specify the name of the side chain when it is created. The chain ID of the side chain is constructed based on the following algorithm:

| Side chain ID construction algorithm |
| ------------------------------------------------------------ |
| 1、Calculate side chain ID：Main Chain ID[any name] |
| 2、For example: main chain id = bcb |
| side chain name = vcity |
| side chain id =bcb[vcity] |
