---
description: Step by step guide
---

# Instruction

#### Subscription workflow and conditions

1. Supported chain for SAFT wNFT: Ethereum, BNB Smart Chain, Polygon
2. Anyone is able to use SAFT wNFT: project or VC representative, OTC dealer, KOL, common user and etc.
3. To proceed the subscription 200’000 NIFTSY tokens are required to be held on the your wallet by which user will form SAFT wNFTs.
4. The subscription involves wrapping and send back to the user wNFT with 200’000 NIFTSY with time lock on 12 month and subscription period 1 month.
5. Only owner/wrapper of wNFT (with 200’000 NIFTSY tokens inside) will be able to make wrapping.
6. After subscription done the user will be able to wrap ANY ERC/BEP-20 tokens from his wallet with vesting periods (time-locks). Also, multi-collateral formation is available — the user can form his unique secured index.
7. The owner is free to choose: hodl wNFT for 12 months and then unwrap it to get NIFTSY tokens back or to sell it on any NFT marketplace including SCOTCH (special wNFT marketplace) or to distribute it via any OTC deal.

{% hint style="success" %}
**We are constantly working to improve the user interface of the dApp, so the screenshots may be a bit different from what you see in your browser**
{% endhint %}

\
**Requirements:**&#x20;

1. You will need a Metamask or a Walletconnect
2. To set up a Metamask Wallet for different chains, please follow our instructions [https://docs.envelop.is/tutorials/metamask-settings-for-different-networks](https://docs.envelop.is/tutorials/metamask-settings-for-different-networks)
3. 200 000 NIFTSY with time lock for 12 months to get SAFT access for 1 month .

**Step-by-step**

Page for creating multiple wNFT ERC721: [https://app.envelop.is/#/saft](https://app.envelop.is/#/saft).&#x20;

The page works in two modes:&#x20;

* Wrap a empty and create a wNFT ERC721 with it;
* Create the original NFT ERC721 and wrap it in wNFT ERC721.

Both modes allow you to add collateral when creating wNFT in the form of native or ERC20 tokens. Both modes allow you to define a time before which wNFT cannot be unwrapped.

Read more about how each mode works.&#x20;

**Wrap a empty and create a wNFT with it.**

![](<../../../../.gitbook/assets/Снимок экрана 2022-03-17 в 11.27.53.png>)

User:&#x20;

* includes the Empty flag;
* specifies a list of recipient addresses who will get wrapped NFTs;&#x20;
* specifies list of Collateral tokens;
* clicks Wrap Batch;
* confirms in the metamask of the approve transaction to use collateral tokens and wrap.

**Create the original NFTs and wrap them in wNFTs**.

![](<../../../../.gitbook/assets/Снимок экрана 2022-03-17 в 11.29.48.png>)

User:

* specifies the contract address of the original NFTs;
* specifies a list of recipient addresses of wrapped NFTs with the tokenId of the original NFTs to be created;
* specifies a list of collateral tokens;
* clicks Wrap Batch;
* confirms in the metamask of the approve transaction to use the collateral tokens and the wrap.

**Important**: The contract of the original NFT must contain a mint method of the following form

![](<../../../../.gitbook/assets/Снимок экрана 2022-03-17 в 11.30.57.png>)

If the mint method of the original NFT contract cannot call any address, but only those to which the owner has assigned a special status (e.g. minter), this status must be assigned to the WrapperDistributor721 contract whose method is called after pressing Wrap Batch. A list of WrapperDistributor721 contract addresses in different networks can be found at https://docs.envelop.is/tech/smart-contracts/deployment-addresses&#x20;

Also, it is important to understand that it is not possible to specify the tokenId of the original NFT which has already been created. Either specify the same tokenId for the same recipient multiple times or multiple recipients. When calling the WrapperDistributor721 contract method in such conditions, an error will occur, the transaction will be reverted by the network.

**The features of working with wNFT mass creation technology**.

Only addresses that are assigned the distributor role can call WrapperDistributor721 contract methods. Only the Envelop project team can assign such a role.

A user can specify the amount of native tokens to be used to add to the collateral of created wNFTs. The specified amount is divided equally between all created wNFTs.

The user can specify the number of ERC20 tokens to be used to add to the collateral of the created wNFTs. The specified amount is added to each created wNFT. The user must have a sufficient balance of ERC20 tokens on his balance.&#x20;

Authorization on the mass wrapping page is done using MetaMask wallet or Walletconnect protocol.

**Loading files**.&#x20;

The recipient list and tokenId of the original NFTs can be uploaded from a csv file.

![](<../../../../.gitbook/assets/Снимок экрана 2022-03-17 в 11.31.59.png>)

The file specifies the destination address and tokenId, separated by semicolons. If the wrapping of a empty is intended, the tokenId does not need to be specified.

The list of collateral tokens can be uploaded from a csv file.

![](<../../../../.gitbook/assets/Снимок экрана 2022-03-17 в 11.32.41.png>)

The file specifies the token address and quantity, separated by semicolons. If user wants to add native tokens for created wNFTs, user has to specify zero address and total number of native tokens (which will be divided among all wNFTs). The fractional part of the number is separated by a dot. If the user wants to add ERC20 tokens for the created wNFTs, they need to specify the contact address of the token and the number of ERC20 tokens to be added to each created wNFT. The quantity is specified in integers only.

A guideline for the number to wrap at a time:&#x20;

* BSC network - 50-70 wNFT;
* Polygon network - 40 wNFT.

After creating a wNFT, the recipient can continue to work with it at [https://app.envelop.is/](https://app.envelop.is/) or can trade your wNFT on OTC marketplace [https://scotch.sale](https://scotch.sale).
