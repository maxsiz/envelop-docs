# DefaultPriceModel.sol

function editCollateralPriceRecordForDisplay( bytes32 \_displayNameHash, address \_erc20, uint256 \_priceIndex, KTypes.DenominatedPrice calldata \_price ) external virtual onlyDisplayOwner(\_displayNameHash)

### Method setCollateralPriceForDisplay

```solidity
function setCollateralPriceForDisplay(
        bytes32 _displayNameHash,
        address _erc20,
        KTypes.DenominatedPrice[] calldata _prices
    ) 
        external virtual
        onlyDisplayOwner(_displayNameHash) 
```

The method sets prices for the sale of ERC-20 tokens that will be sold through wNFT placed on the Kiosk. Multiple types of ERC-20 tokens can be simultaneously sold on the Kiosk. They just need to be added to the wNFT Collateral and placed on the Kiosk. Only the Kiosk owner can invoke this method.&#x20;

**IMPORTANT**: In this example contract model, only the ERC-20 tokens that were added to wNFT first (the 1st token record in the wNFT Collateral array) are considered as the ones being sold with prices and discounts.

The method emits a **CollateralPriceChanged** event for each record in the provided array of prices,  with the following details:

* **The SHA-256 hash** of the Kiosk name on which the wNFT is placed.
* **The address** of the smart-contract of the ERC-20 token being sold.

**Incoming parameters for calling the method:**

| Name              | Type                       | Description                            |
| ----------------- | -------------------------- | -------------------------------------- |
| \_displayNameHash | bytes32                    | SHA-256 hash of the Kiosk name         |
| \_erc20           | address                    | Address of the being sold ERC-20 token |
| \_prices          | KTypes.DenominatedPrice\[] | Array with price data                  |

**KTypes.DenominatedPrice**

| Name        | Type    | Description                                                                                                                                                                                                   |
| ----------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| payWith     | address | The smart-contract address of the token, which can be used to pay for ERC-20 tokens sold. In the case of price setting with the possibility of payment by native network tokens **zero** address is specified |
| amount      | uint256 | Number of tokens to be paid per unit of ERC-20 tokens sold                                                                                                                                                    |
| denominator | uint256 | A divider to define the **price** per unit of ERC-20 tokens sold. Applies if the price of one selling token in payment tokens is either fractional or, less than 1                                            |

### Method editCollateralPriceRecordForDisplay

```solidity
function editCollateralPriceRecordForDisplay(
        bytes32 _displayNameHash,
        address _erc20,
        uint256 _priceIndex,
        KTypes.DenominatedPrice calldata _price
    )
        external virtual
        onlyDisplayOwner(_displayNameHash)
```

The method edits prices for the sale of ERC-20 tokens by completely replacing the record in the price array. Only the Kiosk owner can invoke this method for their Kiosk.

The method emits a **CollateralPriceChanged** event with the following details:

* **The SHA-256 hash** of the Kiosk name on which the wNFT is placed.
* **The address** of the smart-contract of the ERC-20 token being sold.

**Incoming parameters for calling the method:**

| Name              | Type                    | Description                                                                 |
| ----------------- | ----------------------- | --------------------------------------------------------------------------- |
| \_displayNameHash | bytes32                 | SHA-256 hash of the Kiosk name                                              |
| \_erc20           | address                 | Address of the being sold  ERC-20 token                                     |
| \_priceIndex      | uint256                 | The index number of the record in the price array to be edited              |
| \_prices          | KTypes.DenominatedPrice | The price data to be updated. A description of the data type is given above |

### Method setDefaultNFTPriceForDisplay

```solidity
function setDefaultNFTPriceForDisplay(
        bytes32 _displayNameHash,
        KTypes.Price[] calldata _prices
    ) 
       external virtual
       onlyDisplayOwner(_displayNameHash)
```

The method sets prices for the sale of NFTs that will be sold through placing on the Kiosk. If individual prices are not specified when placing the NFTs, the prices set during the invocation of this method will be used for the sale. Only the Kiosk owner can invoke this method for their Kiosk.

