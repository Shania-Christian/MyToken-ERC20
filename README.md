# MyToken (MTK) - ERC-20 Smart Contract

## 📌 Overview
**MyToken (MTK)** is an ERC-20 token implemented in Solidity. It includes additional security features like account freezing, blacklisting, and a pause mechanism. This token is designed to be used for decentralized applications (dApps), tokenized assets, and general blockchain-based transactions.

## 🚀 Features
- ✅ **ERC-20 Standard Compliance** (transfer, approval, allowance)
- ✅ **Minting & Burning** (Controlled supply management)
- ✅ **Pausing Token Transfers** (Owner can pause/unpause transactions)
- ✅ **Blacklisting & Freezing** (Restrict malicious accounts)
- ✅ **Ownership Transfer** (Admin can transfer ownership)

## 🛠️ Technologies Used
- **Solidity** (`^0.8.20`)
- **Ethereum Blockchain**

## 📄 Smart Contract Code
The Solidity contract implements standard ERC-20 functions along with enhanced security features:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MyToken {
    string public name = "MyToken";
    string public symbol = "MTK";
    uint8 public decimals = 18;
    uint256 public totalSupply;
    address public owner;
    
    mapping(address => uint256) public balanceOf;
    
    constructor() {
        owner = msg.sender;
        totalSupply = 1_000_000 * (10 ** uint256(decimals));
        balanceOf[owner] = totalSupply;
    }
}
```


