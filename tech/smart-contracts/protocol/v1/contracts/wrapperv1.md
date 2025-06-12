# WrapperV1

**The main changes included in Protocol version 1:**&#x20;

* **Wrapping** NFT ERC-1155 in wNFT ERC-721;
* Wrapping NFT ERC-1155 in wNFT ERC-1155;
* Wrap NFT ERC-721 in wNFT ERC-1155;
* Adding NFT ERC-721 and 1155 to wNFT;
* Wrapping a empty instead of the original NFT;&#x20;
* **Ability** to prohibit adding a Collateral;
* **Ability** to prohibit transfering of wNFT;
* **Ability** to prohibit re-wrapping of wNFT;
* **Ability** to prohibit unwrapping of wNFT;
* **Multi-royalty**: allocation of transfer fees between several beneficiaries for wNFT;&#x20;
* **Possibility** of specifying for whom a wNFT is created;
* **Ability** to add multiple tokens (including different standards) during the creation of a wNFT;
* Ability to add multiple tokens (including different standards) when adding collateral for wNFT.

## **WrapperBaseV1.sol**

### Method **wrap**

```solidity
function wrap(
        ETypes.INData calldata _inData, 
        ETypes.AssetItem[] calldata _collateral, 
        address _wrappFor
    ) 
        public 
        virtual
        payable 
        nonReentrant 
        returns (ETypes.AssetItem memory) 
```

The method allows to wrap the original NFT ERC-721, 1155, a empty (create wNFT without original NFT). User can create ERC721, 1155 standard wNFT - a container with collateral. If the contract holder has blacklisted the contract address of the original NFT ERC-721 or ERC-1155 token, it will not be possible to create a wrapped NFT for this original NFT.

Only the owner of the original NFT can wrap it. To do so, the owner of the original NFT must give allowance for the **WrapperBaseV1** contract to use it.

The creator of a wrapped NFT can set a fee that any sender of his wrapped NFT will pay when transferring. Several commissions can be set - in different ERC-20 tokens. ERC-20 token contract addresses sent to the method must be added to a whitelist that only the contract owner has access to.

The creator of a wrapped NFT can set the commission in the form of a technical ERC-20 protocol token. This is the token that is minted during the transfer by the **WrapperBaseV1** contract. The wNFT sender does not need to have it on their wallet balance.

If the creator of the wrapped NFT (wNFT) has set the amount of commission for the transfer, it can also define the shares of that commission and the addresses where those shares will be transferred during any transfer of the wrapped NFT. This is how the multi-royalty mechanism is implemented. If the creator of wNFT specifies the **WrapperBaseV1** contract address as the Royalty recipient, the royalty income will be added to wNFT as collateral.

In addition, the wNFT creator can set the total amount of commission to be accumulated during NFT transfers so that the current owner of that NFT can unwrap it and thereby - receive: accumulated collateral tokens, accumulated transfer commission tokens, accumulated native tokens from the blockchain itself, the original NFT itself (if not a empty was wrapped). This limitation applies to all transfer withholding commissions (wNFT can be configured to withhold commissions on multiple tokens).

The creator of the wrapped NFT can also set a date in Unix-time format after which wNFT can be unwrapped.

The creator of the wrapped NFT should specify the address for which the token is being created. This can be the creator itself or a different address.

The creator of a wrapped NFT can specify rules for the behavior of the generated wNFT:&#x20;

* can prohibit to unwrapwNFT
* can disallow adding collateral
* can prohibit to transfer wNFT
* can disallow wrapping of the wNFT

The owner of a **WrapperBaseV1** contract can set individual behavior rules for the contract address of the original NFT. If such rules are set, the user will not be able to create a wNFT with different behavioural rules when wrapping the token of the original NFT contract.

The owner of the **wrapperBaseV1** contract can prohibit for the original NFT contract address from setting individual rules of behaviour. If such a prohibition is set, the user will not be able to create a wNFT with the specified individual rules of behaviour when wrapping the original NFT contract token.&#x20;

In case the user wants to create wNFT of ERC-1155 standard, he must send the method the number of copies to be minted.

