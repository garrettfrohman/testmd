--- 
id: "skrill" 
title: "Skrill"
hide_title: "true"
---
 
![](/img/providers/logos/skrill.png)

# Skrill

## About
Skrill is an e-commerce business that allows payments and money transfers to be made through the Internet, with a focus on low-cost international money transfers.

| Provider Name                | Skrill                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.skrill.com/en/](https://www.skrill.com/en/)                        |
| Classification               | Wallet                                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `SkrillDeposit` <br/> `SkrillWithdrawal`                                        |
| PaymentIQ Configuration File | `SkrillConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.skrill.SkrillConfig>
  <enabled>true</enabled>
  <accounts>    
    <entry>
      <string>deposits</string>
      <account>
        <accountID>??</accountID>
        <username>??</username>
        <password>??</password> <!-- to be MD5 hashed -->
        <secretKey>??</secretKey> <!-- to be MD5 hashed -->
         <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
        <onDemandEnabled>true</onDemandEnabled>
      </account>
    </entry>
    <entry>
      <string>withdrawals</string>
      <account>
        <accountID>??</accountID>
        <username>??</username>
        <password>??</password> <!-- to be MD5 hashed -->
        <secretKey>??</secretKey> <!-- to be MD5 hashed -->
         <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
        <onDemandEnabled>true</onDemandEnabled>
        <multiCurrency>false</multiCurrency> <!-- Set to true for new skrill customers -->
      </account>
    </entry>
    <entry>
      <string>qco</string>
      <account>
        <accountID>??</accountID>
        <storeId>??</storeId>
        <username>??</username>
        <password>??</password> <!-- to be MD5 hashed -->
        <secretKey>??</secretKey> <!-- to be MD5 hashed -->
         <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
  </accounts>
  <confirmationNote>${defaultTransactionDescriptor}</confirmationNote>
  <recipientDescription>${defaultTransactionDescriptor}</recipientDescription> <!-- Custom Descriptor that default to 'PaymentIQ Test'-->
  <oneTapDepositUrl>https://www.skrill.com/app/ondemand_request.pl</oneTapDepositUrl>
  <onDemandNote>${defaultTransactionDescriptor}</onDemandNote>
  <onDemandStatusUrl></onDemandStatusUrl>
  <retryOnDemandCancelAsRegular>true</retryOnDemandCancelAsRegular>
  <!-- Added in 1.3.12 Additional information that is shown in transaction reports
  <detail1Description>Detail:</detail1Description>
  <detail1Text>Text</detail1Text>
   -->
  <!-- Add for additional data
  <detail2Description>Detail Description 2</detail2Description>
  <detail2Text>Detail Text 2</detail2Text>
  -->
  <useMQI>true</useMQI> <!-- Set true if Merchant Query Interface is activated for merchant -->


  <!-- Enable the Skrill customer verification check, true or false -->
 <customerCheck>false</customerCheck>
<!--  Decide which account parameters that need to match, separated by |
        Possible values firstName|lastName|dateOfBirth|country|postCode
        Defaults to firstname|lastname-->
  <customerVerificationMatchingValues>firstName|country|</customerVerificationMatchingValues>
  <!-- Choose which status code on case of a decline. ERR_DECLINED_FRAUD is default
  <pspCodeToStatusCode>
    <entry>
      <string>VERIFICATION_MATCHING_FAIL</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_OTHER_REASON</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
  </pspCodeToStatusCode>-->

</com.devcode.paymentiq.integration.skrill.SkrillConfig>

```

</details>

### Attributes

| Attribute                          | Description                                                                                                                                                                                                                                               |
|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountID                          | Retrieved from the Skrill backoffice Customer ID.                                                                                                                                                                                                         |
| username                           | Retrieved from the Skrill backoffice Processing Mail.                                                                                                                                                                                                     |
| secretKey                          | Generated by the Merchant in Skrill back office under `Change secret word`. Needs to be MD5 hashed before adding to config.                                                                                                                               |
| password                           | Generated by the Merchant in Skrill back office under `Change MQI/API password`. Needs to be MD5 hashed before adding to config.                                                                                                                          |
| doDefaultRedirect                  | Use PIQ default redirect handling instead of the old Skrill specific one.                                                                                                                                                                                 |
| multiCurrency                      | Set to `true` to send the `account_id` param to Skrill for withdrawals. The value is taken from the accountID config mentioned above. Please verify with Skrill that your account is enabled for Multicurrency before setting to `true`                   |
| customerCheck                      | Set to `true` to enable the Customer Verification check for deposits.                                                                                                                                                                                     |
| customerCheckWithdrawal            | Set to `true` to enable the Customer Verification check for withdrawals.                                                                                                                                                                                  |
| customerVerificationMatchingValues | Decide which user values that has to match with the user’s Skrill account when using the Customer Verification check. defaults to firstname&#124;lastname.<br/><br/> Possible values: firstname&#124;lastname&#124;dateOfBirth&#124;country&#124;postCode |
| recipientDescription               | Sets the `recipient_description` parameter to Skrill, defaults to `PaymentIQ Test`.                                                                                                                                                                       |
| confirmationNote                   | Sets the `confirmation_note` parameter to Skrill, defaults to `PaymentIQ Test`.                                                                                                                                                                           |
| onDemandEnabled                    | Enables Skrill on demand (1-tap) if set to `true`, defaults to `false`.                                                                                                                                                                                   |
| onDemandNote                       | Sets the `ondemand_note` parameter to Skrill if on demand is enabled, defaults to `PaymentIQ Test`.                                                                                                                                                       |
| detail1Text                        | Sets the `detail1_text` parameter to Skrill, defaults to `Detail text`.                                                                                                                                                                                   |
| detail1Description                 | Sets the `detail1_description` parameter to Skrill, defaults to `Detail Description`.                                                                                                                                                                     |
| detail2Text                        | Sets the `detail2_text` parameter to Skrill, defaults to empty string.                                                                                                                                                                                    |
| detail2Description                 | Sets the `detail2_description` parameter to Skrill, defaults to empty string.                                                                                                                                                                             |
| storeId                            | Provided by Skrill, necessary parameter for Giropay payment method.                                                                                                                                                                                       |

### Configuration Steps

1. Go to **My Account** > **Customer overview**. Make a note of the **Processing Mail** which will be used as **username** in the Skrill configuration file in PaymentIQ and the **Customer ID** which will be used as **accountID**.     

    ![](/img/providers/skrill01.png)

2. Go to **Settings** > **Developer Settings**.

3. Click **Enable Service** under **Automated Payment Interface (API)** and add the production IP addresses listed on this page: [Provider IP Whitelist](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist)

    ![](/img/providers/skrill02.png)

4. Click **Enable Service** under **Merchant Query Interface (MQI)** and add the production IP addresses listed on this page: [Provider IP Whitelist](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist)

    ![](/img/providers/skrill03.png)

5. Create a password and set it under **Change MQI/API password**. Make note of the password as it will be used to set the **password** in the SkrillConfig in PaymentIQ.

    ![](/img/providers/skrill04.png)


6. Create a secretKey and set it under **Change secret word**. Make note of the key as it will be used to set the **secretKey** in the SkrillConfig in PaymentIQ.

    ![](/img/providers/skrill05.png)

7. MD5 hash the password and secretKey. This can be done in several different ways so please use Google and find a method that works for you.

8. You now have the credentials ready for the Skrill Configuration file in PaymentIQ and can either add them yourself or ask our Technical Support Team to assist.

### Customer Verification Tool
The customer verification service is used to check if one of your customers, identified by an email address, is registered with Skrill (i.e. the customer already has an active Skrill Digital Wallet account). You can also verify information that you hold about the customer against Skrill's registration records. This feature needs to be activated for the merchant’s Skrill account, as well as in PaymentIQ.

The information that can be checked is as follows:
- First Name
- Last Name
- Date of Birth
- Country
- Post Code

If the customer has an active Skrill Wallet account, then the verification service returns a MATCH or NO_MATCH response back to PIQ for each parameter provided in the request. Match information is not shown by default for the email address.

The customer verification service call also returns a verification level for an account which shows:
- Whether the customer has been verified
- Whether the customer has a verified payment instrument e.g. Debit / Credit card or Bank Account registered with their Skrill account.

This code will be shown in the Info column of the transaction view in back office, as well as added to the PSP fraud score column.

Enable Skrill Customer Verification in PaymentIQ for deposits by adding tag `<customerCheck>true</customerCheck>` to either the SkrillConfig or to a specific account within the SkrillConfig. Add `<customerCheckWithdrawal>true</customerCheckWithdrawal>` to enable the check for Skrill withdrawals.

Then to decide which user values that has to match with the user’s Skrill account, add tag customerVerificationMatchingValues with one or several of the following values:
- firstName
- lastName
- dateOfBirth
- country
- postCode

Example where the firstname and lastname of the user has to match with the Skrill account
`<customerVerificationMatchingValues>firstName|lastName</customerVerificationMatchingValues>`

#### Deciding status code
You can also decide which PaymentIQ specific status code the transaction should end up in in case of a declined transaction due to a mismatch with the verification tool. The default code is `ERR_DECLINED_FRAUD` but can be freely chosen with the tag `pspCodeToStatusCode`

Example of choosing a different status code

```xml
<pspCodeToStatusCode>
  <entry>
    <string>VERIFICATION_MATCHING_FAIL</string>
    <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_OTHER_REASON</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
  </entry>
</pspCodeToStatusCode>
```

## Example Routing Rule
![](/img/providers/routing/skrill.png)

## Additional Notes and Information
A common error that may occur when testing a SkrillWithdrawal is the error message<br/>
`Maintenance - We are making a few more improvements to the website so it isn't available right now.`

This error message, in most cases, tends to be an issue with the account ID used for withdrawals. And this is due to them having different account IDs for other regions/currencies. Therefore, it is best to double-check the account ID you use with Skrill to ensure it's correct.

## Test Information


Please ask Skrill for a test account or use your production account for testing.

Please do withdrawals as well to refill the E-wallet.

| Test cards to  add funds to the merchant account |
|--------------------------------------------------|
| 4000001234567890                                 |
| 4016671298391830                                 |
| 4042811234567890                                 |
| 5422011234567890                                 |
