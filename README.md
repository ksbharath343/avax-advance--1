# avax-advance--1
```markdown
# ERC20 and Vault Contracts

This repository contains two Solidity smart contracts: an ERC20 token implementation and a Vault contract for securely storing tokens.

## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [ERC20 Token](#erc20-token)
  - [Features](#features)
  - [Usage](#usage)
- [Vault Contract](#vault-contract)
  - [Features](#features-1)
  - [Usage](#usage-1)
- [License](#license)

## Introduction

The ERC20 contract provides a basic implementation of the ERC20 token standard, which includes functionalities such as transferring tokens, checking balances, and approving allowances. The Vault contract allows users to deposit and withdraw ERC20 tokens securely.


## ERC20 Token

### Features

- **Total Supply**: Get the total supply of tokens.
- **Balance Of**: Check the balance of a specific address.
- **Transfer**: Transfer tokens from one address to another.
- **Approve**: Approve an address to spend a specified amount of tokens.
- **Transfer From**: Transfer tokens from an approved address.
- **Allowance**: Check the remaining number of tokens that an address is allowed to spend.

### Usage

Here is an example of how to deploy and interact with the ERC20 token contract.

```solidity
pragma solidity ^0.8.0;

import "./ERC20.sol";

contract MyToken is ERC20 {
    constructor(uint256 initialSupply) ERC20("MyToken", "MTK") {
        _mint(msg.sender, initialSupply);
    }
}
```

## Vault Contract

### Features

- **Deposit**: Deposit ERC20 tokens into the vault.
- **Withdraw**: Withdraw ERC20 tokens from the vault.
- **Check Balance**: Check the balance of deposited tokens.

### Usage

Here is an example of how to deploy and interact with the Vault contract.

```solidity
pragma solidity ^0.8.0;

import "./IERC20.sol";

contract Vault {
    mapping(address => uint256) private _balances;
    IERC20 private _token;

    constructor(address tokenAddress) {
        _token = IERC20(tokenAddress);
    }

    function deposit(uint256 amount) public {
        require(_token.transferFrom(msg.sender, address(this), amount), "Transfer failed");
        _balances[msg.sender] += amount;
    }

    function withdraw(uint256 amount) public {
        require(_balances[msg.sender] >= amount, "Insufficient balance");
        _balances[msg.sender] -= amount;
        require(_token.transfer(msg.sender, amount), "Transfer failed");
    }

    function balanceOf(address account) public view returns (uint256) {
        return _balances[account];
    }
}
```


## License

This project is licensed under the MIT License.
```