During wrapping the user can pass information to the method about the collateral to be added during wNFT creation. The information is passed as a data array describing the types of collateral tokens, contract addresses, tokenId (if ERC-721, ERC-1155 tokens are added to collateral), number of NFT copies or number of ERC-20 tokens (for ERC-1155 and ERC-20 - value other than 0, for ERC-721 - 0). The user must give the allowance to the **WrapperBaseV1** contract to manage the tokens they want to add to wNFT - in sufficient numbers to be replenished.

There is a limit set by the contract owner WrapperBaseV1 on the number of entries in the collateral array of wNFT - MAX\_COLLATERAL\_SLOTS. If the number is exceeded during a method call, the method will fail (a revert with message about error will happens).

If all conditions for wrapping are met, the method creates a wrapped NFT of ERC-721 or ERC-1155 standard (depends on the type that the user specifies to the method) and assigns it to the address that the wNFT creator (sender of the transaction) specifies. **WrapperBaseV1** becomes the owner of the original NFT as well as the collateral tokens.

At the time the method is called, it is possible to send native blockchain tokens that will be accounted for in the wNFT collateral

The method creates a **WrappedV1** event specifying:

* the contract address of the original NFT;
* wNFT contract address;
* id of the original NFT;
* wNFT id;
* recipient wNFT;
* the number of native tokens that have been transferred as collateral for wNFT;
* description of wNFT rules.

The method returns a value with the following data structure:&#x20;

* type of wNFT to be created (3 - ERC-721, 4 - ERC-1155)&#x20;
* wNFT contract address&#x20;
* wNFT id&#x20;
* number of copies - wNFT balance (for ERC-1155 - value other than zero, for ERC-721 - 0)

The data types are described in contact LibEnvelopTypes.sol, ETypes library.

**Input parameters of the method:**

| Name             | Type                    | Description                                         |
| ---------------- | ----------------------- | --------------------------------------------------- |
| **\_inData**     | **ETypes.INData**       | Data for creating wNFT                              |
| **\_collateral** | **ETypes.AssetItem\[]** | Transferable collateral data for wNFT - as an array |
| **\_wrappFor**   | **address**             | Address for which wNFT is created                   |

#### **ETypes.INData:**

| Name                  | Type                  | Description                                                                                                                                                                                                                                           |
| --------------------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **inAsset**           | **ETypes.AssetItem**  | Data on the original NFT                                                                                                                                                                                                                              |
| **unWrapDestination** | **address**           | Recipient address of the original NFT and collateral after unwrap of wNFT - filled by default with a null address                                                                                                                                     |
| **fees**              | **ETypes.Fee\[]**     | Array of information on transfer fees                                                                                                                                                                                                                 |
| **locks**             | **ETypes.Lock\[]**    | Array of information on unwrap conditions (blocking by time, by amount of commission collected, etc...)                                                                                                                                               |
| **royalties**         | **ETypes.Royalty\[]** | An array of information on royalty beneficiaries                                                                                                                                                                                                      |
| **outType**           | **ETypes.AssetType**  | Type of wNFT created (3 - ERC-721, 4 - ERC-1155)                                                                                                                                                                                                      |
| **outBalance**        | **uint256**           | Number of copies - wNFT balance (for ERC-1155 - value other than zero, for ERC-721 - 0)                                                                                                                                                               |
| **rules**             | **bytes2**            | <p>wNFT rules of conduct (e.g. 1111, where right to left </p><ul><li>pos1 - prohibition to unwrap</li><li>pos2 - prohibition to re-wrap wNFT </li><li>pos3 - prohibition to transfer wNFT </li><li>pos4 - prohibition to add an collateral)</li></ul> |

#### **ETypes.AssetItem:**

<table><thead><tr><th width="160.33333333333331">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>asset</strong></td><td>ETypes.Asset</td><td>Data on the type and contract of original NFT tokens transferred to the WrapperBaseV1 contract</td></tr><tr><td><strong>tokenId</strong></td><td>uint256</td><td>Token number (if a empty are being wrapped, 0 is indicated; if user adds a collateral to wNFT by ERC-20, 0 is indicated)</td></tr><tr><td><strong>amount</strong></td><td>amount</td><td>Number of NFT copies or number of ERC-20 tokens (for ERC-1155 a value other than zero, for ERC-20 a value other than 0; for ERC-721 a value other than 0)</td></tr></tbody></table>

