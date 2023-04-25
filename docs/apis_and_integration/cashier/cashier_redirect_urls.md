---
id: "cashier_redirect_urls"
---

# Redirect URLs

In PaymentIQ backoffice you can define what redirect URLs that should be used for successful and failed transactions.
You do this by adding/editing the MerchantConfig tied to a merchant.

```xml
<com.devcode.paymentiq.integration.merchant.MerchantConfig>
  <properties>
    <entry>
      <string>successUrl</string>
      <string>${baseCashierV2Url}/redirect-success?txId=\${ptx.id}</string>
    </entry>
    <entry>
      <string>failureUrl</string>
      <string>${baseCashierV2Url}/redirect-failure?txId=\${ptx.id}</string>
    </entry>
    <entry>
      <string>pendingUrl</string>
      <string>${baseCashierV2Url}/redirect-pending?txId=\${ptx.id}</string>
    </entry>
    <entry>
      <string>cancelUrl</string>
      <string>${baseCashierV2Url}/redirect-cancel?txId=\${ptx.id}</string>
    </entry>

  </properties>
</com.devcode.paymentiq.integration.merchant.MerchantConfig>
```
**${baseCashierV2Url}** - Will automatically resolve to the baseUrl containing the branch defined to be used for this merchant.

If no specific version is set, ${baseCashierV2Url} will resolve to 'master' (https://pay.paymentiq.io/cashier/master)