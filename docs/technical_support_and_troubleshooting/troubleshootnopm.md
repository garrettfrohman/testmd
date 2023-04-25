---
id: "troubleshootnopm"
---

# Investigate Payment Methods Not Showing

## Problem Description

In the PaymentIQ Cashier the customer is met with a message "No Payment Methods Available" and is unable to proceed with the transaction. Or if you are connecting via the FrontAPI to PaymentIQ and no methods are returned.

## Troubleshooting Steps

### Checking The Payment Method Rules

For payment methods to be available there needs to be payment method rules set up in PaymentIQ under **Rules > Payment Methods**. The rules needs to be set up directly on the MID or on the "Master" MID (the one your MIDs are organized under). You can read about how to configure rules [here](/docs/configuration_and_administration/system_configuration/payment-methods/)

As you can have conditions on your payment method rules your transaction will need to match at least one of the rules to get payment methods to show. So for example if you have "User Country" as a condition on all payment method rules with various country such as SWE, JPN and AGO but the transaction is getting MEX from the verify user response in the [Integration API](/docs/apis_and_integration/integration_api/verifyuser) there are no matching rules and no payment methods to show.

#### Example PaymentIQ cashier with no matching methods configured in the rules

![](/img/troubleshooting/nopaymentmethods.png)

#### Example Front API response with no matching methods configured in the rules

```json
{
  "merchantId": nnnnnnnn,
  "userId": "test",
  "success": true,
  "methods": [],
  "feeInfo": {
    "nextFreeDate": ""
  }
}
```

### Verify User Response

If there is no [verify user](/docs/apis_and_integration/integration_api/verifyuser) response from the merchant platform or if it is incorrect PaymentIQ will not have enough information to display any payment methods and reply with f.ex. a 401 or 503 error when trying to load them.

#### Example PaymentIQ cashier with incorrect verify user response

![](/img/troubleshooting/nopaymentmethods.png)

#### Example (from Insomnia Client) Front API response with incorrect verify user response

![](/img/troubleshooting/401verify.png)

### Contacting PaymentIQ Technical Support or Onboarding Support

If you have checked the above listed suggestions to resolve the issue but still can not find it, please reach out to the Onboarding Team if you are currently Onboarding or the Technical Support Team if you are live.

It is helpful for us when troubleshooting to know the MID you are having issues with and any other related information you have found in your troubleshooting. To check that your verify user response is correct we would be helped to receive a valid userId and sessionId to do further testing.