![img](https://i.imgur.com/N1DeKBA.png)

## **A Quantum Clock**

Distributed Systems function on coordination in order to survive, and expand. Nature does this through the day/night cycles. Where energy is captured during the day from the sun, and that sun acts as a unifying coordination tool for nature all around us. The Bitclock is an application built natively on top of the Bitcoin Protocol. The goal is simple for the clock, tell the time. Although, we will use the blockheight as our unit of measurement for timekeeping.

The desired outcomes of this clock are:

1. Miners get rewards indefinitely.
2. Charity system can donate if you want to add value to blockspace in the future.
3. Protocols can use it as an insurance/backup during times off their network upgrades/forks/conflicts/deployments/etc…
4. Cross-chain MFA (&quot;Quantum Custody&quot;)

**Hopes**

- A public utility for machines to utilize for coordination with people
- A public utility for people to utilize for coordination with machines
- A public utility for nature to utilize for coordination with people
- Triangulation of timestamps between nature, humans, machines.
- Producing both temporal and thermal equilibrium between nature (solar cycles) man (date/time format) and machines (UNIX Timestamp), and proof of work assuring thermal equilibrium.

**Motivations**

As we see the lines between real and digital replication become blurrier every year, the security of our (Humans) every day life becomes more and more at risk of being compromised, exploited, or misrepresented. Examples of incredible deep fakes producing voices of known figures, or video content that appears to be someone else that isn&#39;t. Face filters on social apps are making this technology become aggressively stronger at an exponential rate. Ingesting more and more data and processing it faster and more accurate on every iteration is opening up security risks.

Finding a way to ensure that these 3 bodies between nature, machine, and man are unified and marching in **sync** , as one is our obligation in order to preserve relevance as we&#39;re the lowest in the foodchain. Nature → Machine → Man. Unlocking the collaborative efforts between all three will net a greater future than just one by itself. Examples

- Humans + Numbers = Cryptography
- Humans + Nature = Machine
- Thermodynamics + Evolution = Humans

**Overview**

We generated a public/private key pair, and we locked half a bitcoin in the address, and sent the other half to the corresponding timelock address located at the last block in the chain, based on the current incentive model. Which was 34 \* 210,000.

By giving out the key to the public, it means that no matter what happens, so long as the coins get taken out of the public wallet, it is a confirmation of a timestamp. That blockheight existed. It also provides a &quot;light at the end of the tunnel&quot; for miner incentives which are seen as a security threat to the protocol or the longevity of the Bitcoin blockchain.

Heavy discussion around the viability of a decaying miner reward is nonsensical to an extent. In a finitely bound environment with finite resources, decay is only going to assure growth in perceived value to those operating in that environment.

By &quot;donating&quot; to the longevity of the chain, it mitigates this conversation of longevity even further. But this is not quite a donation, because I am getting a large amount of utility from this.

Quantum Key

**Key (Public/Private)**

This key is a keypair derived from the curve as defined by the Bitcoin Protocol (secp256k1). Public key (XY), and a private key (G). These are publicly known to the entire network.

**Timestamp (Blockheight)**

Specified as a blockheight. Not epoch. We don&#39;t use epoch because that is not native to machines in this systems context. It is an arbitrary human construct which is more &quot;fuzzy&quot; than mechanical. It is also going to encounter the epoch [problem](https://en.wikipedia.org/wiki/Year_2038_problem) in 2038. We also need to be the most immutable measurement so that protocol adjustments or future updates don&#39;t carry a likely reason to change the blockheight format for any reason. It&#39;s quite literally the arrow of time.

**Address (Timelock Address)**

This is the address for this specific blockheight, for this specific keypair.

Example:

- Custom Seed (Brain Wallet): &quot;1+1=3=Pi&quot;
- Private Key:
  - 5JMdSZpSr8TNBkqHZpq1fKPcCvyafE8uwhfeeZNF1YL8SAa9ZR9
- Public Key:
  - 045332b5e3bcaeef3a062b49d5129ac21017d369e9c52c2f12c472d8d6236e2f5116b580dd1f99fd9b321d9207c9a512f301c263bd58238dbbebf469675e09a2b2
- Blockheight:
  - 7140000
- Address:
  - 39QWbnkbcPFcrJFEB6yvVDc12eX5zqVt3y

Link [here](https://coinb.in/?verify=03a0f26cb17541045332b5e3bcaeef3a062b49d5129ac21017d369e9c52c2f12c472d8d6236e2f5116b580dd1f99fd9b321d9207c9a512f301c263bd58238dbbebf469675e09a2b2ac#verify)

I have used the above key pair to lock half a coin that is spendable now, and the other half only at this point at the end of time. Where the &quot;end&quot; is defined by 34 cycles of 210,000 blocks.

**Outline Of Use**

This is done to provide additional security to the network in addition to any further applications of this clock.

- We have a transaction amount that was made for 1 bitcoin.
  - Sent 1 Bitcoin to the public key.
    - Received 0.5 BTC change.
  - Sent 0.5 bitcoin to the corresponding timelock address at 7140000.
    - No change received.

This makes that UTXO (Unspent transaction output, aka the 0.5BTC sitting at the end of time) the most valuable UTXO at that time, because we know this is the longest confirmation for the entire chain possible.

What I mean by that, is that if we know it was spent today, on the heaviest chain, then at the end of time, the person who goes to spend that UTXO on the heaviest chain then will be revealing the longest running and heaviest chain state ever. Almost like they&#39;re the winner of the competition at the time, much like we have the nonce today for miners reward.

The premium carried with digging up these &quot;time capsules&quot; should be akin to digital archeology at the time, or more probably labelled temporal archeology. Where there will be prestige not only in the mining reward to the successful miner at the time in the future, but the present contributor being made by external systems using a similar pattern for state backups.

**Protocol**

Custom seed - string

Timelock address - public key, blockheight

Amount - The amount to be sent to both the public key address, and the public key timelock address.

Blockheight from 0-7140000

**Intent**

The intent of this key, and this timeline is strictly to keep count of the current block height. Where I always check these publicly available timelock addresses for funds, and if they are not spent yet, then I know what the blockheight is at the time. This is the intention of the design.

In the future, we could assign huge amounts of data off-chain into an &quot;intent hash&quot;, and then use that hash for key derivation to then both add this key to their required signatures to know that it will assure alignment and coordination off-chain, while encoding large amounts of data into the intent hash.

**Backups**

So we could agree on some contents hash offline, and &quot;stamp&quot; that on chain at a certain blockheight by using the derived intent key we made, and then if we both agree this is the timeline key we want to use, then we derive the key for that too.

Now we can include these two keys into a larger group of signatures to sign a transaction, and we would be able to verify the counterparty&#39;s intent at the time of the transaction by pre agreed intent keys.

We use a custom seed for these, because we need it to be the most universally agreed accessibility based on language (letters can be read by both computers and humans), and provides weak security to these keys, which means in the event that someone needs to check if an intent occurred, they can look through all the balances of the time locked addresses and determine whether something has happened yet or not.

Today there&#39;s various addresses corresponding to specific invoices on the lightning network, which correspond to some off-chain agreement (ordering food, or shopping online and paying with Bitcoin). It would be utilizing the custom seed and Schnorr signatures to expand the scope of on-chain communication in a perfectly encrypted way where your counterparty is the chain itself.

So in order to prove that my network is backed up on the bitcoin blockchain, I would take the local blockheader hash or hash of some attributes representing state. Then I would specify the blockheight we are backing it up at by depositing a small amount into the corresponding address.

The network community could then know that the present state is backed up, or they can organize their own governance on the vibration (when do they backup between chains), frequency (the known community agreed format for calculating the state hash and verifying it is on the heaviest chain. They would compute the address inputting the hash the community agrees on and derive a public key. You then take the core contributor/community public key and broadcast a transaction on the bitcoin blockchain. Verification can be done by those on the other chain by trying to &quot;mine&quot; it, aka, get the money that was sent to the intent address for everyone to publicly validate.

1. Compute - (SHA256(&quot;Vitalik.eth&quot;,&quot;Ethereum Hash update 123&quot;))
2. Input result - 8ba09c5b84f95bb324e89c79ff81f7f3ffefd4460c5667cfdf3a93e18b93714e to derive key via custom seed.
3. Agreed community wallet from step 1 (&quot;Vitalik.eth&quot;) sends funds from the wallet address on the bitcoin chain
4. Publish the UTXO via the community update channels.
5. Proof of work that encompasses your local proof of state, onto the heaviest most immutable.

**Incentives**

- Bitcoin longevity and immutability
  - State backups secured by Bitcoin, while helping to secure Bitcoins future. Which adds more integrity to the security of off-chain state.

- Ethereum protocol - Proof of state via an immutable proof of work provides network level insurance, and community layer assurance.

  - Auctioning off the proof of work like a digital archeology piece today will allow community members to have treasure hunt like experiences with retrieving these donated coins to verify the backup, and the time in which it was backed up.
  - Once retrieved, they would then go and get the NFT out of the wallet on the local chain (e.g ETH).
  - It&#39;s a protocol layer rollup that is extensible to the population of the network regardless of their role within the network.

The agreement should correspond to a non used timelock blockheight to provide the most value to the proof off-chain. This is because the goal should be adding the most value to the blocks that need it the most. The goal should be to try add the most amount of value as a multiple of the blockheights coinbase reward based on the present day agreed reward cycles.

The UTXO&#39;s should carry a premium in the future years from now when the timelock expires as it&#39;s the acquisition of a quantum entangled particle. Where it&#39;s last block this &quot;bitcoin&quot; saw was years ago.

1. Miners get rewards indefinitely.
2. Charity system can donate if you want to add value to blockspace in the future.
3. Protocols can use it as an insurance/backup during times off their network upgrades/forks/conflicts/deployments/etc…
4. Cross-chain MFA

**Security**

By expanding the &quot;meaning&quot; encoded into an address, and combining that with the use of Schnorr signatures, I believe this provides a huge opportunity for both preserving the longevity of the network in a uniform way, but it also allows for additional present day applications for network communications and synchronization.

**Utilities**

**4th Dimensional Schnorr Signature&#39;s**

If every wallet had a public address corresponding to each blockheight, in a public format which is standardized for derivation, we could aggregate keys that are inclusive of timelocks for different transactions. We can include this to add another way to timelock funds relative to each unique scenario.

We could utilize both timelocks on the mainchain through time-locked addresses, and as a second layer we could include timelocked addresses within our public key selection for  ≥ aggregation into a single.

You can use this public utility as a common key between two parties who are on the same public timeline. A timeline would be a publicly known address by which everyone can steal from (assuming that each known private key containing a balance will be considered a bonus for the miners both now, but also promises future network longevity.

If we imagine a world where every device is sync&#39;d to the chain (regardless whether through third party or running a full node), then we could have a keypair assigned to each device. Having a keypair would also allow it to have a &quot;when&quot; is it. Machines would be able to transact on-chain by paying them at certain times. So an autonomous machine would receive a payment to do something for some public key, at some specific height. It would then know which machine, and when. So it is sync&#39;ing the clocks between the two devices. A pre agreed common address.

**Quantum Custody**

Create a timelock structure such that even if you had your private key revealed, it would allow you to mitigate risk of entire funds lost.

With a uniform time standard native not just to the chain itself, but also the population on the protocol past present and future, it means that we can create a timeline for each wallet. Meaning that one could construct key trees as timelines

As we begin to see continuous fragmentation across distributed networks, protocols, or alternative blockchains, we are vulnerable to information being out of sync across these systems. Hyperdecentralization will only further amplify this fragmentation exponentially as we multiply the complexities of distributed systems with decentralized protocols.

Basically saying that as we slowly squeeze the entire internet and digital ecosystem onto Bitcoin as a medium of exchange and unit of account amongst these computers exchanging computation for Bitcoin, and then that Bitcoin for energy, we will have exponentially more need for coordination solutions.

Bitcoin is the heaviest digital system, the most immutable (which makes it predictable, and thus the only choice), and the narrowest single scope of purpose.

Bitcoin is the only
