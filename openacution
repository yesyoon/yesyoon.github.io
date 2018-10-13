pragma solidity ^0.4.19;

contract OpenAuction {
    
    address public HighestBidder;
    uint public HighestBid;
    uint public auctiontime;
    uint refundamount;
    /*struct User {
        address UserAddress;
        uint amount;
        uint count;
    }
    
    User[] public Userlist;*/
    
    //mapping (address => uint) refund; 
    event AddUser(address UserAddress, uint amount, uint count);
    event NewHighestBidder(address bidder, uint amount);
    event AuctionEnded(address winner, uint amount);
    
    function AuctionTime(uint _Time) public returns (uint) {
         auctiontime = now + _Time;
        return auctiontime;
    }
    
    function AuctionUser() public payable {
        HighestBidder = msg.sender;
        HighestBid = msg.value;
       // Userlist.push(User(msg.sender, msg.value, 0));
    }
    
    function bid() public payable  {
        require(auctiontime > now);
        require(msg.value > HighestBid);
        
        refundamount = HighestBid;
        refunding(HighestBidder);
        
        HighestBidder = msg.sender;
        HighestBid = msg.value; 
        
        emit NewHighestBidder(msg.sender, msg.value);
    }
    
    function refunding(address _refunduser) public {
        
        if(refundamount > 0) {
           _refunduser.transfer(refundamount);
        }
        refundamount = 0;
    }
    
    function AuctionEnd() public payable {
        require(now >= auctiontime);
        emit AuctionEnded(msg.sender, msg.value);
    }
    
}
