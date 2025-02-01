# Storage

```solidity
contract FunWithStorage {
  uin256 favoriteNumber;
  bool someBool;
  uint256[] myArray;
  uint256 constant NOT_IN_STORAGE = 123;
  mapping(address => uint256) balance;
  bytes32[3] private data;
  uint8 private flattening = 10;
  uint8 private denomination = 255;
  uint16 private awkwardness = uint16(block.timestamp);
}
```
favoriteNumber --> storage slot 0;

someBool --> storage slot 1;

myArray length --> storage slot 2;

myArray[2] --> storage slot keccak256(2) + 1.  dynamic array’s elements are stored starting from keccak256(slot) where slot the location where the array's length is stored. (in this case 2).

NOT_IN_STORAGE --> not in storage, saved in the contract's bytecode due to "constant" keyword. Constant and Immutable keywords do not take a slot in storage.

balance(0x23d3957BE879aBa6ca925Ee4F072d1A8C4E8c890) --> keccak256(abi.encodePacked(key, p)) where key is the address in this case (0x23d3957BE879aBa6ca925Ee4F072d1A8C4E8c890); and p is the slot where the mapping itself is stored, in this case 5;

data --> fixed size array of 3 32bytes item, each take a storage slot; in this case they slots: 6, 7, 8.

flatenning + domination + awkardness --> storage slot 9; where flattening (uint8): 1 byte, value = 0x0A. denomination (uint8): 1 byte, value = 0xFF. awkwardness (uint16): 2 bytes, value = 0x3B60 (15200 in decimal). Remaining 28 bytes are empty or zero.


```solidity
function doStuff() public {
uint256 newVar = favoriteNumber + 1;
uint256 otherVar = 7;
}
```

Variables in functions are saved in memory and are only available for the duration of the function call.

Strings are treated as technically a dynamic sized array, so we need to precise the "memory" keyword.
