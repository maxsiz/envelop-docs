# Envelop dApps Troubleshooting

DAO Envelop uses third-party web3 tools and libraries to develop its dApps. These tools may have their limitations, bugs affecting the performance of Envelop dApps.

This article describes some of the typical problems a user may encounter and how to resolve them.

Predominantly, testing of DAO Evnelop dApps is done in the Chrome browser with the Metamask extension. Therefore, technical references will be made to these two applications. However, the user can always find information on the web how to perform this or that action described in this document in his browser and his wallet.

**You can contact our dev team at Telegram chat** [**https://t.me/envelop\_en**](https://t.me/envelop_en)

***

1. **There was an error with the selected network RPC.**

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

This error often occurs when the RPC used in your wallet to communicate with a particular network has returned an error, such as “Too Many Requests”.

To change the RPC for a network in your wallet, use the list of networks at [https://chainlist.org/](https://chainlist.org/).

For MetaMask, you can change the RPC URL here: chrome-extension://nkbihfbeogaeaoehlefnkodbefgpgknn/home.html#settings/networks

2. **The NFT or wNFT metadata is not displayed on the** [**https://app.envelop.is/list**](https://app.envelop.is/list) **dashboard (no picture is displayed).**

This problem can be solved in the following way:

* check that your browser is the latest version. Update your browser if necessary.
* enable VPN (virtual private network) and try again
* check your browser settings and disable ad blocker.
* open the console of your browser (in Chrome, push F12 or select Inspect-Console from the context menu). It may have these errors in it.

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

This means that the hosting that hosts the metadata forbids displaying metadata anywhere other than applications hosted on its domain. In this case, there is no way to fix the problem until the host changes its content access policy.

3. **Network connection error**

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

You can solve this problem by enabling vpn, because your local Internet provider is blocking connection to the RPC URL specified in the network settings.

4. **Earlier you connected to Envelop dApps with your wallet and sent transactions through it, but now the connection to the wallet is not happening. There is a popup with an attempt to log in to the wallet on the screen.**

In this case, you can try to do the following:

* Reload the dApp page
* Log out and log in again with Metamask. Reload the page again
* Revoke approve for connection to the dApp in the wallet. Refresh the page again. Log in to the dApp and approve connection in Metamask.

5. **When a transaction is sent from a dApp, an RPC error occurs with a message that the transaction has been reverted.**

In this case, the reverted message will contain the reason why the transaction will be reverted by the network. You can fix the reason for the revert.

If you have made all the settings in dApp correctly, but the transaction is still reverted, you need to contact the support via chat [**https://t.me/envelop\_en**](https://t.me/envelop_en). In your message, send a screenshot of your browser console (in Chrome, push F12 or select Inspect-Console from the context menu).

6. **When sending a transaction, an RPC error message appears with no reason given.**

Try these steps:

* Enable vpn and try again
* Use a different RPC for your network. To change the RPC in your wallet , use the list of networks at [https://chainlist.org/](https://chainlist.org/). For Metamask, you can change the RPC URL here: chrome-extension://nkbihfbeogaeaoehlefnkodbefgpgknn/home.html#settings/networks
* Contact the support via chat [**https://t.me/envelop\_en**](https://t.me/envelop_en). In your message, send a screenshot of your browser console (in Chrome, push F12 or select Inspect-Console from the context menu).

7. **You don’t see your NFT or wNFT on the dashboard (**[**https://app.envelop.is/list**](https://app.envelop.is/list)**)**

The dashboard interacts with an oracle developed by DAO Envelop. The oracle takes time to receive and process data from the blockchain. If 15 minutes have passed after creating an NFT or wNFT and it does not appear on the dashboard (don’t forget to reload the page), then contact support in chat via chat [**https://t.me/envelop\_en**](https://t.me/envelop_en). In your request, provide a link to the transaction.

8. **Transaction is confirmed in the wallet, but the dApp shows a popup with RPC error**

This happens, especially with Polygon network. In this case, RPC returned an incorrect response, although the transaction was confirmed by the network. DAO Envelop cannot affect RPC in this case. So close the popup and check the dashboard ([https://app.envelop.is/list](https://app.envelop.is/list)) for changes (created NFT/wNFT, added collateral, no NFT if it was deployed, no NFT if it was sent to another address, etc).

9. **The red warning screen from google that this dApp is dangerous to use**

This happens because your wallet address has an NFT that has a link to a phishing site in its metadata. dApp replicates the metadata and shows it to users. In this case you need to:

* make a forced visit to the page
* contact the support in any convenient way and specify in your message which site google warned you about (e.g. circleevent.xyz).

The dev team will blacklist this site so that NFTs with metadata referring to the dangerous site will no longer be displayed in Envelop’s dApps.

10. **The Envelop dApp tries to send a transaction via browser extention Metamask but Metamask does not open the window with an offer to sign it**

This happens sometimes because extention is crashed. In this case you need to:

* open **chrome://extensions/**
* reload browser extention Metamask
* log out and log in to the dApp and approve connection in Metamask.&#x20;
* run the operation in dApp again
* if it does not work contact the support via chat [**https://t.me/envelop\_en**](https://t.me/envelop_en)

11. **The amount of gas which user needs to set in wallet**

The dev team recommends to set market level value of gas fee in wallet, for Polygon to set aggressive level value. It helps to the fast confirmation of a transaction and decreases the probability of the suspending.
