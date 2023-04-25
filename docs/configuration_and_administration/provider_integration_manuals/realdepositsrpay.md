--- 
id: "realdepositsrpay" 
title: "RealdepositsRPay"
hide_title: "true"
---
 
![](/img/providers/logos/realdepositsrpay.png)

# RealDepositsRPay

## About
RealDepositsRPay is an aggregator provider offering Credit Card and several alternative payment methods using their hosted payment page. Credit Card payments supports Deposit, Withdrawal, Refund.
For Alternative Payment Methods it depends on the specific method, where all supports Deposit and some also Withdrawal and Refund.
Please check with the provider for more details.

| Provider Name                | RealDepositsRPay                                                                                     |
|------------------------------|------------------------------------------------------------------------------------------------------|
| Link                         | [https://realdeposits.com](https://realdeposits.com)                                                 |
| Classification               | Debit/Credit Card Processor and WebRedirect                                                          |
| Regions                      | `Internatioal`                                                                                       |
| Currencies                   | `CNY` `EUR` `USD` `JPY`                                                                              |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `WebRedirectDeposit`, `WebRedirectWithdrawal`, `Refund` |
| PaymentIQ Configuration File | `RealDepositsRPayConfig`                                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.realdepositsrpay.RealDepositsRPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
     <string>default</string>
     <account>
     <secretKey>???</secretKey>
     <productName>???</productName>
     <supportedCurrencies>???</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <services>
   <entry>
     <string>WEBMONEY</string>
      <string>webmoney</string>
    </entry>
    <entry>
      <string>BANKCARD</string>
      <string>bank_card</string>
    </entry>
        <entry>
      <string>QIWI</string>
      <string>qiwi_wallet</string>
    </entry>
        <entry>
      <string>SKRILL</string>
      <string>skrill_wallet</string>
    </entry>
       <entry>
      <string>VirtualPay</string>
      <string>paycode54</string>
      </entry>
   </services>
</com.devcode.paymentiq.integration.realdepositsrpay.RealDepositsRPayConfig>

```

</details>

### Attributes

| Attribute   | Description                                                                |
|-------------|----------------------------------------------------------------------------|
| secretKey   | merchant_private_key provided by RealDeposits to be used in authentication |
| productName | product name (Service description) to be send in deposit request           |
| service     | used to map PIQ service to corresponding RealDepositsRPay payment method   |

1. Add the RealDepositsBusinessConfig
2. Configure RealDepositsBusiness service(s):
  - 2.1. Set the service parameter in TxTypeInput to the apm that will be used.

``` xml    
<com.devcode.paymentiq.service.cashier.TxTypeInput>
  <txType>WebRedirectDeposit</txType>
  <providerType>WEBREDIRECT</providerType>
  <service>VIRTUALPAY</service>
  <storeAccounts>true</storeAccounts>
  <inputs>
    <string>amount</string>
  </inputs>
</com.devcode.paymentiq.service.cashier.TxTypeInput>
```                                                        
  - 2.2 Configure `REALDEPOSITSRPAY` service(s) in `MerchantConfig`:

```xml        
<entry>
  <string>WEBREDIRECT</string>
  <string>VIRTUALPAY|SKRILL</string>
</entry>
```           
 3. Enable required payment method(s) in PIQ BO (**Rules > Payment Methods**) e.g. WEBREDIRECT-VIRTUALPAY

## Example Routing Rules

![](/img/providers/routing/realdepositsrpay.png)

## APMs Transaction Flow

### APMs Deposits

1. User enters an amount in the cashier and clicks on "Deposit". 
2. PaymentIQ sends a request to the PSP. An url is received in response, to which the user is redirected and completes the transaction.
3. PaymentIQ receives a callback from the PSP with a transaction status and updates the transaction accordingly.

### APMs Withdrawals

1. User enters an amount in the cashier and clicks on "Withdraw".
2. PaymentIQ sends a request to the PSP. An url is received in response which is stored by PaymentIQ.
3. The withdrawal is initiated and has to be approved in the backoffice if auto-approvals have not been set.
4. Once the withdrawal has been approved, the user receives a link via the registered email address to complete the withdrawal.
5. PaymentIQ receives a callback from the PSP with a transaction status and updates the transaction accordingly.

## Test Information

### Testing Creditcard

Use the following cards with any cvv and expiry date to test creditcard deposits and withdrawals.

| Tx Type | 3DS/N3DS | Card Number      | Result/Info |
|---------|----------|------------------|-------------|
| Deposit | N3DS     | 4392963203551251 | Successful  |
| Deposit | N3DS     | 4730198364688516 | Declined    |
| Deposit | 3DS      | 4617611794313933 | Successful  |
| Deposit | 3DS      | 4626233193837898 | Declined    |
| Payout  | -        | 4627342642639018 | Successful  |
| Payout  | -        | 4968357931420422 | Declined    |

### Testing APMs 

The provider does not have test environment for APMs integration