---
id: "cashier_incognito_mode"
---

# Using The PaymentIQ Cashier In Incognito Mode

From version `1.2.0` of the cashier, the application supports being used in incognito mode. There will however be some features that will not function fully.
An info message will be displayed at the top informing the user about this.

Normal iFrame and window flows will work as expected.

## Examples of limited features:

- Generally features that require the usage of third-party cookies (cookies, localStorage, sessionStorage) will not work fully.
- Auto-closing of a provider opened in a new window if the popup was initially blocked
- Provider redirect (When the outer window is redirected to the provider)
