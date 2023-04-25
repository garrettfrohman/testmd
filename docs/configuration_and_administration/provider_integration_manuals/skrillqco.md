--- 
id: "skrillqco" 
title: "Skrill Quick Checkout"
hide_title: "true"
---
 
![](/img/providers/logos/skrillqco.png)

# Skrill Quick Checkout

## About
Skrill Quick Checkout is a Wallet solution offering Deposits and Withdrawals.

| Provider Name                | Skrill Quick Checkout                                                                                      |
|------------------------------|------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.skrill.com/en/business/hosted-checkout/](https://www.skrill.com/en/business/hosted-checkout/) |
| Classification               | Wallet                                                                                                     |
| Regions                      | International                                                                                              |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                            |
| Methods/PaymentTxTypes       | `SkrillQCODeposit`<br/>`SkrillQCOWithdrawal`                                                               |
| PaymentIQ Configuration File | `SkrillConfig`                                                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
Please check the default SkrillConfig
```

</details>

### Enable Quick Checkout for your account
To enabled Skrill quick checkout on your merchant account you will have to contact Skrill customer service. You will get a new account for the quick checkout functionality. The same goes for withdrawals, you will have to request it in the same way from the Skrill customer service to enable it for you.

### Quick Checkout layouts
The quick checkout has 3 different layout types.
1. Fixed (Fixed Split Gateway)
	- Only the requested payment methods are displayed at Skrill Quick checkout.
2. Flexible (Flexible Split Gateway)
	- The requested payment methods are pre-selected and displayed for the user but the user can change to other method at Skrill Quick checkout.
3. Fixed payment options (Fixed Split Gateway) with Reduced header option enabled
	- Same as fixed but the header is not displayed and is more mobile friendly.

Contact Skrill customer service to learn about the different benefits with each layout type.

### Attributes

PaymentIQ BO SkrillConfig account example (test):

(this is a skrill merchant account that is 1-tap (ondemand) enabled)

```xml
<username>skrill_test_merchant@devcode.se</username>
<secretKey>f6432274349b5cb93433f8ed886a3f37</secretKey>
<password>077fe81fb32721da5238f4ea4ee69311</password>
<useTokenId>true</useTokenId>
```

(this is a skrill merchant account that is quick checkout enabled)

```xml
<username>skrill_qco_test_merchant@devcode.se</username>
<secretKey>8654e1877d25cb83ac03dbd4e68c1da2</secretKey>
<password>90ae9a8a072470989b033f1ed01ecb66</password>
<useTokenId>true</useTokenId>
```

```xml
<confirmationNote>PaymentIQ Test</confirmationNote>
<recipientDescription>PaymentIQ Test</recipientDescription>
```

```xml
<detail1Description>Merchant Brand</detail1Description>
<detail1Text>PIQ Test</detail1Text>
<!-- Add for additional data -->
<detail2Description>Detail Description 2</detail2Description>
<detail2Text>Detail Text 2</detail2Text> -->
```
(this part of the configuration will enable on-tap function only for Skrill-Wallet)

```xml
<onDemandEnabled>true</onDemandEnabled>
<oneTapDepositUrl>https://www.skrill.com/app/ondemand_request.pl</oneTapDepositUrl>
<onDemandNote>PaymentIQ Test</onDemandNote>
<onDemandStatusUrl></onDemandStatusUrl>
<retryOnDemandCancelAsRegular>true</retryOnDemandCancelAsRegular>
```

### MerchantConfig Service Mapping
Skrill quick checkout has many different services/APMs that can be used. They can be configured in the `serviceMapping` of the MerchantConfig for the `SKRILLCQO` payment type so that they can be used for routing and enabling payment methods.

```xml
<serviceMapping>   
….
<entry>
  <string>SKRILLQCO</string>
  <string>CREDITCARD|VISA|MASTERCARD|MAESTRO|VISA_ELECTRON|AMERICAN_EXPRESS|DINERS|JCB|CARTE_BLEUE|DANKORT|POSTE_PAY|CARTESI|SKRILLDIGITALWALLET|NETELLER|PAYSAFECARD|RESURS|RAPIDTRANSFER|GIROPAY|DIRECTDEBIT|SOFORT|IDEAL|EPS|POLI|PRZELEWY24|EPAY|TRUSTLY|ALIPAY|ASTROPAYONLINEBANKTRANSFER|ASTROPAYOFFLINEBANKTRANSFER|ASTROPAYCASH|UNIONPAY|NORDEASOLO</string>
</entry>
….
</serviceMapping>
```

Please find an elaborate guide on how to work with service mapping [here](/docs/configuration_and_administration/system_configuration/servicemapping).

### Quick Checkout Payment Methods

The available methods to use with quick checkout can be found in the below table, and the value in the `Service name` column is the value that should be sent as the `service` parameter in the request to PaymentIQ.

| Payment method                                          | Service name                   | Countries                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Notes                                                                      |
|---------------------------------------------------------|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| Creditcard                                              | CREDITCARD                     | All                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| Visa                                                    | VISA                           | All                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| MasterCard                                              | MASTERCARD                     | All                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| Maestro                                                 | MAESTRO                        | United Kingdom, Spain, Ireland and Austria                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                            |
| Visa Electron                                           | VISA_ELECTRON                  | All. Excluding US                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                            |
| American   express                                      | AMERICAN_EXPRESS               | All                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| Diners                                                  | DINERS                         | All                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| JCB                                                     | JCB                            | All                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| Carte   bleue                                           | CARTE_BLEUE                    | France                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                            |
| Dankort                                                 | DANKORT                        | Denmark                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                            |
| Postepay                                                | POSTE_PAY                      | Italy                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                            |
| CarteSi                                                 | CARTESI                        | Italy                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                            |
| Skrill digital wallet                                   | SKRILLDIGITALWALLET            | All                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| Neteller                                                | NETELLER                       | All except for: Afghanistan, Armenia, Bhutan, Bouvet Island, Myanmar, China, (Keeling) Islands, Democratic Republic of Congo, Cook Islands, Cuba, Eritrea, South Georgia and the South Sandwich Islands, Guam, Guinea, Territory of Heard Island and McDonald Islands, Iran, Iraq, Cote d'Ivoire, Kazakhstan, North Korea, Kyrgyzstan, Liberia, Libya, Mongolia, Northern Mariana Islands, Federated States of Micronesia, Marshall Islands, Palau, Pakistan, East Timor, Puerto Rico, Sierra Leone, Somalia, Zimbabwe, Sudan, Syria, Tajikistan, Turkmenistan, Uganda, United States, US Virgin Islands, Uzbekistan, and Yemen | Requires the container parameter in the SkrillConfig to be set to `window` |
| Paysafecard                                             | PAYSAFECARD                    | American Samoa, Austria, Belgium, Canada, Croatia, Cyprus, Czech Republic, Denmark, Finland, France, Germany, Guam, Hungary, Ireland, Italy, Latvia, Luxembourg, Malta, Mexico, Netherlands, Northern Mariana Islands, Norway, Poland, Portugal, Puerto Rico, Romania, Slovakia, Slovenia, Spain, Sweden, Switzerland, Turkey, United Kingdom, United States Of America and US Virgin Islands                                                                                                                                                                                                                                   |                                                                            |
| Resurs                                                  | RESURS                         | Sweden, Norway, Finland and Denmark                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| Rapid transfer                                          | RAPIDTRANSFER                  | Austria, Denmark, Finland, France, Germany, Hungary, Italy, Norway, Poland, Portugal, Spain, Sweden, United Kingdom.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |                                                                            |
| Giropay                                                 | GIROPAY                        | Germany                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                            |
| Direct debit/SEPA                                       | DIRECTDEBIT                    | Germany                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                            |
| Sofort                                                  | SOFORT                         | Germany, Austria, Belgium, Netherlands, Italy, France, Poland, Hungary, Slovakia, Czech Republic and United Kingdom                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                            |
| iDeal                                                   | IDEAL                          | Netherlands                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                            |
| EPS                                                     | EPS                            | Austria                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                            |
| POLi                                                    | POLI                           | Australia                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                                                            |
| Przelewy24                                              | PRZELEWY24                     | Poland                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                            |
| ePay.bg                                                 | EPAY                           | Bulgaria                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                                            |
| Trustly                                                 | TRUSTLY                        | Austria, Belgium, Bulgaria, Czech Republic, Denmark, Estonia, Finland, Germany, Hungary, Ireland, Latvia, Lithuania, Netherlands, Poland, Romania, Slovakia, Slovenia, Spain, Sweden                                                                                                                                                                                                                                                                                                                                                                                                                                            |                                                                            |
| Alipay                                                  | ALIPAY                         | This is available for merchants in all countries except China.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                            |
| Astropay   – Onlie bank transfer (Direct bank transfer) | ASTROPAYONLINEBANKTRANSFER     | Argentina, Brazil                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                            |
| Astropay – Offline bank transfer                        | ASTROPAYOFFLINEBANKTRANSFER    | Brazil, Chile, China, Colombia                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                            |
| Astrppay – Cache (Invoice)                              | ASTROPAYCASH                   | Argentina, Brazil, Chile, China Columbia, Mexico, Peru, Uruguay                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                                                            |
| Unionpay via Astropay                                   | UNIONPAY                       | China                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                            |
| SafetyPay                                               | ONLINE_BANKING                 | South America                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                            |
| SafetyPay                                               | CASH                           | South America                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                            |
| SafetyPay                                               | PIX                            | South America                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                            |
| SafetyPay                                               | BOLETO                         | South America                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                            |
| SafetyPay                                               | MACH                           | South America                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                            |
| PageEffectivo                                           | PAGOEFECTIVO                   | South America                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                            |

### Payment Methods via Skrill Quick Checkout (Withdrawal)

**Note: In order to perform a withdrawal, a previous successful deposit with the same method must have been made by the user. The withdrawal must be initiated with the account that was saved after the deposit.**

| Payment method | Service   name | Countries                                                                                                            |
|----------------|----------------|----------------------------------------------------------------------------------------------------------------------|
| Rapid transfer | RAPIDTRANSFER  | Austria, Denmark, Finland, France, Germany, Hungary, Italy, Norway, Poland, Portugal, Spain, Sweden, United Kingdom. |
| Neteller       | NETELLER       | --                                                                                                                   |

### Customer Verification Tool

Please see regular [Skrill](/docs/configuration_and_administration/provider_integration_manuals/skrill) payment page for more information.

## Example Routing Rule
![](/img/providers/routing/skrillqco.png)

## Test Information

- Most of the methods that can be found for the Skrill Quick checkout does only require an email and not any specific test data, but some does.

- All methods require that the user is from Germany (DEU).

### Rapid Transfer and Sofort

Rapid Transfer can only be tested using Germany as country with the following credentials:
- IBAN: DE14100100109876543210
- BIC: PBNKDEFFXXX
- Account Number: 9876543210
- Bank code: 10010010
- Country: GER
- Bank: POSTBANK

![](/img/providers/skrillqco01.png)

### Neteller

| Currency | Account ID   | Email                         | Password |
|----------|--------------|-------------------------------|----------|
| AUD      | 451823760529 | netellertest_AUD@neteller.com | NTt3st1! |
| BGN      | 450424149137 | netellertest_BGN@neteller.com | NTt3st1! |
| CAD      | 455781454840 | netellertest_CAD@neteller.com | NTt3st1! |
| CHF      | 452324249609 | netellertest_CHF@neteller.com | NTt3st1! |
| DKK      | 459734233011 | netellertest_DKK@neteller.com | NTt3st1! |
| EUR      | 453501020503 | netellertest_EUR@neteller.com | NTt3st1! |
| GBP      | 458591047553 | netellertest_GBP@neteller.com | NTt3st1! |
| HUF      | 450824149649 | netellertest_HUF@neteller.com | NTt3st1! |
| INR      | 450824016049 | netellertest_INR@neteller.com | NTt3st1! |
| JPY      | 452604251512 | netellertest_JPY@neteller.com | NTt3st1! |
| MAD      | 453123727913 | netellertest_MAD@neteller.com | NTt3st1! |
| MXN      | 456444237546 | netellertest_MXN@neteller.com | NTt3st1! |
| MYR      | 452724116521 | netellertest_MYR@neteller.com | NTt3st1! |
| NGN      | 450924006321 | netellertest_NGN@neteller.com | NTt3st1! |
| NOK      | 455394172769 | netellertest_NOK@neteller.com | NTt3st1! |
| PLN      | 451823629489 | netellertest_PLN@neteller.com | NTt3st1! |
| RON      | 450424018097 | netellertest_RON@neteller.com | NTt3st1! |
| RUB      | 455121038904 | netellertest_RUB@neteller.com | NTt3st1! |
| SGD      | 451523741861 | netellertest_SGD@neteller.com | NTt3st1! |
| SEK      | 453313818311 | netellertest_SEK@neteller.com | NTt3st1! |
| TND      | 453523858985 | netellertest_TND@neteller.com | NTt3st1! |
| TWD      | 451723748785 | netellertest_TWD@neteller.com | NTt3st1! |
| USD      | 454651018446 | netellertest_USD@neteller.com | NTt3st1! |

### Creditcards

| Brand      | Card number      |
|------------|------------------|
| Mastercard | 5438311234567890 |
| Visa       | 4000001234567890 |
| Amex       | 371234500012340  |
