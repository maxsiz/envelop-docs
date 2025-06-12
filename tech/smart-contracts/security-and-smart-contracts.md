---
description: general provisions
---

# Security and smart contracts

We have tried to protect users of the **Protocol** from malicious contracts whose tokens can be used in **Collateral** or to withhold transfer fees by whitelisting - a list of contract addresses from which we accept tokens for Collateral or transfer fees.

The protocol also has a **blacklist** of the addresses of the original nft contracts that cannot be used for wrapping. But this list is replenished post facto when a precedent has happened. Theoretically it can happen now that some intruder creates his own NFTs, wraps it in our Protocol and during the unwrapping there will be some obstacles for it - prohibiting to translate the original NFTs from our contract address to the address of the final owner. This can happen. The buyer of the wrapped NFTs needs to evaluate the code of the original nft for such malicious methods. Probably such an evaluation can be done by a team, e.g. by means of an **Oracle**. But this is still an open question.

For the Collateral we have a check when check a **wrapped** NFTs - if the Collateral contract prevents the transfer of ERC-20 tokens from our contract address (the collateral is stored there) to the address of the wrapped NFTs unfolder, we simply skip such ERC-20 tokens and do not try to send them to the deployer, move on to the next ERC-20 (other contracts) which provide the wrapped NFTs.

Only the owner of the protocol contract can manage the **whitelist** and blacklist. No one else can make or change entries in these lists. This functionality is provided by the embedded EVM logic and token standards.
