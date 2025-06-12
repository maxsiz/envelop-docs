# AdvancedWhiteList.sol

This contract is used by the WrapperBaseV1 protocol contract to manage the white and black list of tokens and to retrieve data from them.&#x20;

There is a whitelist of contract addresses in the protocol:

* ERC-20, ERC-721, ERC-1155 tokens that can be used as Collateral tokens for wNFT;
* ERC-20 tokens that can be used as fee (commission) tokens to be paid when transferring wNFT. The protocol has a blacklist of original NFT contract addresses that the protocol is not allowed to wrap. **Only the ENVELOP project team can manage the lists**. Any user can retrieve data from the lists.

### **Method getWLItem**

```solidity
function getWLItem(address _asset) external view returns (ETypes.WhiteListItem memory)
```

The method returns the settings for a specific smar&#x74;**-**&#x63;ontract address from the white list.

**Input method call parameters:**

| Name        | Type    | Description                                  |
| ----------- | ------- | -------------------------------------------- |
| **\_asset** | address | Token smart-contract address from white list |

A description of the returned data types can be found in the **LibEnvelopTypes.sol** contact, ETypes library.

**Returned values:**

| Name      | Type                 | Description                                  |
| --------- | -------------------- | -------------------------------------------- |
| **value** | ETypes.WhiteListItem | Setting data for the token in the white-list |

**ETypes.WhiteListItem**

| Name                            | Type    | Description                                                                                                                                               |
| ------------------------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **enabledForFee**               | bool    | A sign of permission to use the token as a wNFT transfer fee token                                                                                        |
| **enabledForCollateral**        | bool    | A sign of permission to use token as **Collateral** token wNFT                                                                                            |
| **enabledRemoveFromCollateral** | bool    | A sign of permission to tokens to **remove** (withdrawn) from the wNFT collateral without unwrapping it - used in private implementations of the Protocol |
| **transferFeeModel**            | address | Address of the smart contract defining the rules for the allocation of transfer fees                                                                      |

### **Method getWLItemCount**

```solidity
function getWLItemCount() external view returns (uint256)
```

Method returns the number of tokens in the white address list. It has no input parameters.

**Returned values:**

| Name      | Type    | Description                                           |
| --------- | ------- | ----------------------------------------------------- |
| **value** | uint256 | Number (Quantity)of token addresses in the white list |

### Method getWLAddressByIndex

```solidity
function getWLAddressByIndex(uint256 _index) external view returns (ETypes.Asset memory)
```

**Input method call parameters:**

| Name        | Type    | Description                                              |
| ----------- | ------- | -------------------------------------------------------- |
| **\_index** | uint256 | The serial number of the token address in the white list |

**Returned values:**

| Name      | Type    | Description                                  |
| --------- | ------- | -------------------------------------------- |
| **value** | address | Token smart-contract address from white list |

### **Method getWLAddresses**

```solidity
function getWLAddresses() external view returns (ETypes.Asset[] memory)
```

The method returns a list of whitelist token contract addresses. The method has no input parameters.

**Returned values:**

| Name      | Type       | Description                                  |
| --------- | ---------- | -------------------------------------------- |
| **value** | address\[] | Array of white list token contract addresses |

### **Method getBLItem**

```solidity
function getBLItem(address _asset) external view returns (bool)
```

The method returns an indication of the blacklisting of the original NFT token.

**Input parameters of the method call:**

| Name        | Type    | Description                              |
| ----------- | ------- | ---------------------------------------- |
| **\_asset** | address | Blacklisted token smart contract address |

**Returned values:**

| Name      | Type | Description                                                                   |
| --------- | ---- | ----------------------------------------------------------------------------- |
| **value** | bool | Indication that the smart contract address of the original NFT is blacklisted |

### **Method getBLItemCount**

```solidity
function getBLItemCount() external view returns (uint256)
```

Method returns number of token addresses in blacklist of addresses. It has no input parameters.

**Returned values:**

| Name      | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| **value** | uint256 | Number of token address on the blacklist |

### **Method getBLAddressByIndex**

```solidity
function getBLAddressByIndex(uint256 _index) external view returns (ETypes.Asset memory)
```

The method returns the smart contract address of the blacklisted token by its sequence number in the blacklist.

**Input method call parameters:**

| Name        | Type    | Description                                             |
| ----------- | ------- | ------------------------------------------------------- |
| **\_index** | uint256 | The serial number of the token address on the blacklist |

**Returned values:**

