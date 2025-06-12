---
description: here you can study the general points about the DAO ENVELOP (and token NIFTSY)
---

# F.A.Q.

### What is Envelop?

Envelop is a multichain protocol (and/or oracle, and/or index) to use wrapped NFT as a storage for cryptocurrencies or / and other NFTs. It sets unique settings for wrapped NFTs. For example, add royalties, replenish the collateral with transaction fees, or add time locks for deposited assets.

### What cryptocurrencies can be deposited inside the wrapped NFT?

It depends on the blockchain used for NFT minting. If NFT is minted on Ethereum, ETH and other ERC-20 tokens from the whitelist can be deposited. NFTs minted on BNB chain can be equipped with BNB and other BEP - 20 tokens from the whitelist. Polygon minted NFT is applicable for Matic and other Polygon tokens deposits.

### What blockchains is Envelop protocol deployed on?

Envelop protocol is deployed on:

* **Mainnets**:&#x20;
  * EVM: Ethereum, Binance Smart Chain (BNB Chain), Polygon (Matic), Harmony, Aurora, Arbitrum, OKXchain;
  * NON-EVM: WAX, Zilliqa, Near;
* **Testnets**: BSC testnet, Goerli, GateChain (testnet), OkxChain (testnet), Aurora (testnet);
* **More block chains like**: Aptos, ZkSync, are coming soon.

### Does Envelop have its own token?

Envelop emitted its token named NIFTSY. It has been launched on 4 blockchains: Ethereum, BSC, Polygon and Arbitrum.

### Can I add cryptocurrencies/tokens inside a wrapped NFT after wrappin&#x67;**?**&#x20;

Yes, you can add cryptocurrencies/tokens at any time.

### Who receives the original NFT after unwrapping?

The original NFT is received by the current owner of the wrapped NFT after it is unwrapped.

### Can the owner of a wrapped NFT withdraw tokens from the collateral?

No. All tokens, once added to the wrapped NFT, are stored at the protocol contract address. Withdrawing of these tokens is a part of unwrapping operation only.

## Product FAQ

### What happens to the original nft when it is wrapped?&#x20;

The original NFT takes possession of the Protocol contract. Instead, the owner receives the wrapped NFT.

### Can wrapped NFT be offered for sale on a marketplace?

Yes, a wrapped NFT is an ERC-721 / ERC-1155 and all methods for this standard are applicable to it.&#x20;

### What happens if the owner of the original NFT, initially, places an order to sell it and then he wraps that original NFT?&#x20;

The order will not be executed because the original NFT will belong to the Protocol contract.

### Can a buyer of a wrapped NFT see it on another NFT platform, OpenSea for example?&#x20;

Wrapped NFT is a regular ERC-721 / ERC-1155 standard. If the platform supports this standard functionality and displays all NFT including wrapped ones. OpenSea does it.

### If I see a wrapped NFT on the OpenSea platform, can I put it up for sale there?&#x20;

Yes, because it is a normal nft ERC-721 or ERC-1155.

### Does it change the metadata of the original nft when wrapped?&#x20;

No. The protocol has a tokenURI method which, for a wrapped nft, returns the result of the same method but from the original NFT.

### Can the entire collection be wrapped or just a single NFT? &#x20;

Only one NFT could be wrapped into one wrapped NFT. But non-fungible tokens could be added as a collateral into the wrapped NFT (If a user sales a wrapped NFT containing a Collateral).

### If the user sold a wrapped nft containing collateral in the form of native tokens or ERC-20, will he be able to use those tokens?&#x20;

No. For only the current holder/owner of the wrapped nft disposes of the collateral.

### Can the entire collection be wrapped or just a single NFT?&#x20;

It's the NFT token that gets wrapped (not the collection).

### What can be wrapped now? what tokens, coins?&#x20;

Any ERC-721/1155 token can be wrapped.

### User wraps the original NFT, which NFTs does he have on the balance after? &#x20;

After the wrapping, the user has only wrapped NFT on its balance.

### Who manages the white and black lists of contract addresses that can be used in the protocol contract as the supplier of the original nft, collateral, transfer fee?&#x20;

These lists are only managed by the owner of the Protocol contract (the project team).

### Does it take a long time to whitelist an ERC-20 token contract address?&#x20;

No. Technically, This action is done quickly. Another thing is to reach an agreement with the team about it.

### Why are there the functionalities of time lock, value lock, event lock and other settings available for wrapping NFT?&#x20;

\
There are needs to unlock the assets of the wrapped NFT depending on the time period and or some event occurs. Two parties agree that they "freeze" the assets in collateral of the wrapped NFT until some event occurs. Or the parties are not going to use the locked assets till the particular date.

