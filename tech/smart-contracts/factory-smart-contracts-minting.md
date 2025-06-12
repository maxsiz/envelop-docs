# Factory (smart-contracts) minting

**Smart-сontract Architecture dAPP Factory** for creating **customized** **NFT**-collection contracts:&#x20;

* **UserCollectionPRegistry** is the contract accessed by users to deploy a customized NFT collection proxy contract of ERC-721 or ERC-1155 tokens to themselves on the blockchain.&#x20;
* **UserCollectionPRegistry** checks the relevance/validity of the subscription and call the _UsersCollectionFactory_ contract to deploy the collection proxy-contract to the user (the user will be the **owner** of the proxy-contract).&#x20;
* **UsersCollectionFactory** smart-contract deploys the _UserCollectionProxy_ contract on the blockchain for a collection of ERC-721 or ERC-1155 (NFTs) for the user.&#x20;
* **UserCollectionProxy** smart-contract is a proxy contract that **calls** the methods of _logical contracts_, but stores changes to the proxy contract's state variables. dApp can create two types of proxy contracts: proxy-contracts for the _PublicUsersCollection721BehindProxy_ logical contract and _PublicUsersCollection1155BehindProxy_.&#x20;
* **PublicUsersCollection721BehindProxy** smart-contract is a logical smart-contract (implementation) of ERC-721 tokens whose methods proxy contracts use.&#x20;
* **PublicUsersCollection1155BehindProxy** smart-contract is a logical smart-contract (implementation) of ERC-1155 tokens whose methods proxy contracts use.

