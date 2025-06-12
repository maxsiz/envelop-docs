---
description: >-
  Whitehack2earn (h2e). Use your skills for the good of web3. Make the world a
  better and get profit.
---

# Bug Bounty

\*\*\*

## **Reporting** [form](https://docs.google.com/forms/d/e/1FAIpQLSdD6XFJsbRfPNUf79qczjuc44NnhPl2Tv_c9HViJ_RsQ09iFw/viewform).&#x20;

\*\*\*

Already **780,000 NIFTSY** tokens have been paid out for bugs found

\*\*\*

Tested directions of the applications:

* operation of each implemented functionality
* interaction with crypto wallets
* dAapps interaction with backend

**Prerequisites:**&#x20;

* testing and troubleshooting to perform in Chrome, Firefox browsers?
* Metamask transaction wallet

**List of applications to search for bugs:**

* [https://appv1.envelop.is/list](https://appv1.envelop.is/list)
* [https://appv1.envelop.is/mint/](https://appv1.envelop.is/mint/)
* [https://appv1.envelop.is/saft](https://appv1.envelop.is/saft)

\*\*\*

**Frontend levels of bug severity:**

* **Blocker** (S1). Such an error makes it impossible to proceed with using or testing the software. There aren't any ways to work around it.
* **Critical** (S2). It is an incorrect functioning of a particular area of business-critical software functionality. There is an alternative way to work around it.
* **Major** (S3). An error has a significant impact on an application, but other inputs and parts of the system remain functional, so you can still use it. At the same time, there is more than one entry point to initiate the desired functionality
* **Minor** (S4). A defect is confusing or causes undesirable behavior but doesn’t affect user experience significantly. Many UI/UX bugs belong here.&#x20;
* **Low**/**Trivial** (S5). A bug doesn’t affect the functionality or isn’t evident. It can be a problem with third-party apps, grammar or spelling mistakes, etc.

\
\*\*\*

| Level | Rewards (wNFT with NIFTSY as collateral ) | Time-lock (Weeks) |
| ----- | ----------------------------------------- | ----------------- |
| S1    | 150 000                                   | 40                |
| S2    | 50 000                                    | 20                |
| S3    | 20 000                                    | 10                |
| S4    | 7 000                                     | 4                 |
| S5    | 2 000                                     | 2                 |

\*\*\*

At Envelop, we classify bugs on a widely used scale. For version 1 of the protocol, we identify the following directions of attack:

**Critical**&#x20;

* Blocking to user unwrapping of wNFT and getting collateral
* User\`s funds losing during wrapping or adding collateral
* Withdrawing tokens of collateral without unwrapping of own or someone else's wNFT
* Withdrawing original NFT without unwrapping of own or someone else's wNFT
* Getting collateral tokens during unwrapping of wNFT more than was added in it
* Increasing amount of collateral tokens in accounting registers of smart contracts
* Decreasing amount of collateral tokens in accounting registers of smart contracts
* Changing owner of smart contracts
* Withdrawing native tokens from smart contracts addresses of protocol
* Withdrawing ERC20 tokens from smart contracts addresses of protocol
* Withdrawing ERC721 or ERC1155 tokens from smart contracts addresses of protocol

**High**

* Unauthorized Adding address of smart contract in whiteList
* Unauthorized Adding address of smart contract in blackList

**Medium**

* Unbounded gas consumption
* Increasing of gas consumption with every next operation
* Blocking possibility to wrap NFT
* Blocking possibility to add collateral to wNFT

**Low**

* Creation of conditions to get-methods return wrong data

<table><thead><tr><th>Level</th><th>Rewards, wNFT with NIFTSY as collateral</th><th>Time-lock, week</th><th data-hidden></th></tr></thead><tbody><tr><td>Critical</td><td>1 000 000</td><td>40</td><td></td></tr><tr><td>High</td><td>400 000</td><td>20</td><td></td></tr><tr><td>Medium</td><td>100 000</td><td>10</td><td></td></tr><tr><td>Low</td><td>25 000</td><td>4</td><td></td></tr></tbody></table>
