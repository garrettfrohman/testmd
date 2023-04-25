--- 
id: "capitalmanagement" 
title: "Capital Management"
hide_title: "true"
---

![](/img/providers/logos/capitalmanagement.png)

# CapitalManagement

## About
CapitalManagement is a solution that enables merchants to accept WebRedirect deposit payments.<br/>


| Provider Name                | CapitalManagement                                                  |
|------------------------------|--------------------------------------------------------------------|
| Link                         | [https://www.capitalmgmtinc.com/](https://www.capitalmgmtinc.com/) |
| Classification               | Online Banking                                                     |
| Supported Regions            | USA, Europe                                                        |
| Currencies                   | `EUR`,`USD`,`RUB`                                                  |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                               |
| PaymentIQ Configuration File | `CapitalManagementConfig`                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.capitalmanagement.CapitalManagementConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account> 
        <merchantCode>{account.merchantCode}</merchantCode>
        <merchantId>{account.merchantId}</merchantId>
        <siteId>{account.siteId}</siteId>
        <customerPaymentMethod>{account.paymentMethod}</customerPaymentMethod>
        <supportedCurrencies>EUR|USD|RUB</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.capitalmanagement.CapitalManagementConfig>


```
</details>

| Attribute             | Description                                                        |
|-----------------------|--------------------------------------------------------------------|
| account.merchantCode  | Corresponds to the merchant security token from CapitalManagement. |
| account.merchantId    | Corresponds to the merchant id from CapitalManagement.             |
| account.siteId        | Corresponds to the site id from CapitalManagement.                 |
| account.paymentMethod | Corresponds to the payment method from CapitalManagement           |

## Example Routing Rule
![](/img/providers/routing/capitalmanagement.png)

## Test Information

Requires having account in CapitalManagement Sandbox environment (https://sandbox-console.capital-management.info/) 
to check if transaction is present.
Testing can be done on STAGE env. using TEST account and test currencies (EUR, USD, RUB).

To test different payment results, fill in the desired status in the name of the cardholder:

| Payment status | Description                           |
|----------------|---------------------------------------|
| SUCCESS        | Payment approved                      |
| APPROVED       | Payment approved                      |
| PENDING        | Payment pending                       |
| ERROR          | Rejected by general error             |
| DECLINED       | Rejected with validation to authorize |


