# NFTKiosk.sol

The main changes included in version 1 of the Launchpad are as follows:

1. The contract architecture has been **reworked**.
2. Pricing and discount functionality have been separated into a **separate** contract.
3. The ability to create an individual **storefront (aka** showcas&#x65;**)** for its owner has been added.
4. The ability to use a personalized pricing and **discount** contract for each storefront (aka showcase) has been added.
5. Functionality for selling regular **ERC-721** standard NFTs has been added.
6. The ability to set individual **prices** for NFTs and wNFTs has been added.
7. The ability to set prices at the storefront (aka showcase) **level** for the NFTs and wNFTs placed on it has been added.
8. Various types of **discounts** have been introduced, including time-based discounts, discounts using promo codes, and **referral** discounts.

**Restrictions:**

1. The smart contract can only work with wNFT of Wrapper v.1 version.
2. The sellable ERC-20 tokens should be first in the collateral array of wNFTs.
3. ERC-1155 tokens are not being supported.
4. The contract model of prices and discounts for the showcase should be added in the white list of models. To do it it is necessary to send email to DAO ENVELOP. Email address is tech@niftsy.io. The technical team will contact the email sender to perform the code review of his smart contract.

#### Method setDisplayParams

```solidity
function setDisplayParams(
        string calldata _name,
        address _beneficiary, // who will receive assets from sale
        uint256 _enableAfter,
        uint256 _disableAfter,
        address _priceModel
    ) public virtual 
```

The method registers a storefront (aka showcase) for a user. Only the owner of the storefront  (aka showcase) can configure it, set prices, place **NFTs** and **wNFTs** on their storefront  (aka showcase), and set the size of discounts to them.

The owner needs to come up with a name for the storefront, which users will use in the URL when they visit the launchpad dApp. **For example**, in the URL "[https://stage.appv1.envelop.is/launchpad/5/0xb267e4067886da3566511fa508ffce4b24e656b6/brownie](https://stage.appv1.envelop.is/launchpad/5/0xb267e4067886da3566511fa508ffce4b24e656b6/brownie)", the last part "**brownie**" represents the storefront's **name**.

The method emits a DisplayChanged event with the following details:

* **The hash** of the storefront name using the SHA-256 algorithm.
* **The address** of the storefront owner.
* **The address** of the recipient for funds from the sale of NFTs and wNFTs on the storefront (when sales happen on default storefront (aka showcase)).
* **The start** date of the sales in Unix time format.
* **The end** date of the sales in Unix time format.
* **The address** of the contract for the pricing and discount model for the storefront.
* **The storefront** name.

**Incoming parameters for calling the method:**

| Name           | Type    | Description                                                                                  |
| -------------- | ------- | -------------------------------------------------------------------------------------------- |
| \_name         | string  | Showcase name                                                                                |
| \_beneficiary  | address | Address of the recipient of funds from the sale of NFT and wNFT (for the default storefront) |
| \_enableAfter  | uint256 | Sales start date, unixtime format                                                            |
| \_disableAfter | uint256 | End of sale date, unixtime format                                                            |
| \_priceModel   | address | Address of the contract model of prices and discounts for the showcase                       |

### Method transferDisplay

```solidity
function transferDisplay(address _to, bytes32 _displayNameHash) 
        external 
```

The method transfers ownership of a storefront (aka showcase) from the old owner to a new owner.

The method emits a **DisplayTransfer** event with the following details:

* **The hash** of the storefront name using the SHA-256 algorithm.
* **The old** **owner** of the storefront.
* **|The new** **owner** of the storefront.

**Incoming parameters for calling the method:**

| Name              | Type    | Descriptions                        |
| ----------------- | ------- | ----------------------------------- |
| \_to              | address | New owner of the storefront         |
| \_displayNameHash | bytes32 | SHA-256 hash of the storefront name |

### Method addItemToDisplay

```solidity
function addItemToDisplay(
        bytes32 _displayNameHash,
        ETypes.AssetItem memory _assetItem,
        KTypes.Price[] calldata _prices
    ) 
        public 
        returns  (KTypes.Place memory place)
```

The method places NFTs (non-fungible tokens) and wNFTs (wrapped non-fungible tokens) on a storefront (aka showcase). **Only** the owner of a specific showcase can call this method. Before calling the method, the owner **must** give permission to the Launchpad contract to use their (NFTs and wNFTs). The method transfers the NFTs and wNFTs to the address of the Launchpad smart-contract.

The method emits an event called "ItemAddedToDisplay" with the following details:

* **The hash** of the storefront name using the SHA-256 algorithm.
* **The address** of the NFT/wNFT smart contract.
* **The tokenId** of the NFT/wNFT.
* **The index position** of the NFT/wNFT in the array of tokens placed on the specific showcase case.

**Incoming parameters for the method:**&#x20;

| Name              | Type             | Description                                                                                                                                         |
| ----------------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_displayNameHash | bytes32          | SHA-256 hash of the storefront (showcase) name                                                                                                      |
| \_assetItem       | ETypes.AssetItem | Data about NFT/wNFT                                                                                                                                 |
| \_prices          | KTypes.Price\[]  | An array of **individual** price data for NFT/wNFT. Can be **empty**. In this case the prices set for the storefront (showcase) will be **applied** |

#### ETypes.AssetItem

| Name    | Type         | Description                                                                    |
| ------- | ------------ | ------------------------------------------------------------------------------ |
| asset   | ETypes.Asset | Data about the type and contract of token transferred to the Lunchpad contract |
| tokenId | uint256      | Number of token                                                                |
| amount  | amount       | Value 0 (zero)                                                                 |

**ETypes.Asset**

<table><thead><tr><th width="198.33333333333331">Name</th><th width="174">Type</th><th>Description</th></tr></thead><tbody><tr><td>assetType</td><td>ETypes.AssetType</td><td>The value from Asset Type enum</td></tr><tr><td>contractAddress</td><td>address</td><td>Thr address of the NFT/wNFT smart contract.</td></tr></tbody></table>

**ETypes.AssetType**: 3 - ERC-721.&#x20;

**KTypes.Price**

| Name    | Type    | Description                                                                                                             |
| ------- | ------- | ----------------------------------------------------------------------------------------------------------------------- |
| payWith | address | The smart-contract address of the payment token. In case of payment with native tokens (coin) zero-address is specified |
| amount  | uint256 | Number of payment tokens                                                                                                |

**The method returns values:**

| Name    | Type    | Description                                                                                                 |
| ------- | ------- | ----------------------------------------------------------------------------------------------------------- |
| display | bytes32 | SHA-256 hash of the storefront (showcase) name                                                              |
| index   | uint256 | The serial number of the placed NFT/wNFT record in the array of tokens placed in this storefront (showcase) |

### Method addBatchItemsToDisplayWithSamePrice

```solidity
function addBatchItemsToDisplayWithSamePrice(
        bytes32 _displayNameHash,
        ETypes.AssetItem[] memory _assetItems,
        KTypes.Price[] calldata _prices
    ) 
        external 
        returns  (KTypes.Place[] memory)
```

The method allows the placement of **multiple** NFTs/wNFTs on a showcase in a **single** **call**. Only the owner of a specific showcase can call this method. Before calling the method, the owner must give permission to the Launchpad contract to use their NFTs and wNFTs. The method transfers the NFTs and wNFTs to the address of the Launchpad contract. Individual pricing settings apply to the entire group of NFTs/wNFTs being placed.

The method emits an **event** **called** "**ItemAddedToDisplay**" for each NFT/wNFT being placed, providing the following details:

* **The hash** of the showcase name using the SHA-256 algorithm.
* **The address** of the NFT/wNFT smart contract.
* **The tokenId** of the NFT/wNFT.
* **The index** **position** of the NFT/wNFT in the array of tokens placed on the specific showcase.

**Incoming method call parameters:**

| Name              | Type                | Description                                                                                                                                                                           |
| ----------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_displayNameHash | bytes32             | SHA-256 hash of the showcase name                                                                                                                                                     |
| \_assetItems      | ETypes.AssetItem\[] | An array of NFT/wNFT data. The description of the data type is made above                                                                                                             |
| \_prices          | KTypes.Price\[]     | An array of individual price data for NFT/wNFT. **Can** be **empty**. In this case, the prices set for the showcase will be applied. The description of the data type is given above. |

**The method returns an array of value pairs:**

| Name    | Type    | Description                                                                             |
| ------- | ------- | --------------------------------------------------------------------------------------- |
| display | bytes32 | SHA-256 hash of the showcase name                                                       |
| index   | uint256 | The serial number of the NFT/wNFT record in the array of tokens placed in this showcase |

### Method addAssetItemPriceAtIndex

```solidity
function addAssetItemPriceAtIndex(
        ETypes.AssetItem calldata _assetItem,
        KTypes.Price[] calldata _prices
    ) 
        external 
```

The method adds prices for NFT/wNFT. The method can only be called by the owner of the showcase where the NFT/wNFT is placed.

The method emits an event called "**ItemPriceChanged**" with the following details:

* **The hash** of the showcase name using the SHA-256 algorithm, where the NFT/wNFT is placed.
* **The address** of the NFT/wNFT smart-contract.
* **The tokenId** of the NFT/wNFT.

**Incoming parameters for the method:**

| Name        | Type             | Description                                                                                                       |
| ----------- | ---------------- | ----------------------------------------------------------------------------------------------------------------- |
| \_assetItem | ETypes.AssetItem | Data about the NFT/wNFT for which prices are added. The description of the type was given above                   |
| \_prices    | KTypes.Price\[]  | An array of data about individual prices for NFT/wNFT to be added. A description of the data type is given above. |

### Method editAssetItemPriceAtIndex

```solidity
function editAssetItemPriceAtIndex(
        ETypes.AssetItem calldata _assetItem,
        uint256 _priceIndex,
        KTypes.Price calldata _price
    ) 
        external
```

The method replaces the price record in the array of individual prices for the NFT/wNFT placed on the showcase. The method can only be called by the owner of the showcase where the NFT/wNFT is placed.

The method emits an event called "**ItemPriceChanged**" with the following details:

* **The hash** of the showcase name using the SHA-256 algorithm, where the NFT/wNFT is placed.
* **The address** of the NFT/wNFT smart-contract.
* **The tokenId** of the NFT/wNFT.

**Incoming parameters for the method:**

| Name         | Type             | Description                                                                                                                                             |
| ------------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_assetItem  | ETypes.AssetItem | Data about the NFT/wNFT for which prices are changed. The description of the type was given above                                                       |
| \_priceIndex | uint256          | The **sequence** number of a record in the array of individual prices for NFT/wNFT. Numbering in the array starts with 0                                |
| \_prices     | KTypes.Price     | The individual price data for NFT/wNFT that you want to replace the record in the individual price array. A description of the data type is given above |

### Method removeLastPersonalPriceForAssetItem

```solidity
function removeLastPersonalPriceForAssetItem(
        ETypes.AssetItem calldata _assetItem
    ) 
        external 
```

The method **deletes** the last record in the array of individual prices for the NFT/wNFT placed on the showcase. The method can only be called by the owner of the showcase, where the NFT/wNFT is placed.

The method emits an event called "**ItemPriceChanged**" with the following details:

* **The hash** of the showcase name using the SHA-256 algorithm, where the NFT/wNFT is placed.
* **The address** of the NFT/wNFT smart-contract.
* **The tokenId** of the NFT/wNFT.

**Incoming parameters for the method:**

| Name        | Type             | Description                                                                                                                                |
| ----------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| \_assetItem | ETypes.AssetItem | The NFT/wNFT data for which the **record** from the array of individual prices is **deleted**. The description of the type was given above |

### Method buyAssetItem

```solidity
function buyAssetItem(
        ETypes.AssetItem calldata _assetItem,
        uint256 _priceIndex,
        address _buyer,
        address _referrer,
        string calldata _promo
    ) external payable nonReentrantol
```

The method allows a user to **purchase** the NFT/wNFT placed on the showcase. When **call** the method, the user can send a certain amount of native network coins if he decide to buy for native tokens. Before calling the method, the user **must** give permission to use ERC-20 tokens, which they intend to use for **payment** of the NFT/wNFT (if the payment is made with ERC-20 tokens that the showcase owner is willing to accept as payment). The purchase can only be made during the period **between** the **start** and **end** dates of trading the NFT/wNFT on the showcase.

The method emits an event called "**EnvelopPurchase**" with the following details:

* **The hash** of the showcase name using the SHA-256 algorithm, where the NFT/wNFT is placed.
* **The address** of the NFT/wNFT smart-contract.
* **The tokenId** of the NFT/wNFT.

The method emits an event called "**EnvelopReferrer**" with the following details (if buyer calls method with filled referrer address):

* **The address** of referrer.
* **The address** of buyer.
* **The address** of payment token smart contract using by buyer to pay&#x20;
* **The amount** of payment
* **The percent** of referrer discount

**Incoming parameters for the method:**

| Name         | Type             | Description                                                                                                                                            |
| ------------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| \_assetItem  | ETypes.AssetItem | Data about the NFT/wNFT that is being **purchased**. A description of the type was given above                                                         |
| \_priceIndex | uint256          | **Record** **index** from an array of prices (individual or prices configured for the showcase as a whole) - what will be used to pay for the purchase |
| \_buyer      | address          | The address of the **recipient** of the purchased NFT/wNFT, which may be different from the address of the purchaser calling the method                |
| \_referrer   | address          | <p>Referral address, which is added by the showcase owner in the showcase settings</p><p><br></p>                                                      |
| \_promo      | string           | **Promo**-code added by the showcase owner in the showcase settings                                                                                    |

### Method getDisplayOwner

```solidity
function getDisplayOwner(bytes32 _displayNameHash) public view returns (address)
```

The method returns the address of the showcase owner.&#x20;

**Incoming parameters for the method:**

| Name              | Type    | Description                       |
| ----------------- | ------- | --------------------------------- |
| \_displayNameHash | bytes32 | SHA-256 hash of the showcase name |

**Returned values:**

| owner | address | The address of the owner of the showcase |
| ----- | ------- | ---------------------------------------- |

### Method getDisplay

```solidity
function getDisplay(bytes32 _displayNameHash) 
        public 
        view 
        returns (KTypes.Display memory)
```

The method returns information about the showcase.&#x20;

**Incoming parameters for the method:**

| Name              | Type    | Description                       |
| ----------------- | ------- | --------------------------------- |
| \_displayNameHash | bytes32 | SHA-256 hash of the showcase name |

**Returned values:**

| Name    | Type           | Description                    |
| ------- | -------------- | ------------------------------ |
| display | KTypes.Display | Information about the showcase |

**KTypes.Display**

| Name         | Type                  | Description                                                                                |
| ------------ | --------------------- | ------------------------------------------------------------------------------------------ |
| owner        | address               | The address of the owner of the showcase                                                   |
| beneficiary  | address               | Address of the recipient of funds from the sale of NFT and wNFT (for the default showcase) |
| enableAfter  | uint256               | Sales start date, unixtime format                                                          |
| disableAfter | uint256               | End of sale date, unixtime format                                                          |
| priceModel   | address               | Address of the smart contract model of prices and discounts for the showcase               |
| items        | KTypes.ItemForSale\[] | Array of data about NFT/wNFT placed on the showcase and individual prices for each         |

**KTypes.ItemForSale**

| Name   | Type             | Description                                                                                                                                                                          |
| ------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| owner  | address          | Address of the recipient of **funds** from the sale of a particular NFT/wNFT - for custom showcase                                                                                   |
| nft    | ETypes.AssetItem | Data about placed NFT/wNFT. A description of the type was given above                                                                                                                |
| prices | KTypes.Price\[]  | Array of individual price data for placed NFT/wNFT. **Can** be **empty**. In this case, the prices set for the showcase will be applied. The description of the type was given above |

### Method getAssetItemPlace

```solidity
function getAssetItemPlace(ETypes.AssetItem memory _assetItem) 
        public 
        view 
        returns  (KTypes.Place memory)
```

The method returns data about the showcase where the NFT/wNFT is placed.

**Incoming parameters for the method:**

| Name        | Type             | Description                                                           |
| ----------- | ---------------- | --------------------------------------------------------------------- |
| \_assetItem | ETypes.AssetItem | Data about placed NFT/wNFT. A description of the type was given above |

**Returned values:**

| Name    | Type    | Description                                                                                 |
| ------- | ------- | ------------------------------------------------------------------------------------------- |
| display | bytes32 | SHA-256 hash of the showcase name                                                           |
| index   | uint256 | The serial number of the NFT/wNFT **record** in the array of tokens placed in this showcase |

### Method getAssetItemPricesAndDiscounts

```solidity
function getAssetItemPricesAndDiscounts(
        ETypes.AssetItem memory _assetItem,
        address _buyer,
        address _referrer,
        string calldata _promo
    ) 
        external 
        view
        returns (KTypes.Price[] memory, KTypes.Discount[] memory)
```

The method returns data about prices and discounts for placed NFT/wNFT.

**Incoming parameters for the method:**

| Name        | Type             | Description                                                                                |
| ----------- | ---------------- | ------------------------------------------------------------------------------------------ |
| \_assetItem | ETypes.AssetItem | Data about the NFT/wNFT that is being purchased. A description of the type was given above |
| \_buyer     | address          | Address of the recipient of the purchased NFT/wNFT                                         |
| \_referrer  | address          | Referral address, which is added by the showcase owner in the showcase settings            |
| \_promo     | string           | **Promo**-code added by the showcase owner in the showcase settings                        |

**Returned values:**

<table><thead><tr><th>Name</th><th width="249.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td>prices</td><td>KTypes.Price[]</td><td>Array with prices for placed NFT/wNFT. The description of the data type is given above</td></tr><tr><td>discount</td><td>KTypes.Discount[]</td><td>Array with data about <strong>discounts</strong> that apply to the given NFT/wNFT, taking into account the data passed to the method about the promo-code and referral</td></tr></tbody></table>

**KTypes.Discount:**

| Name        | Type         | Description                                 |
| ----------- | ------------ | ------------------------------------------- |
| dsctType    | DiscountType | The value from discount types enum          |
| dsctPercent | uint16       | Discount size: 100%-10000, 20%-2000, 3%-300 |

**DiscountType:**

* 0 - **promo**-discount (PROMO)&#x20;
* 1 - **referral**-discount (REFERRAL)&#x20;
* 2 - discount by **volume** of purchases (BATCH)&#x20;
* 3 - discount by **time** (TIME)&#x20;
* 4 - discount for members of "**white**-**lists**" (WHITELIST)&#x20;
* 5, 6, 7 - discounts which can be set in the contract price and discount models by the the showcase owner (CUSTOM1, CUSTOM2, CUSTOM3)

### Method getDisplayAssetItems

```solidity
function getDisplayAssetItems(bytes32 _displayNameHash) 
        public 
        view 
        virtual
        returns (KTypes.ItemForSale[] memory) 
```

The method returns for the showcase information about all NFTs and wNFT placed on it and not **yet** **sold**.

**Incoming parameters for the method:**

| Name              | Type    | Description                       |
| ----------------- | ------- | --------------------------------- |
| \_displayNameHash | bytes32 | SHA-256 hash of the showcase name |

**Returned values:**

| Name  | Type           | Description                                                                                                                          |
| ----- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| items | ItemForSale\[] | An array of data about NFTs/wNFTs placed in the showcase and individual prices for each. Description of the data type is given above |

### Method getAssetItem

```solidity
function getAssetItem(ETypes.AssetItem memory _assetItem)
        public
        view
        returns (KTypes.ItemForSale memory)
```

The method returns settings data for a particular NFT/wNFT.&#x20;

**Incoming parameters for the method:**

<table><thead><tr><th>Name</th><th width="197.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td>_assetItem</td><td>ETypes.AssetItem</td><td>Data about NFT/wNFT. A description of the type was given above</td></tr></tbody></table>

**Returned values:**

<table data-header-hidden><thead><tr><th>Name</th><th width="216.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td>items</td><td>ItemForSale</td><td>Data about the placed NFT/wNFT on the showcase and individual prices for it. A description of the data type is given above</td></tr></tbody></table>

### Method hlpHashString

```solidity
function hlpHashString(string memory _name) public pure returns (bytes32)
```

The method returns SHA-256 hash for a value.

**Incoming parameters for the method:**

| Name   | Type   | Description            |
| ------ | ------ | ---------------------- |
| \_name | string | The value for encoding |

**Returned values:**

| Name | Type    | Description              |
| ---- | ------- | ------------------------ |
| hash | bytes32 | SHA-256 hash for a value |
