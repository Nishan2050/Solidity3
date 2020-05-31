# Solidity3
// Multiple smart contracts and inheritance


pragma solidity ^0.6.1;


contract newyork{
   address owner;
   
     modifier onlyowner() {
       require(msg.sender == owner, "not authorized");
       _;
       
   }
   
   constructor() public {
       owner = msg.sender;
   }
}

contract Secretvalue{
    string value;
    
     constructor(string memory _secret) public {
       value = _secret;
       
   }
    
    function getsecret() public view  returns(string memory) {
       return value;
   }
}

contract taken is newyork{
   address secretvalue;
   
   constructor(string memory _secret) public {
       Secretvalue _secretvalue = new Secretvalue(_secret);
       secretvalue = address(_secretvalue);
       super;
   }
   
   function getsecret() public view onlyowner returns(string memory) {
       Secretvalue _secretvalue = Secretvalue(secretvalue);
       return _secretvalue.getsecret();
   }
   
}

