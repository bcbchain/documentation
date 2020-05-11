# BVM与EVM差异说明

## 1. BVM概述

BCB主链的BVM虚拟机，完美兼容了EVM虚拟机，在以太坊上开发的智能合约，可以不用任何更改的移植到BVM中，另外在BVM合约中还可以使用标准代币。本文主要阐述BVM 与EVM的不同点。

## 2. ABI差异说明

- blockhash:

  - BVM：可以获取到当前区块高度hash以及已经产生的任意高度区块的hash；
  - EVM：只能获取到当前区块 -1 至 当前区块 -256 高度的hash；

- block.coinbase:

  - BVM：获取到的是当前区块的提案人地址（BCB主链没有挖矿）；
  - EVM：获取的是当前区块的挖矿地址；

- block.difficulty:

  - BVM：BCB链没有挖矿，所以block.difficulty默认设置为0；
  - EVM：当前区块的出块难度；

  

## 3. 其他差异说明

- 币种精度

  - BVM：币种的最小单位为cong(1 bcb = 1*10^9)，为了兼容EVM合约中的`wei`关键字，我们对BVM的账户余额进行了扩展，增加了BVMBalanceMod字段用于记录十八位精度的后九位数值；

    ```go
    type AccountInfo struct {
    	Address       types.Address `json:"address"`
    	Balance       bn.Number     `json:"balance"`
    	BVMBalanceMod bn.Number     `json:"bbMod,omitempty"` // 十八位精度的后九位
    }
    ```

  - EVM：币种精度(1 eth = 1*10^18)；

- 部署合约
  - BVM：在部署合约时，需要指定该合约支持的标准代币；
  - EVM：在部署合约时，无法指定，默认使用eth。