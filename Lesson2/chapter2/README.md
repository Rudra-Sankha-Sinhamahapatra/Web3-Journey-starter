
# Chapter 2: Mappings and Addresses

Let's make our game multi-player by giving the zombies in our database an owner.

To do this, we'll need 2 new data types: `mapping` and `address`.

## Addresses

The Ethereum blockchain is made up of accounts, which you can think of like bank accounts. An account has a balance of Ether (the currency used on the Ethereum blockchain), and you can send and receive Ether payments to other accounts, just like your bank account can wire transfer money to other bank accounts.

Each account has an address, which you can think of like a bank account number. It's a unique identifier that points to that account, and it looks like this:

`0x0cE446255506E92DF41614C46F1d6df9Cc969183`

(This address belongs to the CryptoZombies team. If you're enjoying CryptoZombies, you can send us some Ether! 😉 )

We'll get into the nitty gritty of addresses in a later lesson, but for now you only need to understand that an address is owned by a specific user (or a smart contract).

So we can use it as a unique ID for ownership of our zombies. When a user creates new zombies by interacting with our app, we'll set ownership of those zombies to the Ethereum address that called the function.

## Mappings

In Lesson 1 we looked at structs and arrays. Mappings are another way of storing organized data in Solidity.

Defining a mapping looks like this:

```solidity
// For a financial app, storing a uint that holds the user's account balance:
mapping (address => uint) public accountBalance;
// Or could be used to store / lookup usernames based on userId
mapping (uint => string) userIdToName;
```

A mapping is essentially a key-value store for storing and looking up data. In the first example, the key is an address and the value is a uint, and in the second example the key is a uint and the value a string.

## Put it to the test

To store zombie ownership, we're going to use two mappings: one that keeps track of the address that owns a zombie, and another that keeps track of how many zombies an owner has.

1. Create a mapping called `zombieToOwner`. The key will be a `uint` (we'll store and look up the zombie based on its id) and the value an address. Let's make this mapping public.

2. Create a mapping called `ownerZombieCount`, where the key is an `address` and the value a `uint`.
