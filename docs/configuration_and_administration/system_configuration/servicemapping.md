---
id: "servicemapping"
---

# Configure Service Mapping

## About

If you are using more than one provider or APM with for example the BankDeposit or WebRedirectDeposit transaction type, you may want to separate these in the cashier with their own logos etc. This guide will show you how to do that.

## 1 - Add Service Mapping

In the Merchant Configuration file (**Admin > Configuration > MerchantConfig**) in PaymentIQ you should find the serviceMapping entry.  

```xml
<serviceMapping>
```

An entry needs to be added for each transaction type, in this example BANK and WEBREDIRECT, with separate labels for the different providers/APMs you are using, separated with the pipe character:

```xml
<serviceMapping>
  <entry>
    <string>BANK</string>
    <string>CITADEL|EUTELLER|INTERAC|ENTERCASH|ASTROPAY</string>
  </entry>
  <entry>
    <string>WEBREDIRECT</string>
    <string>BOLETO|MULTIBANCO|YANDEX</string>
  </entry>
</serviceMapping>
```

## 2 - Update Payment Methods

Under **Rules > Payment Methods** these mapping labels will now show up as payment method options and need to be added in their respective place in order to show up as payment options in the cashier.

![](/img/settingsandadmin/AdminServicemapping/01.png)

## 3 - Update Routing Rules

The final setting step in PaymentIQ is to update the Routing Rules.

In **Rules > Routing** for each corresponding PSP/APM you will need to add a condition called `PSP service` in order to enable the correct routing based on the service value.

![](/img/settingsandadmin/AdminServicemapping/02.png)

## 4 - Updating the cashier

Now that the PaymentIQ setup is complete with step 1-3, the final step will be to get these to display in the cashier. If you are using PIQ's standardized cashier you don't have to follow this step since it will work automatically, however, if you are using your own in-house built cashier please continue with the below.

This is done when you get the payment methods for a user (See the Front End API guide for more details on how to do this). You need to look for the 'service' parameter and adapt how that is shown in your cashier.

### Example response:

```json
{
    "merchantId": 1000,
    "userId": "BANKSERVICE_EUR",
    "success": true,
    "methods": [
        {
            "txType": "BankDeposit",
            "accountSettings": null,
            "accounts": [],
            "limit": null,
            "fees": [],
            "pspToUserCurrencyBuyRate": 0,
            "providerType": "BANK",
            "service": "CITADEL",
            "pspCurrency": "",
            "canAddAccount": true,
            "maintenanceInfo": {
                "maintenance": false
            },
            "toUserCurrencyBuyRate": 0
        },
        {
            "txType": "BankDeposit",
            "accountSettings": null,
            "accounts": [],
            "limit": null,
            "fees": [],
            "pspToUserCurrencyBuyRate": 0,
            "providerType": "BANK",
            "service": "ENTERCASH",
            "pspCurrency": "",
            "canAddAccount": true,
            "maintenanceInfo": {
                "maintenance": false
            },
            "toUserCurrencyBuyRate": 0
        },
        {
            "txType": "BankDeposit",
            "accountSettings": null,
            "accounts": [],
            "limit": null,
            "fees": [],
            "pspToUserCurrencyBuyRate": 0,
            "providerType": "BANK",
            "service": "INTERAC",
            "pspCurrency": "",
            "canAddAccount": true,
            "maintenanceInfo": {
                "maintenance": false
            },
            "toUserCurrencyBuyRate": 0
        },
        {
            "txType": "BankDeposit",
            "accountSettings": null,
            "accounts": [],
            "limit": null,
            "fees": [],
            "pspToUserCurrencyBuyRate": 0,
            "providerType": "BANK",
            "service": "EUTELLER",
            "pspCurrency": "",
            "canAddAccount": true,
            "maintenanceInfo": {
                "maintenance": false
            },
            "toUserCurrencyBuyRate": 0
        }
    ],
    "feeInfo": {
        "nextFreeDate": null
    }
}
```

With this information you then need to include the 'service' parameter in the deposit request so that the right routing rule is invoked (See the Front End API documentation for examples).

## Summary

So by adding a label in the service mapping and setting up the payment methods you can build routing rules with a condition to map to the 'service'.

With this setup you get the service tag in the payment methods request in the Front End API and can use that to configure how it should show in your cashier. And with that information you then include the service parameter in the transaction request to get the right routing.
