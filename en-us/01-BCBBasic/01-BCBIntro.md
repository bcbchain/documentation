# Introduction

## 1.What is BCB

​        BCB is a blockchain system developed based on Tendermint. It is a platform for developing applications fast, with high performance and scalability, relied on system security, it carries out technological innovation to achieve efficient value information transmission between things and people, people and things.

​        Tendermint is a modular framework of the blockchain and supports developers to personalize their own blockchains. It provides an engine including a network layer and a consensus layer, and uses an ABCI (Application Blockchain Interface) interface based on the socket protocol to connect applications, which is convenient for building arbitrary applications on it.

## 2.System Structure

![BCB Architecture](./p/BCB-arch-3.png)

## 3. Core Design

### 3.1 Double Consensus Mechanism

​        Actually, all blockchains are deterministic state machines built on transactions. Consensus is a process in determining the order of transactions and filtering invalid transactions. Based on the PBFT (Practical Byzantine Fault Tolerance) algorithm, BCB proposed a consensus algorithm of PBFT + DPOS. In this mechanism, there are two participants, one is a node for professional block producer, and the other is the ordinary user in the system. Ordinary users vote to determine block producers based on the proportion of the number of tokens they held. When a consensus needs to be achieved, a block validator is randomly selected from these block producers to verify the block, and then other block producers use the PBFT, that is, the minority obeys the majority principle. If more than 66% of the block producers agree to the result of the block validator, consensus is reached; otherwise, the block validator is re-elected and the voting process is repeated.

​        Under the PBFT + DPOS consensus mechanism, the algorithm time is effectively reduced, thereby increasing the block production speed, improving the robustness and security of the algorithm, and reducing the transaction confirmation cycle. The transaction throughput can reach thousands of TPS. Combined with the side chain technology, it can easily achieve tens of thousands of TPS and has excellent performance in the public chain. It can support large-scale commercial applications.

### 3.2 Smart Contract

​        The smart contract is a computer protocol, and its purpose is to verify the negotiation of a contract digitally. Not only do they define agreement-related rules and penalties in the same way as traditional contracts, they can also automate these obligations. If the predefined rules are met, the agreement is executed automatically. Smart contract code facilitates, verifies, and executes the negotiation or execution of an agreement or transaction. It is the simplest form of decentralized automation.

​        BCB's smart contracts support [Solidity](https://en.wikipedia.org/wiki/Solidity) and Golang to develop. BCB's Solidity contract is completely compatible with the EVM environment of Ethereum. Developers can easily migrate smart contracts in Ethereum to BVM in the BCB blockchain. At the same time, developers can build in a mixed environment with Solidity, debug and execute smart contracts.

​        The Golang language contract in the BCB blockchain is implemented through plug-in technology, which mainly solves the problem that today's mainstream smart contracts can't write complex logic (such as tens of thousands of lines of code), and and that a large number of contracts call each other, which makes the complexity of contract development, debugging, and upgrading very large.

### 3.3 Side Chain

​        The BCB side chain realizes the mutual transfer of digital assets on the BCB blockchain between the main chain and the side chain through two-way anchoring technology, IBC contracts and relay services. The side chain itself is an independent blockchain with its own node network, and the code and data are also relatively independent, so it will not increase the burden on the main chain during the operation process, avoiding the situation of excessive data inflation. Through the side chain technology, we can achieve application isolation and privacy protection between different businesses, and at the same time can improve TPS.

​        Sidechain technology further expands the application range and innovation space of blockchain technology, enabling traditional blockchains to support multiple asset types, as well as small and micro payments, smart contracts, security processing mechanisms, property registration and so on, and can enhance block chain privacy protection. With sidechains, we can easily build various intelligent applications such as financial contracts, stocks, futures, derivatives and so on.

### 3.4 Governance mechanism

​        Blockchain is not just a technology, it also contains a lot of knowledge about economics, sociology, and politics. In order to understand the blockchain, in addition to understanding the consensus mechanism, scalability, security and so on, you also need to understand the design of the blockchain's token economic system and the long-lasting governance mechanism.

​        BCB mainly adopts on-chain governance: the holders of BCB tokens are the owner and manager of the BCB network, and the management rights and network use rights are realized by sending voting transactions on the BCB network.

## 4. Main advantages

​        Traditional systems have problems such as troublesome reconciliation, centralization, and tampering with data. But in the blockchain systems, it can improve the efficiency of multi-center collaboration, decentralize, increase multi-party trust, data cannot be tampered with, traceability, auditability and so on. BCBChain investigates many mainstream open source blockchain solutions such as ETH, Fabric, Tendermint, Cosmos and so on, and forms four major advantages of their own.

### 4.1 High Performance

- High-performance consensus algorithm, BCB uses PBFT + DPOS double consensus algorithm.

- Efficient smart contract engine, BCB's smart contracts support [Solidity](https://en.wikipedia.org/wiki/Solidity) language and Golang language to develop.

- Support side chain, its TPS can reach 10,000 TPS.

### 4.2 Security Privacy

- High-security signature algorithm: BCBChain signature algorithm uses Ed25519. Ed25519 has the advantages of being completely open, high security, and fast.

- High-strength hashing algorithm SHA3-256.

- Through side chain technology, we can achieve application isolation and privacy protection between different businesses.

### 4.3 High availability

- Supports adding and removing nodes dynamically.

- Detection with node failure and fast recovery mechanism.

- Easy to publish your own token.

### 4.4 High scalability

- Supports side chain, it makes business applications can be infinitely expanded.

- Support Solidity language and Golang language smart contract.

- The solidity smart contract is completely compatible with Ethereum and easy to migrate.

## 5. BCB's future direction

​        If you want to solve the large-scale use of blockchain, the most important thing is to solve the problem of on-chain and off-chain. On-chain means the blockchain, and off-chain means all traditional information systems.

​        Both traditional information systems and blockchain systems have certain limitations. One one hand, blockchain systems need to expand computing and storage capabilities through off-chain systems, on the other hand, the current off-chain systems need to interface with the blockchain to solve problems such as information isolated island and tamper resistance. How can we embed the blockchain system into the existing traditional system, or how to use the blockchain to release the traditional information system, is the main mission of the BCB in the future. It mainly includes four parts:

- Large-scale high-performance point-to-point network

- Modular secure cryptography protocol

- High-performance programmable computing engine

- Definable data distribution protocol
