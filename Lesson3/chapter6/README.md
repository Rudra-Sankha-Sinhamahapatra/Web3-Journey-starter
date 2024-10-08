
# Chapter 6: Zombie Cooldowns

Now that we have a `readyTime` property on our Zombie struct, let's jump to `zombiefeeding.sol` and implement a cooldown timer.

We're going to modify our `feedAndMultiply` such that:

- Feeding triggers a zombie's cooldown, and
- Zombies can't feed on kitties until their cooldown period has passed

This will make it so zombies can't just feed on unlimited kitties and multiply all day. In the future, when we add battle functionality, we'll make it so attacking other zombies also relies on the cooldown.

First, we're going to define some helper functions that let us set and check a zombie's `readyTime`.

## Passing Structs as Arguments

You can pass a storage pointer to a struct as an argument to a private or internal function. This is useful, for example, for passing around our Zombie structs between functions.

The syntax looks like this:

```solidity
function _doStuff(Zombie storage _zombie) internal {
  // do stuff with _zombie
}
```

This way we can pass a reference to our zombie into a function instead of passing in a zombie ID and looking it up.

## Put it to the Test

1. Start by defining a `_triggerCooldown` function. It will take 1 argument, `_zombie`, a `Zombie` storage pointer. The function should be `internal`.

2. The function body should set `_zombie.readyTime` to `uint32(now + cooldownTime)`.

3. Next, create a function called `_isReady`. This function will also take a `Zombie` storage argument named `_zombie`. It will be an `internal view` function, and return a `bool`.

4. The function body should return `(_zombie.readyTime <= now)`, which will evaluate to either true or false. This function will tell us if enough time has passed since the last time the zombie fed.

Here's an example of how these functions should look:

```solidity
function _triggerCooldown(Zombie storage _zombie) internal {
  _zombie.readyTime = uint32(now + cooldownTime);
}

function _isReady(Zombie storage _zombie) internal view returns (bool) {
  return (_zombie.readyTime <= now);
}
```

By implementing these helper functions, we can now manage the cooldown period for our zombies and ensure they have to wait before feeding or attacking again.


# Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a Hardhat Ignition module that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat ignition deploy ./ignition/modules/Lock.ts
```
