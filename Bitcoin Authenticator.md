  ## Bitcoin Organic One-time Security Token (BOOST)

### Background Context

Device based authentication is the most reliable security setup for MFA purposes as it removes things such as Sim swapping. Device based authenticators like Google Authenticator are bound to the device, and not the phone number associated with the device.

With Google Authenticator, a secret is created, and shared between Google and the users device, (by scanning the secret QR code).

Then, using time, it will keep refreshing a secret code, based on the time on your device and the server (which are essentially paired when you set it up).

The two systems remain in sync, because they’re marching to the same beat together effectively. The initial sync allows offline synchronisation, such that when you go back online, the server and your device should still be in sync, thus the codes are valid. This is why you are able to watch the codes update on your phone, even if you’re not connected to the internet after you have sync’d!

When you are asked for the Google Authenticator code upon logging in to a vendor (e.g. exchange, or wallet, etc…) the vendor will check what you entered, and compare it with what Google thinks the code is.

If Google and you have the same code, the vendor knows that it is legitimate, and then to grant permission to the user.

![example authenticator flow](https://i.imgur.com/fWyuJtl.png)

### The Problem

To do this without Google, there’s nothing to validate against. If Google isn’t there, then vendors aren't able to verify the code received from the user initially, against anything. So it then means the vendor never really is able to confirm it.

To replace Google’s role in this context, we need to find a way to sync the user who is attempting verification, the vendor awaiting verification, and then another entity operating as Google (who was in sync with the user).

### Outline

![example flow](https://i.imgur.com/w6MKGjM.png)

But we don't have a timestamp for each block, beyond the blockheight number itself. That is problematic because it doesn't give any additional context as to what chain specifically that blockheight is referring to.

### Design

Generate a private key, and publish it for public use.

We time lock funds into this address, at a specific point in the future.

Give everyone on the network the private/public key pair, making it more of a “utility” key, than a private key protecting funds. This functions as our “shared secret” if we think in terms of Google Authenticator.

Using the public key, and BIP65, we derive a HODL address as far into the future as we can. This allows for the most longevity (like having the largest possible amount of potential timestamps basically!).

HODL addresses derived now have numerous attributes:
* The secret key (which we all know).
* Blockheight (Unique address based on the blockheight).
* Redeem Script (Used for collecting the deposited coins from the HODL address derived).

These attributes can be used for initial alignment of external parties should they disconnect from the network for some amount of time. Once the time is met, we now are ready to receive our input from the network. This input is then put through the hash function (specified by the parties participating outside of the network).

Example Inputs
* UTXO of transaction that took coins that were publicly available, from the HODL wallet.
* Address of the successful retriever of the funds (e.g. first to sign and broadcast a transaction moving the coins from the HODL wallet, likely a miner on the network).

We’re now in sync with a common point on the network that exists in the future.

We prove that we have arrived at the future point in time, by using the inputs now available.

Use Cases

DAO Backups

1. DAO proposes to save a snapshot of the user balances before commencing an upgrade. Due to the risk of deploying and not being able to rollback in an elegant way, they decide they want to “back up” their current state of user balances in case of any issues post deployment.

2. The DAO votes to deposit some amount into a HODL wallet at some point in time. Referencing a blockheight and redeem script in the proposal. This is done to ensure alignment initially, and have a clearly defined success/failure scenario.

3. The DAO votes to approve the backup is successful, e.g. if the SHA256(SHA256(redeem script + UTXO))) is equal to whatever the DAO proposes is the successful hash, then we have a backup snapshot agreed by the DAO.

4. DAO participants vote, and can vote however they wish, but it’s likely that DAO’s would publish their proposal of the correct hash, and await for consensus from the DAO participants (i.e the voters all vote for the same correct value).

```json
"WIF": "(private key 5JMdSZpSr8TNBkqHZpq1fKPcCvyafE8uwhfeeZNF1YL8SAa9ZR9)",

"hex": "(private key 472ab2a7873f7703d94d90252a82988f766f520b002a9036fff663a0372e0003)",

"decimal/numbers": "(private key 32189652853536695172679377773646593004206396237826201273814483054019734274051)",

"string":"(brain wallet plain text “1+1=3=Pi”)",

"Blockheight": "7140000",

"Address": "39QWbnkbcPFcrJFEB6yvVDc12eX5zqVt3y"
```

This key, now that it is publicly known to contain some form of future energy (verifiable on chain), it should provide a motivation to be "preserved" or, it should make it easier for two parties to agree on using it, because they both hold it, as it has value in it in 100 years.
