---
description: >-
  The NIFTSY token contract of the ERC-20 standard is classic in terms of
  OpenZeppelin standards.
---

# Contract NiftsyERC20.sol

The NIFTSY token contract of the ERC-20 standard is classic in terms of **OpenZeppelin standards**.&#x20;

The only deviation from the standard is that all tokens are issued to the address of the protocol owners at the time the contract is being deployed into the network. No one has the ability to issue additional tokens or burn them. **The burn and mint methods are not available**.&#x20;

Below is a list and description of the methods that users can call either in web scanner applications (e.g. [https://etherscan.io/](https://etherscan.io/)) or through various frameworks that have the ability to access the contract methods programmatically.

This smart contract was audited by a well-known independent company, Certik: [https://www.certik.org/projects/niftsy](https://www.certik.org/projects/niftsy).

### Method "aprove"

```
function approve(address spender, uint256 amount) public virtual override returns (bool) {
     _approve(_msgSender(), spender, amount);
     return true;
}
```

The method allows the token holder to give permission to another user to manage their tokens. After invoking this method, the spender (who has been given permission) will be able to make transfers of the owner's tokens within the allowed amount. The method checks that the owner's address is not zero.

**Parameters:**

| Name        | Type    | Description                                      |
| ----------- | ------- | ------------------------------------------------ |
| **spender** | address | Address of the token  spender (disposer/manager) |
| **amount**  | uint256 | Number of tokens allowed to be managed           |

**Returns values:**

| Name       | Type | Description   |
| ---------- | ---- | ------------- |
| **result** | bool | True or False |



### Method "**transferFrom"**

```
function transferFrom(
     address sender, 
     address recipient, 
     uint256 amount
) public virtual override returns (bool) 
```

The method transfers tokens from the sender's balance to the recipient's balance. If the sender has given permission for another user to manage their tokens, then they can make the transfer by specifying the owner of the tokens in the sender parameter. In this case, the method will compare the number of tokens the sender is allowed to manage with the number of tokens it is trying to transfer. And disallow the transfer if the former is less than the latter. Otherwise the transfer will be made, reducing the number of owner tokens in the permission that the the spender can manage.

The method also verifies that the recipient's address is not zero and that the sender's token balance is sufficient to make the transfer.

**Parameters:**

| Name          | Type    | Description                                                         |
| ------------- | ------- | ------------------------------------------------------------------- |
| **sender**    | address | Token sender address                                                |
| **recipient** | address | The address of the recipient of the tokens                          |
| **amount**    | uint256 | Number of tokens that the user calling the method wants to transfer |

**Returns values:**

| Name       | Type | Description   |
| ---------- | ---- | ------------- |
| **result** | bool | True or False |

### Method "**transfer"**

```
function transfer(address recipient, uint256 amount) public virtual override returns (bool) 
```

The method transfers tokens from the balance of the user calling the method to the recipient's balance. The method checks that the recipient's address is not zero and that the sender's token balance is sufficient to make the transfer. If all conditions are met, the token balance of the user calling the method is reduced and the token balance of the recipient is increased.

**Parameters:**

| Name          | Type    | Description                                                         |
| ------------- | ------- | ------------------------------------------------------------------- |
| **recipient** | address | The address of the recipient of the tokens                          |
| **amount**    | uint256 | Number of tokens that the user calling the method wants to transfer |

**Returns values:**

| Name       | Type | Description   |
| ---------- | ---- | ------------- |
| **result** | bool | True of False |

### Method "**increaseAllowance"**

```
function increaseAllowance(address spender, uint256 addedValue) public virtual returns (bool)
```

The method allows the owner to increase the number of tokens that can be managed by another user. When this method is called, the spender (who has been given permission) will be able to make transfers of the owner's tokens within the updated amount. The method checks that the spender's address is not zero.

**Parameters:**

| Name           | Type    | Description                                           |
| -------------- | ------- | ----------------------------------------------------- |
| **spender**    | address | Address of the token spender (disposer/manager)       |
| **addedValue** | uint256 | Number of tokens by which the resolution is increased |

**Returns values:**

| Name        | Type | Description   |
| ----------- | ---- | ------------- |
| **result**  | bool | True or False |

### Method "**decreaseAllowance"**

```
function decreaseAllowance(address spender, uint256 subtractedValue) public virtual returns (bool)
```

The method allows the owner to reduce the number of tokens that can be managed by another user. After invoking this method, the spender (who has been given permission) will be able to make transfers of the owner's tokens within the updated amount. The method checks that the spender's address is not zero.

**Parameters:**

| Name           | Type    | Description                                           |
| -------------- | ------- | ----------------------------------------------------- |
| **spender**    | address | Token spender (disposer/manager)                      |
| **addedValue** | uint256 | Number of tokens by which the resolution is increased |

**Returns values:**

| Name       | Type | Description   |
| ---------- | ---- | ------------- |
| **result** | bool | True of False |

### Method "**allowance"**

```
function allowance(address owner, address spender) public view virtual override returns (uint256)
```

The method returns the number of tokens the owner has allowed the spender to use.

**Parameters:**

| Name        | Type    | Description                                     |
| ----------- | ------- | ----------------------------------------------- |
| **owner**   | address | Token owner                                     |
| **spender** | address | Address of the token spender (disposer/manager) |



**Returns values:**

| Name       | Type    | Description                                                   |
| ---------- | ------- | ------------------------------------------------------------- |
| **result** | uint256 | Number of tokens the holder has authorised the spender to use |

### **Method "balanceOf"**

```
function balanceOf(address account) public view virtual override returns (uint256)
```

The method returns the remainder of the tokens passed to the method address.

**Parameters:**

| Name        | Type    | Description     |
| ----------- | ------- | --------------- |
| **account** | address | The token owner |

**Returns values:**

| Name       | Type    | Description   |
| ---------- | ------- | ------------- |
| **result** | uint256 | Token balance |