The method emits a **DefaultPriceChanged** event for each record in the provided array of prices, with the following details:

* **The SHA-256 hash** of the Kiosk name on which the NFT is listed.
* **The address** of the smart-contract token that can be used to **purchase** the NFT.
* **The quantity** of tokens required to be paid for the NFT.

**Incoming parameters for calling the method:**

| Name              | Type            | Description                      |
| ----------------- | --------------- | -------------------------------- |
| \_displayNameHash | bytes32         | SHA-256 hash of the Kiosk name   |
| \_prices          | KTypes.Price\[] | An array of price data for NFT.  |

**KTypes.Price**

<table><thead><tr><th width="180">Name</th><th width="142.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td>payWith</td><td>address</td><td>The smart-contract address of the payment token. In case of payment with native tokens (coin) zero-address is specified</td></tr><tr><td>amount</td><td>uint256</td><td>Number of payment tokens</td></tr></tbody></table>

### Method editDefaultNFTPriceRecordForDisplay

```solidity
function editDefaultNFTPriceRecordForDisplay(
        bytes32 _displayNameHash,
        uint256 _priceIndex,
        KTypes.Price calldata _price
    )
        external virtual
        onlyDisplayOwner(_displayNameHash)
```

The method edits prices for the sale of NFTs that will be sold through placing on the Kiosk. Only the Kiosk owner can invoke this method for their Kiosk.

The method emits a **DefaultPriceChanged** event with the following details:

* **The SHA-256 hash** of the Kiosk name on which the NFT is placed.
* **The address** of the smart-contract token that can be used to **purchase** the NFT.
* **The quantity** of tokens required to be paid for the NFT.

**Incoming parameters for calling the method:**

<table><thead><tr><th width="249.33333333333331">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>_displayNameHash</td><td>bytes32</td><td>SHA-256 hash of the Kiosk name</td></tr><tr><td>_priceIndex</td><td>uint256</td><td>The index number of the record in the price array to be edited</td></tr><tr><td>_prices</td><td>KTypes.Price</td><td>The price data for NFT. The description of the data type is given above</td></tr></tbody></table>

### Method setTimeDiscountsForDisplay

```solidity
function setTimeDiscountsForDisplay(
        bytes32 _displayNameHash,
        DiscountUntil[] calldata _discounts
    ) 
       external virtual
       onlyDisplayOwner(_displayNameHash)
```

The method sets time-based discounts that will be applied during the sale of NFTs and wNFTs on the Kiosk. It is possible to configure step-by-step application of discounts. For example, a 10% discount is applicable until 01.01.2024, and a 5% discount is applicable from 01.01.2024 to 01.02.2024. Only the Kiosk owner can invoke this method for their Kiosk.

The method emits a DiscountChanged event for each record in the provided array of time-based discounts, with the following details:

* **The SHA-256 hash** of the Kiosk **name** on which the NFT/wNFT is placed.
* **The discount type**, "TIME," which is a value from the DiscountType enumeration.&#x20;
* **The date** in Unix time format until which the discount is valid.
* **The discount percentage**. For example, 1% would be represented as 100, 20% as 2000, and 100% as 10000.

**Full list of discount types:**&#x20;

* 0 - **promo**-discount (PROMO)&#x20;
* 1 - **referral**-discount (REFERRAL)&#x20;
* 2 - discount by **volume** of purchases (BATCH)&#x20;
* 3 - discount by **time** (TIME)&#x20;
* 4 - discount for members of "**white**-**lists**" (WHITELIST)&#x20;
* 5, 6, 7 - discounts which can be set in the contract price and discount models by the the kiosk owner (CUSTOM1, CUSTOM2, CUSTOM3)

**Incoming parameters for calling the method:**

| Name              | Type             | Description                            |
| ----------------- | ---------------- | -------------------------------------- |
| \_displayNameHash | bytes32          | SHA-256 hash of the Kiosk name         |
| \_discounts       | DiscountUntil\[] | Array with data on temporary discounts |

**DiscountUntil**

