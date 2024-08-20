# Storage

```
contract FunWithStorage {
  uin256 favoriteNumber;
  bool someBool;
  uint256[] myArray;
  uint256 constant NOT_IN_STORAGE = 123;
}
```

favoriteNumber --> storage slot 0;
someBool --> storage slot 1;
myArray length --> storage slot 2;
myArray[2] --> storage slot [keccak256(2)]
NOT_IN_STORAGE --> not in storage, saved in the contract's bytecode due to "constant" keyword. Constant and Immutable keywords do not take a slot in storage.

```
function doStuff() public {
uint256 newVar = favoriteNumber + 1;
uint256 otherVar = 7;
}
```

Variables in functions are saved in memory and are only available for the duration of the function call.

Strings are treated as technically a dynamic sized array, so we need to precise the "memory" keyword.
