---
id: "activate_integration_api"
---

# Activate The Integration API

The default setting on both the PaymentIQ Test and Production environment is for a merchant MID to be in "Mock Mode". This means a mock version of the Integration API is used which responds with customer data from the MockMerchantConfig. This is so that you can start testing the cashier and payment flows before you have the Integration API ready.

When you want to start testing with your Integration API it must be enabled. This is done in the MerchantConfig file in PaymentIQ.

The relevant settings will be the `<integrationService>` and the `<apiIntegrationUrl>`.

Typically in the MerchantConfig it will look like this:

### Integration API set to Mock-mode not utilizing the Merchant Operator Platform 

```xml
<!-- Comment to disable mockMerchantIntegration service when activating standardMerchantIntegrationService-->
<integrationService>mockMerchantIntegrationService</integrationService> 


<!-- Uncomment the below when you want PIQ to send request to the URL defined in defined in apiIntegrationUrl
<integrationService>standardMerchantIntegrationService</integrationService>
<apiIntegrationUrl>http://yourdomain.com/{action}</apiIntegrationUrl> -->
```

As you can see the `<integrationService>` is set to "mockMerchantIntegrationService" for the mock flow and the template for how the setting should look for the standard flow is commented out.

To enable the standard flow you should comment out (or remove, but it is good to keep it especially on the testing environment) the "mock" setting and enable the "standard" settings. You should also add the URL for your specific integration.

### Integration API set to Standard-mode connected to the Merchant Operator Platform

```xml
<!-- Comment to disable mockMerchantIntegration service when activating standardMerchantIntegrationService
<integrationService>mockMerchantIntegrationService</integrationService> -->


<!-- Uncomment the below when you want PIQ to send request to the URL defined in defined in apiIntegrationUrl -->
<integrationService>standardMerchantIntegrationService</integrationService>
<apiIntegrationUrl>http://yourdomain.com/{action}</apiIntegrationUrl>
```

:::info

In this case your endpoints will be:

http://yourdomain.com/verifyuser

http://yourdomain.com/authorize

http://yourdomain.com/transfer

http://yourdomain.com/cancel

http://yourdomain.com/notification

http://yourdomain.com/lookupuser

:::



Indicated by the `http://yourdomain.com/{action}` setting.

There can only be one integration URL enabled for a MID at a time.