--- 
id: "addfilenamehere"
title: "addprovidernamehere"
hide_title: "true"
---

[comment]: <> (the logo should have the providers name in lower caps and be in png format)
[comment]: <> (the logo should be exactly 300px wide. height max 300px, preferably less)
![](/img/providers/logos/[providername].png)

# [Provider Name and if needed Product Name]
## About
[comment]: <> (short text describing what the provider offers and its benefits.)

| Provider Name                | NameOfTheProvider                                                  |
|------------------------------|--------------------------------------------------------------------|
| Link                         | [https://providerurl/](https://providerurl/)                       |
| Classification               | Mobile Payment                                                     |
| Regions                      | `Uganda`                                                           |
| Currencies                   | `SEK`, `EUR`			                                                  |
| Methods/PaymentTxTypes       | `MethodDeposit` <br/> `MethodWithdrawal`                           |  
| PaymentIQ Configuration File | `ProviderNameConfig`                                               |

[comment]: <> (Link should be to the main provider page, not the API)
[comment]: <> (classification can be one or more of:)
  [comment]: <> (Debit/Credit Card Processor)
  [comment]: <> (Aggregator)
  [comment]: <> (Wallet)
  [comment]: <> (PrePaid Card / Voucher)
  [comment]: <> (Online Banking)
  [comment]: <> (Crypto Currency)
  [comment]: <> (Mobile Payment)

### Supported APMs (services)

| Payment Method  | PaymentIQ Service  | TxType | Comment |
|-----------------|--------------------|--------|---------|
|                 |                    |        |         |
|                 |                    |        |         |

[comment]: <> (list the supported payment methods and the corresponding service names/service parameters and TxTypes that are supported. Describe in details when relevant.)

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

[comment]: <> (live configuration file. replace credentials with ?? and do not leave test credentials in)

```xml
[config goes here]
```

</details>

### Attributes

[comment]: <> (list all attributes in the configuration file. describe what the options are when relevant. make sure to mention how they connect to what the provider calls them when relevant.)

| Attribute   | Description        |
|-------------|--------------------|
|             |                    |
|             |                    |

[comment]: <> (Write a step by step setup guide. See provider CoinsPaid as an example.)

## Example Routing Rule

[comment]: <> (lowercaps name, png file format screenshot of an example routing rule)
![](/img/providers/routing/[providername].png)

## Transaction Flow

[comment]: <> (If possible add a multi image example tx flow.)


[comment]: <> (Test information should be added in the Test Credentials view in test backoffice)
