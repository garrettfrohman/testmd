--- 
id: "pay4fungo" 
title: "Pay4Fun Go"
hide_title: "true"
---

![](/img/providers/logos/pay4fungo.png)

# Pay4Fun Go

## About
Pay4Fun GO is a gateway system for direct deposit (Pay In) and withdrawal (Pay Out) on the merchant website.

Pay4Fun's API works with a redirect integration model: you will redirect* customers
from your website to the Pay4Fun Authentication page where they type their
Pay4Fun credentials to complete the payment.

| Provider Name                | Pay4Fun Go                                     |
|------------------------------|------------------------------------------------|
| Link                         | [https://p4f.com/](https://p4f.com/)           |
| Classification               | Online Banking                                 |
| Regions                      | `Brazil`                                       |
| Currencies                   | `BRL`, `GBP`, `USD`, `EUR`                     |
| Methods/PaymentTxTypes       | `Pay4FunGoDeposit` <br/> `Pay4FunGoWithdrawal` |
| PaymentIQ Configuration File | `Pay4fungoConfig`                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pay4fungo.Pay4fungoConfig>
    <enabled>true</enabled>
    <testMode>false</testMode>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <merchantId>??</merchantId>
                <secretKey>??</secretKey>
                <encryptionKey>??</encryptionKey>
                <supportedCurrencies>BRL|EUR|USD|GBP</supportedCurrencies>
                <defaultCurrency>BRL</defaultCurrency>
                <customerCheck>[true|false]</customerCheck>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.pay4fungo.Pay4fungoConfig>
```
Example with set variables:
```xml
<com.devcode.paymentiq.integration.pay4fungo.Pay4fungoConfig>
    <enabled>true</enabled>
    <testMode>false</testMode>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <merchantId>123</merchantId>
                <secretKey>1234567</secretKey>
                <encryptionKey>1234567</encryptionKey>
                <supportedCurrencies>BRL|EUR|USD|GBP</supportedCurrencies>
                <defaultCurrency>USD</defaultCurrency>
                <customerCheck>false</customerCheck>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.pay4fungo.Pay4fungoConfig>
```

</details>

### Attributes

| Attribute             | Description                                                                                                                                                                                                                                                             |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId    | This is a unique identifier provided to every merchant by Pay4Fun. MID is part of your account credentials and is different on staging and production environment.                                                                                                      |
| account.secretKey     | This is a secret piece of information used as part of the seed string to generate communication hash. It can be obtained/generated from Pay4Fun back-office (Account -> API -> Credentials -> DIRECT API).                                                              |
| account.encryptionKey | This is a private key used for secure encryption of every request. It can be obtained/generated from Pay4Fun back-office (Account -> API -> Credentials -> DIRECT API).                                                                                                 |
| account.customerCheck | Boolean flag to let the merchant share customer's info upon deposit with the provider if available (Zipcode, email, full name, date of birth, CPF). If not set or by default, the property is treated as set to "false", so no user's data is shared with the provider. |
| labelId               | LabelId which corresponds to the labelId set in the Pay4Fun backoffice to be sent for all transactions on a MID.                                                                                                                                                        |

### APMs

| Payment Method  | PaymentIQ Service |
|-----------------|-------------------|
| PIX             | PIX               |
| Boleto          | BOLETO            |
| Bank Transfer   | BANK_TRANSFER     |
| CPF             | CPF               |
| Email           | EMAIL             |
| Telefone        | TELEFONE          |
| Dados Bancarios | DADOS_BANCARIOS   |

### Note

Loading any Pay4Fun URL inside an iframe is not allowed!

### Proper setup of a customer data
For a flawless work of the integration, customer's data should meet the following requirements:
 - in case of providing **phone number** it should be in a format:
 ```
  +AA-BB-CCCCCCCC
  +AA-BB-CCCCCCCCC
 ```
 where
 `AA` -  2-digit country code<br/>
 `BB` -  2-digit area code<br/>
 `CCCCCCCC`, `CCCCCCCCC` -  8- or 9-digit phone number<br/>
 
 Example of valid representation of phone numbers:<br/>
 `+55-11-12345678`<br/>
 `+55-11-123456789`

 - in case of providing **CPF** number (11 digits) it should be provided within `<attributes>` attribute of the user/customer entity:
 ```xml
 <attributes>
    <entry>
        <string>cpf</string>
        <string>12345678901</string>
    </entry>
 </attributes>
 ```

## Example Routing Rule

![](/img/providers/routing/pay4fungo.png)

## Transaction Flow

### Deposit (Pay In):
A Pay In transaction occurs when a Customer starts a direct deposit on the Merchant website.
Confirmed deposits will be credited into the Merchant wallet account.

1. Customer selects payment type for the deposit (PIX, Boleto, Bank transfer, or just Pay4FunGo).<br/>
2. Customer sets the desired amount to be deposited and submits the request for an authentication step.<br/>
3. If initial request is validated successfully at the provider's side - a redirect to authentication page will occur.<br/>
4. At the authentication page the customer enters authentication data (CPF) and submits the data.<br/>
5. If authentication is successful the customer is redirected to the actual deposit processing page, where the customer makes final decision on the payment and obtains deposit instructions.<br/>
6. After obtaining deposit instructions - the customer should follow them in order to have the deposit processed at the provider's side and so the merchant's side as well.<br/>
7. Upon arriving of the funds to the provider's side - the provider issues a notification to the merchant for top-up of the customer's funds.<br/>

### Withdrawal (Pay Out):
A Pay Out transaction occurs when a Customer requests a withdrawal on the Merchant website.
Confirmed withdrawals will be debited from the Merchant wallet account.
Pay Out process has two distinctive parts:
 - Screening
 - Pay Out

1. Customer selects payment type for the withdrawal (Email, Cpf, Telefone, Dados_bancarios) and enters all the required details (email, phone, cpf, amount).<br/>
2. Merchant sends all the Pay Out data (screening endpoint), Pay4Fun then validates CPF, full name, telephone, date of birth and e-mail.
3. If screening is successful the customer is redirected to the authentication page.<br/>
4. The customer initializes authentication process (by requesting pin to be send to email).<br/>
5. Pin is sent to the customer's email - which needs to be entered on the authentication page.<br/>
7. If authentication is successfully validated at the provider's side - merchant sends the actual payload to the Pay Out endpoint.<br/>
8. Pay4Fun processes the Pay Out request and sends respective notification/confirmation upon status change of the transaction to the merchant.<br/>
9. When successful confirmation received at merchant's side - the funds are ready to be released in the customer's favor.<br/>

## Test Information

Requires having account in Pay4Fun UAT environment.

Url for test access:
[http://backtest.p4f.com/Auth/Merchant/Login](http://backtest.p4f.com/Auth/Merchant/Login)

When logged in, please navigate in the top menu to the Account -> API -> Credentials page.
At the Credentials page there could be obtained data which is required for interacting with the Pay4Fun Go API.

From a customer perspective, there are two scenarios: existing Pay4Fun customer or a new user.
Existing customers will have fewer steps and new users will have to provide additional details.

For a new user CPF can be generated at [https://www.4devs.com.br/gerador_de_cpf](https://www.4devs.com.br/gerador_de_cpf)

In the test environment CPF/Full name/DoB are not checked, but email address is.
