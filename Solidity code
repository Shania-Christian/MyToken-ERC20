// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

interface IERC20 {
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
    
    function totalSupply() external view returns (uint256);
    function balanceOf(address account) external view returns (uint256);
    function transfer(address to, uint256 value) external returns (bool);
    function allowance(address owner, address spender) external view returns (uint256);
    function approve(address spender, uint256 value) external returns (bool);
    function transferFrom(address from, address to, uint256 value) external returns (bool);
}

contract MyToken is IERC20 {
    string public name = "MyToken";
    string public symbol = "MTK";
    uint8 public decimals = 18;
    uint256 public override totalSupply;
    address public owner;
    bool public paused = false;

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowances;
    mapping(address => bool) public frozenAccounts;
    mapping(address => bool) public blacklisted;

    modifier onlyOwner() {
        require(msg.sender == owner, "Not contract owner");
        _;
    }
    
    modifier notPaused() {
        require(!paused, "Token transfers are paused");
        _;
    }
    
    constructor() {
        owner = msg.sender;
        totalSupply = 1_000_000 * (10 ** uint256(decimals));
        balanceOf[owner] = totalSupply;
        emit Transfer(address(0), owner, totalSupply);
    }
    
    function transfer(address to, uint256 value) external override notPaused returns (bool) {
        require(!frozenAccounts[msg.sender], "Sender account is frozen");
        require(!blacklisted[msg.sender] && !blacklisted[to], "Address is blacklisted");
        require(balanceOf[msg.sender] >= value, "Insufficient balance");
        require(to != address(0), "Invalid recipient");
        
        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;
        
        emit Transfer(msg.sender, to, value);
        return true;
    }
    
    function allowance(address _owner, address spender) external view override returns (uint256) {
        return allowances[_owner][spender];
    }
    
    function approve(address spender, uint256 value) external override returns (bool) {
        require(spender != address(0), "Invalid spender");
        allowances[msg.sender][spender] = value;
        emit Approval(msg.sender, spender, value);
        return true;
    }
    
    function transferFrom(address from, address to, uint256 value) external override notPaused returns (bool) {
        require(!frozenAccounts[from], "From account is frozen");
        require(!blacklisted[from] && !blacklisted[to], "Address is blacklisted");
        require(balanceOf[from] >= value, "Insufficient balance");
        require(allowances[from][msg.sender] >= value, "Allowance exceeded");
        require(to != address(0), "Invalid recipient");
        
        allowances[from][msg.sender] -= value;
        balanceOf[from] -= value;
        balanceOf[to] += value;
        
        emit Transfer(from, to, value);
        return true;
    }
    
    function mint(address to, uint256 amount) external onlyOwner {
        require(to != address(0), "Invalid address");
        totalSupply += amount;
        balanceOf[to] += amount;
        emit Transfer(address(0), to, amount);
    }
    
    function burn(uint256 amount) external {
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");
        totalSupply -= amount;
        balanceOf[msg.sender] -= amount;
        emit Transfer(msg.sender, address(0), amount);
    }
    
    function freezeAccount(address account) external onlyOwner {
        frozenAccounts[account] = true;
    }
    
    function unfreezeAccount(address account) external onlyOwner {
        frozenAccounts[account] = false;
    }
    
    function pause() external onlyOwner {
        paused = true;
    }
    
    function unpause() external onlyOwner {
        paused = false;
    }
    
    function blacklist(address account) external onlyOwner {
        blacklisted[account] = true;
    }
    
    function unblacklist(address account) external onlyOwner {
        blacklisted[account] = false;
    }
    
    function transferOwnership(address newOwner) external onlyOwner {
        require(newOwner != address(0), "Invalid owner");
        owner = newOwner;
    }
}