#### **ETypes.Asset:**

| Name                | Type                 | Description                          |
| ------------------- | -------------------- | ------------------------------------ |
| **assetType**       | **ETypes.AssetType** | Value from the type dictionary       |
| **contractAddress** | **address**          | Address of the original NFT contract |

#### **ETypes.AssetType:**

* 0 - empty;
* 1 - native token (coin);
* 2 - ERC-20;
* 3 - ERC-721;
* 4 - ERC-1155.

#### **ETypes.Fee:**

| Name        | Type        | Description                                |
| ----------- | ----------- | ------------------------------------------ |
| **feeType** | **bytes1**  | Commission type - 0                        |
| **param**   | **uint256** | Amount of commission                       |
| **token**   | **address** | Transfer commission token contract address |

#### **ETypes.Lock**

| Name         | Type        | Description                                                                                                                                                                 |
| ------------ | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **lockType** | **bytes1**  | <p>Blocking type: </p><p>0x00 - blocking by time </p><p>0x01 - blocking by volume of accumulated transfer fee for wNFT<br>0x02 - count of max collateral slots for wNFT</p> |
| **param**    | **uint256** | Value                                                                                                                                                                       |

#### **ETypes.Royalty:**

| Name            | Type        | Description                        |
| --------------- | ----------- | ---------------------------------- |
| **beneficiary** | **address** | Royalty beneficiary address        |
| **percent**     | **uint16**  | Value - no more than 10,000 (100%) |

**The method returns values:**

| Name      | Type                 | Description                                                                                                                                                                                                                                                                                |
| --------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **value** | **ETypes.AssetItem** | <p>Data set in the following structure (see above): </p><ul><li>type of wNFT to be created (3 - ERC-721, 4 - ERC-1155); </li><li>wNFT contract address;</li><li>wNFT id</li><li>number of copies - wNFT balance (for ERC-1155 a value other than zero, for ERC-721 a value of 0)</li></ul> |

### **Method addCollateral**

```solidity
function addCollateral(
        address _wNFTAddress, 
        uint256 _wNFTTokenId, 
        ETypes.AssetItem[] calldata _collateral
    ) public payable virtual
```

The method adds wrapped NFT **Сollateral** in the form of ERC-20, ERC-721, ERC-1155, native tokens. The user can add multiple tokens of different types to wNFT Сollateral or multiple tokens of the same type (e.g. multiple NFT ERC-721 of the same contract or different) in a single method call.

There are a number of conditions that can be met for a method call to succeed:&#x20;

* The method is passed an existing wNFT id and a valid wNFT smart-contract address;&#x20;
* Contract addresses of ERC-20, ERC-721, ERC-1155 tokens have been added to the white list by the contract owner;&#x20;
* There is no ban on adding collateral at wNFT;&#x20;
* The address from which the method is called has enough ERC-20 tokens, NFT ERC-1155 token balance or owns NFT ERC-721 to add them to the collateral of the wrapped NFT;&#x20;
* The sender of the transaction has given the WrapperBaseV1 contract address permission to use all its ERC-20, NFT ERC-721, NFT ERC-1155 tokens in sufficient quantity according to the **transmitted** token array to the method.&#x20;

If all conditions are met, the method:&#x20;

* Adds entries to the wrapped NFT collateral array with the following information: token contract address, token type, tokenId (not 0 for ERC-721 and 1155, 0 for native tokens and ERC-20) and number of tokens (0 for ERC-721, value other than 0 for others);&#x20;
* Does the transfer of tokens to the WrapperBaseV1 contract address from the sender address of the transaction.&#x20;

If someone has previously deposited the same ERC-20 tokens into the Collateral of the wrapped NFT, the method does not add a new entry into the collateral array, but increases the number of tokens deposited. If someone has previously deposited the same NFT ERC-1155 token (with the same contract address and tokenId) in the collateral of the wrapped NFT, the method does not add a new entry to the collateral array, but increases the number of token copies deposited.

