# Subscription service

### Release notes

This version of the subscription service includes the following changes:

1. The **architecture** of the service has been redesigned.
2. Added possibility to connect **agents** to subscription sales.
3. The ability to charge an agency **fee** for subscription sales has been added.
4. Added direct payment method for **ERC-20** tokens and native tokens (coins) to buy the subscriptions.
5. Developed smart-contract templates to be **inherited** by contracts that act as an agent or service provider.
6. Added charging a service fee on **each** **sale** of provider subscriptions. The fee is paid by the purchaser at the time the subscription is purchased.
7. Added functionality to maintain a **list** of available payment tokens.

### **Restrictions:**

1. You **cannot** **delete** tariffs. You can only deactivate them.
2. Only one way to deduct agent and service fee is **implemented** is percent (%) of the amount of payment for a subscription.
3. User can have **only** **one** active subscription to provider's services at a time.

### **A few words about the architecture:**

1. The central part of the service is the **SubscriptionRegistry.sol** contract. This contract records information about all services for which subscriptions are sold, their **rates** and agents.
2. **Various services** that provide services to their users can connect to the subscription service. Let's call them **providers**. For example, services for listening to music, audio-books, watching movies, analytical resources and so on. Smart-contracts of providers must inherit the smart-contract **ServiceProvider.sol**. It contains the minimum required set of methods to create rates and register agents who will sell subscriptions to providers. One provider can have several agents at the same time or act as an agent for **itself**.
3. **Agents** are another participant in the subscription service. Agents sell subscriptions to service providers for compensation **or** free of charge. Only providers can add agents to the subscription service and set the rates at which they will sell subscriptions. Providers also determine the amount of agent fees. To interact with the subscription service, agents' smart-contracts must inherit the **ServiceAgent.sol** smart-contract. It contains the minimum required set of methods: sell subscriptions to providers. One agent can sell subscriptions for multiple providers simultaneously. If a provider wants to sell subscriptions for their own services, they must also inherit the smart-contract ServiceAgent.sol in their contract.&#x20;
4. **Agents and providers**, when preparing their smart-contracts to work with the subscription service, decide for themselves which methods to use the onlyOwner modifier from the **Ownable.sol** smart contract of the OpenZeppelin package.
5. The **repository** address of the contract package: [https://github.com/dao-envelop/subscription](https://github.com/dao-envelop/subscription)

Below are links to examples of smart contracts that inherit the developed provider and agent smart-contract templates.

## Abstract Smart-Contract ServiceProvider

### Method \_registerServiceTariff&#x20;

<pre class="language-solidity"><code class="lang-solidity">function _registerServiceTariff(Tariff memory _newTariff) 
<strong>        internal virtual returns(uint256)
</strong></code></pre>

The method creates tariffs for provider.

The method emits **TariffChanged** event with the following values:&#x20;

* The address of the smart-contract of the provider;
* The serial number of the rates in the array of registered rates for the provider;

**Input parameters of the method for calling:**

| Name        | Type   | Description              |
| ----------- | ------ | ------------------------ |
| \_newTariff | Tariff | Data describing the rate |

**Tariff:**&#x20;

| Name         | Type             | Description                                                                                                   |
| ------------ | ---------------- | ------------------------------------------------------------------------------------------------------------- |
| subscription | SubscriptionType | Data with rate settings                                                                                       |
| payWith      | PayOption\[]     | Data array with a list of tokens (ERC-20 or native (coins)) that can be used to pay for the subscription rate |

**SubscriptionType:**&#x20;

| Name              | Type    | Description                                                                                                                                                                                         |
| ----------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| timelockPeriod    | uint256 | For rates with subscription payment method "blocking ERC-20 tokens in **wNFT**" the **blocking** period is specified. Date format is unixtime. For rates with direct payment method 0 is specified. |
| ticketValidPeriod | uint256 | For rates with a subscription validity period, the period in seconds during which the subscription purchased under the rate will be valid is specified.                                             |
| counter           | uint256 | For rates with the volume of provider services usage, a value other than 0 is specified.                                                                                                            |
| isAvailable       | bool    | The rate activity flag.                                                                                                                                                                             |
| beneficiary       | address | Receiver of payment tokens for rates with direct payment method.                                                                                                                                    |

**PayOption:**&#x20;

| Name            | Type    | Description                                                                                                                                                                      |
| --------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| paymentToken    | address | The smart contract address of the payment token. If the rate assumes payment with native network tokens (coins), then a null address 0x0000000000000000000000000000000000000000. |
| paymentAmount   | uint256 | Number of tokens to be paid.                                                                                                                                                     |
| agentFeePercent | uint16  | Amount of agent's fee. Specified if the agent will sell subscriptions at this rate. Examples: 100%-10000, 20%-2000, 3%-300                                                       |

**The method returns values:**

| Name  | Type    | Description                                                                              |
| ----- | ------- | ---------------------------------------------------------------------------------------- |
| index | uint256 | The serial number of the **rate** in the **array** of registered rates for the provider. |

### Method \_editServiceTariff&#x20;

```solidity
function _editServiceTariff(
        uint256 _tariffIndex, 
        uint256 _timelockPeriod,
        uint256 _ticketValidPeriod,
        uint256 _counter,
        bool _isAvailable,
        address _beneficiary
```

The method **changes** the provider's rate settings.

The method emits the **TariffChanged** event with the following values:&#x20;

* Provider smart-contract address.
* The serial number of the rate in the array of registered rates for provider.

**Input parameters of the method for the calling:**

| Name                | Type    | Description                                                                                                                                                                                     |
| ------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_tariffIndex       | uint256 | The serial number of the rate in the array of registered rates for the provider.                                                                                                                |
| \_timelockPeriod    | uint256 | For rates with subscription payment method "blocking ERC-20 tokens in **wNFT**" the blocking period is specified. Date format is unixtime. For rates with direct payment method 0 is specified. |
| \_ticketValidPeriod | uint256 | For rates with a subscription validity period, the period in seconds during which the subscription purchased under the rate will be valid is specified.                                         |
| \_counter           | uint256 | For rates with the volume of provide services usage, a value other than 0 is specified.                                                                                                         |
| \_isAvailable       | bool    | The rate activity flag.                                                                                                                                                                         |
| \_beneficiary       | address | Receiver of payment tokens for rates with direct payment method.                                                                                                                                |

### Method \_addTariffPayOption&#x20;

```solidity
function _addTariffPayOption(
        uint256 _tariffIndex,
        address _paymentToken,
        uint256 _paymentAmount,
        uint16 _agentFeePercent
    ) internal virtual returns(uint256)
```

The method adds a payment token for the provider's rate.

The method emits the TariffChanged event with the following values:&#x20;

* Provider's smart contract address.&#x20;
* The serial number of the rate in the array of registered rates for provider.

**Input parameters of the method for the calling:**

| Name              | Type    | Description                                                                                                                                                                    |
| ----------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| \_tariffIndex     | uint256 | The serial number of the rate in the array of registered rates for the provider.                                                                                               |
| \_paymentToken    | address | The smart-contract address of the payment token. If the rate assumes payment with native network tokens (coins), then zero address 0x0000000000000000000000000000000000000000. |
| \_paymentAmount   | uint256 | The number of tokens to be paid.                                                                                                                                               |
| \_agentFeePercent | uint16  | Amount of agent's fee. Specified if the agent will sell subscriptions at this rate. Examples: 100%-10000, 20%-2000, 3%-300.                                                    |

**The method returns values:**

| Name  | Type    | Description                                                                           |
| ----- | ------- | ------------------------------------------------------------------------------------- |
| index | uint256 | The sequence number of the added token record to the payment token array of the rate. |

### Method \_editTariffPayOption

```solidity
function _editTariffPayOption(
        uint256 _tariffIndex,
        uint256 _payWithIndex, 
        address _paymentToken,
        uint256 _paymentAmount,
        uint16 _agentFeePercent
    ) internal virtual 
```

The method changes the payment token settings for the provider's rate.

The method emit the **TariffChanged** event with the following values:&#x20;

* Provider's smart contract address.
* The serial number of the rate in the array of registered rates for the provider.

**Input parameters of the method for the calling:**

| Name              | Type    | Description                                                                                                                                                                    |
| ----------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| \_tariffIndex     | uint256 | The serial number of the rate in the array of registered rates for the provider.                                                                                               |
| \_payWithIndex    | uint256 | The serial number of the token record in the payment token array for the provider's rate.                                                                                      |
| \_paymentToken    | address | The smart-contract address of the payment token. If the rate assumes payment with native network tokens (coins), then zero address 0x0000000000000000000000000000000000000000. |
| \_paymentAmount   | uint256 | The number of tokens to be paid.                                                                                                                                               |
| \_agentFeePercent | uint16  | Amount of agent's fee. Specified if the agent will sell subscriptions at this rate. Examples: 100%-10000, 20%-2000, 3%-300.                                                    |

### Method \_authorizeAgentForService

```solidity
function _authorizeAgentForService(
        address _agent,
        uint256[] memory _serviceTariffIndexes
    ) internal virtual returns (uint256[] memory)
```

The method registers an agent and his available rates for the provider. Only the rates with the Active flag enabled are added for the agent.

**Input parameters of the method for the calling:**

| Name                   | Type       | Description                                                                   |
| ---------------------- | ---------- | ----------------------------------------------------------------------------- |
| \_agent                | address    | The agent's smart-contract address.                                           |
| \_serviceTariffIndexes | uint256\[] | An array of rate indexes from the array of rates registered for the provider. |

**The method returns values:**

| Name   | Type       | Description                                        |
| ------ | ---------- | -------------------------------------------------- |
| indexs | uint256\[] | An array of rate indexes for the registered agent. |

### Method \_checkAndFixSubscription

```solidity
function _checkAndFixSubscription(address _user) 
        internal 
        returns (bool ok)
```

This method should be called in the provider's target action method. For example, the target action is to provide a link to download some content to the user who bought a subscription. The **\_checkAndFixSubscription** method checks the validity of the subscription purchased by the user.

In the case of a rate with a volume of usage of the provider's services, the method reduces the available volume by one. For example, if subscription has allowed 10 times to get a link to download some file on the Internet, each time the method of getting the link is called, the **\_checkAndFixSubscription** method will reduce the number of attempts to download the link, which can be used by the buyer of such subscription.

In the case of a subscription with an expiration date, calling the **\_checkAndFixSubscription** method will result in checking if the subscription has not expired. The period of validity of a subscription is defined by the boundaries:

* The subscription purchase date.
* The date of subscription purchase plus the period of validity for the subscription according to the rate.

**Attention! It is not recommended** to make this method call publicly available, outside of calling the target action method. It can lead to loss of subscription in case of rate with usage volume.

**Input parameters of the method for the calling:**

| Name   | Type    | Description                                                            |
| ------ | ------- | ---------------------------------------------------------------------- |
| \_user | address | The address of the user for whom the subscription validity is checked. |

**The method returns values:**

| Name | Type | Description                                                                                         |
| ---- | ---- | --------------------------------------------------------------------------------------------------- |
| ok   | bool | Boolean value. **True** - the subscription is still valid. **False** - the subscription is invalid. |

### Method \_checkUserSubscription

```solidity
function _checkUserSubscription(address _user) 
        internal 
        view 
        returns (bool ok, bool needFix)
```

The method checks the validity of the service subscription purchased by the user.

In the case of a rate with the amount of provider usage, the method checks that the number of attempts to use provider services is not equal to 0.

In the case of a subscription with an expiration date, the method checks if the subscription has not expired. The subscription expiration date is defined by the boundaries:

* The subscription purchase date.
* The date of subscription purchase plus the period of validity for the subscription according to the rate.

**Input parameters of the method for the calling:**

| Name   | Type    | Description                                                            |
| ------ | ------- | ---------------------------------------------------------------------- |
| \_user | address | The address of the user for whom the subscription validity is checked. |

**The method returns values:**

| Name    | Type | Description                                                                                                                                                                                                                                                  |
| ------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ok      | bool | Boolean value. **True** - the subscription is still active. **False** - the subscription is invalid.                                                                                                                                                         |
| needFix | bool | Boolean value. **True** - for rate subscriptions with a volume of provider usage (an indication that the volume available to the user must be reduced each time the subscription is used). **False** - always for rate subscriptions with a validity period. |

## Abstract Smart Contract ServiceAgent.sol

### Method buySubscription

```solidity
function buySubscription(
        address _service,
        uint256 _tarifIndex,
        uint256 _payWithIndex,
        address _buyFor,
        address _payer
    ) public payable returns(Ticket memory ticket)
```

The method allows the user to purchase a subscription for the **selected** **provider**, for the selected rate and pay for the subscription with tokens from the list of available tokens for the rate he has selected.

Before invoking the method, the user needs to give the SubscriptionRegistry contract **permission** to use his tokens in the required amount on the ERC-20 smart-contract of the token with which he decided to pay for the subscription.

The method performs all payment processing:

* Sends the service provider the subscription cost (to the specified recipient address from the rate settings);
* Sends the agent's fee to the his smart-contract;
* Send the fee of Subscription service to the recipient (specified in the **platformOwner** public variable);&#x20;

**Or**

* Creates a wNFT with locked ERC-20 payment tokens.

The method emit a **TicketIssued** event with the following values:&#x20;

* Service provider's smart contract address.
* Address of the agent's smart-contract.
* Address of the user for whom the subscription was purchased.
* Rate **index** from the array of rates registered for the service provider, for which the subscription was purchased.

**Input parameters of the method for the calling:**

| \_service      | address | The address of the service provider's smart-contract.                                                |
| -------------- | ------- | ---------------------------------------------------------------------------------------------------- |
| \_tarifIndex   | uint256 | Rate index from the array of rates registered for the service provider.                              |
| \_payWithIndex | uint256 | The serial number of the token record in the payment token array for the provider's rate.            |
| \_ buyFor      | address | The address of the recipient of the subscription (a subscription can be purchased for another user). |
| \_payer        | address | Subscription buyer address.                                                                          |

**The method returns values:**

| Name       | Type    | Description                                                                                                                                                                                                                                           |
| ---------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| validUntil | uint256 | The date until which the subscription is valid - in case buyer purchased a subscription with an expiration date. In the case of a rate with the amount of provider usage, it is the date the subscription was purchased. Date in **unixtime** format. |
| countsLeft | uint256 | The amount of usage of the provider's services purchased. If a subscription was purchased with an expiration date, 0 will be returned.                                                                                                                |

### Method \_withdrawEther

```solidity
function _withdrawEther(address _feeReceiver) internal
```

The method withdraws accumulated native agent fee tokens from the agent contract. We **recommend** calling this method in the method with **onlyOwner** modifier from the **Ownable.sol** smart-contract of the **OpenZeppelin** package. Otherwise, the agent may lose the accumulated fee from subscription sales.

**Input parameters of the method for the calling:**

| Name          | Type    | Description                                                                         |
| ------------- | ------- | ----------------------------------------------------------------------------------- |
| \_feeReceiver | address | The address where to send the accumulated agent fee tokens from subscription sales. |

### Method \_withdrawTokens

```solidity
function _withdrawTokens(address _erc20, address _feeReceiver) internal
```

The method withdraws accumulated ERC-20 agent fee tokens from the agent contract. We recommend to call this method in method with modifier **onlyOwner** from smart-contract **Ownable.so**l of **OpenZeppelin** package. Otherwise agent can lose accumulated fee from subscription sales.

**Input parameters of the method for the calling:**

| Name          | Type    | Description                                                                                |
| ------------- | ------- | ------------------------------------------------------------------------------------------ |
| \_erc20       | address | The smart-contract address of the ERC-20 tokens to be withdrawn from the agent's contract. |
| \_feeReceiver | address | The address where to send the accumulated agent fee tokens from subscription sales.        |

## SubscriptionRegistry.sol

Additional methods that Agents, Providers and Buyers can use.

### Method getUserTicketForService

```solidity
function getUserTicketForService(
        address _service,
        address _user
    ) public view returns(Ticket memory)
```

The method returns data about the user's subscription to the provider's services.

**Input parameters of the method for the calling:**

| Name      | Type    | Description                                         |
| --------- | ------- | --------------------------------------------------- |
| \_service | address | The smart-contract address of the service provider. |
| \_user    | address | The address of the **owner** of the subscription.   |

**The method returns values:**

| Name       | Type    | Description                                                                                                                                                                                                                                           |
| ---------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| validUntil | uint256 | The date until which the subscription is valid - in case buyer purchased a subscription with an expiration date. In the case of a rate with the amount of provider usage, it is the date the subscription was purchased. Date in **unixtime** format. |
| countsLeft | uint256 | The remaining amount of usage of the provider's services. If a subscription was purchased with an expiration date, 0 will be returned.                                                                                                                |

### Method getTariffsForService

```solidity
function getTariffsForService(address _service) external view returns (Tariff[] memory)
```

The method returns an array of data about all rates registered for the provider.

**Input parameters of the method for the calling:**

| Name      | Type    | Description                                         |
| --------- | ------- | --------------------------------------------------- |
| \_service | address | The smart contract-address of the service provider. |

**The method returns values:**

| Name    | Type      | Description                                                                                                   |
| ------- | --------- | ------------------------------------------------------------------------------------------------------------- |
| tariffs | Tariff\[] | An array of data about all rates registered for the provider. The description of the data type is made above. |

### Method getTicketPrice

```solidity
function getTicketPrice(
        address _service,
        uint256 _tariffIndex,
        uint256 _payWithIndex
    ) public view virtual returns (address, uint256)
```

The method returns the total price to pay for the subscription (including all fees).

**Input parameters of the method for the calling:**

| Name           | Type    | Description                                                                               |
| -------------- | ------- | ----------------------------------------------------------------------------------------- |
| \_service      | address | The smart-contract address of the service provider.                                       |
| \_tarifIndex   | uint256 | Rate index from the array of rates registered for the service provider.                   |
| \_payWithIndex | uint256 | The serial number of the token record in the payment token array for the provider's rate. |

**The method returns values:**

| Name     | Type    | Description                                                                                                                                                                                                      |
| -------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| payToken | address | The smart-contract address of the payment token. In case the price request was made for payment with native tokens (coins), the method will return a null address of 0x0000000000000000000000000000000000000000. |
| amount   | uint256 | Number of tokens to be paid or blocked in the wNFT (depending on the selected payment method).                                                                                                                   |

### Method getAvailableAgentsTariffForService

```solidity
function getAvailableAgentsTariffForService(
        address _agent, 
        address _service
    ) external view virtual returns(uint256[] memory, Tariff[] memory)
```

The method returns data about available rates for the specified agent and service provider.

**Input parameters of the method for the calling:**

| Name      | Type    | Description                                         |
| --------- | ------- | --------------------------------------------------- |
| \_ agent  | address | Agent's smart-contract address.                     |
| \_service | address | The smart contract address of the service provider. |

**The method returns values:**

| Name    | Type       | Description                                                                                                                                         |
| ------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| indexes | uint256\[] | An array of ordinal numbers from the array of rate data registered for the provider that he assigned to the agent.                                  |
| tariffs | Tariff\[]  | An array of data about all rates registered for the provider according to list of returned indexes. The description of the data type is made above. |

### Examples of rate descriptions

#### Ex. 01. Rate with direct subscription payment method and subscription validity period

<pre class="language-solidity"><code class="lang-solidity"><strong>subscriptionType = {
</strong>        timelockPeriod: 0,
        ticketValidPeriod: 2592000,
        counter: 0,          
        isAvailable: true,
        beneficiary: "0xE0E4EC54ed883d7089895C0e951b4bB8E3c68888"
}

payOptions = [
        {
                paymentToken: "0x6b175474e89094c44da98b954eedeac495271d0f",
                paymentAmount: 2000000000000000000,
                agentFeePercent: 20,
        },
        {
                paymentToken: "0xdAC17F958D2ee523a2206206994597C13D831ec7", 
                paymentAmount: 5000000,
                agentFeePercent: 20,
        }
]

tariff = {
                subscription: subscriptionType
                payWith: payOptions
        }
</code></pre>

#### Ex. 02. Rate with direct subscription payment method and volume of service usage

```solidity
subscriptionType = {
        timelockPeriod: 0,
        ticketValidPeriod: 0,
        counter: 5,          
        isAvailable: true,
        beneficiary: "0xE0E4EC54ed883d7089895C0e951b4bB8E3c68888"
}

payOptions = [
        {
                paymentToken: "0x0000000000000000000000000000000000000000",
                paymentAmount: 6000000000000000000,
                agentFeePercent: 20,
        },
        {
                paymentToken: "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48", 
                paymentAmount: 30000000,
                agentFeePercent: 20,
        }
]

tariff = {
                subscription: subscriptionType
                payWith: payOptions
        }
```

#### Ex. 03. Rate with the payment method "blocking ERC-20 tokens in wNFT" and subscription validity period

```solidity
subscriptionType = {
        timelockPeriod: 15552000,
        ticketValidPeriod: 5184000,
        counter: 0,          
        isAvailable: true,
        beneficiary: "0xE0E4EC54ed883d7089895C0e951b4bB8E3c68888"
}

payOptions = [
        {
                paymentToken: "0x6b175474e89094c44da98b954eedeac495271d0f",
                paymentAmount: 40000000000000000000,
                agentFeePercent: 20,
        },
        {
                paymentToken: "0xdAC17F958D2ee523a2206206994597C13D831ec7", 
                paymentAmount: 100000000,
                agentFeePercent: 20,
        }
]

tariff = {
                subscription: subscriptionType
                payWith: payOptions
        }
```

#### Ex. 04. Rate with the payment method "blocking ERC-20 tokens in wNFT" and  volume of service usage

```solidity
subscriptionType = {
        timelockPeriod: 23328000,
        ticketValidPeriod: 0,
        counter: 7,          
        isAvailable: true,
        beneficiary: "0xE0E4EC54ed883d7089895C0e951b4bB8E3c68888"
}

payOptions = [
        {
                paymentToken: "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
                paymentAmount: 180000000000000000000,
                agentFeePercent: 20,
        },
        {
                paymentToken: "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48", 
                paymentAmount: 540000000,
                agentFeePercent: 20,
        }
]

tariff = {
                subscription: subscriptionType
                payWith: payOptions
        }
```
