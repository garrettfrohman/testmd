---
id: "configure_authentication"
---

# Configure Authentication

If you as a merchant has enforced access control on the API with an HTTP authentication scheme, additional configuration elements has to be added to the `MerchantConfig` in order for PaymentIQ to be able to make requests against your server.

Current supported schemes:
- Basic
- Bearer (static token)

:::info

Only one scheme can be used at a time.
:::

## How to Configure

The configuration element should be added in the root level of the `MerchantConfig`.

### Basic authentication

Use elements `apiIntegrationUsername` and `apiIntegrationPassword`, which PIQ will convert to the base64 encoded token string.

 ```xml
<com.devcode.paymentiq.integration.merchant.MerchantConfig>
    ...
    <apiIntegrationUsername>username</apiIntegrationUsername>
    <apiIntegrationPassword>password</apiIntegrationPassword>
    ...
</com.devcode.paymentiq.integration.merchant.MerchantConfig>
```

### Bearer authentication

Use element `apiBearerToken` to add the encoded token value. Please note that we only support a static token.

```xml
<com.devcode.paymentiq.integration.merchant.MerchantConfig>
   ...
   <apiBearerToken>QUJDRA==</apiBearerToken>
   ...
</com.devcode.paymentiq.integration.merchant.MerchantConfig>
```

