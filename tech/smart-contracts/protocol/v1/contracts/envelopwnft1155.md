# EnvelopwNFT1155

This contract is based on the classic ERC-1155 standard token contract. A detailed description of the methods of the standard can be found in the documentation ([https://docs.openzeppelin.com/contracts/4.x/api/token/erc1155](https://docs.openzeppelin.com/contracts/4.x/api/token/erc1155)). The contract is used for minting, burning and wNFT ERC-1155 transfers that the **WrapperBaseV1** protocol contract creates for users.

The mint, burn methods are defined in the EnvelopwNFT1155 contract, taking into account the logic of the protocol.

The mint, burn method can only call the WrapperBaseV1 contract. No other address can call these methods.

### Method wnftInfo&#x20;

```solidity
function wnftInfo(uint256 tokenId) external view returns (ETypes.WNFT memory)
```

The method returns all data about wNFT.

**Input method call parameters:**

| Name          | Type        | Description          |
| ------------- | ----------- | -------------------- |
| **\_tokenId** | **uint256** | **tokenId wrap NFT** |

A description of the returned data types can be found in the **LibEnvelopTypes.sol** contact, ETypes library.

**Returned values:**

| Name      | Type        | Description |
| --------- | ----------- | ----------- |
| **value** | ETypes.WNFT | wNFT data   |

**ETypes.WNFT**

| Name                  | Type                | Description                                                                                                                                                                                                                                                                                                                             |
| --------------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **inAsset**           | ETypes.AssetItem    | Data on the original NFT                                                                                                                                                                                                                                                                                                                |
| **collateral**        | ETypes.AssetItem\[] | Data on collateral                                                                                                                                                                                                                                                                                                                      |
| **unWrapDestination** | address             | Recipient address of the original NFT and collateral after unwrap of wNFT - filled by default with a null address                                                                                                                                                                                                                       |
| **fees**              | ETypes.Fee\[]       | Array of information on transfer fees                                                                                                                                                                                                                                                                                                   |
| **locks**             | ETypes.Lock\[]      | Array of information on unwrap conditions (blocking by time, by amount of commission collected, etc...)                                                                                                                                                                                                                                 |
| **royalties**         | ETypes.Royalty\[]   | An array of information on royalty beneficiaries                                                                                                                                                                                                                                                                                        |
| **rules**             | bytes2              | <p>wNFT rules of conduct (e.g. 1111, where right to left<strong>:</strong></p><p><strong>pos1</strong> - prohibition to unwrap</p><p><strong>pos2</strong> - prohibition to wrap wNFT </p><p><strong>pos3</strong> - prohibition to transfer (send) wNFT </p><p><strong>pos4</strong> - prohibition to add something to collateral)</p> |

**ETypes.AssetItem**

| Name        | Type         | Description                                                                                                                                                                                                                          |
| ----------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **asset**   | ETypes.Asset | Data on the type and contract of tokens transferred to the WrapperBaseV1 contract for wrapped NFT or added to collateral of wrapped NFT                                                                                              |
| **tokenId** | uint256      | <p>Token number </p><p>(if a empty was wrapped</p><p>it will return 0;</p><p>if the collateral was topped up with ERC-20 tokens, it will return 0; </p><p>if the collateral was topped up with native tokens, it will return 0).</p> |
| **amount**  | amount       | <p>Number of NFT copies or number of tokens( for ERC-1155 - a value other than 0, for ERC-20 - value other than 0 </p><p>for native tokens - value other than 0 </p><p>for ERC-721 - 0)</p>                                          |

**ETypes.Asset**

| Name                | Type            | Description                                                                                          |
| ------------------- | --------------- | ---------------------------------------------------------------------------------------------------- |
| **assetType**       | contractAddress | Value from the token type dictionary                                                                 |
| **contractAddress** | address         | Address of token contract transferred to WrapperBaseV1 protocol contract as security or original NFT |

ETypes.AssetType:&#x20;

* 0 - **empty;**
* 1 - **native** **token** (coin);
* 2 - ERC-20;
* 3 - ERC-1155;
* 4 - ERC-1155.

**ETypes.Fee**

| Name        | Type    | Description                         |
| ----------- | ------- | ----------------------------------- |
| **feeType** | bytes1  | Fee type - 0                        |
| **param**   | uint256 | Fee amount                          |
| **token**   | address | Transfer fee token contract address |

**ETypes.Lock**

| Name         | Type    | Description                                                                                                                                                                 |
| ------------ | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **lockType** | bytes1  | <p>Blocking type: </p><p>0x00 - blocking by time </p><p>0x01 - blocking by volume of accumulated transfer fee for wNFT<br>0x02 - count of max collateral slots for wNFT</p> |
| **param**    | uint256 | Value                                                                                                                                                                       |

**ETypes.Royalty**

| Name            | Type    | Description                       |
| --------------- | ------- | --------------------------------- |
| **beneficiary** | address | Royalty beneficiary address       |
| **percent**     | uint16  | Value - no more than 10000 (100%) |

### Method URI

```solidity
function uri(uint256 _tokenID) public view override 
        returns (string memory _uri) 
```

Method returns reference to metadata of original NFT for wNFT. If empty, the metadata generated by the **EnvelopwNFT1155** contract will be returned.

**Input method call parameters:**

| Name          | Type    | Description  |
| ------------- | ------- | ------------ |
| **\_tokenId** | uint256 | tokenId wNFT |

**Returned values:**

| Name      | Type   | Description      |
| --------- | ------ | ---------------- |
| **uri\_** | string | Link to metadata |

### Method safeTransferFrom

The method works based is based on the ERC-1155 method. Link to documentation ([https://docs.openzeppelin.com/contracts/4.x/api/token/erc1155#IERC1155-safeTransferFrom-address-address-uint256-uint256-bytes-](https://docs.openzeppelin.com/contracts/4.x/api/token/erc1155#IERC1155-safeTransferFrom-address-address-uint256-uint256-bytes-)).&#x20;

When a transfer is made, the transfer fee is calculated if the creator of wNFT has made the appropriate settings for it. The fee is held in ERC-20 tokens whose smart-contract address **the wNFT creator** has specified when he wrapped. The fee can be allocated to royalty beneficiaries, or part or all of the fee can be added to wNFT's Collateral.

The method does not return anything.

**Input method call parameters:**

| Name       | Type    | Description                                                       |
| ---------- | ------- | ----------------------------------------------------------------- |
| **from**   | address | Address from which wNFT is being transferred                      |
| **to**     | address | The address to which the wNFT is transferred                      |
| **id**     | uint256 | tokenId wNFT                                                      |
| **amount** | uint256 | Number of copies-**amount** to be transferred from address **to** |
| **data**   | bytes   | Data                                                              |
