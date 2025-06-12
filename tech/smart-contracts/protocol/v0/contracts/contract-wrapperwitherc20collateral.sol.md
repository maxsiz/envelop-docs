# WrapperWithERC20Collateral (V.0)

### Method wrap721

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 08.40.29.png>)

Creates a wrap NFT for an **ERC-721** NFT with **Collateral**. If the contract owner has blacklisted the contract address of the original ERC-721 token, it will not be possible to create a wrap NFT.

Only the owner of the original NFT can wrap it. To do so, the owner of the original NFT must give permission for the **WrapperWithERC20Collateral** contract to use it.

**The originator of a wrapped NFT may set a fee that any sender of its wrapped NFT will pay on transfer. The fee must not exceed the limit set by the WrapperWithERC20Collateral (default is 100%).**

If the **Creator** of a wrapped NFT (**wNFT**) has set the amount of commission for the transfer, it can also define a share of that commission and the address where that share will be transferred to during any transfer of a wrapped NFT. In this way a simple **Royalty** mechanism is implemented. The remainder of the transfer commission is accumulated at the WrapperWithERC20Collateral contract address before wNFT is unwrapped.

In addition, the creator of a wNFT can set the total amount of commission to be accumulated during NFT transfers so that the current owner of that NFT can deploy it and thereby receive: accumulated Collateral tokens, accumulated transfer commission tokens, accumulated native tokens from the blockchain itself, the original NFT itself. The value of the accumulated commission cannot be greater than the value set by the owner of the WrapperWithERC20Collateral contract.

The creator of the wrapped NFT can also set a date in **Unix-time format** after which the NFT can be unwrapped.

The Creator of the wrapped NFT can pass the ERC-20 token address to the method where the transfer fee will be charged. This address **must** **be** **whitelisted** by the contract owner in advance. If the creator has not given the method the ERC-20 address of the token to be charged for the transfer, the transfer of the wrapped NFT will accrue and accumulate technical project tokens for the creator and the last owner of the wrapped NFT.

The WrapperWithERC20Collateral contract holder can set up commissions for wrapping the original NFT. The commission is charged in ERC-20 tokens. The creator must have a certain amount of ERC-20 tokens in the contract balance to pay the conversion fee. In addition, the creator of the wrapped NFT must give the WrapperWithERC20Collateral contract permission to use its ERC-20 tokens to pay the turnover fee.

If all conditions for wrapping are met, the method creates a wrapped NFT of the ERC-721 standard. The owner of the original NFT becomes the WrapperWithERC20Collateral contract.

The method creates a Wrapped event with the contract address of the original NFT, id of the original NFT, id of the wrapped NFT.

When the method is called, it is possible to send a native blockchain token that will be accounted in the provision of the original NFT.

**Method returns id of wrapped NFT of ERC-721 standard**.

**Parameters:**

| Name                      | Type    | **Description**                                                                                                      |
| ------------------------- | ------- | -------------------------------------------------------------------------------------------------------------------- |
| **\_underlineContract**   | address | Contract address of the original NFT                                                                                 |
| **\_tokenId**             | uint256 | ID of the original NFT                                                                                               |
| **\_unwrapAfter**         | uint256 | Date after which the NFT can be deployed                                                                             |
| **\_transferFee**         | uint256 | Amount of transfer fee for wrapped NFT                                                                               |
| **\_royaltyBeneficiary**  | address | Address for receiving a share of the transfer fee by the creator of the wrapped NFT                                  |
| **\_royaltyPercent**      | uint256 | Share of transfer fee of the creator of a wrapped NFT; integer, no decimals                                          |
| **\_unwraptFeeThreshold** | uint256 | The total transfer fee of the wrapped NFT that needs to be accumulated in order to be able to deploy the NFT         |
| **\_transferFeeToken**    | address | The address of the ERC-20 token contract where the transfer fee of the wrapped NFT is charged. Can be a null address |

Returns values:

| Name                 | Type    | **Description**             |
| -------------------- | ------- | --------------------------- |
| **lastWrappedNFTId** | uint256 | ID ERC721 token wrapped NFT |

### Method AddNativeCollateral&#x20;

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 08.58.48.png>)