| Name      | Type            | Description                                              |
| --------- | --------------- | -------------------------------------------------------- |
| untilDate | uint256         | Date in unixtime format until which the discount applies |
| discount  | KTypes.Discount | Discount data                                            |

**KTypes.Discount:**

| Name        | Type         | Description                                 |
| ----------- | ------------ | ------------------------------------------- |
| dsctType    | DiscountType | The value from discount types enum          |
| dsctPercent | uint16       | Discount size: 100%-10000, 20%-2000, 3%-300 |

### Method editTimeDiscountsForDisplay

```solidity
function editTimeDiscountsForDisplay(
        bytes32 _displayNameHash,
        uint256 _discountIndex,
        DiscountUntil calldata _discount
    )
        external virtual
        onlyDisplayOwner(_displayNameHash)
```

The method updates time-based discount data that will be applied during the sale of NFTs and wNFTs on the Kiosk. Only the Kiosk owner can invoke this method for their Kiosk.

The method emits a **DiscountChanged** event with the following details:

* **The SHA-256 hash** of the Kiosk name on which the NFT/wNFT is placed.
* **The discount type**, a value from the **DiscountType** enumeration.
* **The date** in Unix time format until which the discount is valid.
* **The discount** **percentage**. For example, 1% would be represented as 100, 20% as 2000, and 100% as 10000.

**Incoming parameters for calling the method:**

| Name              | Type          | Description                                                                      |
| ----------------- | ------------- | -------------------------------------------------------------------------------- |
| \_displayNameHash | bytes32       | SHA-256 hash of the Kiosk name                                                   |
| \_discountIndex   | uint256       | The serial number of the record in the array of temporary discounts to be edited |
| \_discounts       | DiscountUntil | Data about the temporary discount. A description of the data type is given above |

### Method setPromoDiscountForDisplay

```solidity
function setPromoDiscountForDisplay(
        bytes32 _displayNameHash,
        bytes32 _promoHash,
        DiscountUntil calldata _discount
    ) 
        external virtual
        onlyDisplayOwner(_displayNameHash) 
```

The method sets discounts based on promo codes that will be applied during the sale of NFTs and wNFTs on the Kiosk. It is possible to create multiple promo codes for the Kiosk. Only the Kiosk owner can invoke this method for their Kiosk.

The method emits a **DiscountChanged** event with the following details:

* **The SHA-256 hash** of the Kiosk name on which the NFT/wNFT is placed.
* **The discount type**, "PROMO," which is a value from the **DiscountType** enumeration.
* **The SHA-256 hash** of the promo-code (words or phrases).
* **The discount percentage**. For example, 1% would be represented as 100, 20% as 2000, and 100% as 10000.

**Incoming parameters for calling the method:**

| Name              | Type          | Description                                                                             |
| ----------------- | ------------- | --------------------------------------------------------------------------------------- |
| \_displayNameHash | bytes32       | SHA-256 hash of the Kiosk name                                                          |
| \_promoHash       | bytes32       | SHA-256 hash of promo-code (words or phrases)                                           |
| \_discounts       | DiscountUntil | Data about the promotional code discount. A description of the data type is given above |

### Method setRefereerDiscountForDisplay

```solidity
function setRefereerDiscountForDisplay(
        bytes32 _displayNameHash,
        address _referrer,
        DiscountUntil calldata _discount
    ) 
        external virtual
        onlyDisplayOwner(_displayNameHash)
```

The method sets discounts based on the refereer address that will be applied during the sale of NFTs and wNFTs on the Kiosk. It is possible to create multiple refereer addresses for the Kiosk. Only the Kiosk owner can invoke this method for their Kiosk.

The method emits a **DiscountChanged** event with the following details:

* **The SHA-256 hash** of the Kiosk name on which the NFT/wNFT is placed.
* **The discount type**, "REFERRAL," which is a value from the **DiscountType** enumeration.
* **The SHA-256 hash** of the refereer address.
* **The discount percentage**. For example, 1% would be represented as 100, 20% as 2000, and 100% as 10000.

**Incoming parameters for calling the method:**

