--- 
id: "interac" 
title: "Interac"
hide_title: "true"
---
 
![](/img/providers/logos/interac.png)

# Interac

## About
Interac Association operates under an order issued by the Government of Canada's Competition Tribunal ("Interac Consent Order"), which dictates that the Association must operate on a not-for-profit basis. This means that Interac Association charges only a fee to members that is sufficient to cover its operating costs.

| Provider Name                | Interac                                                                                        |
|------------------------------|------------------------------------------------------------------------------------------------|
| Link                         | [http://www.interac.ca/en/](http://www.interac.ca/en/)                                         |
| Classification               | Online Banking                                                                                 |
| Regions                      | `Canada`                                                                                       |
| Currencies                   | `CAD`                                                                                          |
| Methods/PaymentTxTypes       | `BankDeposit` <br/> `InteracDeposit` <br/> `InteracWithdrawal` <br/> `InteracDirectWithdrawal` |
| PaymentIQ Configuration File | `InteracConfig`                                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.interac.InteracConfig>
  <container>window</container>
<width>700</width>
<height>700</height>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>Interac2Pay</string>
      <account>
        <accountID>??</accountID>     <!--  Campaign ID -->
        <username>??</username>       <!--  Campaign Name -->
        <apiKey>??</apiKey>           <!--  Access token  -->
        <secretKey>??</secretKey>     <!--  Security token  -->
        <supportedCurrencies>CAD</supportedCurrencies>
        <method>E_TRANSFER</method> <!-- or method ONLINE or COMBINED. Defaults to ONLINE if missing  -->
        <!--showConfirmation>true</showConfirmation--> <!-- enable when using PaymentIQ cashier to dsiplay the applied exchange rate to the user  -->
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <!-- Site parameter --> 
  <defaultDescriptor>www.merchantsite.com</defaultDescriptor>
  <waitForWithdrawalNotification>false</waitForWithdrawalNotification> <!--option to set Interac withdrawals to a pending state in PIQ in order to wait for the final state from a callback notification. Not recommended, merchants can use on their own risk -->
</com.devcode.paymentiq.integration.interac.InteracConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                         |
|---------------------|-------------------------------------------------------------------------------------|
| accountID           | Campaign ID                                                                         |
| username            | Campaign Name                                                                       |
| apiKey              | access token                                                                        |
| secretKey           | security token                                                                      |
| supportedCurrencies | Need to be verified according the account.                                          |
| method              | Deposit method. See table below for valid values. Defaults to ONLINE if not present |

### End User IPs

Please note that Interac require end user IPs to be sent.

Instructions on how to do so can be found [here](/docs/apis_and_integration/front_api/ip-address)

### Deposit Methods

| Value      | Description                |
|------------|----------------------------|
| ONLINE     | Interac Online (default)   |
| E_TRANSFER | E-Transfer (ETI)           |
| COMBINED   | Combined Pay-In Flow (CPI) |

Note: As mentioned above in the attributes table, the deposit method of choice has to be set with its respective value in the 'method' attribute.

### Setting Endpoint

Endpoints will need to be set on Interacs side. In order to configure those, merchants will need first to create a Campaign (A Campaign is a kind of subscription or sub-account), this contain a form that will need to be completed.

![](/img/providers/interac01.png)

| Field            | Description                                                          |
|------------------|----------------------------------------------------------------------|
| Id               | This will be automatically set by Interact.                          |
| Name             | Should be chosen by the merchant.                                    |
| Test Success Uri | https://test-api.paymentiq.io/paymentiq/api/interac/redirect/success |
| Test Failure Uri | https://test-api.paymentiq.io/paymentiq/api/interac/redirect/failure |
| Test Listener    | https://test-api.paymentiq.io/paymentiq/api/interac/callback         |
| Prod Success Uri | https://api.paymentiq.io/paymentiq/api/interac/redirect/success      |
| Prod Failure Uri | https://api.paymentiq.io/paymentiq/api/interac/redirect/failure      |
| Prod Listener    | https://api.paymentiq.io/paymentiq/api/interac/callback              |

### Deposits

The request to Interac must include end-user's name and email (for "COMBINED" type there should be provided phone number as well).
The values are taken from the initial request (input).
Alternatively, if the email (and/or phone number) isn't provided within the request - the values are taken from MerchantVerifyUserRes.

### Withdrawals

| Type                       | TxType                  | Service      | Comments                                                                                                            |
|----------------------------|-------------------------|--------------|---------------------------------------------------------------------------------------------------------------------|
| E-Transfer (ETO)           | InteracWithdrawal       | blank or ETO | To use this type, it is best to map ETO to INTERAC in service mapping; works by default without any mapping as well |
| Real-time E-Transfer (RTO) | InteracWithdrawal       | RTO          | To use this type, mapping RTO to INTERAC in service mapping is needed                                               |
| eCashout                   | InteracDirectWithdrawal | NA           | No service mapping needed                                                                                           |

#### How to configure withdrawals
- Configure a specific service for INTERAC provider type inside MerchantConfig: ETO or RTO
- Rules > Payment Methods: enable INTERAC-RTO or INTERAC-ETO as a withdrawal payment option

Notes: 
- For InteracWithdrawal txType: it is always good to send the service parameter, and in case of invalid or missing service, transactions will fallback to ETO.
- For InteracDirectWithdrawal txType: no specific service has to be set in MerchantConfig for INTERACDIRECT provider type, but if done, any service will default to eCashout

Name, email and mobile number is mandatory in the request to Interac. If the values are not included in the request, the information will be taken from MerchantVerifyUserRes.

#### Wait For withdrawal Notification

By default, regular withdrawal requests with Interac in PaymentIQ will be directly set to the `SUCCESSFUL` state. However, with a configuration change, it is possible to choose to instead have the transactions put to state `WAITING_INPUT` and await the callback notification from Interac in order to update to the final state in PaymentIQ. This is done by adding the following entry in the `InteracConfig`:

`<waitForWithdrawalNotification>true</waitForWithdrawalNotification>`

## Example Routing Rule

![](/img/providers/routing/interac.png)
![](/img/providers/routing/interac1.png)
![](/img/providers/routing/interac2.png)

## Test Information

### Deposit

To test e-Transfer deposits, first you have to initiate a payment as usual which will open the iframe/window with deposit details, and then contact Interac which can simulate a success or failed payment.

### Withdrawal

For withdrawals, the process is similar. The difference is that no iframe/window will be shown, instead the withdrawal request is directly accepted, but Interac will have to be contacted to simulate success or failure.

Please note that the final state for withdrawal tests in PIQ for Interac E-Transfer is `WAITING_INPUT`.