There is a limit set by the contract owner WrapperBaseV1 on the number of entries in the collateral array of wNFT - MAX\_COLLATERAL\_SLOTS. If the number is exceeded during a method call, the method will fail (a revert with message about error will happens).

During method call it is possible to send native blockchain tokens, which will be counted in the wNFT collateral array.

**The method does not return anything in response.**

The method creates CollateralAdded events for each token to be added, specifying:&#x20;

* wNFT smart contract address
* tokenId wNFT
* token type
* Collateral token's smart contract address (null address will be returned for native tokens)
* tokenId NFT ERC-721 or ERC-1155 token of collateral, or 0 if native/ERC-20 tokens are added
* number of tokens (for NFT ERC-721 - 0, for other token types a value other than 0)

Description of data types is located in LibEnvelopTypes.sol, ETypes library.&#x20;

**Input method call parameters:**

| Name              | Type                | Description                                         |
| ----------------- | ------------------- | --------------------------------------------------- |
| **\_wNFTAddress** | address             | Smart contract address wNFT                         |
| **\_wNFTTokenId** | uint256             | tokenId wNFT                                        |
| **\_collateral**  | ETypes.AssetItem\[] | Transferable collateral data for wNFT - as an array |

#### **ETypes.AssetItem**

| Name        | Type         | Description                                                                                                                                                                                                      |
| ----------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **asset**   | ETypes.Asset | Data on the type and contract of tokens transferred to the WrapperBaseV1 contract                                                                                                                                |
| **tokenId** | uint256      | <p>Token number ( </p><p>if tokens are topped up with wNFT ERC-20 <strong>Collateral</strong>, 0; If tokens are topped up with native tokens, 0)</p>                                                             |
| **amount**  | amount       | <p>Number of NFT copies or number of tokens ( </p><p>for ERC-1155 - a value other than 0 (zero);</p><p>for ERC-20 - value other than 0;</p><p>for native tokens - value other than 0;</p><p>for ERC-721 - 0)</p> |

#### **ETypes.AssetType**

1. \- native token (coin);
2. \- ERC-20;
3. \- ERC-721;
4. \- ERC-1155.

### Method **unwrap**

```solidity
function unWrap(address _wNFTAddress, uint256 _wNFTTokenId) external virtual
```

Method performs unwrapping of wrapped NFT ERC-721 or ERC-1155. Only current owner can call method for id of wrapped NFT.

There is a number of conditions that must be met before a method call can be successfully completed:&#x20;

* A time has **arrived** after which the wrapped NFT can be unwrapped - if the creator of the wrapped NFT has defined this time. Time in unixtime format.&#x20;
* Accumulated during transfers of the wrapped NFT enough ERC-20 fee tokens (for each fee token). At the time of wrapping the original NFT the creator of the wrapped NFT has specified the amount to be accumulated.&#x20;
* The creator of wNFT did not prohibit the unwrapped.
* For wNFT ERC-1155 - the sender of the transaction calling the method owns all copies of the token.

If all conditions are met, the method:&#x20;

* transfers of all collateral tokens of the ERC-20 standard wrapped NFT address from which the method is called.&#x20;
* transfers all collateral tokens of the ERC-721 standard wrapped NFT address from which the method is called.&#x20;
* transfers all tokens of the ERC-1155 standard wrapped NFT token to the address from which the method is called.&#x20;
* transfers all native NFT wrapped tokens collateral to the address from which the method is called.&#x20;
* burns the wrapped NFT and transfer the original NFT to the address from which the method is called.
* transfers the accumulated ERC-20 fee tokens for transfers of the wrapped NFT to the address from which the method call is made, if any are accumulated for the wrapped NFT.&#x20;
* creates an UnWrappedV1 event specifying:&#x20;
  * wNFT smart contract address;
  * Address of the original NFT smart contract;
  * id of wrapped NFT's
  * id of the original NFT&#x20;
  * The number of native tokens transferred to the recipient;
  * Description of the wNFT behaviour rules (given during wrapping)

The method returns nothing in response.

**Input method call parameters:**

| Name              | Type             | Description                                                      |
| ----------------- | ---------------- | ---------------------------------------------------------------- |
| **\_wNFTType**    | ETypes.AssetType | Type wNFT from token type dictionary (3 - ERC-721, 4 - ERC-1155) |
| **\_wNFTAddress** | address          | Smart-contract address wNFT                                      |
| **\_wNFTTokenId** | uint256          | tokenId wNFT                                                     |

