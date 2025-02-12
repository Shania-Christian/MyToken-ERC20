# MyToken-ERC20

# 📜 Description
MyToken (MTK) is an Ethereum-based ERC-20 token designed with enhanced security features and administrative controls. This smart contract follows the ERC-20 token standard while incorporating additional functionalities like pausing transactions, blacklisting addresses, freezing accounts, and ownership transfer.

The contract is built in Solidity (0.8.20) and can be deployed on Ethereum or any EVM-compatible blockchain.

# 🚀 Features
✅ Standard ERC-20 Functions – Transfer, Approve, Allowance, etc.
✅ Minting & Burning – Owner can create or destroy tokens as needed
✅ Account Freezing – Prevents specific accounts from transacting
✅ Blacklist Functionality – Blocks malicious actors from using tokens
✅ Pause & Unpause Transfers – Temporarily stops all token transfers
✅ Ownership Transfer – Enables safe handover of contract ownership

# ⚙️ Smart Contract Implementation
The contract implements the IERC20 interface and includes:

-> Mapping for token balances and allowances
-> Events for Transfer and Approval
-> Modifiers for access control (onlyOwner, notPaused)
-> Functions for safe token transfer, approval, minting, and burning
-> Security Enhancements: Blacklisting, Freezing, and Emergency Pause
