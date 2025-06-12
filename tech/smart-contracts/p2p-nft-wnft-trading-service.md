# P2P NFT/wNFT trading service

This is the group of the smart contracts which give the opportunity to sell and buy NFTs and wNFTs ERC721. There are two smart contracts: P2POrderManager.sol and OrderBook721.sol.

The first one responses for the actions, the second one responses for the storing the informations about the orders. There are sell orders and buy offers. The owners of NFTs/wNFTs can create the sell orders only. The buyers can create offers to buy any NFTs/wNFTs. The sell orders can be created with the native and ERC20 tokens as the price. The buy offers can be created with ERC20 tokens as the price only. The sellers of NFTs/wNFTs should give the allowance to **P2POrderManager** to use them. The buyers of NFTs/wNFTs and creators of the buy offers should give the allowance to **P2POrderManager** to use their ERC20 tokens to pay.

## P2POrderManager

### Method makeOrder

```solidity
function makeOrder(
        ET.AssetItem memory _assetItem,
        ET.Price calldata _price,
        ET.OrderType _ordeType
    ) external returns (bytes32 orderId)
```

The method creates the orders.

**Input parameters of the method:**

<table><thead><tr><th width="148">Name</th><th width="149">Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>_assetItem</strong></td><td><strong>ET.AssetItem</strong></td><td>The data about NFT/wNFT. The type description is above. Github link of the <a href="https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol">library</a></td></tr><tr><td><strong>_price</strong></td><td><strong>ET.Price</strong></td><td>The data about a price. The type description is above. Github link of the <a href="https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol">library</a></td></tr><tr><td><strong>_orderType</strong></td><td><strong>ET.OrderType</strong></td><td>Order type. There two types of orders: Sell, Buy. This is enum from ET library - enum OrderType {SELL, BUY}. Github link of the <a href="https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol">library</a></td></tr></tbody></table>

**ET.AssetItem**

<table><thead><tr><th width="126.33333333333331">Name</th><th width="102">Type</th><th>Description</th></tr></thead><tbody><tr><td><strong>asset</strong></td><td><strong>ET.Asset</strong></td><td>Data on the type and contract of tradable NFT/wNFT tokens</td></tr><tr><td><strong>tokenId</strong></td><td><strong>uint256</strong></td><td>Token number</td></tr><tr><td><strong>amount</strong></td><td><strong>amount</strong></td><td>Number of NFT/wNFT copies. Zero value</td></tr></tbody></table>

**ET.Asset**

| Name                | Type             | Type                                      |
| ------------------- | ---------------- | ----------------------------------------- |
| **assetType**       | **ET.AssetType** | Value from the type dictionary            |
| **contractAddress** | **address**      | Address of the tradable NFT/wNFT contract |

#### **ET.AssetType:**

* 3 - ERC-721;

**ET.Price**

| Name          | Type        | Description                                                                                               |
| ------------- | ----------- | --------------------------------------------------------------------------------------------------------- |
| **payToken**  | **address** | The smart contract address of the price token. If the price is in the native tokens fill in zero address. |
| **payAmount** | **uint256** | The token amount of the price.                                                                            |

**The method returns values:**

| Name        | Type        | Description          |
| ----------- | ----------- | -------------------- |
| **orderId** | **bytes32** | The created order id |

The method emits **EnvelopP2PNewOrder** event with the follow data:

| Name             | Type        | Description                                                                                                    |
| ---------------- | ----------- | -------------------------------------------------------------------------------------------------------------- |
| **OrderId**      | **bytes32** | The created order id                                                                                           |
| **OrderMaker**   | **address** | The creator of the order                                                                                       |
| **AssetAddress** | **address** | The smart contract address of tradable NFT/wNFT                                                                |
| **TokenId**      | **uint256** | The token id of tradable NFT/wNFT                                                                              |
| **AssetAmount**  | **uint256** | The copy amount of NFT/wNFT tokens. For ERC721 is zero                                                         |
| **PayToken**     | **address** | The smart contract address of the price token. If the price is in the native tokens the value is zero address. |
| **PayAmount**    | **uint256** | The token amount of the price.                                                                                 |
| **OrderType**    | **uint8**   | The id of the order type from enum ET. OrderType                                                               |

### Method removeOrder

```solidity
function removeOrder(
        bytes32  _orderId,
        ET.AssetItem memory _assetItem
    ) external returns(bool deleted)
```

The method removes the orders.

**Input parameters of the method:**

| Name            | Type             | Description                                                                                                                                                              |
| --------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **\_orderId**   | **bytes32**      | The id of the order which will be removed.                                                                                                                               |
| **\_assetItem** | **ET.AssetItem** | The data about NFT/wNFT. The type description is above. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |

**The method returns values:**

| Name        | Type     | Description                    |
| ----------- | -------- | ------------------------------ |
| **deleted** | **bool** | The flag the order is deleted. |

The method emits **EnvelopOrderRemoved** event with the follow data:

| Name             | Type        | Description                                            |
| ---------------- | ----------- | ------------------------------------------------------ |
| **OrderId**      | **bytes32** | The removed order id                                   |
| **AssetAddress** | **address** | The smart contract address of tradable NFT/wNFT        |
| **TokenId**      | **uint256** | The token id of tradable NFT/wNFT                      |
| **AssetAmount**  | **uint256** | The copy amount of NFT/wNFT tokens. For ERC721 is zero |
| **OrderType**    | **uint8**   | The id of the order type from enum ET.OrderType        |

