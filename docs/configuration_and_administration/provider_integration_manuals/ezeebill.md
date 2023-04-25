--- 
id: "ezeebill" 
title: "Ezeebill"
hide_title: "true"
---
 
![](/img/providers/logos/ezeebill.png)

# Ezeebill

## About
Ezeebill is providing payment services via WebRedirectDeposits and withdrawals.

| Provider Name                | Ezeebill                                                                  |
|------------------------------|---------------------------------------------------------------------------|
| Link                         | [https://ezeebillasia.com/](https://ezeebillasia.com/)                    |
| Classification               | Mobile Payment                                                            |
| Regions                      | `China`, `Japan`, `India`, `Indonesia`, `Vietnam`, `Thailand`, `Malaysia` |
| Currencies                   | `CNY`, `JPY`, `INR`, `IDR`, `VND`, `THB`, `MYR`                           |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `EzeebillBankWithdrawal`                       |
| PaymentIQ Configuration File | `EzeebillConfig`                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.ezeebill.EzeebillConfig>
  <enabled>true</enabled>
  <version>1.0</version>
  <container>window</container>
  <accounts>
    <entry>
      <string>EZEEBILL_CU</string>
      <account>
        <use3Dsecure>true</use3Dsecure>
        <merchantId>??</merchantId>
        <supportedCurrencies>CNY</supportedCurrencies>
        <apiKey>??</apiKey>
        <terminalId>??</terminalId>
        <secretKey>??</secretKey>
        <username>??</username>
        <password>??</password>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.ezeebill.EzeebillConfig>
```

</details>

### Attributes


| Attribute           | Description                                                                                                 |
|---------------------|-------------------------------------------------------------------------------------------------------------|
| version             | Defines the Ezeebill API version that should be used. By default it's set to "1.0"                          |
| container           | Indicates the container for redirections - for best user experience it's required to set it to "window"     |
| use3Dsecure         | Indicates that the payment should go through Ezeebill's 3DS endpoint, must be set to "true                  |
| merchantId          | Individually assigned by Ezeebill to each merchant, it is being sent over with requests                     |
| supportedCurrencies | List of supported currencies for the current account - more on that in the "Accounts" section below         |
| apiKey              | Individually assigned by Ezeebill to each merchant, sent over with requests                                 |
| terminalId          | Individually assigned by Ezeebill to each merchant, sent over with requests                                 |
| secretKey           | Individually assigned by Ezeebill to each merchant, used to calculate signatures for requests and callbacks |
| username            | Individually assigned by Ezeebill to each merchant, used for status check requests                          |
| password            | Individually assigned by Ezeebill to each merchant, used for status check requests                          |

### Accounts

Ezeebill provides support for four different groups of regions and currencies:
- China: `CNY`
- Japan: `JPY`
- India: `INR`
- SEA (Vietnam, Thailand, Malaysia): `VND`, `THB`, `MYR`

Each of these regions will require you to create a separate account in your configuration file in order to control the
parameters that are sent over to the provider and route the traffic to a payment method which is specific for the region. <br/>
It is therefore recommended to create a separate account for each of the regions that you want to support and indicate 
the currencies supported by that region in the ``<supportedCurrencies>`` field. 

### NOTE

In order to obtain all the necessary credentials (merchantId, apiKey, terminalId, secretKey, username and password)
please contact Ezeebill's tech support.

## Provider Configuration

For all the payment methods, please make sure to follow these steps to configure Ezeebill:

1. Run PaymentIQ and add the aforementioned EzeebillConfig under Admin -> Configuration.
2. Add Ezeebill to the `<psp>` section in MerchantConfig under Admin -> Configuration.
3. Make sure that the `ezeebill-deposit-redirect` html template available for your MID - please contact PaymentIQ's tech
support to get it configured.

The additional steps that are required for each method will be described further on in this manual.

## Alipay Deposits - China

Additional configuration:

1. Enable WEBREDIRECT-AP deposit method in Rules -> Payment methods.

## CUPP2P Deposits - China

Additional configuration:

1. Enable WEBREDIRECT-BT deposit method in Rules -> Payment methods.

## P2P Deposits - Japan

Additional configuration:

1. Enable WEBREDIRECT-BT deposit method in Rules -> Payment methods.

## P2P Deposits - India

Additional configuration:

1. Enable WEBREDIRECT-IB deposit method in Rules -> Payment methods.

## SEA Deposits - Thailand and Indonesia

Additional configuration:

1. Enable WEBREDIRECT-IB deposit method in Rules -> Payment methods.

## SEA Deposits - Malaysia

Additional configuration:

1. Enable WEBREDIRECT-BT deposit method in Rules -> Payment methods.

## CUPP2P Withdrawals - China

Additional configuration:

1. Enable EZEEBILL-BTCNY withdrawal method in Rules -> Payment methods.
2. Cashier Payment Method-settings has to be configured - please contact PaymentIQ's tech support to configure this method.

## CUPP2P Withdrawals - China

Additional configuration:

1. Enable EZEEBILL-BTCNY withdrawal method in Rules -> Payment methods.
2. Cashier Payment Method-settings has to be configured - please contact PaymentIQ's tech support to configure this method.

## China Withdrawals

Additional configuration:

1. Enable EZEEBILL-BTCNY withdrawal method in Rules -> Payment methods.
2. Cashier Payment Method-settings has to be configured - please contact PaymentIQ's tech support to configure this method.

## Japan Withdrawals

Additional configuration:

1. Enable EZEEBILL-BTJPN withdrawal method in Rules -> Payment methods.
2. Cashier Payment Method-settings has to be configured - please contact PaymentIQ's tech support to configure this method.

## India Withdrawals

Additional configuration:

1. Enable EZEEBILL-BTINR withdrawal method in Rules -> Payment methods.
2. Cashier Payment Method-settings has to be configured - please contact PaymentIQ's tech support to configure this method.

## SEA Withdrawals - Thailand, Malaysia and Indonesia

Additional configuration:

1. Enable EZEEBILL-BTSEA withdrawal method in Rules -> Payment methods.
2. Cashier Payment Method-settings has to be configured - please contact PaymentIQ's tech support to configure this method.

## Transaction Flow

### Deposits

1. The user enters the amount to be transferred in the cashier.
2. PaymentIQ collects the data required by Ezeebill and sends a POST form over to the PSP.
3. The user gets redirected to the Ezeebill's checkout page and follows the instructions to complete the payment.
4. The user gets redirected back to the cashier and PaymentIQ performs a status check on the transaction and the
   payment's status will be updated accordingly to the response from the PSP. In case of pending payments, PaymentIQ
   will wait on a notification related to the transaction, then perform the status check once again and update the status
   of the transaction.
   
### Withdrawals

1. The user enters the amount to be transferred in the cashier and fills out all the fields specifically required for
   the currently used method.
2. Once the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends a payout request to Ezeebill.
3. In case of successful or pending response, PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION
   and the transfer will be made to deduct the amount from the user's balance.
4. PaymentIQ awaits for a callback from Ezeebill regarding the status of the withdrawal. In case of a callback with 
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the
   user's balance.

## Example Routing Rule

![](/img/providers/routing/ezeebill.png)

## Test Information

Please check directly with the provider.
