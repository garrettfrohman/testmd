--- 
id: "ecobanq" 
title: "ECOBANQ"
hide_title: "true"
---
 
![](/img/providers/logos/ecobanq.png)

# ECOBANQ

## About
ECOBANQ is a wallet payment solution. ECOBANQ support deposit and withdrawal.
User should enter her/his ECOBANQ ID (e.g. Q000985) and password to deposit. But just password for repeat payment.

| Provider Name                | ECOBANQ                                              |
|------------------------------|------------------------------------------------------|
| Link                         | [https://www.ecobanq.com/](https://www.ecobanq.com/) |
| Classification               | Wallet Payment                                       |
| Regions                      | `International`                                      |
| Currencies                   | `INR`                                                |
| Methods/PaymentTxTypes       | `EcoBanqDeposit`<br/> `EcoBanqWithdrawal`            |
| PaymentIQ Configuration File | `EcobanqConfig`                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.ecobanq.EcoBanqConfig>
 <enabled>true</enabled>
 <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <password>??</password>
        <supportedCurrencies>INR</supportedCurrencies>
      </account>
    </entry>
  </accounts> 
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.ecobanq.EcoBanqConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential                                                                                                 |
|-------------------------|---------------------------------------------------------------------------------------------------------------------|
| merchantId              | Merchant's ECOBANQ ID (e.g. Q000985)                                                                                |
| password                | Merchant's ECOBANQ login password                                                                                   |
| withdrawalUrl           | Withdrawal URL set at config level. Already profiled with right value. Yet can be use in case they change the URL.  |
| statusCheckUrl          | Status Check URL set at config level. Already profiled with right value. Yet can be use in case they change the URL |

## Example Routing Rule
![](/img/providers/routing/ecobanq.png)
## Test Information

- Currency: INR (E.g TEST_INR as mock user)
- ECOBANQ ID: Q000985
- ECOBANQ login password: testuser15
- Amount: 1 INR (Please also return the balance to the test user wallet after testing is completed, i.e. perform a withdrawal transaction of the same amount)