The sender of the transaction invoking this contract method sends native contract blockchain tokens to the WrapperWithERC20Collateral contract address. To invoke the method, an existing ERC-721 wrapped NFT id must be sent. The method for the wrapped NFT increases the collateral in the native contract blockchain tokens.

**Parameters**:

| Name                 | Type    | Description           |
| -------------------- | ------- | --------------------- |
| **\_wrappedTokenId** | uint256 | ID of the wrapped NFT |

### Method **unWrap721**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 09.01.05.png>)

Method performs deployment of wrapped NFT of ERC-721 standard. Only current owner can call method for id of wrapped NFT.

There are a number of conditions that must be met for method call to be successful:&#x20;

* A time has arrived after which the wrapped NFT can be deployed - if the creator of the wrapped NFT has defined this time. Time in unixtime format.&#x20;
* Accumulated during transfers of the wrapped NFT to the ERC-721 standard - enough ERC-20 tokens. During the wrapping of the original NFT the creator of the wrapped NFT has specified the amount to be accumulated.

If all conditions are met, the method:

* Makes a transfer of all ERC-20 provisioning tokens of the wrapped NFT to the address from which the method is called. Either in one method call or in several.&#x20;
* Burns the wrapped NFT of the ERC-721 standard and translates the original NFT of the same standard to the address the method is called from.&#x20;
* Translates the native blockchain tokens of the contract to the address from which the method call is made, if any are accumulated for the wrapped NFT.&#x20;
* Makes a transfer of accumulated ERC-20 tokens of the wrapped NFT transaction fee to the address from which the method call is made, if any are accumulated for the wrapped NFT.&#x20;
* Creates an UnWrapped event with the id of the wrapped NFT, the address that called the method, the amounts of accumulated native blockchain tokens and ERC-20 transfer fee tokens for the original NFT.

The method returns nothing in response.

**Parameters:**

| **Name**      | Type        | Description           |
| ------------- | ----------- | --------------------- |
| **\_tokenId** | **uint256** | ID of the wrapped NFT |

### Method **tokenURI**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 09.03.38.png>)

The method returns the metadata of the original NFT standard ERC-721.

**Parameters:**

| Name          | Type        | Description           |
| ------------- | ----------- | --------------------- |
| **\_tokenId** | **uint256** | ID of the wrapped NFT |

**Returns values:**

| Name          | Type       | Description                  |
| ------------- | ---------- | ---------------------------- |
| **meta data** | **string** | Metadata of the original NFT |

### Method **getTokenValue**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 09.07.35.png>)

The method returns the amounts of accumulated native contract blockchain tokens and ERC-20 commission tokens during transfers for wrapped NFT.

**Parameters:**

| **Name**      | Type    | Description           |
| ------------- | ------- | --------------------- |
| **\_tokenId** | uint256 | ID of the wrapped NFT |

**Returns values:**

| **Name**         | Type    | Description                                                                 |
| ---------------- | ------- | --------------------------------------------------------------------------- |
| **backedValue**  | uint256 | Sum of accumulated native contract blockchain tokens for wrapped NFT        |
| **backedTokens** | uint256 | Amount of ERC-20 commission tokens accumulated during NFT wrapped transfers |

### Method **getWrappedToken**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 10.59.44.png>)

The method returns all wrapped NFT data of the ERC-721 standard.

**Parameters:**

| **Name**      | Type    | Description           |
| ------------- | ------- | --------------------- |
| **\_tokenId** | uint256 | ID of the wrapped NFT |

**Returns values:**

| **Name**                | Type       | Description                                                                                                          |
| ----------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------- |
| **tokenContract**       | address    | Address of the original NFT contract                                                                                 |
| **tokenId**             | uint256    | ID of the original NFT                                                                                               |
| **backedValue**         | uint256    | Sum of accumulated native contract blockchain tokens for wrapped NFT                                                 |
| **unwrapAfter**         | uint256    | The date after which the NFT can be deployed. Unixtime format                                                        |
| **transferFee**         | uint256    | Amount of transfer fee for wrapped NFT                                                                               |
| **royaltyBeneficiary**  | address    | Address for receiving a share of the transfer fee by the creator of the wrapped NFT                                  |
| **royaltyPercent**      | uint256    | Share of transfer fee of the creator of the wrapped NFT                                                              |
| **unwraptFeeThreshold** | uint256    | The total transfer fee of the wrapped NFT that needs to be accumulated in order to be able to deploy the NFT         |
| **transferFeeToken**    | address    | The address of the ERC-20 token contract where the transfer fee of the wrapped NFT is charged. Can be a null address |
| **asset**               | enum.value | Asset type number - including ERC standard token                                                                     |
| **balance**             | uint256    | Wrapped balance for ERC-1155                                                                                         |

