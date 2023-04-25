--- 
id: "oktopay" 
title: "Oktopay"
hide_title: "true"
---
 
![](/img/providers/logos/oktopay.png)

# Oktopay

## About
OKTO is a leading fintech firm specialised in innovative digital payment solutions and applications across multiple industries, including banking, retail, hospitality and gaming.
The company’s bespoke 360 cashless payment environment is designed for the mobile world, connecting online and retail platforms through smartphone technology, while its offering comprises digital banking, mobile payment and retail solutions, as well as cash-based gaming. 

| Provider Name                | Oktopay                                                                                                                                                         |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [www.oktopay.eu/](http://www.oktopay.eu/)                                                                                                                       |
| Classification               | Cash operations / Ewallet                                                                                                                                       |
| Regions                      | `International`                                                                                                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                 |
| Methods/PaymentTxTypes       | `OktoPayCashDeposit`<br/>  `OktoPayCashWithdrawal`<br/>  `OktoPayWalletDeposit`<br/>  `OktoPayWalletWithdrawal`<br/> `PixDeposit`<br/> `BankDomesticWithdrawal` |
| PaymentIQ Configuration File | `OktopayConfig`                                                                                                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.oktopay.OktoPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>xxxxx</merchantId>
        <secretKey>xxxxxx</secretKey>
        <notificationSecret>xxxxxx</notificationSecret>
        <transactionChannel>xx_xxx_xxxx->xxxxxxx,xx_xxx_xxxx->xxxxxxx,xx_xxx_xxxx->xxxxxxx</transactionChannel>
        <requestKyc>true</requestKyc>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>DevCode payment</defaultDescriptor>
  <cashRedirectTemplateName>oktopay-barcode-redirect-template</cashRedirectTemplateName>
  <gs1Pattern>010%s211000000000000%s</gs1Pattern>
</com.devcode.paymentiq.integration.oktopay.OktoPayConfig>

```

</details>

### Attributes

| Attribute                | Description                                                                                                                                                                                                                                                                                                                 | Example                                      |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| merchantId               | Provided by OktoPay                                                                                                                                                                                                                                                                                                         |                                              |                                                             |
| secretKey                | Provided by OktoPay                                                                                                                                                                                                                                                                                                         |                                              |                                                                                |
| notificationSecret       | PIQ Tech Support will generate an API key for psp, that will be used for callbacks                                                                                                                                                                                                                                          |                                              |    
| transactionChannel       | PIQ Tech Support can map combination of CountryCode_Currency_AmountInFractionalUnits with the PackageId. Merchant can request PackageId data from OktoPay, applicable for particular Country, Currency & Amount value                                                                                                       | `IT_EUR_1000->8055348521276`                 |
| gs1Pattern               | This String pattern will be used to generate GS1 Barcode, wherein PackageId & PaymentCode values received in the Tx response, would replace the corresponding params from the pattern String. The pattern given in ExampleConfig is used by default. OktoPay will provide us with the pattern, if there is any change to it | `010{packageId}211000000000000{paymentCode}` |
| cashRedirectTemplateName | Specify the name of HTML template that will be used to display the generated barcode. "oktopay-barcode-redirect-template" is used by default.                                                                                                                                                                               | `oktopay-barcode-redirect-template`          |
| requestKyc               | This controls if a KYC request should be performed before the transaction is done or not. This is specified on account level.                                                                                                                                                                                               |                                              |

### Notification/Callback setup
Callback/Notification URL can be set by the merchant using Oktopay webhook API. The apiKey value equals the notificationSecret value entered in the config and the Bearer value equals the secretKey entered in the config. 
While using the Oktopay webhook API for setting the Callback/Notification URL would be the fastest approach, one can also reach out to Oktopay support and ask for their assistance to manually set the Callback/Notification URL

#### Notification/Callback setup test
`curl --request POST \
  --url 'https://sit.oktopay.eu:9443/api/integration/webhook' \
  --header 'Accept: application/vnd.okto-merchant-api.v1+json' \
  --header 'Authorization: Bearer xxxxxxxxxxxxxxxx' \
  --data 'url=XXXXX' \
  --data 'apiKey=XXXXX'`

#### Notification/Callback setup production
`curl --request POST \
  --url 'https://api.oktopay.eu/api/integration/webhook' \
  --header 'Accept: application/vnd.okto-merchant-api.v1+json' \
  --header 'Authorization: Bearer xxxxxxxxxxxxxxxx' \
  --data 'url=XXXXX' \
  --data 'apiKey=XXXXX'`


### Callback URL test
`https://test-api.paymentiq.io/paymentiq/api/oktopay/callback`

### Callback URL hosted production
`https://api.paymentiq.io/paymentiq/api/oktopay/callback`

### Notification/Callback setup OKTO.PIX
Setting the notification secret key and callback URLs can be requested to OKTO.PIX or by using their Operator API.
It is important to specify a notificationToken (signature key) different from the accessToken(apiKey) due to security reasons.
By default, the apiKey and notificationSecret will have the same value (notificationSecret inherits the apiKey). Using this API deposit and withdrawal URLs are both set.
The Bearer value is the apiKey OKTO.PIX provides.

#### Notification/Callback setup test - OKTO.PIX
`curl --location --request PUT 'https://demo-pix.oktopay.eu:9443/operator' \
--header 'accept: */*' \
--header 'Authorization: Bearer xxxxxxxxxxxxxxxx \
--header 'Content-Type: application/json' \
--data-raw '{
"depositUrl": XXXXX,
"withdrawUrl": XXXXX,
"notificationToken": XXXXX
}'`

#### Notification/Callback setup production - OKTO.PIX
`curl --location --request PUT 'https://pix-sit.oktopay.eu:9443//operator' \
--header 'accept: */*' \
--header 'Authorization: Bearer xxxxxxxxxxxxxxxx \
--header 'Content-Type: application/json' \
--data-raw '{
"depositUrl": XXXXX,
"withdrawUrl": XXXXX,
"notificationToken": XXXXX
}'`

#### Callback URL test - OKTO.PIX
`https://test-api.paymentiq.io/paymentiq/api/oktopay/callback/pix`

#### Callback URL hosted prod - OKTO.PIX
`https://api.paymentiq.io/paymentiq/api/oktopay/callback/pix`

## Transaction Flow

## OktoCash flow
After user first request of OktoPay transaction he will be redirected to T&A page that he suppose to accept to proceed the transaction

Deposit:
1. After successful request to OktoPay GS1 barcode is generated and user is redirected to page with GS1 barcode that has to be shown in the shop to proceed payment.
2. After shop handle cash operation Bambora receives callback with tx status

Withdrawal
1. After successful request to OktoPay QR Code is generated and is sent to users email.
2. After shop handle cash operation Bambora receives callback with tx status

## OktoWallet flow
1. After successful request to OktoPay QR code is generated and user is redirected to page with QR code that has to be scanned with Okto SIT app to proceed payment.
2. After user approves transaction in the app Bambora receives callback with tx status

## OKTO.PIX flow
Deposit:
1. User specifies the amount to be deposited and the national id number(CPF) in cashier.
2. User is redirected to a page where he can scan or copy the QR code generated for the PIX transaction.
3. Using a mobile banking app the user scans the code and completes the transfer.
4. Notification is sent to PIQ to update transaction to final state.

Withdrawal:
1. User specifies the amount to be withdrawn and the national id number(CPF) in cashier.
2. Withdrawal is approved if not auto-approved.
3. Notification is sent to PIQ to update transaction to final state.

## Example Routing Rules
![](/img/providers/routing/oktopay.png)
![](/img/providers/routing/oktopay_pix.png)

## Test Information
To test OktoWallet OktoSIT app should be installed. It can be requested from OktoPay team.

### OKTO.PIX
| Name                      | CPF            |
|---------------------------|----------------|
| Joao Pedro Ferreira Lopez | 051.233.865-56 |
| Mineiro Chiotiz           | 141.040.632-66 |
| Joãão Silvãã              | 707.726.010-03 |


 For more test information and examples visit [https://demo-pix.oktopay.eu:9443/swagger-ui.html](https://demo-pix.oktopay.eu:9443/swagger-ui.html).