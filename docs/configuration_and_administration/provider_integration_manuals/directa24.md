---
id: "directa24"
title: "Directa24 (formerly AstroPay Direct 2.0)"
hide_title: "true"
---

![](/img/providers/logos/directa24.png)

# Directa24 (formerly AstroPay Direct 2.0)

## About
Directa24 offers direct payments - in local currency - from the most popular banks (those that can offer the requisite enabling technology). It consists of a simple integration of the merchant's cashier with our Directa24 (formerly AstroPayDirect 2.0) solution.

Customers go directly from the merchant checkout page to a (customizable for each merchant) payment interface which connects them with their bank of preference. They simply enter some personal data and are forwarded to their online banking page to confirm the payment. Customers immediately receive payment confirmation.

| Provider Name                | Directa24                                                                                   |
|------------------------------|---------------------------------------------------------------------------------------------|
| Link                         | [https://directa24.com/](https://directa24.com/)                                            |
| Classification               | Online Banking                                                                              |
| API                          | Please contact our technicals support team for information.                                 |
| Regions                      | Brazil, Argentina, Mexico, Uruguay, Chile, Columbia, Peru, Bolivia, Venezuela, China, India |
| Currencies                   | Please check directly with the provider regarding what currencies are supported             |
| Methods/PaymentTxTypes       | `BankDeposit`, `AstroPayBankWithdrawal`, `CreditcardWithdrawal`                             |
| PaymentIQ Configuration File | `Directa24Config`                                                                           |

## Migration from AstroPayBankConfig

Migration from AstroPayBankConfig is straightforward and seamless:

1. Configure Directa24 according to the instructions below
2. Route transactions to Directa24 instead of AstroPayBank

## Configuration

### Attributes

| Attribute                           | Description                                                                                                                              |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| username                            | Merchant API Key (X-Login)                                                                                                               |
| password                            |                                                                                                                                          |
| secretKey                           | API Signature                                                                                                                            |
| readOnlyApiKey                      | Read-Only API Key (for fetching payment methods)                                                                                         |
| requestPayerDataOnValidationFailure | Boolean flag sent to Directa24 to request payer data on validation failure. Defaults to `true`.                                          |
| defaultLanguage                     | Decides what default language to use in case the used locale language is not one of the supported `en`, `es`, or `pt`. Defaults to `en`. |

### Bank codes list
#### Get Available Banks (codes) by Country

Directa24 offers a service to retrieve the available bank options for a certain country. This feature is a completely separate request and should be used before a transaction is made in order to display the user its corresponding bank options for their specific country.

The response will also contain the URL for the corresponding logotype for each payment method in order to display it in the merchant's cashier/checkout.

Request: `POST https://api.paymentiq.io/paymentiq/api/directa24/getBanksByCountry`

| JSON params | Type   | M/O | Description                                                                            |
|-------------|--------|-----|----------------------------------------------------------------------------------------|
| merchantId  | String | M   | PaymentIQ merchant which will process the payment. Number is assigned by DevCode.      |
| countryCode | String | M   | ISO Alpha-2 country code representing the user's country to retrieve bank options for. |

**JSON request example**
```json
{
 "merchantId": "1",
 "countryCode": "BR"
}
```

**JSON response example**
```json
[{
  "country": "BR",
  "code": "BL",
  "name": "Boleto",
  "type": "VOUCHER",
  "status": "OK",
  "logo": "https://resources.directa24.com/cashin/payment_method/square/BL.svg",
  "daily_average": 905,
  "monthly_average": 31449
},{
  "country": "BR",
  "code": "BB",
  "name": "Banco do Brasil",
  "type": "BANK_DEPOSIT",
  "status": "OK",
  "logo": "https://resources.directa24.com/cashin/payment_method/square/BB.svg",
  "daily_average": 2506,
  "monthly_average": 7722
}
```
#### Merchant Front-End Configuration
Based on the bank name response above, the merchant should display the banks accordingly in the cashier/checkout, and based on the bank chosen by the end-user to do a payment, the merchant needs to send the `code` of the bank as the `service` parameter to PIQ.

### Sending national/document ID in verifyuser
The standard way is to let the end-user populate their national/document ID in the cashier, however, if the merchant already has this value registered on their users, they can send it in the verifyuser response of the Integration API to PIQ.

The value needs to be sent in the `attributes` object with attribute name `nationalIdentificationNumber`.

## Integration Configuration

To complete the setup with your Directa24 account, you need to access the Directa24 back office to configure the following settings under settings > integration [https://merchants.directa24.com/](https://merchants.directa24.com/).

![](/img/providers/directa2401.png)

### IP Whitelisting

To make sure that Directa24 allow the traffic coming from PaymentIQ, add the [Provider IP Whitelisting](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist) IPs in both the IP address lists.

![](/img/providers/directa2402.png)

## PaymentIQ Back Office Configuration

Once the setup is done in Directa24's back office, the following details should be added to the Directa24Config in the PIQ back office.

Since credentials for deposits and withdrawals are different, two accounts need to be added if both methods are to be used.


**Credentials**

API Key:       ```<username>??</username>```

API Passphrase:   ```<password>??</password>```

API Signature:    ```<secretKey>??</secretKey>```

**Web Status Credentials**

API Key:       ```<readOnlyApiKey>??</readOnlyApiKey>```

```xml
<com.devcode.paymentiq.integration.directa24.Directa24Config>
  <enabled>true</enabled>
  <readOnlyApiKey>??</readOnlyApiKey>
  <accounts>
    <entry>
      <string>withdrawal</string>
      <account>
        <username>??</username>
        <password>??</password>
        <secretKey>??</secretKey>
        <supportedCurrencies>USD|BRL|PEN|MXN|CLP</supportedCurrencies>
      </account>
    </entry>
       <entry>
      <string>deposit</string>
      <account>
        <username>??</username>
        <password>??</password>
        <secretKey>??</secretKey>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.directa24.Directa24Config>
```

#### Wait For Withdrawal Notifications
The normal scenario is that PaymentIQ sets the withdrawal to success after it has been successfully received by Directa24 and waiting for it to be processed. If anything goes wrong during processing a reversal is created. To instead wait with setting success until a notification that the money has reached the user's account can be done by adding this to Directa24Config:

`<waitForWithdrawalNotification>true</waitForWithdrawalNotification>`

Note that there is always a risk invovled with using this configuration that the merchant needs to be aware of. If anything goes wrong with the transaction (e.g. misconfiguration, human error, connection issues etc) while it is waiting to be processed at the provider that causes PaymentIQ to set it to FAILED means that a cancel will be sent to the merchant. At the same time it is possible that the provider successfully executed it and the user received the money on their end. So be very careful using this setting.

### PIX Configuration
1. Use `AstroPayBankWithdrawalInput`
2. MerchantConfig: configure `PIX` service for `ASTROPAYBANK`
```json
<entry>
  <string>ASTROPAYBANK</string>
  <string>DIRECTA24|PIX</string>
</entry>
```
3. Rules > Payment Methods: enable `ASTROPAYBANK-PIX` deposit option

## Example Routing Rule
![](/img/providers/routing/directa24.png)
![](/img/providers/routing/directa24_2.png)

## Test Information

### Deposit
- The test user/customer must use the correct currency supported for the country code, e.g `BRL` for country `BRA`.

1. Make sure to use the correct service (bank) parameter based on the country, e.g `BB` for `BRA`. An example of available values can be found below. To fetch all available codes use the [Get available banks](./directa24#get-available-banks-codes-by-country) request.
2. Follow the instructions in the window to complete the payment.
3. Once the process is completed in the window, the transaction has to be approved from the Directa24 [back office](https://merchants-stg.directa24.com) by navigating to `Transactions > Deposits` and selecting the deposit, then in the upper hand corner choose Approve deposit from the menu.

![](/img/providers/astropaybank04.png)

#### Available Staging Bank Codes (service value)

| Country   | Code/Service |
|-----------|--------------|
| Argentina | SI           |
| Brazil    | B            |
| Brazil    | BB           |
| Brazil    | CA           |
| Brazil    | I            |
| Mexico    | BM           |
| Mexico    | BQ           |
| Uruguay   | RE           |

### Withdrawals

| Country | National ID    | Bank Code | Bank Branch | Bank Account       | Account Type | Document type |
|---------|----------------|-----------|-------------|--------------------|--------------|---------------|
| BRA     | 747.873.778-17 | 003       | 7197        | 88365484           | S(Savings)   |               |
| COL     | 7478737781     | 006       | 7197        | 88365484           | S(Savings)   | CC            |
| CHL     | 76086428-5     | 001       | 7197        | 88365484           | S(Savings)   | RUT           |
| MEX     | 747.873.778-17 | 006       | 7197        | 032180000118359719 | S(Savings)   |               |

More bank codes are listed at https://docs.directa24.com/deposits-api/payment-methods#considerations


### Debit Cards cashout
For withdrawals to Mexican debit cards, the tx type **CreditcardWithdrawal** should be used with a service. In the payment methods rules, the merchant should activate the withdrwal metho **CreditcardWithdrawal-DIRECTA24**.

### JSON examples
**Request for credit card withdrawal**
```json
{
  "merchantId": "1",
  "userId": "DIRECTA_IND",
  "sessionId": "asdf",
  "amount": "1",
  "encCreditcardNumber": "X810WchqvsY8tww12//rEIGrJapsQDQ7TdBAzxCBgd8i3Fn1mXblPBbOSyGk5gWDKEdyHOr/+zPyVIBBpmHy76WoYq7HRvir6bIazBbh+8M8XWGBRrI/AHGeUR8msr4p4a5+uyLybcOvA6JaS/LXuIqR77ACpc+yA+2szvKc4LOuE74XrQnNAoYGWRyjxRj3+LliKdNqtxy6+iHSy8k4QEHj/zBoEqfmDEnNflMXp/4+qCi5pDxVUGNwTyP0QMeEZzy1qnlOO9GDwz5i7MIhaTpByl+yi/2SNlIcE38KO5WEMNr9XKSyphE7yeWN9+wibtxBsgacv68a/uQm597FZA==",
   "nationalId":"747.873.778-17",
   "bankCode":"006",
   "bankBranch":"7197",
   "accountType":"C",
   "service":"DIRECTA24"
}

```

**Response**
```json
{
    "txState": "SUCCESSFUL",
    "messages": [
        {
            "label": "creditcardwithdrawal.receiptWithdrawalAccountToCharge",
            "keys": [
                "creditcardwithdrawal.receiptWithdrawalAccountToCharge",
                "receiptWithdrawalAccountToCharge"
            ],
            "value": "491629******5597"
        },
        {
            "label": "creditcardwithdrawal.receiptWithdrawalAmount",
            "keys": [
                "creditcardwithdrawal.receiptWithdrawalAmount",
                "receiptWithdrawalAmount"
            ],
            "value": "1.00 INR"
        },
        {
            "label": "creditcardwithdrawal.receiptWithdrawalFee",
            "keys": [
                "creditcardwithdrawal.receiptWithdrawalFee",
                "receiptWithdrawalFee"
            ],
            "value": "0.00 INR"
        },
        {
            "label": "creditcardwithdrawal.receiptWithdrawalTxAmount",
            "keys": [
                "creditcardwithdrawal.receiptWithdrawalTxAmount",
                "receiptWithdrawalTxAmount"
            ],
            "value": "1.00 INR"
        },
        {
            "label": "creditcardwithdrawal.receiptWithdrawalInProgressExtraMsg",
            "keys": [
                "creditcardwithdrawal.receiptWithdrawalInProgressExtraMsg",
                "receiptWithdrawalInProgressExtraMsg"
            ],
            "value": ""
        },
        {
            "label": "creditcardwithdrawal.receiptWithdrawalPspRefId",
            "keys": [
                "creditcardwithdrawal.receiptWithdrawalPspRefId",
                "receiptWithdrawalPspRefId"
            ],
            "value": "69688"
        }
    ],
    "txRefId": "1A161456542",
    "statusCode": "SUCCESS_WITHDRAWAL_AUTO_APPROVAL",
    "txId": 161456542,
    "maskedAccount": "491629******5597",
    "success": true
}
```

## Test Information

### Withdrawals


| Country | National ID    | Bank Code | Bank Branch | Debit Card       | Account Type         | Document type |
|---------|----------------|-----------|-------------|------------------|----------------------|---------------|
| MEX     | 747.873.778-17 | 006       | 7197        | 4916297181305597 | S/C(Savings/Current) |               |

The merchant can also create its own debit cards for testing at https://generator-credit-card.com/