### Method **addERC20Collateral**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 11.11.43.png>)

The method adds collateral in the form of ERC-20 tokens to the wrapped NFT.

There are a number of conditions that can be met to successfully complete a method call:&#x20;

* The method is passed the existing id of the wrapped NFT created by the contract; the contract address of the ERC-20 tokens contract has been added by the contract owner to the whitelist;&#x20;
* The address from which the method is called has enough ERC-20 tokens to add them to the provision of the wrapped NFT;&#x20;
* The sender of the transaction has given the WrapperWithERC20Collateral contract address permission to use its ERC-20 tokens in sufficient quantity.

If all conditions are met, the method: Creates an entry in the ERC-20 token collateral register of the wrapped NFT: the contract address of the ERC-20 token and the amount of tokens; makes a transfer of ERC-20 tokens to the WrapperWithERC20Collateral contract address from the sender address of the transaction.

If someone has previously deposited the same ERC-20 tokens into the collateral of the wrapped NFT, the method does not create a new entry in the registry, but increases the number of tokens deposited.

There is a limit set by the WrapperWithERC20Collateral contract holder on the number of ERC-20 token types contributed to the wrapped NFT provision. If the number is exceeded when the method is called, the method will fail (an error message is issued).

The method returns nothing in response.

**Parameters:**

| **Name**             | Type    | Description                                                                                                        |
| -------------------- | ------- | ------------------------------------------------------------------------------------------------------------------ |
| **\_wrappedTokenId** | uint256 | ID of the wrapped NFT                                                                                              |
| **\_erc20**          | address | ERC-20 token contract address                                                                                      |
| **\_amount**         | uint256 | Number of tokens that are transferred to the WrapperWithERC20Collateral contract address to secure the wrapped NFT |

### Method **getERC20Collateral**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 11.15.06.png>)

The method returns information about all ERC-20 tokens added to the wrapped NFT collateral. The data is returned as an array of collateral registry entries.

**Parameters:**

| **Name**        | Type    | Description           |
| --------------- | ------- | --------------------- |
| **\_wrappedId** | uint256 | ID of the wrapped NFT |

**Returns values:**

| **Name**       | Type    | Description                                                                                                                         |
| -------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **erc20Token** | address | ERC-20 token contract address                                                                                                       |
| **amount**     | uint256 | The number of ERC-20 tokens that have been transferred to the WrapperWithERC20Collateral contract address to secure the wrapped NFT |

### Method **getERC20CollateralBalance**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 11.21.03.png>)

The method returns the number of ERC-20 tokens of a particular kind transferred to the wrapped NFT provision.

**Parameters:**

| **Name**        | Type    | Description                   |
| --------------- | ------- | ----------------------------- |
| **\_wrappedId** | uint256 | ID of the wrapped NFT         |
| **\_erc20**     | address | ERC-20 token contract address |

**Returns values:**

| Name       | Type    | Description                                                                                               |
| ---------- | ------- | --------------------------------------------------------------------------------------------------------- |
| **amount** | uint256 | Number of ERC-20 tokens sent to the WrapperWithERC20Collateral contract address to secure the wrapped NFT |

### Method **enabledForCollateral**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-08-30 в 11.24.42.png>)

The method checks whether the ERC-20 token contract address is on the whitelist for entry into the wrapped NFT collateral, used to pay the wrapped NFT transfer fee and returns true or false.

**Parameters:**

| **Name**    | Type    | Description                   |
| ----------- | ------- | ----------------------------- |
| **\_erc20** | address | ERC-20 token contract address |

**Returns values:**

| **Name**   | Type | Description                                                                                             |
| ---------- | ---- | ------------------------------------------------------------------------------------------------------- |
| **result** | bool | Result of check if ERC-20 token contract address is blacklisted for enrolment in wrapped NFT collateral |

