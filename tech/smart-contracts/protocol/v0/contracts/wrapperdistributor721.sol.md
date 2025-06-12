# WrapperDistributor721.sol

This contract inherits all methods of the **WrapperWithERC20Collateral** contract, the methods of which can be found [here](https://docs.envelop.is/tech/smart-contracts/contract-wrapperwitherc20collateral.sol). The WrapperDistributor721 contract is a separate implementation that extends the functionality of the **Protocol**. It is designed to perform bulk wrapping of NFTs and creation of wrappers without depositing the original NFT.

### WrapAndDistrib721WithMint method

![](<../../../../../.gitbook/assets/Снимок экрана 2021-12-02 в 13.54.01.png>)

Not any address can call the method. Only the one that the contract owner has assigned the distributor role to. The method checks that the number of recipients equals the number of token id of the original NFT. If all checks are met, method:&#x20;

* **Transfers** ERC-20 tokens to the WrapperDistributor721 contract address for each "address and number of ERC-20 tokens" pair specified in the provisioning array, the aggregate amount of these tokens. These tokens will be deposited into all the wrapped NFTs being created. The aggregate volume to transfer ERC-20 tokens is defined as the number of tokens from the "pair" multiplied by the number of recipients of the wrapped NFTs. It is mandatory that the contracts of the ERC-20 tokens deposited as collateral for the wrapped nfts must have permission for WrapperDistributor721 to use the tokens.&#x20;
* **Mint** on the contract of the original nft tokens according to the transferred array with the token id. The recipient of the original NFT data will be the contact WrapperDistributor721. Obligatorily the contract address WrapperDistributor721 must be assigned the mint role for the original NFT contract. Mandatory the mint method of the original nft contract must have two input parameters - the NFT recipient address and the token id with which the original NFT is to be issued.&#x20;
* **Mint** **wrapped** nft ERC-721 to each address in the recipient array&#x20;
* for each wrapped NFT the unlock date is fixed, passed to the method (in unixtime format) - the date from which the wrapped nft can be unlocked.&#x20;
* **If native network tokens are transferred** to the contract when the method is called, Collateral in native tokens is recorded for each wrapped NFT. The volume of Collateral in native tokens for this fixation is calculated as the volume of native tokens sent to the contract divided by the number of recipients of wrapped NFTs.&#x20;

The method results in the user is creating the mass-wrapped ERC-721 nfts with the provisioning in native and/or ERC-20 tokens and minting of the original ERC-721 nfts. The method also checks that if there is not enough gas to complete the transaction, an event will be created to capture how many wrapped nfts were created - to retry and create the remaining wrapped NFTs (wNFTs).&#x20;

Parameters:

| Name              | Type                   | Description                                                                                                                                         |
| ----------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_original721** | **address**            | Contract address of the original NFT ERC-721                                                                                                        |
| **\_receivers**   | **address\[]**         | An array of recipient addresses which will get the wrapped NFTs (wNFT)                                                                              |
| **\_tokenIds**    | **uint256\[]**         | Array of token id of original NFTs                                                                                                                  |
| **\_forDistrib**  | **ERC20Collateral\[]** | An array of Collateral with pairs of "ERC-20 token contract address and number of tokens" to be deposited as Collateral for each wrapped NFT (wNFT) |
| **\_unwrapAfter** | **uint256**            | Date of the unlocking wrapped NFT (wNFT)                                                                                                            |

### WrapAndDistribEmpty method

![](<../../../../../.gitbook/assets/Снимок экрана 2021-12-02 в 14.10.52.png>)

Not any address can call the method. Only the one to which the contract owner has assigned the distributor role. The method checks that the number of recipients is not greater than 256.&#x20;

If all checks are met, the method:&#x20;

* **Transfers ERC-20 tokens** to the WrapperDistributor721 contract address for each "address and number of ERC-20 tokens" pair specified in the provisioning array, the aggregate amount of these tokens. These tokens will be deposited into all the wrapped NFTs being created. The aggregate volume to transfer ERC-20 tokens is defined as the number of tokens from the "pair" multiplied by the number of recipients of the wrapped NFTs. It is mandatory that the contracts of the ERC-20 tokens deposited to secure the wrapped nfts must have permission for WrapperDistributor721 to use the tokens.&#x20;
* **Mints** a wrapped nft ERC-721 to each address in the recipient array (a **blank envelope** in which the collateral will be stored)&#x20;
* for each wrapped nft the unlock date is given to the method is recorded (in unixtime format) - the date from which the wrapped nft can be unlocked.&#x20;
* **If native tokens** are transferred to the contract when the method is called, Collateral in native tokens is recorded for each wrapped NFT. The volume of Collateral in native tokens for this fixation is calculated as the volume of native tokens sent to the contract divided by the number of recipients of wrapped NFTs.&#x20;

The method results in the user is creating the mass-wrapped ERC-721 NFTs (without creating and wrapping the original ERC-721 NFTs) with the provisioning in native and/or ERC-20 tokens. The method also checks that if there is not enough gas to complete the transaction, an event will be created to capture how many wrapped NFTs were created - to retry and create the remaining wrapped NFTs.

Parameters:

| Name              | Type                   | Description                                                                                                                                         |
| ----------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_receivers**   | **address\[]**         | An array of recipient addresses wrapped NFTs                                                                                                        |
| **\_forDistrib**  | **ERC20Collateral\[]** | An array of collateral with pairs of "ERC-20 token contract address and number of tokens" to be deposited as collateral for each wrapped NFT (wNFT) |
| **\_unwrapAfter** | **uint256**            | Date of the unlocking wrapped NFT (wNFT)                                                                                                            |
