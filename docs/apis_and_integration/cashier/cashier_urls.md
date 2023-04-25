---
id: "cashier_urls"
---

# Cashier URLs

Both test and production environment can target PaymentIQ in test and production. Default [if nothing set] is set to production.
The PIQ-environment is set by specifying an environment parameter.

:::caution
Please note that when using the cashier on your site you should always initialize it according to our setup guides and not target it directly with URL.
Some features depend on the cashier being initialized with the bootstrapper script.
:::


```js
development || test || production
https://pay.paymentiq.io/cashier/develop/?environment=test
```
<!--
Setting environment to test or development will trigger it to be showed at the top at all times

<img src="/assets/public/images/documentation/cashier/cashierv2-app-badges.png" alt="drawing" width="700"/>
-->

## Test
[https://pay.paymentiq.io/cashier/develop/?environment=test&merchantId=1000&userId=test](https://pay.paymentiq.io/cashier/develop/?environment=test&merchantId=1000&userId=test)


## Production
[https://pay.paymentiq.io/cashier-live](https://pay.paymentiq.io/cashier-live)

Redirects to the latest deployed version
