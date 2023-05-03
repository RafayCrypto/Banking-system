# Banking-system
*/a simple banking system having functions to add balance into your account (the account is automatically detected because of address msg.sender) 
another function of transferring money from one address. to another address with the logic that is somebody 
tranfer money then the money from his account is deducted and transferred to other's account just similar to P2P trading wallet account/*

pragma solidity ^0.8.5;

contract banking
{
    mapping(address => uint) balance;

    function addBalance(uint toAdd) public returns (uint)
    {
        balance[msg.sender] += toAdd;
        return balance[msg.sender];
    }

    function getBalance() public view returns(uint)
    {
        return balance[msg.sender];
    }

    function transfer(address reciver, uint amount) public {
        require(balance[msg.sender] >= amount, "You have insuffiecent balance!");
        require(msg.sender != reciver, "You can't be reciver or sender at a time");
        balance[msg.sender] -= amount;
        balance[msg.sender] += amount;
    }
}



// This portion is by uisng ASSERT. 

pragma solidity ^0.8.5;

contract banking
{
    mapping(address => uint) balance;

    function addBalance(uint toAdd) public returns (uint)
    {
        balance[msg.sender] += toAdd;
        return balance[msg.sender];
    }

    function getBalance() public view returns(uint)
    {
        return balance[msg.sender];
    }

    function transfer(address reciver, uint amount) public {
        require(balance[msg.sender] >= amount, "You have insuffiecent balance!");
        require(msg.sender != reciver, "You can't be reciver or sender at a time");

    uint previousSenderBalance = balance[msg.sender];

        balance[msg.sender] -= amount;
        balance[msg.sender] += amount;

    assert (balance[msg.sender] == previousSenderBalance - amount);
    }
}


// doing by modifier to restrict others addresses from trasnferring money to othe only admin can do thattt

pragma solidity ^0.8.5;

contract banking
{
    mapping(address => uint) balance;

    modifier  onlyOwner
    {
        require(owner == msg.sender, "You are not the owner"); 
        _;
    }

    function addBalance(uint toAdd) public returns (uint)
    {
        balance[msg.sender] += toAdd;
        return balance[msg.sender];
    }

    function getBalance() public view returns(uint)
    {
        return balance[msg.sender];
    }

    function transfer(address reciver, uint amount) public onlyOwner {
        require(balance[msg.sender] >= amount, "You have insuffiecent balance!");
        require(msg.sender != reciver, "You can't be reciver or sender at a time");

    uint previousSenderBalance = balance[msg.sender];

        balance[msg.sender] -= amount;
        balance[msg.sender] += amount;

    assert (balance[msg.sender] == previousSenderBalance - amount);
    }
}
