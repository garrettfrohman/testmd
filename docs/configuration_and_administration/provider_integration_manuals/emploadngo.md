--- 
id: "emploadngo" 
title: "EMP LoadnGo"
hide_title: "true"
---
 
![](/img/providers/logos/emploadngo.png)

# EMP LoadnGo

## About
LoadnGo is a Payment Solution Provided by EMP-CORP in order to provide a solution that is designed to allow clients to reload the prepaid card anywhere,
transfer currency from wallet to wallet and view transactions in real time.

| Provider Name                | EMP/LoadnGo      |
|------------------------------|------------------|
| Link                         | -                |
| Classification               | Wallet           |
| Regions                      | `International`  |
| Currencies                   | `EUR`            |
| Methods/PaymentTxTypes       | `LoadngoDeposit` |
| PaymentIQ Configuration File | `LoadNgoConfig`  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

### LoadNgoConfig

```xml
<com.devcode.paymentiq.integration.loadngo.LoadNgoConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <supportedCurrencies>EUR</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.loadngo.LoadNgoConfig>
```

</details>

### Configuration Steps
1. Merchant should request a API PGP Public key from EMP-CORP and then provide it to PaymentIQ Technical Support.
2. PaymentIQ Technical Support will then return a Public key which the merchant should provide to EMP.

## Example Routing Rule

![](/img/providers/routing/loadngo.png)

## Flow

### LoadngoDeposit

The flow of LoadnGo deposit is not our typical flow in PaymentIQ. 
1. The transactions are initiated from the users APP and are then sent to the EMP-CORP system that will send a `Deposit` request to PaymentIQ. 
2. PaymentIQ will not be able to check the userid via the verifyuser request like in the normal flow. 
3. PIQ will now use [lookupuser](/docs/apis_and_integration/integration_api/lookupuser) that is available in the IntegrationAPI (needs to be added by merchant).
4. A [authorize](/docs/apis_and_integration/integration_api/authorize) will be sent from PaymentIQ to merchant system if lookupuser was `Successful`.
5. When [authorize](/docs/apis_and_integration/integration_api/authorize) is `Successful` PaymentIQ will send a [transfer](/docs/apis_and_integration/integration_api/transfer) request to merchant.
6. After [transfer](/docs/apis_and_integration/integration_api/transfer) is done a response from PaymentIQ is sent to EMP-CORP with results of payment (including status and txRefId).


## Test Information

One need to ask EMP-CORP team to send test transactions on the following urls:

test: 	https://test-api.paymentiq.io/paymentiq/api/loadngo/deposit/process/{merchantId}

live:  	https://api.paymentiq.io/paymentiq/api/loadngo/deposit/process/{merchantId}
