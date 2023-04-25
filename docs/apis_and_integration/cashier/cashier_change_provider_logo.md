---
id: "cashier_change_provider_logo"
---

# Change A Provider Logo

:::warning
This is a deprecated way of uploading custom payment method logos, please see the new admin section [`Payment Method Logos`](../../configuration_and_administration/system_configuration/payment-method-logos).
:::

You can configure another logo to be used based on your mid by adding a translation in PaymentIQ-backoffice.
For example, if you want to change the logo used for `Creditcard`.


:::info
Currently PaymentIQ only support PNG-logos
:::

1. Add a translation in PaymentIQ Backoffice -> Admin -> Messages

2. Add a new key called `{provider}_logo` (`creditcard_logo`, `trustly_logo` etc). **Note: lowercaps**

3. Give the key a value that matches the image you want to show (e.g creditcard_alternate)

4. Send the image, named as the translation value you added (e.g creditcard_alternate) to you boarding/support agent to upload to [static git-repo](https://github.com/devcode-git/static.paymentiq.io/tree/master/content). Recommended image size is ~100px height.

5. Reload the cashier and Creditcard should now show the `creditcard_alternate.png` logo

## Naming convention

If you upload an alternate version of an already existing provider logo that you think will get re-used, pick a generic name like provider_alternate.png.
If it's a logo specific to the merchant, then name it provider_{mid}.png.

<img src='https://static.paymentiq.io/cashier/provider_logo_faq.png' />

