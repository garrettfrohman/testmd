---
id: "limits"
---

# Limit Rules

The Limits tab is the area where we can define the individual transaction limits on transaction values that occur in the cashier.  This means the minimum and maximum limits for deposits and withdrawals.

As with other rule set, we define limits using conditions to activate actions.  Rules can be set using any of the available conditions.

It is good practice to first setup catch-all backup rules that are quite broad in scope and will apply to any transactions that do not have specific rules defined.  These would always be placed at the bottom of any rule set, and are only intended to ensure that rules are present for all transactions.

![](/img/rulesettings/RulesLimits/1.png)

It is important to add the currency definition to any Min or Max amount, and separate multiple definitions with a comma.

Once the back-up rules are in place it is preferable to set more specific limits as desired.

We can imagine an example where we wish to define higher limits for depositors who are using a 3D secure card MID, and lower limits for first time depositors who are using a non 3D secure MID.

In these two examples, the rules would be defined as shown

![](/img/rulesettings/RulesLimits/2.png)

These rules would be position above the ‘Catch-all’ rules in order to be active on transactions.

## Limits for specific payment method accounts

This feature allows setting limits for specific payment methods based on saved user PSP account UUIDs, instead of using regular limit rules. Just like regular limit rules it's supposed to work both in displaying the limits in the cashier, and applying the limits when the transaction is processed. For this to work the merchant will have to send a new attribute in the /verifyuser response called "limits" and the value will be a JSON object as a string containing the limits per accountId. It is also mandatory to set up a limit rule as the topmost rule with the new action "Use attribute limits" with the value "Yes".

If this limit rule is set up but PaymentIQ can't find or resolve any limits from attributes, PaymentIQ will evaluate the regular limit rules that are set up below this rule.

Reasons for not resolving any limits from attributes could be that the received data is invalid, or that the provided accountIds does not match with the user's accounts/methods.

### Verifyuser "limits" attribute

The attribute that the merchant has to send is called "limits" and the value has to be a json formatted string with the following fields:

| **value** | **Type** | **Mandatory** | **description**                                                                                                  | **example**                          |
|:----------|:---------|:--------------|:-----------------------------------------------------------------------------------------------------------------|:-------------------------------------|
| accountId | String   | Yes           | The accountId (sometimes referred to as accountUUID) of the saved user PSP account of a previous payment in PaymentIQ. | d22ea42d-e3c8-4773-b91a-cb16902d1ead |
| max       | String   | Yes           | The limit max value                                                                                              | 10                                   |
| min       | String   | No            | The limit min value. Defaults to 0.                                                                              | 1                                    |

:::note
Make sure to escape the quotation marks inside the JSON string with a backslash, for example: \"accountId\"
:::

##### Full example

```json
"limits": "[{\"accountId\": \"d22ea42d-e3c8-4773-b91a-cb16902d1ead\", \"min\": \"1\", \"max\": \"10\"}]" 
```

##### Example without min

The min value will default to 0.

```json
"limits": "[{\"accountId\": \"d22ea42d-e3c8-4773-b91a-cb16902d1ead\", \"max\": \"10\"}]" 
```

##### Attributes example

```json
"attributes": { "limits": "[{\"accountId\": \"d22ea42d-e3c8-4773-b91a-cb16902d1ead\", \"min\": \"1\", \"max\": \"10\"}]" } 
```

##### Full Verifyuser example

```json
{
    "userId": "user_123",
    "success": true,
    "userCat": "VIP_SE",
    "kycStatus": "Approved",
    "sex": "UNKNOWN",
    "firstName": "John",
    "lastName": "Jonsson",
    "street": "Example street 1",
    "city": "Stockholm",
    "state": "Stockholm or ISO 2 abbreviated state for countries where this is applicable",
    "zip": "177 32",
    "country": "SWE",
    "email": "test@example.com",
    "dob": "1981-12-23",
    "mobile": "+46733123123",
    "balance": 100.5,
    "balanceCy": "SEK",
    "locale": "sv_SE",
    "attributes": {
        "allow_manual_payout": "true",
        "limits": "[{\"accountId\": \"d22ea42d-e3c8-4773-b91a-cb16902d1ead\", \"min\": \"1\", \"max\": \"10\"}]"
    }
}
```

### Limit Rule

In order for PaymentIQ to know that it should look for limits from attributes, there has to be a limit rule at the topmost level with the action "Use attribute limits" and the value "Yes".

If this limit rule is set up but PaymentIQ can't find or resolve any limits from attributes, PaymentIQ will evaluate the regular limit rules that are set up below this rule.

Since it is mandatory to add the "min" and "max" actions to a limit rule, this rule will have to have them added, however, they won't have any effect and can be set to any random values.

![](/img/rulesettings/RulesLimits/3.png)

If this action is not visible for the merchant, you need to add the following into the DecisionTableConfig under actions in T5 Limit:

```xml
<com.devcode.service.decisiontable.action.ActionType>USE_ATTRIBUTE_LIMITS</com.devcode.service.decisiontable.action.ActionType>
```