| Name  | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| value | address | Blacklisted token smart contract address |

### **Method getBLAddresses**

```solidity
function getBLAddresses() external view returns (ETypes.Asset[] memory)
```

The method returns a list of blacklist token contract addresses. The method has no input parameters.

**Returned values:**

| Name      | Type       | Description                                 |
| --------- | ---------- | ------------------------------------------- |
| **value** | address\[] | Array of blacklist token contract addresses |

### **Method enabledForCollateral**

```solidity
function enabledForCollateral(address _asset) external view returns (bool)
```

The method for the token smart-contract address returns an indication if the tokens can be used to add to wNFT collateral.

**Input method call parameters:**

| Name        | Type    | Description                                  |
| ----------- | ------- | -------------------------------------------- |
| **\_asset** | address | Token smart contract address from white list |

**Returned values:**

| Name      | Type | Description                                                        |
| --------- | ---- | ------------------------------------------------------------------ |
| **value** | bool | Indication of permission to use token as collateral token for wNFT |

### Method enabledForFee

```solidity
function enabledForFee(address _asset) external view returns (bool)
```

The method for the token smart-contract address returns an indication if the tokens can be used to pay the wNFT transfer fee.

**Input method call parameters:**

| Name        | Type    | Description                                  |
| ----------- | ------- | -------------------------------------------- |
| **\_asset** | address | Token smart-contract address from white list |

**Returned values:**

| Name      | Type | Description                                                         |
| --------- | ---- | ------------------------------------------------------------------- |
| **value** | bool | Token permission sign to use the token to pay the wNFT transfer fee |

### **Method enabledRemoveFromCollateral**

```solidity
function enabledRemoveFromCollateral(address _asset) external view returns (bool)
```

The method for the token smart -contract address returns an indication if tokens can be removed (withdrawn) from wNFT collateral without being unwrapped.

**Input (Incoming) method call parameters:**

| Name        | Type    | Description                                  |
| ----------- | ------- | -------------------------------------------- |
| **\_asset** | address | Token smart contract address from white-list |

**Returned values:**

| Name      | Type | Description                                                                            |
| --------- | ---- | -------------------------------------------------------------------------------------- |
| **value** | bool | Indication of permission to withdraw tokens from wNFT collateral without unwrapping it |

### **Method rulesEnabled**

```solidity
function rulesEnabled(address _asset, bytes2 _rules) external view returns (bool)
```

The protocol has the option to set up rules of behavior for wNFTs created based on the specific original NFT (**for all bits in rules two-bytes bitmask**). It’s available for project team only (owner of contract). The method will return false if it do not match the rules bitmask passed to the method.

If the ENVELOP project team has banned individual rules for wNFTs created based on the original NFT (**only for some particular bits in rules two-bytes bitmask**) and the method is passed a description of individual rules with the same value in the banned bit of rules wNFT, then the method will return false.&#x20;

For example, for the original NFT 1 in the lowest significant bit is forbidden (set to rule value 0001 for rules wNFT by the ENVELOP team). Then when passing individual rules behavior (e.g. 1110), the method will return true - such rules are allowed, the disallowed bit of rules wNFT is 0. When passing another value (e.g. 1001), the method will **return false** - such rules are not allowed.

**Input method call parameters:**

| Name        | Type    | Description                                                   |
| ----------- | ------- | ------------------------------------------------------------- |
| **\_asset** | address | The smart-contract address of the original NFT                |
| **\_rules** | bytes2  | Description of wNFT behaviour rules based on the original NFT |

**Returned values:**

| Name      | Type | Description                                                |
| --------- | ---- | ---------------------------------------------------------- |
| **value** | bool | Indication that the passed rules are allowed or disallowed |

### **Method validateRules**

```solidity
function validateRules(address _asset, bytes2 _rules) external view returns (bytes2)
```

The method for the contract address of the original NFT returns a description of the allowed individual rules of behavior of the wNFT created on its basis as set by the **ENVELOP** project team.

If the ENVELOP project team has set such rules **for all bits in rules two-bytes bitmask**, the method will return the rule description set by the team. If the ENVELOP project team has restricted only particular wNFT rules (particular bits of rules wNFT) - it has prohibited particular values, then the method will return one of the allowed behavior rule descriptions.

For example, for the original NFT 1 in the lowest bit is forbidden (set rule value 0001 by the ENVELOP team in rules wNFT). Then when passing individual behavior rules (e.g. 1100), the method will return the value 1100. When passing a different value (e.g. 1001), the method will return 1000.
