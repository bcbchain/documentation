# Difference between BVM and EVM

## 1. BVM overview

The BVM virtual machine of the BCBchain is perfectly compatible with the EVM virtual machine. The smart contracts developed on Ethereum can be transplanted into BVM without any changes. In addition, standard tokens can also be used in BVM contracts. This article mainly explains the differences between BVM and EVM.

## 2. ABI differences

- blockhash:

  - BVM：You can get the hash of the current block height and the hash of any block of any height that has been generated;
  - EVM：Only the hash of the current block -1 to -256 height can be obtained;

- block.coinbase:

  - BVM：What is obtained is the address of the sponsor of the current block (the BCBchain has no mining);
  - EVM：What is obtained is the mining address of the current block;

- block.difficulty:

  - BVM：BCBchain is not mining, so block.difficulty is set to 0 by default;
  - EVM：Difficulty of mining the current block;

## 3. Other differences

- Currency accuracy

  - BVM：The minimum unit of currency is cong (1 bcb = 1 * 10 ^ 9). In order to be compatible with the `wei` keyword in the EVM contract, we have expanded the BVM account balance and added the BVMBalanceMod field to record eighteen digits. Last nine digits of precision;

    ```go
    type AccountInfo struct {
      Address       types.Address `json:"address"`
      Balance       bn.Number     `json:"balance"`
      BVMBalanceMod bn.Number     `json:"bbMod,omitempty"` // last nine digits of eighteen digits of precision
    }
    ```

  - EVM：Currency accuracy (1 eth = 1 * 10 ^ 18);

- Deployment contract
  - BVM：When deploying a contract, you need to specify the standard tokens supported by the contract;
  - EVM：When the contract is deployed, it cannot be specified, and eth is used by default.
