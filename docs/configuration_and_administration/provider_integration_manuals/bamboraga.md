--- 
id: "bamboraga" 
title: "Bambora Global Acquiring (BamboraGA)"
hide_title: "true"
---
 
![](/img/providers/logos/bamboraga.png)

# Bambora Global Acquiring (BamboraGA)

## About
Bambora is a card acquirer and processor. Support for 3DS (via independent MPI (Epay Zero), N3DS and OCT.

| Provider Name                | BamboraGA                                                                                                                                                                      |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.bambora.com/in-store/acquiring/](https://www.bambora.com/in-store/acquiring/)                                                                                     |
| Classification               | Debit/Credit Card Processor                                                                                                                                                    |
| Regions                      | `International`                                                                                                                                                                |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Void`<br/> `Capture`<br/> `ApplePayDeposit`<br/> `ApplePayWithdrawal`<br/> `CreditcardAccountVerification` |
| PaymentIQ Configuration File | `BamboraGAConfig`                                                                                                                                                              |

## Configuration Information

### Attributes

| Attributes         | Description                                                                                                                                                                                                                                               |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId         | The id of the merchant.<br/> The Id is assigned when signing an agreement with Bambora                                                                                                                                                                    |
| authType           | The type of the authorization:<br/> - FINAL_AUTH for running final authorizations.<br/> - AUTH_CAPTURE for running authorizations followed immediately by a capture operation.<br/> - PRE_AUTH  for running pre-authorizations.<br/>Default value is NULL |
| paymentFacilitator | Enables configuration as a payment facilitator.<br/>Default value is FALSE                                                                                                                                                                                |
| addCardHolderName  | Enables sending card holder name (firstName and lastName) in authorization requests.<br/>Default value is FALSE                                                                                                                                           |

### Authorization/Sale
An authorization places a hold on the funds. For most industries the final amount to be cleared at the time of the authorization is known, the authorizations then are called final authorizations. But for some industries where the final amount is not known, the authorization to be send then is a pre-authorization. A pre-authorization is sent with an estimated amount and are later either:
* Cleared for the same amount.
* Incremented to match the correct amount.
* Adjusted to match the correct amount.

To be compliant with the schemes, final authorizations have 7 days until clearing has to have reached the issuer. Pre-authorizations, on the other hand, have a limit of 30 days. If no clearing has been done after the 7 or 30 day limit the issuer should release the funds.  

Most schemes have no restrictions on which MCCs ( Merchant Category Code) an authorization can be made on. But for VISA only merchants with certain MCCs are allowed to do pre-authorizations, for example Hotel and Car Rental businesses.

An authorization, that is, a final authorization immediately followed by a capture operation within the same request is normally known as a sale, direct debit or purchase transaction.



<details>
<summary>Click to see Authorization (Final Authorization) configuration </summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <merchantId>MIDNUMBER</merchantId> 
        <authType>FINAL_AUTH</authType>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>  
  </accounts>
</com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
```
</details>


<details>
<summary>Click to see Pre-authorization configuration </summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <merchantId>MIDNUMBER</merchantId> 
        <authType>PRE_AUTH</authType>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>  
  </accounts>
</com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
```
</details>


<details>
<summary>Click to see Sale (authorization+capture) configuration </summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <merchantId>MIDNUMBER</merchantId> 
        <authType>AUTH_CAPTURE</authType>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>  
  </accounts>
</com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
```
</details>

<details>
<summary>Click to see VISA MCC restrictions </summary>
<br/>

#### Visa Allowed Pre-authorization MCC:s 

| MCC       | Description                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| 3351–3500 | Car rental agencies                                                                                 |
| 3501–3999 | Lodging – hotels, motels, resorts                                                                   |
| 4111      | Local and suburban commuter passenger transportation, including ferries                             |
| 4112      | Passenger railways                                                                                  |
| 4121      | Taxicabs and limousines (NOTE This will only be applicable for card-not-present transactions.)      |
| 4131      | Bus lines                                                                                           |
| 4411      | Steamship and cruise lines                                                                          |
| 4457      | Boat rentals and leasing                                                                            |
| 5812      | Eating places and restaurants                                                                       |
| 5813      | Drinking places (alcoholic beverages)–bars, taverns, nightclubs, cocktail lounges, and discotheques |
| 7011      | Lodging – hotels, motels, resorts, central reservations services (not elsewhere classified)         |
| 7033      | Trailer parks and campgrounds                                                                       |
| 7394      | Equipment, tool, furniture, and appliance rental and leasing                                        |
| 7512      | Automobile rental agency                                                                            |
| 7513      | Truck and utility trailer rentals                                                                   |
| 7519      | Motor home and recreational vehicle rentals                                                         |
| 7996      | Amusement parks, circuses, carnivals, and fortune tellers                                           |
| 7999      | Recreation services (not elsewhere classified)                                                      |


</details>

### Account Verifications
Account verifications are final authorizations with zero amount. An account verification transaction verifies that the account is an actual issued account, that it is in good standing and is not in lost or stolen status. Account verifications can not be cleared, that is, no capture operation can be performed on them.

Using PaymentIQ Cashier you can do Account Verifications with the same parameters as with credit card transactions but by adding the following parameters and values to the URL:

```
mode=ecommerce
disableBtnAtZero=false
amount=0
```

<details>
<summary>Click to see how to do Account Verifications in PaymentIQ Cashier </summary>
<br/>

![](/img/providers/bamboraga03.png)

</details>

<details>
<summary>Click to see Account Verification configuration </summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>ACCOUNT_VER</string>
      <account>
        <merchantId>MIDNUMBER</merchantId> 
        <authType>FINAL_AUTH</authType>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>  
  </accounts>
</com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
```
</details>



### Void
A void is used to release the funds reserved on the cardholder’s account as a result of an approved authorization. A void is made by referring to a previous authorization. An already captured authorization can not be voided.

### Capture
An authorization is cleared by sending a capture transaction. In the case of final authorizations if no clearing has arrived within 7 days the reserved amount should be released by the issuer. The same applies for pre-authorizations but in those cases the time limit is of 30 days. Some schemes will issue fines if a clearing arrives after those limits.

#### Partial Capture

If the merchant needs to split a shipment of goods, a partial capture should be used.

There are time limits between the original authorization and the last partial capture is executed that depends on whether the original authorization was a final authorization or a pre-authorization:

* **Authorization:** to be compliant with all schemes, you have 7 days before the last capture must be cleared with the issuer.
* **Pre-Authorization:** to be compliant with all schemes, you have 30 days before the last capture must be cleared with the issuer.

In the Investigate View In PaymentIQ BackOffice you can do multiple captures until the authorization amount is reached.
  
![](/img/providers/bamboraga02.png)
  
### Refund
A refund should be used when the cardholder is returning/cancelling the purchased goods/services. A refund is done by referring to an old capture transaction. It is only possible to refer to an old capture transaction that has been processed by the Acquiring API and that has not passed the retention time of storing old transactions. Bambora has a retention time of one year for keeping old transactions. This means that you can not do a refund of a transaction older than one year.  


### Payment Facilitator

For merchants set up as Payment Facilitators some additional information is required:

| Name                  | Description                                                                      |
|-----------------------|----------------------------------------------------------------------------------|
| merchantId            | Know as ProxyMID                                                                 |
| subMerchantId         | Id of the sub-merchant                                                           |
| subMerchantName       | Name of the sub-merchant.<br/> NOTE: Also known as DBA name (Doing Business As). |
| subMerchantAddress    | Address of the sub-merchant                                                      |
| subMerchantPostalCode | Postal Code of the sub-merchant                                                  |
| subMerchantCity       | City location of the sub-merchant                                                |
| subMerchantCountry    | Country location of the sub-merchant                                             |
| subMerchantURL        | URL inkl. https://                                                               |
| merchantMcc           | MCC for the sub-merchant                                                         |

The additional information should be sent as an attribute list as part of the response of a merchant Authorize call in the Integration API. At this moment there are no Payment Facilitator ids in the staging environment so this setup can only be run in production. For more information regarding Payment Facilitators, please see [Payment Facilitators](/docs/integration_overview/integration_options#Payment Facilitator).


<details>
<summary>Click to see an example of a Payment Facilitator attribute list </summary>
<br/>

```xml
<attributes>
  <entry>
    <string>subMerchantPostalCode</string>
    <string>12345</string>
  </entry>
        <entry>
          <string>subMerchantId</string>
          <string>5678</string>
        </entry>
        <entry>
          <string>paymentFacilitatorId</string>
          <string>123456789</string>
        </entry>
        <entry>
          <string>merchantId</string>
          <string>MIDNUMBER</string>
        </entry>
        <entry>
          <string>subMerchantAddress</string>
          <string>Drottninggatan 1</string>
        </entry>
        <entry>
          <string>subMerchantCountry</string>
          <string>SWE</string>
        </entry>
        <entry>
          <string>subMerchantCity</string>
          <string>Stockholm</string>
        </entry>
        <entry>
          <string>merchantMcc</string>
          <string>3333</string>
        </entry>
        <entry>
          <string>subMerchantName</string>
          <string>Demoshop</string>
        </entry>
        <entry>
          <string>subMerchantURL</string>
          <string>www.sub-merchant.com</string>
        </entry>
</attributes>
```
</details>

<details>
<summary>Click to see Payment Facilitator configuration </summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <authType>FINAL_AUTH</authType>
        <use3Dsecure>false</use3Dsecure>
        <paymentFacilitator>true</paymentFacilitator>
      </account>
    </entry>      
  </accounts>
</com.devcode.paymentiq.integration.bambora.ga.BamboraGaConfig>
```
</details>


## Example Routing Rule
![](/img/providers/routing/bamboraga.png)
![](/img/providers/routing/bamboraga2.png)
## Test Information

### Test credentials

Merchant id values for BamboraGa configuration.

| TEST     | OCT TEST |
|----------|----------|
| 62941828 | 63056030 |

Payment Facilitator test credentials to be used in Authorize response. 

```json
{
	"userId": "User_123",
	"success": true,
	"attributes": {
    "merchantId": "66227919",                <!-- Proxy MID -->
		"subMerchantName": "TestSubMerchant",
		"subMerchantId": "VTX1800",              
		"subMerchantCountry": "SWE",
		"subMerchantCity": "Stockholm",
     "subMerchantPostalCode": "11120",
		"subMerchantAddress": "Vasagatan 16",
		"subMerchantURL": "https://www.example.com",
		"merchantMcc": "5812",
	}
}
```

### Test Cards

BamboraGa uses Visa’s and Mastercard’s test system for validating transactions. 
All of their cards can be used for N3DS. 

### N3DS / 3DS

| PAN for N3DS / 3DS testing | CVC | Exp. date |
|----------------------------|-----|-----------|
| 5457210002001420           | Any | 12/2025   |
| 5457210002001461           | Any | 12/2025   |

| PAN for simulating "Insufficient funds" response | CVC | Exp. date |
|--------------------------------------------------|-----|-----------|
| 5186170070001140                                 | Any | 12/2025   |

### Account Verification

| PAN for Account Verification testing | CVC | Exp. date |
|--------------------------------------|-----|-----------|
| 5457210002001420                     | Any | 12/2025   |

### OCT

| Card Brand | Account          | CVV | Expiry date | Note                          |
|------------|------------------|-----|-------------|-------------------------------|
| MasterCard | 5204740000001002 | Any | Any         |                               |
| MasterCard | 5457210002001420 | Any | Any         | Test card declined withdrawal |
