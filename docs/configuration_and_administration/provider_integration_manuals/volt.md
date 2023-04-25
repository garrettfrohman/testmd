--- 
id: "volt" 
title: "Volt"
hide_title: "true"
---
 
![](/img/providers/logos/volt.png)

# Volt

## About
Volt allows online merchants to accept payments direct from their customers' bank accounts. By using Open Banking connectivity Volt provide your customer access to their own bank account at checkout.

| Provider Name                | Volt                                                                            |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.getvolt.io/](https://www.getvolt.io)                               |
| Classification               | Online Banking                                                                  |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `BankDeposit`, `WebRedirectDeposit`                                             |
| PaymentIQ Configuration File | `VoltConfig`                                                                    |

## Configuration

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.volt.VoltConfig>
  <enabled>true</enabled>
  <!-- Optional field -->
  <!--<voltHostedBankSelection>true</voltHostedBankSelection>-->
  <!--<enableVoltConnect>true</enableVoltConnect>-->
  <!-- End optional field -->
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>?????</username>
        <password>?????</password>
        <apiKey>?????</apiKey>
        <secretKey>?????</secretKey>
        <notificationSecret>?????</notificationSecret>
        <accountID>?????</accountID>
        <merchantName>?????</merchantName>
        <container>window</container>
        <!-- Optional -->
        <!--<merchantCountry>GBR,NOR</merchantCountry>-->
        <!--<supportedCurrencies>GBP</supportedCurrencies>-->
        <!--<productCategory>SERVICES</productCategory>-->
      </account>
    </entry>
    <entry>
      <string>embedded</string>
      <account>
        <username>?????</username>
        <password>?????</password>
        <apiKey>?????</apiKey>
        <secretKey>?????</secretKey>
        <notificationSecret>?????</notificationSecret>
        <accountID>?????</accountID>
        <merchantName>?????</merchantName>
        <container>window</container>
        <!-- Optional -->
        <!--<merchantCountry>GBR,NOR</merchantCountry>-->
        <!--<supportedCurrencies>GBP</supportedCurrencies>-->
        <!--<productCategory>SERVICES</productCategory>-->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.volt.VoltConfig>
```
</details>

### Attributes

| Attribute               | Description                                                                                                                                                        |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username                | Provided by Volt.                                                                                                                                                  |
| password                | Provided by Volt.                                                                                                                                                  |
| apiKey                  | client_id from Volt.                                                                                                                                               |
| secretKey               | client_secret from Volt.                                                                                                                                           |
| notificationSecret      | notification secret from Volt.                                                                                                                                     |
| accountID               | (Optional) Merchant Bank account id from Volt.                                                                                                                     |
| merchantCountry         | (Optional) List of country codes to filter which banks should be available for the customer to choose. If omitted filtering will be done on basis of user country. |
| productCategory         | (Optional) BILL, GOODS, PERSON_TO_PERSON, OTHER, SERVICES will default to OTHER if not provided.                                                                   |
| voltHostedBankSelection | (Optional) Set to true to redirect the user to Volt's own hosted bank selection page. Defaults to false.                                                           |
| enableVoltConnect       | (Optional) Enables Volt Connect support, needs to be activated on Volt's side as well in order to work.                                                            |

**For config values with complex characters you can add the CDATA tag, example:** 

*\<password><\![CDATA[COMPLEX_PASSWORD_HERE]]>\</password>*

The merchant must also configure and enable these URLs in Volts system:

Notification URL (callback)
 * https://test-api.paymentiq.io/paymentiq/api/volt/callback (Test)
 * https://api.paymentiq.io/paymentiq/api/volt/callback (Production)

Return URLs (use the same URL for success/failure/pending)
 * https://test-api.paymentiq.io/paymentiq/api/volt/redirect (Test)
 * https://api.paymentiq.io/paymentiq/api/volt/redirect (Production)

**Please note** that Volt may send a second callback in certain instances, which can trigger a new transaction.<br/>
The new transaction will make use of the Integration API's [LookupUser method](/../docs/apis_and_integration/integration_api/lookupuser); this means that to use this provider, you're required to handle that API request. 

### Originating bank
There are different ways to pass the originating bank parameter to Volt (the customer bank where the money will be sent from).
1. The merchant can choose to obtain the list of available banks from Volt themselves (filter according to users country) and include the selected bank id in the call to PIQ Front API
/api/bank/deposit/process as the parameter 'token'.
2. If the parameter 'token' is not included in the Front API call the customer will be redirected to a page where he/she can pick a bank from a list that is filtered according to this:
    * If the 'merchantCountry' parameter is configured in VoltConfig the customer will see a list of banks available in those countries.
    * If 'merchantCountry' is not configured, the filtering will be done on the basis of either the optional parameter 'countryCode' in the Front API call, 
    OR the users 'country' parameter obtained by PIQ in the response of the verifyuser call to the merchant.
    
### Volt Connect
When enabling Volt Connect in PaymentIQ the status mappings will change, instead of having COMPLETED as a SUCCESSFUL state it will now be called VC:COMPLETED which will put the transaction into WAITING_DEPOSIT_CONFIRMATION. Later PIQ will wait for a notification with the status either RECEIVED/NOT RECEIVED from Volt. 

To read more about Volt Connect please refer to Volt's documentation: [https://docs.volt.io/docs/connect/welcome_to_connect](https://docs.volt.io/docs/connect/welcome_to_connect)

### Volt Embedded (WebRedirectDeposit)
Volt embedded should have separate Volt application and PaymentIQ provider account
1. Create separate application client in Volt backoffice. 
2. Set callback URL (Volt BO) to 
   - https://test-api.paymentiq.io/paymentiq/api/volt/callback?embedded=true (Test)
   - https://api.paymentiq.io/paymentiq/api/volt/callback?embedded=true (Production)
3. Set redirect url (Volt BO) to:
   - https://test-api.paymentiq.io/paymentiq/api/volt/redirect/embedded (Test)
   - https://api.paymentiq.io/paymentiq/api/volt/redirect/embedded (Production)
4. Add new accountConfig (PaymentIQ BO) for embedded with newly created application credentials

## Example Routing Rules

![](/img/providers/routing/volt.png)

## Test Information
Select the bank option "ob-gold (United Kingdom)" and proceed through the steps without changing anything to test the deposit flow   
(make sure the user has the country tag set to GBR in MockMerchantConfig to be able to see UK banks). 