<table><thead><tr><th width="205">Name</th><th width="159.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td>_displayNameHash</td><td>bytes32</td><td>SHA-256 hash of the Kiosk name</td></tr><tr><td>_referrer</td><td>address</td><td>The refereer address which buyers can use to get refereer discount during the purchase</td></tr><tr><td>_discounts</td><td>DiscountUntil</td><td>Data about the refereer discount. A description of the data type is given above</td></tr></tbody></table>

### Method getItemPrices

```solidity
function getItemPrices(
        ETypes.AssetItem memory _assetItem
    ) external view virtual returns (KTypes.Price[] memory)
```

The method returns the price data specified in the Kiosk settings (default prices). If the \_assetItem is a **wNFT**, the method will return all prices for the ERC-20 token being sold (the first token in the wNFT collateral array) as specified in the Kiosk settings. If the \_assetItem is an NFT, the method will return all prices specified in the storefront settings for the NFTs being sold.

**Incoming parameters for calling the method:**

| Name        | Type             | Description                                |
| ----------- | ---------------- | ------------------------------------------ |
| \_assetItem | ETypes.AssetItem | Data on the NFT/wNFT that are being sold.  |

**ETypes.AssetItem**

<table><thead><tr><th width="163">Name</th><th width="181.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td>asset</td><td>ETypes.Asset</td><td>Data about the type and contract of token transferred to the Lunchpad contract</td></tr><tr><td>tokenId</td><td>uint256</td><td>Number of token</td></tr><tr><td>amount</td><td>amount</td><td>Value 0 (zero)</td></tr></tbody></table>

**ETypes.Asset**

<table><thead><tr><th width="184">Name</th><th width="177.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td>assetType</td><td>ETypes.AssetType</td><td>The value from Asset Type enum</td></tr><tr><td>contractAddress</td><td>address</td><td>Thr address of the NFT/wNFT smart contract.</td></tr></tbody></table>

**ETypes.AssetType**: 3 - ERC-721.&#x20;

**Returned values:**

| Name   | Type            | Description                                                                     |
| ------ | --------------- | ------------------------------------------------------------------------------- |
| prices | KTypes.Price\[] | Array with prices for NFT/wNFT. The description of the data type is given above |

### Method getDefaultDisplayPrices

```solidity
function getDefaultDisplayPrices(
        ETypes.AssetItem memory _assetItem
    ) public view virtual returns (KTypes.Price[] memory _prices)
```

The method returns data about prices specified in the Kiosk settings for sold nfts (regular NFTs).

**Incoming parameters for calling the method:**

| Name        | Type             | Description                                                                   |
| ----------- | ---------------- | ----------------------------------------------------------------------------- |
| \_assetItem | ETypes.AssetItem | Data on the NFT that is being sold. A description of the type was given above |

**Returned values:**

| Name   | Type            | Description                                                                |
| ------ | --------------- | -------------------------------------------------------------------------- |
| prices | KTypes.Price\[] | Array with prices for NFT. The description of the data type is given above |

### Method getDisplayTimeDiscounts

```solidity
function getDisplayTimeDiscounts(
        bytes32 _displayNameHash
    ) public view virtual returns (DiscountUntil[] memory)
```

The method returns data about temporary discounts set for the Kiosk.

**Incoming parameters for calling the method:**

| Name              | Type    | Description                    |
| ----------------- | ------- | ------------------------------ |
| \_displayNameHash | bytes32 | SHA-256 hash of the Kiosk name |

**Returned values:**

| discounts | DiscountUntil\[] | Array with data about temporary discounts for NFT/wNFT. The description of the data type is given above |
| --------- | ---------------- | ------------------------------------------------------------------------------------------------------- |

### Method getItemDiscounts

```solidity
function getItemDiscounts(
        ETypes.AssetItem memory _assetItem,
        address _buyer,
        address _referrer,
        bytes32 _promoHash
    ) public view virtual returns (KTypes.Discount[] memory)
```

The method returns discount data for an NFT/wNFT that will be applied during its sale.&#x20;

