# ERC20 tokens trading

### The prologue

Envelop launchpad allows the owners to trade ERC20 tokens. The mechanics of the sale are as follows: the showcase owner creates wrapped NFTs. They add in the collateral of them the tradable ERC20 tokens. Then place wrapped NFTs to the showcases, put the prices. The buyers purchase wrapped NFTs and unwrap them to get ERC20 tokens from the collateral.

We will show how to use Envelop launchpad for the ERC20 tokens trading in this guide.  We will use Google Chrome Browser, Metamask browser extension, Sepolia testnet for the demoing. To start to use the dapp user should connect to it by your wallet.

### The showcase creating&#x20;

**Step 0**. Open [https://app.envelop.is/launchpad\_admin](https://app.envelop.is/launchpad_admin)

**Step 1.** Connect wallet

<figure><img src="../../../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

**Step 2.** Choose Metamask

<figure><img src="../../../../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

**Step 3.** Choose an account in the wallet

<figure><img src="../../../../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

**Step 4**. Confirm the allowance for dapp to use the account

<figure><img src="../../../../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

**Step 5.** Before the using of the launchpad we should create showcase where buyers will be able to buy your ERC20 tokens.

Press create button

<figure><img src="../../../../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

**Step 6.** Fill in all fields of the form. Be carefull with the title and life time. The first one is the unique part of the link that buyers will enter in a browser to visit your showcase (the example of the finish showcase url: [https://app.envelop.is/launchpad/11155111/0x379bf612a830413c6a08d2732b6afd491a12955b/showcase-wNFT](https://app.envelop.is/launchpad/11155111/0x379bf612a830413c6a08d2732b6afd491a12955b/showcase-wNFT)). The second one is responsible for the start and finish time of the sale.

<figure><img src="../../../../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

**Step 7.** Press Save button

**Step 8.** Sign the transaction in the crypto wallet.

<figure><img src="../../../../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

**Step 9.** Sign the message in the crypto wallet.

<figure><img src="../../../../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

We have created the own showcase

### The showcase editing

**Step 0.** Only owner can change the showcase settings. Go to the step Showcase. Edit the data in all fields of the forms.&#x20;

<figure><img src="../../../../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

**Step 1.** Press save button

**Step 2.** Sign the transaction in the wallet

**Step 3.** Sign the message in the crypto wallet for the envelop oracle.

### **The default price putting**

**Step 0.** Envelop launchpad allows the owners to put the prices for tradable ERC20 tokens.

There are two ways of the price putting. The first way is the default price putting using step three. The owner puts how many tokens one unit of ERC20 tokens will cost and which tokens the buyers will be able to use to pay.

**Pay attention!** This way allows to put the price only for wrapped NFTs with one tradable ERC20 token in collateral. For example the owner want to trade only Niftsy tokens via wrapped NFTs. He can add in the collateral other ERC20 tokens except for Niftsy. But they will not be factored in the final price of wrapped NFTs. The tradable ERC20 tokens for this way should be placed the first in the collateral. Remember about it when you will create wrapped NFT with the collateral.

The final price of wrapped NFT is calculated as the multiplying the number of tradable tokens in its collateral by the price per the unit of tradable token.

The prices can be in native or ERC20 tokens. The showcase can have several prices per the unit of the tradable token. For example the buyers will be able to buy wrapped NFT per different stable coins if owner puts several prices in the stable coins per the unit of the tradable tokens placed in its collateral.

**Step 1**. Put the several prices. Choose the tradable token from the list or fill in its smart contract address.

<figure><img src="../../../../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

**Step 2.** Choose the price token from the list and enter amount per the unit of tradable ERC20 token. Don't forget to press Add button for every price.

<figure><img src="../../../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

**Step 3.** To save changes in the blockchain press Save button.

<figure><img src="../../../../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

**Step 4.** Sign the transaction in the wallet

**Step 5.** Check our changes on Price tab. They are applied.

### The time discount putting

**Step 0**. Envelop launchpad allows an owners to put time discounts. Owner can put the several time period with the different values of the discounts

Set the several time discounts. Enter an amount and choose the date for which the discount value is valid . Don't forget press Add button for every discount line.

<figure><img src="../../../../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

**Step 1.** Press Save button

<figure><img src="../../../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

**Step 2**. Sign the transaction in the wallet

**Step 3.** Check our changes on Discount tab. They are applied

### The wrapped NFTs placing on the showcase

**Step 0.** The next step is the placing the wrapped NFTs on the showcase. Only showcase owner have the permissions to do it.

Select the wrapped NFTs which we want to sell on the showcase.&#x20;

<figure><img src="../../../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

The dAPP gives the possibility to select the wrapped NFTs by the collateral tokens.&#x20;

<figure><img src="../../../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

The owner can see which tokens were added in the wrapped NFT.

<figure><img src="../../../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

&#x20;The owner can pick the several wrapped NFTs by using the range of the token ids and the smart contract address.

<figure><img src="../../../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

The owner can add the wrapped NFTs on the showcase by the batches with the different settings. Make it created two batches.

<figure><img src="../../../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

**Step 1.** Put the individual prices for the wrapped NFTs of the second batch. It is the second way of the price putting. The owner puts the final prices for the wrapped NFTs generally. This way is fit in case when the owner created the index based on wrapped NFT technology with the several collateral tokens inside it. The owner can create the different collections of tradable ERC20 tokens via the wrapped NFTs and put for them the individual prices.

<figure><img src="../../../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

**Step 2.** Don't forget to press Save price button

<figure><img src="../../../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

**Step 3.** Press save button

<figure><img src="../../../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

**Step 4.** Sign the approve transaction in the wallet the smart contract of launchpad can use the owner's wrapped NFTs

**Step 5.** Sign the transactions of the placing wrapped NFTs on the showcase in the wallet. The owner should sign two transactions because he has collected two the wrapped NFT batches for the placing.

**Step 6.** After that the owner's wrapped NFTs are placed on the showcase.

<figure><img src="../../../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

### The editing of the prices

**Step 0.** The owner can edit the prices for any time. Edit the default prices put for whole showcase on Price tab.

<figure><img src="../../../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

**Step 1.** Don't forget to press Save button for every price that is changed.

<figure><img src="../../../../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

**Step 2.** Press save button.

<figure><img src="../../../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

**Step 3.** Sign the transactions in the wallet.

**Step 4.** Check the changes on the showcase.

**Step 5.** Pay attention! The owner can change prices for any wrapped NFT that has only the default prices to the individual prices. Go to NFTs tab.

<figure><img src="../../../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

**Step 6.** Add the individual prices for the wrapped NFT. Don't forget to press Add and Save buttons

<figure><img src="../../../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

**Step 7.** Press save button

<figure><img src="../../../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

**Step 8.** Sign the transactions in the wallet

**Step 9.** Check the changes on the showcase.

<figure><img src="../../../../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

Now the wrapped NFT has individual prices.

### The deleting of the prices

**Step 0.** Envelop launchpad has the functional of the prices deleting. Try to do it with the common for whole showcase prices on Price tab.

Delete the several prices and save the changes.

<figure><img src="../../../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

**Step 1.** Press save button.

<figure><img src="../../../../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

**Step 2.** Sign the transaction of the deleting in the wallet.

**Step 3.** Check our changes. They are applied

<figure><img src="../../../../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

**Step 4.** The owner can delete the individual prices of one wrapped NFT per an operation on NFTs tab.

<figure><img src="../../../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Try to do it for one wrapped NFT.

<figure><img src="../../../../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

**Step 5.** Press Save price button

<figure><img src="../../../../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

**Step 6.** Press Save button

<figure><img src="../../../../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

**Step 7.** Sign the transaction of the deleting in the wallet.

**Step 8.** Check our changes. They are applied

<figure><img src="../../../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

### The checking of the tuning result

Now we have tuned all needed parametrs for the working of showcase before the start of the sale.

Go to the showcase to check how the showcase will look like for the buyers.

<figure><img src="../../../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

That's all. Now your tradable ERC20 tokens are on the showcase and can be bought by your contributors. Thanks for your attention!

<figure><img src="../../../../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>
