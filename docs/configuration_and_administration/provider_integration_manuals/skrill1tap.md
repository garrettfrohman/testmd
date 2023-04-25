--- 
id: "skrill1tap" 
title: "Skrill 1-Tap"
hide_title: "true"
---
 
![](/img/providers/logos/skrill1tap.png)

# Skrill 1-Tap

## About
Skrill 1-Tap can be set up for Skrill or Skrill Quick Checkout and enables a quick and easy way to transfer funds from the customers Skrill eWallet in 'one tap' rather than having to re-enter your Skrill account details each time you deposit.

| Provider Name                | Skrill                                                                                    |
|------------------------------|-------------------------------------------------------------------------------------------|
| Link                         | [https://www.skrill.com/en/](https://www.skrill.com/en/)                                  |
| Classification               | Wallet                                                                                    |
| Regions                      | `International`                                                                           |
| Currencies                   | Please check directly with the provider regarding what currencies are supported           |
| Methods/PaymentTxTypes       | `SkrillDeposit` <br/> `SkrillWithdrawal`<br/>`SkrillQCODeposit`<br/>`SkrillQCOWithdrawal` |
| PaymentIQ Configuration File | `SkrillConfig`                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
Please check the default SkrillConfig
```

</details>

### Notes

- To enable the 1-Tap service for your Skrill account, please contact merchantservices@skrill.com.

- When it is enabled it can be activated in PaymentIQ via the Skrill configuration by adding `<onDemandEnabled>true</onDemandEnabled>` to the account level of the account you wish to enable it for.

- After it's enabled, the end-users should be able to choose if they want to use 1-Tap in the Skrill-frame, and then all subsequent transactions that are recurring payments with PaymentIQ and Skrill will be 1-Tap.

## Test Information

Please check directly with the provider.