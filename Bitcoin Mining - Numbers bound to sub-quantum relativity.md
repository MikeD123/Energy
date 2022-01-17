## Bitcoin Mining - Numbers bound to sub-quantum relativity

![miningLol](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQQSqnlNvnoOR_B2C7f4xYTb9Om47SF__YrpRWJP4dGrKSbXJtUrymMW5DcvqQrmaXJ9pg&usqp=CAU)

This is a historical data plot for the Bitcoin nonce values, over time. You can see a very distinct change of behaviour/tactic in the nonce discovery process. Many have given hand wavy answers, such as "Satoshi playing around" or "multiple nodes running off the same network participant" and others have just dismissed it to thing relating to ASIC boost. All of those are pretty much incorrect.

What you are seeing is a visual representation of formulaic vs brute force. The left hand side, and early days, we see an obvious formula being implemented, and the right hand side is a slew of guess work. That is modern day bitcoin mining. Smash power.

Well, below is the formula/approach for a more successful implementation and efficiency gain for any miner that chooses to do so.

### tl;dr

- Miners have a limited search space. There's a finite number of valid guesses.
- Everytime they increment their CPU clock time (timestamp), while they are increasing the nonce value, they are making it exponentially more difficult to find a correct value.
- By freezing the timestamp first, then searching all nonces, and then repeating this pattern, they will discover the correct value far more efficiently.
- It optimizes mining by over 1,000,000x

This is napkin math, so don't bother with the specifics, as they're rounding errors in the scheme of things.

### History/Context

Current Bitcoin TH/s (total hashes per second) is 166.034M Terahashes per That is 166034000 * 1,000,000,000,000. Approximately, 166 million billion hashes per second.

Mining a block requirements in Bitcoin

* Version
* Block Header
* Merkle Root
* Timestamp
* Nonce
* Bits

If a miner were to try randomly picking a nonce, they're going to have a chance between 0 and 10 Billion (or whatever is the max number possible for that *field* specifically, to satisfy the requirements for the network).

Machines, by default, will incramemnt the timestamp automatically. That's there way of keeping the time. If a users machine is trying to increment the nonce, but simultaneously incrementing the timestamp (which occurs by default on the device afaik) this means that every change to the timestamp, should result in resetting the search for the nonce value. Much like resetting the search when a new block is found, miners start over and "work" on a new block. This means that every time the timestamp changes (which is every second I believe?) it should mean that we are 1/10 billion for each miner, at any given second. So pure brute force means that each miner will be constructing a different block, with a different receiving address for the block reward, etc... These variables will add to the delay in discovering the correct nonce, as it will be relative to the miner mining that block at that time, on that machine.

**Optimisation question**

(I have a limited understanding of this all so please take this with a grain of salt)

Assuming the above logic is correct, it means that a more elegant solution presents itself for miners to secure the network exponentially.

A miner can fix the block header requirements specifically, the timestamp that is included into the block headerat some point in the future, to then work on guessing the correct nonce for that timestamp that corresponds with that version, blockheader, merkle root, bits, and then the nonce value.

Now we are only required to guess the nonce value, which requires 10B guesses. Because we know that if the timestamp is satisfactory, and the other fields are too, then we know with absolute certainty that there will be a successful hash at that timestamp we put in (which was some point in the future from when we commenced attempting to change the nonce value).

If every timestamp has a corresponding correct hash, then so does every nonce value if that timestamp is fixed in place.

Assuming this all to be true, mining a block should take no longer than time it takes to try the maximum number of possible values for the given field. In our case, 10 billion guesses

Block template
* Version - Provided by the miner
// impossible to get incorrect

* Block Header - Provided by network
// impossible to get incorrect once known

* Merkle Root - Provided by network
// impossible to get incorrect once known. The merkle root can be for an empty block, or a simple structure of the highest to lowest fee paying transactions. But it *can* be deterministic.

* Timestamp - Provided by the miner
// Changes locally for each miner

* *Nonce - Guessed by the miner*
// This is incremented by the miner

* Bits - Provided by network
// impossible to get incorrect once known

So essentially what we're doing differently here is we are setting the timestamp value to some point in the future (instead of our machine telling us the timestamp), and then we complete 10B guesses. At some point we will find the correct nonce, then we would go and broadcast that to the network once we found a hash that satisfies the network requirements, and be rewarded bitcoins for securing the network.

If we assume that there is not a satisfactory hash available for every timestamp, it means that we still have an optimization of 10B guesses per second, and 600 seconds per estimated target block time.

Example in practice
If you take 600 miners who are all capable of guessing 10B guesses in 1 second we would have 10 minute block times still.

We can agree that this is 6,000B guesses per block that are possible now. There should not be a larger possible domain that is possible for finding the correct hash.

The current bitcoin network has 166M billion hashes per second. Which is ~166M billion* 600 seconds is 99,600 million billion guesses per block.or we could say 99.6 Billion billion.

99.6B / 6000 = 16,600,000

If this above logic is correct, then we could optimise the network by 16,600,000x or 1.6B% optimization in bitcoin mining.

If everyone is mining, then we are all satoshi nakamoto :)
