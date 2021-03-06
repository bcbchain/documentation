# BCB介绍

## 1. BCB是什么

​        BCB是以Tendermint为基础开发的区块链体系，以系统安全性为依归，进行技术创新，实现物与物、人与物之间高效的价值信息传递，打造快速应用，具备高性能及高扩展性的平台。

​        Tendermint 是一个模块化的区块链软件框架，支持开发者个性化定制自己的区块链，它提供了一个已存在的包含网络层和共识层的通用引擎，通过一个基于socket协议的ABCI（ Application  Blockchain  Interface）接口来连接应用，便于在之上构建任意的应用程序。 

## 2. 系统架构

<img src=".\p\BCB-arch-3.png" style="zoom:75%;" />

## 3. 核心设计

### 3.1 双共识机制

​        所有区块链实际是建立在交易之上的确定性状态机。共识是在确定交易顺序，过滤无效交易的一个达成一致意见的流程。BCB 在 PBFT（Practical Byzantine Fault Tolerance， 实用拜占庭容错）算法的基础上，提出了 PBFT+DPOS的共识算法。在这个机制当中，存在两个参与者，一个是专业记账的“记账节点”，一个是系统当中的普通用户。普通用户基于持有权益的比例来投票决定记账节点，当需要通过一项共识时，在这些记账节点中随机推选出一名发言人拟定方案，然后由其他记账节点根据拜占庭容错算法，即少数服从多数的原则进行表态，如果超过66%的节点表示同意发言人方案，则共识达成；否则，重新推选发言人，重复投票过程。

​       在PBFT+DPOS的共识机制下，有效降低了算法耗时，从而提高了出块速度，提升了算法的鲁棒性和安全性，同时降低了交易确认周期。交易吞吐量实测可达到上千tps，再结合侧链技术，可以轻松实现上万tps，在公有链中性能优秀。可以支持大规模的商业化应用。

### 3.2 智能合约

​        智能合约是一种计算机协议，其目的是以数字方式验证合约的协商。 他们不仅以与传统合同相同的方式定义与协议相关的规则和处罚，而且还可以自动执行这些义务。 如果满足预定义规则，则自动执行协议。 智能合约代码促进、验证和执行协议或交易的协商或执行。 它是去中心化自动化的最简单形式。

​        BCB的智能合约支持[Solidity](https://en.wikipedia.org/wiki/Solidity) 编程语言开发和go语言开发。 BCB的Solidity合约，完全与以太坊的EVM环境兼容，开发者可以非常方便的把以太坊中的智能合约移植到BCB区块链的BVM中，同时开发人员可以在具有Solidity的混合环境中构建，调试和执行智能合约。

​      BCB区块链中的go语言合约，通过插件技术实现，主要解决当今的主流智能合约，无法编写复杂的业务逻辑（比如上万行代码），且大量合约之间的互相调用，使得合约的开发调试和维护升级的复杂度变得非常大的问题。

### 3.3 侧链

​       BCB侧链通过双向锚定技术、IBC合约以及中继服务，实现BCB区块链上的数字资产在主链以及侧链之间的互相转移。  侧链本身是独立的区块链，有自己的节点网络，代码以及数据也是相对独立的，所以它在运行过程中不会增加主链的负担，避免数据过度膨胀的情况出现。 通过侧链技术，我们可以实现不同业务之间的应用隔离，隐私保护，同时可以提高交易吞吐量。 

​        侧链技术进一步扩展了区块链技术的应用范围和创新空间，使传统区块链可以支持多种资产类型，以及小微支付、智能合约、安全处理机制、财产注册等，并可以增强区块链的隐私保护。利用侧链，我们可以轻松的建立各种智能化的应用如金融合约，股票、期货、衍生品等。 

### 3.4 治理机制

​       区块链不仅仅是一门技术，它也包含了经济学、社会学以及政治学的诸多知识，要理解区块链，除了要理解共识机制、扩展性、安全等，还要了解区块链的token经济体系设计、让项目长久持续的治理机制。

​        BCB主要采用链上治理：BCB 管理代币的持有人是 BCB 网络的所有者和管理者，通过在 BCB网络上构造投票交易来实现管理权和网络使用权。

## 4. 主要优势

​        传统系统存在互相对账麻烦、中心化、篡改数据等问题，区块链系统可以提升多中⼼的协作效率、去中介，提升多⽅信任、数据不可篡改，可追溯，可审计等等特点。
​        BCBChain参考了ETH，Fabric，Tendermint，Cosmos等多家主流开源区块链方案，取其精华，形成自己的四大主要优势。

### 4.1 高性能

- 高性能的共识算法，BCB采用PBFT+DPOS双共识算法。

- 高效智能合约引擎，BCB的智能合约支持[Solidity](https://en.wikipedia.org/wiki/Solidity) 编程语言开发和go语言开发。

- 支持侧链，TPS可达到1w。

### 4.2 安全隐私

- 高安全性的签名算法：BCBChain签名算法采用Ed25519，Ed25519具有完全开放、安全性高，速度快等优点。
- 高强度的散列算法SHA3-256。

- 通过侧链技术，实现不同业务之间的数据隔离，隐私保护。

### 4.3 高可用性

- 支持动态增删节点。
- 节点失效检测及快速恢复机制。

- 一键发币。

### 4.4 高可扩展性

- 支持侧链，业务应用可以通过侧链技术无限扩展。
- 支持go语言与solidity智能合约。
- solidity智能合约与以太坊完全兼容，方便移植。



## 5. BCB未来方向

​        如果要解决区块链⼤规模应⽤，最重要应该解决链上链下的问题，所谓的链上就是区块链，链下就是所有传统的信息系统。

​        传统信息系统与区块链系统都有⼀定的局限性。⼀⽅⾯，区块链系统需要通过链下系统扩展计算和存储能⼒。另 ⼀⽅⾯，现有链下系统需要与区块链对接以解决信息孤岛、防篡改等问题。 我们怎样把区块链系统嵌入到现有的传统系统，或者如何用区块链把传统信息系统释放出来，是BCB未来研究的主要方向。主要研究的技术点包括四个方面：

- 大规模高性能点对点网络

- 模块化安全密码学协议

- 高性能可编程计算引擎

- 可定义的数据分发协议