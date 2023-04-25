--- 
id: "vpag"
title: "VPag"
hide_title: "true"
---

![](/img/providers/logos/vpag.png)

# VPag

## About
VPag Gateway is a product focused in Latin America, offering secure solutions that enable international digital commerce using local payment methods.

| Provider Name                | VPag                              |
|------------------------------|-----------------------------------|
| Link                         | https://vpag.com/                 |
| Classification               | Banking                           |
| Regions                      | `Brazil`                          |
| Currencies                   | `BRL`                             |
| Methods/PaymentTxTypes       | `PixDeposit`<br/> `PixWithdrawal` |
| PaymentIQ Configuration File | `VPagConfig`                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.vpag.VPagConfig>
    <enabled>true</enabled>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <contentType>???</contentType>
                <username>???</username>
                <password>???</password>
                <merchantApprovalRequired>true</merchantApprovalRequired>
                <supportedCurrencies>BRL</supportedCurrencies>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.vpag.VPagConfig>
```
</details>

### Attributes

| Attribute                        | Description                                                       |
|----------------------------------|-------------------------------------------------------------------|
| account.contentType              | Corresponds to the "grant_type" provided by VPag.                 |
| account.username                 | Corresponds to the "client_id" provided by VPag.                  |
| account.password                 | Corresponds to the "client_secret" provided by VPag.              |
| account.merchantApprovalRequired | Indicate which flow will be used for withdrawal (see info below). |

### Payment Methods

Under Admin->Cashier->Payment Methods and Input you will find PixDeposit and PixWithdrawal payment methods with VPAG service. If you need to reconfigure it please contact PaymentIQ technical support.
Please add VPAG service under PIX entry in MerchantConfig:

```xml
<serviceMapping>
    <entry>
        <string>PIX</string>
        <string>VPAG</string>
    </entry>
</serviceMapping>
```

## Example Routing Rule

![](/img/providers/routing/vpag.png)
![](/img/providers/routing/vpag1.png)

## Transaction Flows
### Deposit
User should use Brazil CPf for "nationalId" field. On redirection user should scan QR code and proceed payment.

### Withdrawal (merchantApprovalRequired - false; merchant's approval is not needed)
1. In PaymentIQ backoffice go to Rules -> Approval and create Auto Approval rule.
   ![](/img/providers/routing/vpag2.png)
2. Set \<merchantApprovalRequired>false\</merchantApprovalRequired> under accountConfig.
3. User should use Brazil CPF for "nationalId" field. On redirection user should fill in PVag form and proceed payment.

### Withdrawal (merchantApprovalRequired - true; auto approval)
1. In PaymentIQ back office go to Rules -> Approval and create Auto Approval rule.
   ![](/img/providers/routing/vpag2.png)
2. Set \<merchantApprovalRequired>true\</merchantApprovalRequired> under accountConfig.
3. User should use Brazil CPF for "nationalId" field. On redirection user should fill in PVag form and proceed payment.
4. Merchant's approval will perform automatically.

### Withdrawal (merchantApprovalRequired - true; manual approval)
1. Set \<merchantApprovalRequired>true\</merchantApprovalRequired> under accountConfig.
2. User should use Brazil CPF for "nationalId" field. On redirection user should fill in PVag form and proceed payment.
3. In PaymentIQ backoffice you can Approve you Deny transaction.

## Test Information

Please use following info as test user info

nationalId = 08744603444

```xml
<com.devcode.paymentiq.integration.merchant.mock.MockUser>
   <firstName>Alina Mira</firstName>
   <lastName>Maria Coriolano</lastName>
   <dob>1993-07-04</dob>
   <email>test5@test.com</email>
   <street>Customer Address</street>
   <city>Sao Paulo</city>
   <zip>05303000</zip>
   <country>BRA</country>
   <state>SP</state>
</com.devcode.paymentiq.integration.merchant.mock.MockUser>
```