If the WrapperBaseV1 contract cannot perform a transfer of collateral tokens or the original NFT because the token contract prevents such transfer, the user can call the unWrap method in emergency mode by specifying the optional \_isEmergency parameter with the value true. The contract will skip the token which cannot be transferred to the recipient of the collateral and the original NFT when unwrapping, and will transfer everything else.

### Method **getWrappedToken**

```solidity
function getWrappedToken(address _wNFTAddress, uint256 _wNFTTokenId) 
        public 
        view 
        returns (ETypes.WNFT memory)
```

Method returns all wrapped NFT data of ERC-721 or ERC-115&#x35;**.**

**Input method call parameters:**

| Name              | Type    | Description                          |
| ----------------- | ------- | ------------------------------------ |
| **\_wNFTAddress** | address | Address of the contract wrapped wNFT |
| **\_wNFTTokenId** | uint256 | tokenId wNFT                         |

A description of the returned data types can be found in the LibEnvelopTypes.sol contact, ETypes library.

Returned values:

| Name      | Type        | Description       |
| --------- | ----------- | ----------------- |
| **value** | ETypes.WNFT | Wrapped wNFT data |

#### **ETypes.WNFT**

| Name                  | Type                | Description                                                                                                                                                                                                                               |
| --------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **inAsset**           | ETypes.AssetItem    | Data on the original NFT                                                                                                                                                                                                                  |
| **collateral**        | ETypes.AssetItem\[] | Collateral data                                                                                                                                                                                                                           |
| **unWrapDestination** | address             | Recipient address of the original NFT and collateral after unwrapping of wNFT - filled by default with a null address                                                                                                                     |
| **fees**              | ETypes.Fee\[]       | Array of information on transfer fees                                                                                                                                                                                                     |
| **locks**             | ETypes.Lock\[]      | Array of information on unwrapping conditions (blocking by time, by amount of **fee** collected, etc...)                                                                                                                                  |
| **royalties**         | ETypes.Royalty\[]   | An array of information on royalty beneficiaries                                                                                                                                                                                          |
| **rules**             | bytes2              | <p>wNFT rules of conduct (e.g. 1111, </p><p>where right to left </p><p>pos1 - prohibition to unwrap </p><p>pos2 - prohibition to wrap wNFT </p><p>pos3 - prohibition to transfer wNFT </p><p>pos4 - prohibition to add an Collateral)</p> |

#### **ETypes.AssetItem**

| Name        | Type         | Description                                                                                                                                                                                                                                                       |
| ----------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **asset**   | ETypes.Asset | Data on the type and contract of tokens transferred to the WrapperBaseV1 contract for wrapped NFT                                                                                                                                                                 |
| **tokenId** | uint256      | <p>Token number (if a empty was wrapped, it will return 0<strong>;</strong></p><p>if the wNFT ERC-20 token was added to collateral, it will return 0<strong>;</strong> if the Collateral was <strong>topped</strong> up with native tokens, it will return 0)</p> |
| **amount**  | amount       | <p>Number of NFT copies or number of tokens (</p><p>for ERC-1155 - a value other than 0 (zero);</p><p>for ERC-20 - value other than 0;</p><p>for native tokens - value other than 0;</p><p>for ERC-721 - 0)</p>                                                   |

#### **ETypes.Asset**

| Name                | Type             | Description                                                                                                |
| ------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------- |
| **assetType**       | ETypes.AssetType | Value from the token type dictionary                                                                       |
| **contractAddress** | address          | Address of token contract transferred to WrapperBaseV1 protocol contract as **Collateral** or original NFT |

#### ETypes.AssetType:

* **0 - empty;**
* 1 - native token (coin);
* 2 - ERC-20;
* 3 - ERC-721;
* 4 - ERC-1155.

#### **ETypes.Fee**

| Name        | Type    | Description                         |
| ----------- | ------- | ----------------------------------- |
| **feeType** | bytes1  | Type of fee - 0                     |
| **param**   | uint256 | Size of fee                         |
| **token**   | address | Transfer fee token contract-address |

