# WrapperFarming.sol

### General mechanics

The contract inherits the methods of the WrapperWithERC20Collateral.sol contract. Its description can be found [here](https://docs.envelop.is/tech/smart-contracts/contract-wrapperwitherc20collateral.sol). Inheritance means that the WrapperFarming contract has methods similar to those of the WrapperWithERC20Collateral.sol contract. The main function of the contract is to provide farming, a reward for locking ERC-20 tokens on the farming contract. In order to participate in farming, the user needs to deposit their ERC-20 tokens into the farming contract.&#x20;

The deposit of tokens is done through a wraparound mechanism - by creating a special container - an ERC-721 token with collateral in the form of ERC-20 tokens sent to the farming contract. The user deposits their assets (ERC-20 tokens) into the collateral of such an ERC-721 token for a specified period of time. The user cannot withdraw (unwrap the ERC-721 token) before this period of time. The user receives a reward in the form of such ERC-20 tokens like in the collateral. The reward is added to the collateral of the ERC-721 token.&#x20;

After receiving the reward for holding ERC-20 tokens on the farming contract, the user can unwrap the ERC-721 token - receive the ERC-20 tokens held on the farming contract and the reward in the same. A significant role in farming is played by the farming settings - for which periods for which types of tokens the user can transfer their ERC-20 tokens to the farming contract and what % on the frozen amount will be credited to them. Not all ERC-20 tokens can be used for farming. Only those tokens, for which contract address the owner of the farming contract has made settings of periods and % reward.&#x20;

### Important note

The user can send any ERC-20 tokens to the farming. But the reward will be credited and paid only for those types of ERC-20 tokens for which the owner of the farming contract has made farming periods and % reward settings.

### **Method WrapForFarming**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-12-02 в 15.03.53.png>)

The method creates an ERC-721 token with Collateral in the form of ERC-20 tokens that the user chooses to use for farming. The method verifies that:&#x20;

* the recipient of the ERC-721 is not a null address&#x20;
* the farming is not stopped for all users

If all conditions are met, the ERC-20 tokens are transferred from the user's address to the farming contract address. Before it the user must give the allowance for the farming contract to use his ERC-20 tokens (on the token contract). An ERC-721 token is then created, which is owned by the user who invoked the contract method. A record of the characteristics of the created wNFT and its the collateral with ERC-20 tokens is created in the Protocol repository. The method captures the farming start date for the created ERC-721 token. A Staked event is created for the transaction in the blockchain, specifying:

* token id of the created ERC-721 token;
* contract address of the ERC-20 tokens that the user chooses to farm;
* the number of ERC-20 tokens that the user decided to send to the farming.

**Parameters:**

| Name                  | Type    | Description                                                                                                                                                                |
| --------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_receiver**        | address | Recipient address of ERC-721 token                                                                                                                                         |
| **\_erc20Collateral** | array   | <p>An array of values: </p><ul><li>ERC-20 token contract address </li><li>number of ERC-20 tokens</li></ul>                                                                |
| **\_unwrapAfter**     | uint256 | Date after which farming reward can be received, unwrap ERC-721 token, receive ERC-20 tokens that have been frozen at the farming contract address + farming reward tokens |

### Method **harvest**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-12-02 в 15.10.03.png>)

The method can only be triggered by the owner of an ERC-721 token with ERC-20 tokens wrapped in it. The method is triggered if there is a reward token amount available for accrual that is not 0. The method adds ERC-20 tokens to the ERC-721 token collateral amount. The method for the transaction in the blockchain creates a Harvest event specifying:

* token id of the created ERC-721 toke&#x6E;**;**
* the contract address of the ERC-20 tokens for which the user received the farming reward;
* remuneration amount.

**Parameters:**

| Name                 | Type        | Description                                                                                                                                 |
| -------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_wrappedTokenId** | **uint256** | Token id ERC-721 token                                                                                                                      |
| **\_erc20**          | **address** | Address of the ERC-20 token contract that the user has transferred to the contract for farming and for which the user wishes to be rewarded |

### Method **getAvailableRewardAmount**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-12-02 в 15.14.20.png>)

The method for token id of ERC-721 token and contract address of ERC-20 tokens that are stored in Collateral (are in farming) returns the available amount of reward for farming. The method analyses how much time has elapsed from the creation of the ERC-721 token with collateral in the form of ERC-20 tokens to the current moment. Relative to the time period obtained, the method determines the % reward according to the farming settings for that type of ERC-20 tokens. And applies the % to the number of ERC-20 tokens in the ERC-721 token collateral (being farmed) in the calculation. This calculates the available amount of reward for farming.

**Parameters:**

| Name                 | Type    | Description                                                                                                                                 |
| -------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_wrappedTokenId** | uint256 | Token id ERC-721 token                                                                                                                      |
| **\_erc20**          | address | Address of the ERC-20 token contract that the user has transferred to the contract for farming and for which the user wishes to be rewarded |

**Returns values:**

| Name              | Type    | Description                                    |
| ----------------- | ------- | ---------------------------------------------- |
| **rewardAccrued** | uint256 | Number of ERC-20 tokens availabled for harvest |

### Method **getCurrenntAPYByTokenId**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-12-02 в 15.22.29.png>)

The method for token id of ERC-721 token and contract address of ERC-20 tokens that are collateralized (in farming) returns % of the farming reward if the reward would have been received at the current time. The method analyses how much time has elapsed from the creation of the ERC-721 token with collateral in the form of ERC-20 tokens to the current moment. Relative to the time period obtained, the method determines the % reward according to the farming settings for that type of ERC-20 token.

**Parameters:**

| Name                 | Type    | Description                                                                                                                                 |
| -------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_wrappedTokenId** | uint256 | Token id ERC-721 token                                                                                                                      |
| **\_erc20**          | address | Address of the ERC-20 token contract that the user has transferred to the contract for farming and for which the user wishes to be rewarded |

**Returns values:**

| Name         | Type    | Description                                                             |
| ------------ | ------- | ----------------------------------------------------------------------- |
| **percents** | uint256 | Percentage of remuneration for farming ERC-20 tokens of a specific type |

### Method **getPlanAPYByTokenId**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-12-02 в 15.27.16.png>)

The method for token id of ERC-721 token and contract address of ERC-20 tokens that are stored in collateral (are in farming) returns a scheduled % reward for farming. The user may not have specified the token lock period on the farming contract (farming on demand), or they may have.&#x20;

Accordingly, the method analyses:

* how much time has elapsed from the creation of the ERC-721 token with collateral in the form of ERC-20 tokens to the current moment
* or how long the farming will last (when the farming is urgent - the period of time for which the user locks ERC-20 tokens on the farming contract has been specified by the user). In relation to the time period obtained, the method determines the % reward according to the farming settings for that type of ERC-20 tokens.

**Parameters:**

| Name                 | Type    | Description                                                                                                                                 |
| -------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_wrappedTokenId** | uint256 | Token id ERC-721 token                                                                                                                      |
| **\_erc20**          | address | Address of the ERC-20 token contract that the user has transferred to the contract for farming and for which the user wishes to be rewarded |

**Returns values:**

| Name         | Type    | Description                                                                    |
| ------------ | ------- | ------------------------------------------------------------------------------ |
| **percents** | uint256 | Scheduled remuneration percentage for farming ERC-20 tokens of a specific type |

### Method **getRewardSettings**

![](<../../../../../.gitbook/assets/Снимок экрана 2021-12-02 в 15.31.25.png>)

The method for ERC-20 token contract address returns the available farming period and % reward settings. These settings are made by the owner of the farming contract.

**Parameters:**

| Name                      | Type    | Description                                                                               |
| ------------------------- | ------- | ----------------------------------------------------------------------------------------- |
| **\_farmingTokenAddress** | address | ERC-20 contract address of the tokens for which the user is requesting farming conditions |

**Returns values:**

| Name         | Type  | Description                                                                          |
| ------------ | ----- | ------------------------------------------------------------------------------------ |
| **settings** | tuple | The array of available periods of farming and % of reward for requested ERC-20 token |
