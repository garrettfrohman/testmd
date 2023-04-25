---
id: "1click_api_route_identity_providers"
---

# Routing Identity Providers

:::info
- No routing needed for Devcode Identity(GII)

- In test you do not need to add routing since its configured by the PaymentIQ Team.

- Please note that this is the default account names, you can create new accounts and use them instead.
:::


## Trustly 

1. Click "New?"
2. Choose a name for the rule, for example "1-click Trustly"
3. Choose a name for the condition, for example "trustly signin"
4. In Conditions, choose "Identity Type"
5. Choose "Trustly Pay & Play"
6. On "PSP account" write "SignIn". The account "SingIn" must be configured in `TrustlyConfig`.
7. On PSP, choose "Trustly".

![](/img/1clickapi/routing_trustly.png)

### Trustly Hybrid setup

If you have a Trustly Hybrid setup you need to do a different routing.

![](/img/1clickapi/hybrid_routing.png)

Please note that this new routing rule needs to be above the Banking rule or any other rule containing `TrustlyDeposit`.

## Zimpler

1. Click "New?"
2. Choose a name for the rule, for example "1-click Zimpler"
3. Choose a name for the condition, for example "Zimpler signin"
4. In Conditions, choose "Identity Type"
5. Choose "Zimpler"
6. On "PSP account" write "default". The account "default" must be configured in `ZimplerConfig`.
7. On PSP, choose "Zimpler".

![](/img/1clickapi/routing_zimpler.png)

## PayPal

1. Click "New?"
2. Choose a name for the rule, for example "1-click PayPal"
3. Choose a name for the condition, for example "PayPal signin"
4. In Conditions, choose "Identity Type"
5. Choose "PayPal"
6. On "PSP account" write "default". The account "default" must be configured in `PayPalConfig`.
7. On PSP, choose "PayPal".

![](/img/1clickapi/routing_paypal.png)

## All identity providers at the same time

![](/img/1clickapi/routing.png)