**IMPORTANT**: In this example of the price and discount contract, this method always returns an array of three records. The first record contains information about the time-based discount, the second record contains information about the promo-code discount, and the third record contains information about the referral discount. The Kiosk owner is allowed to develop their own price and discount contract and modify the algorithm of this method.

**Incoming parameters for calling the method:**

| Name        | Type             | Description                                                                        |
| ----------- | ---------------- | ---------------------------------------------------------------------------------- |
| \_assetItem | ETypes.AssetItem | Data on the NFT/wNFT that is being sold. A description of the type was given above |
| \_buyer     | address          | Address of the recipient of the being purchased NFT/wNFT                           |
| \_referrer  | address          | Referral address, which is added by the Kiosk owner in the Kiosk settings          |
| \_promo     | string           | Promo-code added by the Kiosk owner in the Kiosk settings                          |

**Returned values:**

| Name     | Type               | Description                                                                                                                                        |
| -------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| discount | KTypes.Discount\[] | Array with data on discounts that apply to the given NFT/wNFT, taking into account the data passed to the method about the promo code and referral |

### Method getBatchPrices

```solidity
function getBatchPrices(
        ETypes.AssetItem[] memory _assetItemArray
    ) external view virtual returns (KTypes.Price[] memory)
```

The method can return an array of prices for the NFT/wNFT array. The method is for the case when the user buys several NFT/wNFT and a discount for the volume of purchases should be applied. The logic of the method is not implemented in this contract of prices and discounts.

**Incoming parameters for calling the method:**

| Name        | Type                | Description                                                                                           |
| ----------- | ------------------- | ----------------------------------------------------------------------------------------------------- |
| \_assetItem | ETypes.AssetItem\[] | An array of NFT/wNFT data for which prices are requested. The description of the type was given above |

**Returned values:**

| prices | KTypes.Price\[] | Array with data on prices that apply to the **passed** NFT/wNFT to method |
| ------ | --------------- | ------------------------------------------------------------------------- |

### Method getBatchDiscounts

```solidity
function getBatchDiscounts(
        ETypes.AssetItem[] memory _assetItemArray,
        address _buyer,
        address _referrer,
        bytes32 _promoHash
    ) external view virtual returns (KTypes.Discount[] memory)
```

The method can return an array of discounts for an array of NFTs/wNFTs. This method is used when a user **purchases** multiple NFTs/wNFTs and a volume discount should be applied. The logic for this method is not implemented in this price and discount contract.

**Incoming parameters for calling the method:**

| Name        | Type                | Description                                                                                              |
| ----------- | ------------------- | -------------------------------------------------------------------------------------------------------- |
| \_assetItem | ETypes.AssetItem\[] | An array of NFT/wNFT data for which discounts are requested. The description of the type was given above |
| \_buyer     | address             | Address of the recipient of the being purchased NFT/wNFT                                                 |
| \_referrer  | address             | Referral address, which is added by the Kiosk owner in the Kiosk settings                                |
| \_promo     | string              | Promo-code added by the Kiosk owner in the Kiosk settings                                                |

**Returned values:**

| Name      | Type               | Description                                                                                                                                 |
| --------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| discounts | KTypes.Discount\[] | Array with data about discounts, which are applied to the passed NFT/wNFT to method, taking into account data about promo code and referral |

### Method getCollateralUnitPrice

```solidity
function getCollateralUnitPrice(
        bytes32 _displayNameHash, 
        address _erc20
    ) external view returns(KTypes.DenominatedPrice[] memory)
```

The method returns prices per unit of ERC-20 token being sold in the Kiosk.

**Incoming parameters for calling the method:**

| Name              | Type    | Description                                                               |
| ----------------- | ------- | ------------------------------------------------------------------------- |
| \_displayNameHash | bytes32 | SHA-256 hash of the Kiosk name                                            |
| \_erc20           | address | Address of the smart-contract of the ERC-20 token being sold in the Kiosk |

**Returned values:**

| Name   | Type                       | Description                                                               |
| ------ | -------------------------- | ------------------------------------------------------------------------- |
| prices | KTypes.DenominatedPrice\[] | An array with price data. The description of the data type is given above |
