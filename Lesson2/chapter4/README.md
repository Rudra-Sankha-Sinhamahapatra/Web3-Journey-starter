
# Chapter 4: Require

In lesson 1, we made it so users can create new zombies by calling `createRandomZombie` and entering a name. However, if users could keep calling this function to create unlimited zombies in their army, the game wouldn't be very fun.

Let's make it so each player can only call this function once. That way new players will call it when they first start the game in order to create the initial zombie in their army.

## How can we make it so this function can only be called once per player?

For that, we use `require`. `require` makes it so that the function will throw an error and stop executing if some condition is not true:

```solidity
function sayHiToVitalik(string memory _name) public returns (string memory) {
  // Compares if _name equals "Vitalik". Throws an error and exits if not true.
  // (Side note: Solidity doesn't have native string comparison, so we
  // compare their keccak256 hashes to see if the strings are equal)
  require(keccak256(abi.encodePacked(_name)) == keccak256(abi.encodePacked("Vitalik")));
  // If it's true, proceed with the function:
  return "Hi!";
}
```

If you call this function with `sayHiToVitalik("Vitalik")`, it will return "Hi!". If you call it with any other input, it will throw an error and not execute.

Thus, `require` is quite useful for verifying certain conditions that must be true before running a function.

## Put it to the test

In our zombie game, we don't want the user to be able to create unlimited zombies in their army by repeatedly calling `createRandomZombie` — it would make the game not very fun.

Let's use `require` to make sure this function only gets executed one time per user, when they create their first zombie.

1. Put a `require` statement at the beginning of `createRandomZombie`. The function should check to make sure `ownerZombieCount[msg.sender]` is equal to `0`, and throw an error otherwise.

**Note:** In Solidity, it doesn't matter which term you put first — both orders are equivalent. However, since our answer checker is really basic, it will only accept one answer as correct — it's expecting `ownerZombieCount[msg.sender]` to come first.
