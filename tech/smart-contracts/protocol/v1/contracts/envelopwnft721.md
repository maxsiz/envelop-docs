# EnvelopwNFT721

This contract is based on the classic ERC-721 standard token contract. A detailed description of the methods of the standard can be found in the documentation: [https://docs.openzeppelin.com/contracts/4.x/api/token/erc721](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721).&#x20;

The contract is used for mint, burn and wNFT ERC-721 transfers that the WrapperBaseV1 protocol contract creates for users. The mint, burn methods are defined in the EnvelopwNFT721 contract, taking into account the logic of the protocol. Only the WrapperBaseV1 contract can call the mint, burn methods. No other address can call these methods.

### Method **wnftInfo**

```solidity
function wnftInfo(uint256 tokenId) external view returns (ETypes.WNFT memory)
```

The method returns all data about wNFT.

**Input method call parameters:**

| Name          | Type        | Description                |
| ------------- | ----------- | -------------------------- |
| **\_tokenId** | **uint256** | tokenId of the wrapped NFT |

A description of the returned data types can be found in the LibEnvelopTypes.sol contact, ETypes library.

**Returned values:**

| Name      | Type            | Description       |
| --------- | --------------- | ----------------- |
| **value** | **ETypes.WNFT** | Wrapped wNFT data |

**ETypes.WNFT**

| Name                  | Type                    | Description                                                                                                                                                                                                                                  |
| --------------------- | ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **inAsset**           | **ETypes.AssetItem**    | Data on the original NFT                                                                                                                                                                                                                     |
| **collateral**        | **ETypes.AssetItem\[]** | Data on collateral                                                                                                                                                                                                                           |
| **unWrapDestination** | **address**             | Recipient address of the original NFT and collateral after unwrap of wNFT - filled by default with a null address                                                                                                                            |
| **fees**              | **ETypes.Fee\[]**       | Array of information on transfer fees                                                                                                                                                                                                        |
| **locks**             | **ETypes.Lock\[]**      | Array of information on unwrap conditions (blocking by time, by amount of fees collected, etc ...)                                                                                                                                           |
| **royalties**         | **ETypes.Royalty\[]**   | An array of information on royalty beneficiaries                                                                                                                                                                                             |
| **rules**             | **bytes2**              | <p>wNFT rules of conduct (e.g. 1111, where right to left <br>pos1 - prohibition to unwrap</p><p> pos2 - prohibition to reverse wNFT </p><p>pos3 - prohibition to transfer wNFT </p><p>pos4 - prohibition to add something to collateral)</p> |

**ETypes.AssetItem**

| Name        | Type             | Description                                                                                                                                                                                                                          |
| ----------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **asset**   | **ETypes.Asset** | Data on the type and contract of tokens transferred to the WrapperBaseV1 contract for wrapped NFT or added to collateral of wrapped NFT                                                                                              |
| **tokenId** | **uint256**      | <p>Token number </p><p>(if a empty was wrapped</p><p>it will return 0;</p><p>if the collateral was topped up with ERC-20 tokens, it will return 0; </p><p>if the collateral was topped up with native tokens, it will return 0).</p> |
| **amount**  | **amount**       | <p>Number of NFT copies or number of tokens( for ERC-1155 - a value other than 0, for ERC-20 - value other than 0 </p><p>for native tokens - value other than 0 </p><p>for ERC-721 - 0)</p>                                          |

**ETypes.Asset**

| Name                | Type                 | Description                                                                                                |
| ------------------- | -------------------- | ---------------------------------------------------------------------------------------------------------- |
| **assetType**       | **ETypes.AssetType** | Value from the token type dictionary                                                                       |
| **contractAddress** | **address**          | Address of token contract transferred to WrapperBaseV1 protocol contract as **collateral** or original NFT |

**ETypes.AssetType**:&#x20;

* 0 - empty&#x20;
* 1 - native token&#x20;
* 2 - ERC-20&#x20;
* 3 - ERC-721&#x20;
* 4 - ERC-1155

**ETypes.Fee**

| Name        | Type        | Description                         |
| ----------- | ----------- | ----------------------------------- |
| **feeType** | **bytes1**  | Fee type - 0                        |
| **param**   | **uint256** | Amount of fee                       |
| **token**   | **address** | Transfer fee token contract address |

**ETypes.Lock**

| Name         | Type        | Description                                                                                                                                                                 |
| ------------ | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **lockType** | **bytes1**  | <p>Blocking type: </p><p>0x00 - blocking by time </p><p>0x01 - blocking by volume of accumulated transfer fee for wNFT<br>0x02 - count of max collateral slots for wNFT</p> |
| **param**    | **uint256** | Value                                                                                                                                                                       |

**ETypes.Royalty**

| Name            | Type        | Description                       |
| --------------- | ----------- | --------------------------------- |
| **beneficiary** | **address** | Royalty beneficiary address       |
| **percent**     | **uint16**  | Value - no more than 10000 (100%) |

### **Method tokenURI**

```solidity
function tokenURI(uint256 _tokenId) public view override returns (string memory _uri)
```

Method returns reference to metadata of original NFT for wNFT. If a empty was wrapped, the metadata generated by the EnvelopwNFT721 contract will be returned.

**Input method call parameters:**

| Name          | Type        | Description     |
| ------------- | ----------- | --------------- |
| **\_tokenId** | **uint256** | tokenId wrapNFT |

**Returned values:**

| Name      | Type       | Description      |
| --------- | ---------- | ---------------- |
| **uri\_** | **string** | Link to metadata |

### TransferFrom method&#x20;

The method works based on the ERC-721 method. Link to documentation ([https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#IERC721-transferFrom-address-address-uint256-](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#IERC721-transferFrom-address-address-uint256-)) When a transfer is made, a transfer fee is calculated if the creator of wNFT has made the appropriate settings for it. The fee is held in ERC-20 tokens whose smart contract address the creator of wNFT specified when he wrapped. The fee can be allocated to royalty beneficiaries, or part or all of the fee can be added to wNFT's collateral.

The method does not return anything.

**Input method call parameters:**

| Name        | Type        | Description                                  |
| ----------- | ----------- | -------------------------------------------- |
| **from**    | **address** | Address from which wNFT is being transferred |
| **to**      | **address** | The address to which the wNFT is transferred |
| **tokenId** | **uint256** | tokenId wNFT                                 |
