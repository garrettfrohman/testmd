--- 
id: "wallee" 
title: "Wallee"
hide_title: "true"
---
 
![](/img/providers/logos/wallee.png)

# Wallee

## About

| Provider Name                | Wallee                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://wallee.com/](https://wallee.com/)                                      |
| Classification               | Aggregator                                                                      |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `BankDeposit` <br/> `WebRedirectDeposit` <br/> `Refund`                         |
| PaymentIQ Configuration File | `WalleeConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.wallee.WalleeConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>?????</username>
        <groupId>????</groupId>
        <apiKey>????</apiKey>
        <productName>????</productName>
        <productId>????</productId>
        <supportedCurrencies>XXX|YYY</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.wallee.WalleeConfig>
```

</details>

### Attributes

| Attribute   | Description                                                |
|-------------|------------------------------------------------------------|
| username    | ID of the application user that is making the API requests |
| groupId     | ID of the Wallee space                                     |
| apiKey      | Key belonging to the application user                      |
| productName | Name of the "line item"                                    |
| productId   | ID of the "line item"                                      |

The username (User ID) is found by navigating to Account -> Application Users. If no application user have been created yet, please follow the guide below.

The groupId (Space ID) is found by navigating to Account -> Spaces. A list of all available spaces is displayed. Click on the space that should be used and the ID shown under tha name.

### Application User
If the Wallee account doesn't have an application user that should be used by PaymentIQ already it has to be created and assigned the correct roles first.

1. When logged in to Wallee's Backoffice, navigate to Account -> Roles and click "Create role"

    ![](/img/providers/wallee-user-step1.png)

2. Enter a name, select the checkbox "Payment Processing" and then click "Create"

    ![](/img/providers/wallee-user-step2a.png)

    ![](/img/providers/wallee-user-step2b.png)

3. Navigate to "Application Users" and click "Create application user"
4. Enter a name in the popup and click "Create application user"

    ![](/img/providers/wallee-user-step4.png)

5. The User ID and Authentication Key of the created user will now be displayed. Enter the User ID in the `<username>` field and the Authentication Key in the `<apiKey>` field of your WalleeConfig in PaymentIQ

    ![](/img/providers/wallee-user-step5.png)

6. On the newly created user's page click "Assign a Role" in order to give it the correct permissions

    ![](/img/providers/wallee-user-step6.png)

7. Click the "+" icon to the right of "Space Roles"

    ![](/img/providers/wallee-user-step7.png)

8. Select the space that should be used in the "Context" dropdown and the role that was created in step 2 in the "Roles" field

    ![](/img/providers/wallee-user-step8.png)

9. Click "Assign Role" to close the popup and then "Save Roles" to save the changes

### Webhooks
A webhook must be registered so that Wallee will send callbacks to PaymentIQ when the transaction state changes. In order to register a new webhook follow these steps:

1. Navigate to Space -> Webhooks. Click the "URL" tab and then click "Create webhook URL"

    ![](/img/providers/wallee-webhook-step1.png)

2. Enter a name and the URL to use. In the image below we're setting up the hosted production environment. If you are setting up a different environment please change the values accordingly

    ![](/img/providers/wallee-webhook-step2.png)

| Environment | URL                                                         |
|-------------|-------------------------------------------------------------|
| Production  | https://api.paymentiq.io/paymentiq/api/wallee/callback      |
| Test        | https://test-api.paymentiq.io/paymentiq/api/wallee/callback |

3. Click "Create" and then navigate to the "LISTENER" tab and click "Create webhook listener"

  ![](/img/providers/wallee-webhook-step3.png)

4. Select "Transaction" in the "Entity" dropdown and click "Continue"

  ![](/img/providers/wallee-webhook-step4.png)

5. Enter a name, select the URL created in earlier steps and select the following values in the "Entity State" field: Authorized, Fulfill, Decline, Failed, Voided

  ![](/img/providers/wallee-webhook-step5.png)

6. Click "Create"

### Services
A service can be used to redirect directly to a specific payment method. If no service is used the first redirect will be to Wallee's payment selection page where the user will be able to select from the configured payment methods. Services must be mapped in WalleeConfig, see example below.

```xml
<services>
  <entry>
    <string>POSTFINANCE</string>
    <string>29660</string>
  </entry>
</services>
```

The ID of a payment method is found by navigating to Space -> Configuration -> Payment Methods. This will display a list of all configured payment methods. Click on one and the ID is shown under the method name as in the image below.

![](/img/providers/wallee-pm-id.png)

## Example Routing Rule
![](/img/providers/routing/wallee.png)

## Test Information
Transactions can be simulated to successed or failed on the redirect payment page.
