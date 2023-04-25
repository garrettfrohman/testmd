--- 
id: "connectpay" 
title: "ConnectPay"
hide_title: "true"
---
 
![](/img/providers/logos/connectpay.png)

# ConnectPay

## About
ConnectPay is one of the fastest growing Electronic Money Institutions (EMI) in Lithuania – the leading fintech hub in continental Europe - providing banking services for Internet based companies.

ConnectPay’s main activity and focus is banking payment services for business and institutional clients:

SEPA & SWIFT payments, Multicurrency accounts, Corporate cards, Merchant accounts.

| Provider Name                | ConnectPay                                         |
|------------------------------|----------------------------------------------------|
| Link                         | [https://connectpay.com/](https://connectpay.com/) |
| Classification               | Online Banking                                     |
| Regions                      | `EU`                                               |
| Currencies                   | `EUR`                                              |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `BankIBANWithdrawal`         |
| PaymentIQ Configuration File | `ConnectPayConfig`                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.connectpay.ConnectPayConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>CONNECTPAY</string>
            <account>
                <use3Dsecure>false</use3Dsecure>
                <beneficiaryAccountNumber>??</beneficiaryAccountNumber>
                <beneficiaryName>Jonah Jameson</beneficiaryName>
                <username>??</username> <!--api key from ConnectPay devapp-->
                <password>??</password> <!--api secret corresponding to api key from ConnectPay devapp-->
                <apiKey>??</apiKey> <!--authCode from ConnectPay account-->
                <brandId>??</brandId>
                <supportedCurrencies>EUR</supportedCurrencies>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.connectpay.ConnectPayConfig>
```

</details>

### Attributes

| Attribute                              | Description                                                                                                                                                                                                                                                                                                                                                                                                                     |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.beneficiaryAccountNumber | Merchant's IBAN number                                                                                                                                                                                                                                                                                                                                                                                                          |
| accountConfig.beneficiaryName          | Holder name of the merchant's IBAN account.                                                                                                                                                                                                                                                                                                                                                                                     |
| accountConfig.username                 | API key from ConnectPay dev app                                                                                                                                                                                                                                                                                                                                                                                                 |
| accountConfig.password                 | Corresponding API secret to API key from ConnectPay dev app                                                                                                                                                                                                                                                                                                                                                                     |
| accountConfig.brandId                  | Corresponds to *brandId* from ConnectPay. This parameter is provided by ConnectPay.                                                                                                                                                                                                                                                                                                                                             |
| accountConfig.apiKey                   | One-time auth code generated in ConnectPay Online Banking account. For both payment methods (`WebRedirectDeposit`, `BankIBANWithdrawal`) should be used different types of auth code - for `WebRedirectDeposit` - Merchant API type, for `BankIBANWithdrawal` - OnlineBanking API. On how to generate the auth code see more [here](https://developers.connectpay.com/cp/security/generate-authcode-via-online-banking-portal). |
| variable1                              | Optional parameter. Corresponds to *generic1* from ConnectPay.                                                                                                                                                                                                                                                                                                                                                                  |
| variable2                              | Optional parameter. Corresponds to *generic2* from ConnectPay.                                                                                                                                                                                                                                                                                                                                                                  |
| variable3                              | Optional parameter. Corresponds to *generic3* from ConnectPay.                                                                                                                                                                                                                                                                                                                                                                  |

Note: for generating auth code it is required to have ConnectPay Online Banking account as well as ConnectPay dev account. Please reach out to ConnectPay support, so they can assist you with this.

Note: for generating API key (accountConfig.username) and corresponding API secret (accountConfig.password), it is required to create dev app in ConnectPay dev account. Information about opening dev account is [here](https://developers.connectpay.com/cp/dev-portal/open-developer-account). Information about opening a dev app within dev account can be found [here](https://developers.connectpay.com/cp/dev-portal/create-developer-application).

## Example Routing Rule

![](/img/providers/routing/connectpay.png)

## Test Information

IBAN number for testing withdrawals: LT103740020000000123