### Method takeOrder

```solidity
function takeOrder(
        bytes32  _orderId, 
        address _orderBook,
        ET.OrderType _orderType,
        ET.AssetItem memory _assetItem
    ) 
        external 
        payable
```

The method marks the orders like closed and run the changing by the assets between the seller and the buyer. If the owner of **P2POrderManager** smart contract set the fee for the deal this method would charge the fee from the payment asset and make the transfer to fee beneficiary address. If

**Input parameters of the method:**

| Name            | Type             | Description                                                                                                                                                                                                                   |
| --------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_orderId**   | **bytes32**      | The order id which will be closed.                                                                                                                                                                                            |
| **\_orderBook** | **address**      | The address of OrderBook721 smart contract where info about the order is storing                                                                                                                                              |
| **\_orderType** | **ET.OrderType** | Order type. There two types of orders: Sell, Buy. This is enum from ET library - enum OrderType {SELL, BUY}. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |
| **\_assetItem** | **ET.AssetItem** | The data about NFT/wNFT.  The type description is above. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol)                                                     |

The method emits **EnvelopP2POrderTaked** event with the follow data:

| Name             | Type        | Description                                                                                                    |
| ---------------- | ----------- | -------------------------------------------------------------------------------------------------------------- |
| **AssetAddress** | **address** | The smart contract address of tradable NFT/wNFT                                                                |
| **TokenId**      | **uint256** | The token id of tradable NFT/wNFT                                                                              |
| **OrderId**      | **bytes32** | The closed order id                                                                                            |
| **OrderMaker**   | **address** | The creator of the order                                                                                       |
| **OrderTaker**   | **address** | The user who closed the order                                                                                  |
| **PayToken**     | **address** | The smart contract address of the price token. If the price is in the native tokens the value is zero address. |
| **PayAmount**    | **uint256** | The token amount of the price.                                                                                 |
| **OrderType**    | **uint8**   | The id of the order type from enum ET. OrderType                                                               |

### Method getOrdersForItem

```solidity
function getOrdersForItem(ET.AssetItem memory _assetItem) 
        external view returns(ET.Order[] memory orderList) 
```

This view method returns the information about all existing orders for the tradable asset.

**Input parameters of the method:**

| Name            | Type             | Description                                                                                                                                                              |
| --------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **\_assetItem** | **ET.AssetItem** | The data about NFT/wNFT. The type description is above. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |

**The method returns values:**

| Name          | Type            | Description                                                                                                                                                                                    |
| ------------- | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **orderList** | **ET.Order\[]** | The array of the records with the information about the every existing order. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |

### ET.Order

| Name                  | Type        | Description                                                                                                                                                             |
| --------------------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **orderId**           | **bytes32** | The order id                                                                                                                                                            |
| **orderType**         | **uint8**   | The id of the order type from enum ET. OrderType                                                                                                                        |
| **orderBook**         | **address** | The address of OrderBook721 smart contract where info about the order is storing                                                                                        |
| **orderMaker**        | **address** | The creator of the order                                                                                                                                                |
| **amount**            | **uint256** | The copy amount of NFT/wNFT tokens. For ERC721 is zero                                                                                                                  |
| **Price**             | **price**   | The data about a price. The type description is above. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |
| **assetApproveExist** | **bool**    | The flag there is the allowance for P2POrderManager smart contract to use the assets of the order maker (NFT/wNFT or ERC20 tokens)                                      |

## OrderBook721

### Method getOrdersForItem

```solidity
function getOrdersForItem(ET.AssetItem memory _assetItem) 
        external 
        view 
        returns(ET.Order[] memory orderList) 
```

This view method returns the information about all existing orders for the tradable asset.

#### **Input parameters of the method:**

| Name            | Type             | Description                                                                                                                                                              |
| --------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **\_assetItem** | **ET.AssetItem** | The data about NFT/wNFT. The type description is above. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |

**The method returns values:**

| Name          | Type            | Description                                                                                                                                                                                                                   |
| ------------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **orderList** | **ET.Order\[]** | The array of the records with the information about the every existing order. The type description is above. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |

### Method getPriceForOrder

```solidity
function getPriceForOrder(
        bytes32  _orderId,
        ET.OrderType _orderType,
        ET.AssetItem memory _assetItem
    ) 
        external view returns(ET.Price memory pr, address payer, address maker) 
```

The method returns the information about the orders.

**Input parameters of the method:**

| Name            | Type             | Description                                                                                                                                                                           |
| --------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_orderId**   | **bytes32**      | The id of the order for which user asks the price information.                                                                                                                        |
| **\_orderType** | **ET.OrderType** | The id of the order type from enum ET. OrderType                                                                                                                                      |
| **\_assetItem** | **ET.AssetItem** | The data about NFT/wNFT of the order. The type description is above. Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |

**The method returns values:**

| Name      | Type         | Description                                                                                                                                                                           |
| --------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **pr**    | **ET.Price** | The data about a price of the order. The type description is above.  Github link of the [library](https://github.com/dao-envelop/envelop-protocol-v2/blob/master/src/utils/LibET.sol) |
| **payer** | **address**  | For sell order – zero address. For buy order – the order creator                                                                                                                      |
| **maker** | **address**  | For sell order – the owner of tradable asset (NFT/wNFT). For buy order – the order creator                                                                                            |

\