The dApp architecture for proxy contracts is based on **EIP-1967**, which you can read more about here: [https://eips.ethereum.org/EIPS/eip-1967](https://eips.ethereum.org/EIPS/eip-1967).

Proxy contracts do not have the ability to change the logical smart-contract and use methods of new logical smart-contract. **Only the owner of a proxy-contract** can call "mint NFT" method of it.&#x20;

## UserCollectionPRegistry.sol

### Method deployNewCollection

```solidity
function deployNewCollection(
        address _implAddress, 
        address _creator,
        string memory name_,
        string memory symbol_,
        string memory _baseurl
    ) external
```

The method **calls** the **UsersCollectionFactory** contract to **deploy** the **UserCollectionProxy** proxy-contract in the blockchain. Only a user with a valid subscription can call the method. It is purchased from agents selling subscriptions to the services of this dApp.

**Input parameters of the method for calling:**

<table><thead><tr><th>Name</th><th>Type</th><th>Description </th><th data-hidden>Type</th><th data-hidden>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>_implAddress</td><td>address</td><td>Address of the logical smart-contract</td><td>address</td><td>Address of the logical smart-contract</td><td></td></tr><tr><td>_creator</td><td>address</td><td>The address that will own the proxy-contract</td><td>address</td><td>The address that will own the proxy-contract</td><td></td></tr><tr><td>name_</td><td>string</td><td>Name of NFT-collection</td><td>string</td><td>Name of the NFT-collection</td><td></td></tr><tr><td>symbol_</td><td>string</td><td>Abbreviation of the NFT -collection, e.g.: ELEM</td><td>string</td><td>Abbreviation of the NFT -collection, e.g.: ELEM</td><td></td></tr><tr><td>_baseurl</td><td>string</td><td>Part of the metadata reference for NFT that do not have personal metadata</td><td>string</td><td>Part of the metadata reference for NFT that do not have personal metadata</td><td></td></tr></tbody></table>

The method emits an **Initialized** event specifying the address of the proxy-contract deployed in the blockchain.

### Method getSupportedImplementation

```solidity
function getSupportedImplementation() external view returns(Asset[] memory) 
```

The method returns an array of data about logical smart-contracts for which proxy-contracts can be **deployed** on the blockchain.

**The method returns values:**

<table><thead><tr><th width="161.33333333333331">Name</th><th width="142">Type</th><th>Description</th></tr></thead><tbody><tr><td>supportedImplementations</td><td>Asset[]</td><td>Array of data about logical-smart contracts for which proxy-contracts can be <strong>deployed</strong> on the blockchain</td></tr></tbody></table>

**Asset**:

| Name            | Type      | Description                               |
| --------------- | --------- | ----------------------------------------- |
| assetType       | AssetType | Value from the token type data dictionary |
| contractAddress | address   | Address of the logical smart-contract     |

**AssetType:**&#x20;

* 3 - ERC-721&#x20;
* 4 - ERC-1155

### Method getUsersCollections

```solidity
function getUsersCollections(address _user) external view returns(Asset[] memory)
```

The method returns an array of data about the proxy-contracts that belong to the user.

**Input parameters of the method for calling:**

| Name   | Type    | Description                                                                                                     |
| ------ | ------- | --------------------------------------------------------------------------------------------------------------- |
| \_user | address | The address of the user for whom the **array** of proxy contracts deployed in the blockchain is being requested |

**The method returns values:**

| Name   | Type     | Description                                                                                                 |
| ------ | -------- | ----------------------------------------------------------------------------------------------------------- |
| assets | Asset\[] | Array of data about proxy-contracts owned by the user. The **description** of the data type is given above. |

### Method isImplementationSupported

```solidity
function isImplementationSupported(address _impl) public view  returns(bool isSupported, uint256 index)
```

The method returns the result of checking whether a smart contract is included in the list of available logical smart-contracts for which a proxy contract can be deployed.

**Input parameters of the method for calling:**

| Name   | Type    | Description                                                            |
| ------ | ------- | ---------------------------------------------------------------------- |
| \_impl | address | Address of the logical smart-contract for which the check is performed |

**The method returns values:**

| Name        | Type    | Description                                                                                                                        |
| ----------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| isSupported | bool    | Boolean value. Flag whether it is possible to **deploy** a proxy-contract on the blockchain for a logical smart-contract.          |
| index       | uint256 | Order number from the array of available logical smart-contracts for which a proxy-contract can be **deployed** on the blockchain. |

### Method checkUserSubscription&#x20;

```solidity
function checkUserSubscription(address _user) 
            external 
            view 
            returns (bool ok, bool needFix)
```

The method checks the activity of a **subscription** purchased by the user, which allows the user to deploy a proxy-contract in the blockchain.

A detailed description of the method operation is given in the documentation describing the operation of the subscription service, which can be found here: [https://docs.envelop.is/tech/smart-contracts/subscription-service#method-\_checkusersubscription](https://docs.envelop.is/tech/smart-contracts/subscription-service#method-_checkusersubscription).

**Input parameters of the method for calling:**

| Name   | Type    | Description                                                                          |
| ------ | ------- | ------------------------------------------------------------------------------------ |
| \_user | address | The address of the user for whom the subscription **activity** is being **checked**. |

**The method returns values:**

<table><thead><tr><th width="146.33333333333331">Name</th><th width="119">Type</th><th>Description</th></tr></thead><tbody><tr><td>ok</td><td>bool</td><td>Boolean value. <strong>True</strong> - the subscription is still valid, active. <strong>False</strong> - subscription is not valid, inactive.</td></tr><tr><td>needFix</td><td>bool</td><td>Boolean value. <strong>True</strong> - for subscriptions at the tariff (rate) with the volume of use of provider's services (an indication that the volume available to the user should be reduced each time the subscription is used). <strong>False</strong> - always for tariff (rate) subscriptions with validity period.</td></tr></tbody></table>

## UsersCollectionFactory

### Method deployProxyFor

```solidity
function deployProxyFor(
        address _implAddress, 
        address _creator,
        string memory name_,
        string memory symbol_,
        string memory _baseurl
    ) public returns(address proxy) 
```

The method deploys the **UserCollectionProxy** contract in the blockchain for the user. Only a "trusted" user can call the method.

**Input parameters of the method for calling:**

<table><thead><tr><th width="170.33333333333331">Name</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>_implAddress</td><td>address</td><td>Address of the logical smart-contract.</td></tr><tr><td>_creator</td><td>address</td><td>The address that will own the proxy-contract.</td></tr><tr><td>name_</td><td>string</td><td>Name of the NFT-collection.</td></tr><tr><td>symbol_</td><td>string</td><td>Abbreviation of the NFT-collection, e.g.: ELEM.</td></tr><tr><td>_baseurl</td><td>string</td><td>Part of the metadata reference for NFTs that do not have personal metadata</td></tr></tbody></table>

**The method returns values:**

| Name  | Type    | Description                                               |
| ----- | ------- | --------------------------------------------------------- |
| proxy | address | Address of the proxy-contract deployed in the blockchain. |

## UserCollectionProxy

The contract has **no** public methods. The contract "constructor" method emits an **Upgraded** event specifying: **address of the proxy-contract** deployed in the blockchain.

## PublicUsersCollection721BehindProxy&#x20;

The contract inherits the **ERC721EnumerableUpgradeable** contract from the OpenZeppelin library. A description of the contract can be found here: [https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#ERC721Enumerable](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#ERC721Enumerable).

## PublicUsersCollection1155BehindProxy

The contract inherits the ERC1155URIStorageUpgradeable contract from the OpenZeppelin library. A description of the contract can be found here: [https://docs.openzeppelin.com/contracts/4.x/api/token/erc1155#ERC1155URIStorage](https://docs.openzeppelin.com/contracts/4.x/api/token/erc1155#ERC1155URIStorage).
