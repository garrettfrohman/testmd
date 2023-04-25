---
id: "bank-mapping"
---

# Bank Mapping

This area of PaymentIQ is used to define custom bank mappings that will be used to enrich the bank information sent to the provider. This information is required for some bank transactions and since it is similar between customers the purpose of adding bank mapping is to remove the need to collect it from the customer.

![](/img/settingsandadmin/AdminBankMapping/1.png)

## Columns

The columns can be divided up in to groups. 
* [Conditions](conditionsandactions#conditions)
* [Actions](conditionsandactions#actions)

### Conditions

The conditions are used to match against a bank mapping.

| Name            | Description                   | Type                    | Example Usage                |
|-----------------|-------------------------------|-------------------------|------------------------------|
| Bic             | Bic regex to match            | Regex input             | SE.*                         |
| Name            | Bank name regex to match      | Regex input             | SEB                          |
| Clearing number | Clearing number regex to match| Regex input             | 03.*|73.*                    |
| Account number  | Account number regex to match | Regex input             | 111.*                        |
| Currency code   | Currency code to match        | Single select           | EUR                          |
| Country code    | Country code to match         | Single select           | SWE                          |

### Actions

The actions are the data that will enrich the bank information that will be sent to the provider.

| Name                         | Description                                        | Type                    | Example Usage                |
|------------------------------|----------------------------------------------------|-------------------------|------------------------------|
| From clearing house          | From clearing house                                | Free text               | SE                           |
| Swift                        | Swift code                                         | Free text               | HANDSESSXXX                  |
| Bank country code            | Bank country code                                  | Single select           | SWE                          |
| Bank name                    | Bank name                                          | Free text               | HANDELSBANKEN                |
| Bank address                 | Bank address                                       | Free text               | KUNGSTRADGARDSGATAN 2        |
| Bank id                      | Bank id                                            | Free text               | 123                          |
| Transfer type                | Transfer type                                      | Free text               | Instant                      |
| Bank code                    | Bank code                                          | Free text               | SGFSNO21                     |
| Branch code                  | Bank branch code                                   | Free text               | MADHYA PRADESH               |
| Branch name                  | Bank branch name                                   | Free text               | SVENSKA HANDELSBANKEN AB     |
| Branch city                  | Bank branch city                                   | Free text               | STOCKHOLM                    |
| Branch state                 | Bank branch state                                  | Free text               | XXX                          |
| Beneficiary name max size    | Max number of characters of the beneficiary name   | Numeric                 | 20                           |
| Beneficiary address max size | Max number of characters of the beneficiary address| Numeric                 | 20                           |

## How it works together with existing bankmapping supported configurations

The bank mapping will have a higher prio then bank mapping supported configurations. if nothing matched in the bank mapping then we will fallback to existing bank mapping supported configurations. 

## Page actions

Under the action button you will find the following actions.

![](/img/settingsandadmin/AdminBankMapping/2.png)

### Add bank mapping

To add a new bank mapping use the `Action > New bank mapping`. When selecting this menu item a new row in the bank mapping grid will be added to the top.

![](/img/settingsandadmin/AdminBankMapping/6.png)

Double-click in each column of the grid to edit the value of that column. Press `Action > Save changes` when done editing all rows.

![](/img/settingsandadmin/AdminBankMapping/3.png)

### Edit bank mapping

Double-click in each column of the grid to edit the value of that column. Press `Action > Save changes` when done editing all rows.

![](/img/settingsandadmin/AdminBankMapping/4.png)

### Delete bank mapping

Select the bank mappings by checking the checboxes to the left and then click `Action > Delete`. 

### Export bank mappings to XML

To export all bank mappings select this options. The export file can be imported between environment or merchants.

<details><summary>Click to view export Example</summary>
<p>

```xml
<list>
  <bankMapping>
    <clearingNumber>03.*|73.*</clearingNumber>
    <countryCode>AUS</countryCode>
    <swift>WPACAU2SXXX</swift>
    <bankName>Westpac Banking Corporation</bankName>
  </bankMapping>
  <bankMapping>
    <clearingNumber>06.*|76.*</clearingNumber>
    <countryCode>AUS</countryCode>
    <swift>CTBAAU2SXXX</swift>
    <bankName>Commonwealth Bank of Australia</bankName>
  </bankMapping>
  <bankMapping>
    <clearingNumber>08.*|78.*</clearingNumber>
    <countryCode>AUS</countryCode>
    <swift>NATAAU3303M</swift>
    <bankName>National Australia Bank</bankName>
  </bankMapping>
</list>
```
</p>
</details>

### Import bank mapping

The import does support both the exported format and also PaymentIQ provider configurations that support bank mappings: 

* BankConfig
* ManualBankConfig
* CallpayConfig
* CardPayRestConfig
* CitadelConfig
* EasyEftConfig
* EntercashConfig
* EnvoyConfig
* IMerchantPayConfig
* InpayConfig
* IDebitConfig
* MifinityConfig
* MoneyPayConfig
* MuchBetterConfig
* NetBankingConfig
* PProConfig
* SafteypayConfig
* TrustlyConfig
* UPayConfig

### Find bank mapping for tx

This feature allows you to find the bank mapping that matched a specific tx. You will get what bank mapping it matched or if it was a provider config that matched and on what mid it matched.

![](/img/settingsandadmin/AdminBankMapping/5.png)