#### **ETypes.Lock**

<table><thead><tr><th width="247.33333333333331">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>lockType</strong></td><td>bytes1</td><td><p>Blocking type: </p><p>0x00 - blocking by time </p><p>0x01 - blocking by volume of accumulated transfer fee for wNFT<br>0x02 - count of max collateral slots for wNFT</p></td></tr><tr><td><strong>param</strong></td><td>uint256</td><td>Value</td></tr></tbody></table>

#### **ETypes.Royalty**

| Name            | Type    | Description                        |
| --------------- | ------- | ---------------------------------- |
| **beneficiary** | address | Royalty beneficiary address        |
| **percent**     | uint16  | Value - no more than 10,000 (100%) |

**Public variable protocolTechToken**:&#x20;

Returns the address of the ERC-20 technical fee token, which is accrued during wNFT transfers if its creator has set it as a fee token. This token is used to demonstrate the protocol's transfer fee and royalty income deduction capabilities. The user does not need to have technical tokens on their balance in order to make transfers.

**Public variable protocolWhiteList**:

Returns the address of the white and black list contract, with contract addresses and optional settings. The lists and settings are only managed by the ENVELOP project team.

**Public variable MAX\_COLLATERAL\_SLOTS**:

Returns the maximum number of entries in the collateral array for wNFT that are added with each new token added.

**wNFT public contract registry - wnftTypes**:

Returns a type by contract address. This registry is used to capture all contracts wrapped by NFT that have ever been wrapped through the WrapperBaseV1 contract methods. Type 3 is wNFT ERC-721, 4 is wNFT ERC-1155.

**Public registry last tokenID - lastWNFTId**:

&#x20;The registry by wNFT token type returns the last tokenId and address of the ERC-721 or ERC-1155 standard wNFT smart contract currently used by the WrapperBaseV1 contract for wNFT minting. Type 3 is wNFT ERC-721, 4 is wNFT ERC-1155.

### **Method getOriginalURI**

```solidity
function getOriginalURI(address _wNFTAddress, uint256 _wNFTTokenId) 
        public 
        view 
        returns(string memory uri_)
```

The method returns the metadata of the original NFT for wNFT. If a empty was wrapped, the method will return empty.

**Input method call parameters:**

| Name              | Type    | Description                         |
| ----------------- | ------- | ----------------------------------- |
| **\_wNFTAddress** | address | Address of the contract wrapped NFT |
| **\_wNFTTokenId** | uint256 | tokenId wNFT                        |

**Returned values:**

| Name      | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| **uri\_** | string | Link to the metadata of the original NFT |

### **Method getCollateralBalanceAndIndex**

```solidity
function getCollateralBalanceAndIndex(
        address _wNFTAddress, 
        uint256 _wNFTTokenId,
        ETypes.AssetType _collateralType, 
        address _erc,
        uint256 _tokenId
    ) public view returns (uint256, uint256)
```

The method returns the number of collateral tokens and the sequence number of the entry for the token in the wNFT collateral array.

**Input method call parameters:**

| Name                 | Type             | Description                                                                                                                           |
| -------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **\_wNFTAddress**    | address          | Address of the contract wrapped NFT                                                                                                   |
| **\_wNFTTokenId**    | uint256          | tokenId  **w**NFT                                                                                                                     |
| **\_collateralType** | ETypes.AssetType | <p>1 - native token (coin) </p><p>2 - ERC-20 </p><p>3 - ERC-721 </p><p>4 - ERC-1155</p>                                               |
| **\_erc**            | address          | Smart contract address for Collateral tokens                                                                                          |
| **\_tokenId**        | uint256          | <p>the tokenId of the collateral token (For collateral type 1 and 2 always pass 0, </p><p>for type 3 and 4 the tokenId is passed)</p> |

**Returned values:**

| Name       | Type    | Description                                                                  |
| ---------- | ------- | ---------------------------------------------------------------------------- |
| **value1** | uint256 | Number of collateral tokens (for ERC-721 collateral tokens always returns 0) |
| **value2** | uint256 | Serial number of the collateral token record in the wNFT collateral array    |

