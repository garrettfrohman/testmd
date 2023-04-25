--- 
id: "AstroPayCard" 
title: "AstroPay Card"
hide_title: "true"
---
 
![](/img/providers/logos/astropaycard.png)

# AstroPay Card

## About
**AstroPay Card** is a virtual voucher designed for customers who need to perform real-time operations in their local currency.

**One Touch** is AstroPay virtual wallet that allows users to easily and securely make deposits and withdrawals directly from the merchant site.

**Pay by Astropay** is a feature that allows you to show the local payment methods on your site to tell the user he can pay with that method through his Astropay wallet in a single checkout instead of having to top up the wallet first.

| Provider Name                | AstroPayCard                                                                                                                             |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Links                        | [https://www.astropay.com/](https://www.astropay.com/)<br/><br/>[https://merchant.astropaycard.com/](https://merchant.astropaycard.com/) |
| Classification               | Virtual pre-paid card / Wallet                                                                                                           |
| Regions                      | `International`                                                                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                          |
| Methods/PaymentTxTypes       | `AstroPayCardDeposit`<br/>`AstroPayCardWithdrawal`<br/>`Refund`<br/>~~`CreditcardDeposit`~~                                              |
| PaymentIQ Configuration File | `AstroPayCardConfig`                                                                                                                     |

- Please note that `CreditcardDeposit` is deprecated for AstroPay Card and should not be used for new integrations. Please use `AstroPayCardDeposit` instead.
- Please note that `Refund` is not usable with the new OneTouch API.

## Configuration Information

You need to log in to your [AstroPay merchant account](https://merchant.astropaycard.com) and navigate to `Integration -> Credentials & Settings` to find the credentials needed to configure your AstroPayCardConfig in PIQ.

### Migrate to the new API (OneTouch)
AstroPay is now offering a new API called OneTouch, and their old API was to be terminated at the end of 2020 (31/12). If you as a merchant is using their existing old API, please follow these steps to move over to the OneTouch API.

__Note__: Before you do anything live, it is highly recommended to do these steps on the test environment first.

- Make sure you have received access to the new API with your existing account by contacting AstroPay.
- Create a new account entry in your `AstroPayCardConfig` on your MID in PaymentIQ. See the configuration example [below](/docs/configuration_and_administration/provider_integration_manuals/AstroPayCard#example-account-config-entry-for-new-api) on how the entry should look like.
- Add the needed `secretKey` and `apiKey` values to the new config entry. You will find these values on your merchant account with AstroPay. Also check with AstroPay what your "Merchant category code" (`mcc`) and "Merchant product code" (`merchantCode`) should be and update those values.
- Make sure the `serviceEndpoint` entry is present with the correct value. The correct endpoints are `https://onetouch-api-sandbox.astropay.com` for sandbox/staging and `https://onetouch-api.astropay.com` for production.
- Make sure the `defaultDescriptor` entry is added to the root level of the AstroPayCardConfig. Example: `<defaultDescriptor>Bambora Payment</defaultDescriptor>`.
- Create a new routing rule which points to your newly created configuration PSP account, and make sure to add the action `PSP version` with value `REST`. Please see the [example routing rule](/docs/configuration_and_administration/provider_integration_manuals/AstroPayCard#example-routing-rule) section for more details.
- Before processing, please read the additional notes about the API [here](/docs/configuration_and_administration/provider_integration_manuals/AstroPayCard#additional-notes-about-new-onetouch-api).
- All done! You are now ready to use the new API.

__Note__: If you are not confident enough to update the configurations in PIQ yourselves, please contact our [Technical Support](/docs/technical_support_and_troubleshooting/contacttechsupport) for assistance.

#### Example account config entry for new API
```xml
<entry>
  <string>default_new</string>
  <account>
    <secretKey>??</secretKey>  <!-- Secret key  -->
    <apiKey>??</apiKey> <!-- Key -->
    <mcc>7995</mcc> <!-- Merchant category code, e.g 7995 -->
    <merchantCode>gambling</merchantCode> <!-- Merchant product code, e.g gambling -->
    <container>window</container>
    <serviceEndpoint>https://onetouch-api.astropay.com</serviceEndpoint>
      <merchantName>Test Merchant</merchantName>
      <logoUrl>https://resources.merchant.com/logo.png</logoUrl>
  </account>
</entry>
```

<details>
<summary>Click to view full example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.astropay.AstroPayCardConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <width>800</width>
  <height>850</height>
  <accounts>
    <!-- New API account -->
    <entry>
      <string>default_new</string>
      <account>
        <secretKey>??</secretKey>  <!-- Secret key  -->
        <apiKey>??</apiKey> <!-- Key -->
        <mcc>7995</mcc> <!-- Merchant category code, e.g 7995 -->
        <merchantCode>gambling</merchantCode> <!-- Merchant product code, e.g gambling -->
        <container>window</container>
        <serviceEndpoint>https://onetouch-api-sandbox.astropay.com</serviceEndpoint>
      </account>
    </entry>
    <!-- Old API account -->
    <entry>
      <string>default</string>
      <account>
        <username>??</username>    <!-- x_login     -->
        <password>??</password>    <!-- x_trans_key -->
        <secretKey>??</secretKey>  <!-- Secret key  -->
      </account>
    </entry>
  </accounts>
  <sendCardToMerchant>false</sendCardToMerchant>
  <testMode>true</testMode>
  <defaultDescriptor>Bambora Payment</defaultDescriptor>
</com.devcode.paymentiq.integration.astropay.AstroPayCardConfig>
```

</details>  

### Attributes

#### New API (OneTouch)
| Attribute         | Description                                                                                                                                                                  |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| secretKey         | Corresponds to "Secret Key" found in your AstroPay merchant account under `Integration -> Credentials & Settings`                                                            |
| apiKey            | Corresponds to "Key" found in your AstroPay merchant account under `Integration -> Credentials & Settings`                                                                   |
| mcc               | Merchant category code, e.g 7995                                                                                                                                             |
| merchantCode      | Merchant product code, e.g gambling                                                                                                                                          |
| defaultDescriptor | Populates the value of the "description" parameter to AstroPayCard. Defaults to "NA" if not set.                                                                             |
| version           | Set the value to `2` if you want to use the v2 Cashouts. It can be set both on the root level of AstroPayCardConfig or directly on a specific account. Default value is `1`. |
| merchantName      | (Optional) Merchant name which will appear on OneTouch cashier when user will be redirected.                                                                                 |
| logoUrl           | (Optional) Merchant logo URL will appear on OneTouch cashier when user will be redirected. Note the logo needs to be hosted on a public https URL.                           |

#### Old API
| Attribute          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username           | Corresponds to "x_login" found in your AstroPay merchant account under `Integration -> Credentials & Settings`                                                                                                                                                                                                                                                                                                                                                                                                                    |
| password           | Corresponds to "x_trans_key" found in your AstroPay merchant account under `Integration -> Credentials & Settings`                                                                                                                                                                                                                                                                                                                                                                                                                |
| secretKey          | Corresponds to "Secret Key" found in your AstroPay merchant account under `Integration -> Credentials & Settings`                                                                                                                                                                                                                                                                                                                                                                                                                 |
| sendCardToMerchant | This flag set in the root (higher level) xml and will determine how AstroPayCard will handle the created card during a payout.  <br/> *False* = AstroPay will directly send an email to the customer. <br/> *True* = AstroPay will directly send an email to the merchant. The merchant will send the card to the customer. The merchant email address has to be configured in AstroPaysCard Back Office. The email will be sent to the customer after the transaction is Approved. <br/>  ![](/img/providers/astropaycard03.png) |
| sendPhoneNumber    | This flag set in the root (higher level) xml and will determine if we should use new endpoint and send mobile phone number to AstroPay on withdrawals. Can't be used with the setting `sendCardToMerchant`. Default is true. Set to false to use old endpoint.                                                                                                                                                                                                                                                                    |

### Whitelisting PaymentIQ IPs
In your merchant account under `Integration -> Credentials & Settings`, you will also have to whitelist the PaymentIQ IP addresses. Please find the IPs that needs to be whitelisted [here](/docs/configuration_and_administration/system_configuration/provider_ip_whitelist)

#### Merchant account example
![](/img/providers/astropaycard06.png)

---
### Going LIVE
When you are ready to go Live, you need to login to your AstroPay merchant account and select LIVE up in the left corner. This information will appear.

![](/img/providers/astropaycard05.png)

---
### Production information for cashouts (Old API)
When a user does a cashout, it is sent to their mobile app. If the user doesn't have the app and doesn't download the app within 24 hours (Astropay send an SMS informing the user he has a card to cashout and to download the app) then the cashout is canceled.
If the user has the app installed, the cashout is instant.

---
### Additional notes about new OneTouch API
You still use the same `AstroPayCardDeposit` and `AstroPayCardWithdrawal` transaction types, however the input parameters are changed. You no longer give an AstroPay card as input values for deposits, instead you just choose the amount, initiate the deposit, and then get redirected to AstroPay's window where you either log in to your account, or use an already owned virtual card.

A deposit using an AstroPay account will save the AstroPay user ID in PIQ to be later used for withdrawals. To perform a withdrawal the user can use a saved account from a previous successful deposit while being logged in to their Astropay account, or using the phone number either provided from the cashier or using the value registered on the user. If the user made a deposit with the "existing Astropay Card" option there won't be any account saved in PIQ which means a withdrawal can not be made using a saved account, instead a withdrawal using the phone number will have to be made.

For more information about the PIQ endpoints and input parameters for AstroPayCard, see the front api voucher section.

---
### Pay by Astropay

To use the "Pay by Astropay" feature you as a merchant need to send the correct APM code to PIQ as the `service` parameter in the AstroPayCardDeposit request. The available APMs can be found in this [document](https://developers-wallet.astropay.com/images/Payment_methods%20Codes.rtf).

The document lists the available APMs per country, for example:

| country | code | name |
|---------|------|------|
| BR      | IX   | Pix  |

The value in the **code** column is the value you need to send as the `service` value to PIQ. To use the APM **Pix** as in this example, the `service` value has to be `IX`.

If you want to separate each APM in the cashier you can add service mapping for the `ASTROPAYCARD` payment method. [Here](/docs/configuration_and_administration/system_configuration/servicemapping) is a guide on how to achieve this.

---
### Cashouts V2

AstroPay provides a new version of their Cashouts API (withdrawals) called V2. The main feature with this version is that the end-user will now get redirected to AstroPay's checkout when performing a withdrawal. This is an attempt to improve the end-users experience and reduce the cases where withdrawals get rejected because of invalid or incorrectly formatted phone numbers.

#### How to use
- Contact AstroPay and make sure that your merchant account is enabled for Cashouts V2.
- In the PaymentIQ back office, add the entry `<version>2</version>` to your AstroPayCardConfig on the account where you want to enable Cashouts V2.
- In order for the end-user to be redirected, you **must** configure an approval rule in PaymentIQ that automatically and instantly approves the withdrawal request. See image below for an example rule.

![](/img/providers/astropaycard07.png)

#### Using a "withdrawal method code"
Similarly to the **Pay by Astropay** feature for deposits, it is possible with Cashouts V2 to send a **withdrawal method code** in the request to AstroPay. This is done by sending the correct method code as the `service` value to PIQ in the AstroPayCardWithdrawal request.

The currently known code (from PaymentIQ's perspective) is `TR` for Indian Bank transfers. Please contact your AstroPay account manager for more methods.

---
## Example Routing Rule
### New API (OneTouch)
To use the OneTouch API, it is required to use action `PSP version` with value `REST`
![](/img/providers/routing/astropaycard03.png)

### Old API
![](/img/providers/routing/astropaycard04.png)

## Test Information

### Deposits

Please test with the smallest amount possible, since the funds are being depleted from the account/cards.

#### With an AstroPay account

When redirected, follow these steps:

- Enter Sweden (46) as country and phone number `0721231212`, then press "Continue".
- Enter code `000000` and press "Continue".
- Select "Use my AstroPay wallet", then choose "Confirm Deposit" on the next page to complete the payment.

If for some reason the above account does not work (not enough funds or monthly limit exceeded) you can easily register your own test user account by navigating to [this page](https://web-app-stg.astropay.com/signup).

#### With an existing AstroPay Card

**If you want to use an existing card, note that you should choose the "I have an AstroPay Card" option at the bottom of the page.**

| Number           | Code | Currency | Expiry date |
|------------------|------|----------|-------------|
| 1616676129354180 | 6992 | USD      | 07-2022     |
| 1612005076819108 | 9850 | EUR      | 07-2022     |
| 1613557082485349 | 5757 | BRL      | 07-2022     |

##### Old API

Send to mobile number.

| Number      | Status    |
|-------------|-----------|
| 59899473333 | COMPLETED |
| 59898535435 | COMPLETED |

### Withdrawals

#### New API

##### With a saved account

Use the saved account from a previous successful deposit to initiate the withdrawal. The previous deposit has to have been [with an Astropay account](/docs/configuration_and_administration/provider_integration_manuals/AstroPayCard#with-an-astropay-account).

If using **Cashouts V2** you will be redirected to AstroPay's window to complete the withdrawal.

##### Without a saved account

If no previous successful deposit has been made using the Astropay account, you can initiate a withdrawal using the phone number `+460721231212`. You can either provide the phone number via the cashier and input parameter `phoneNumber`, or if this is not provided the phone number registered on the user will be used (the `mobile` value).

If using **Cashouts V2** you will be redirected to AstroPay's window to complete the withdrawal.

#### Old API
When testing withdrawals please use phone number 59899473334. For this number, the “virtual end-user” has the app installed and an instant notification will be sent to PaymentIQ that the withdrawal is approved.
