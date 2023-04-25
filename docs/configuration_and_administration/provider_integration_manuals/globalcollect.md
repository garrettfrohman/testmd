--- 
id: "globalcollect"
title: "Global Collect"
hide_title: "true"
---

![](/img/providers/logos/globalcollect.png)

# Global Collect

## About

| Provider Name                | Global Collect                                                                                     |
|------------------------------|----------------------------------------------------------------------------------------------------|
| Link                         | [Global Collect Docs](https://epayments-api.developer-ingenico.com/?paymentPlatform=GLOBALCOLLECT) |
| Classification               | Credit Card Processor                                                                              |
| Regions                      | International                                                                                      |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                    |
| Methods/PaymentTxTypes       | `Creditcard Deposit` <br/> `Capture` <br/> `Void`<br/> `Refund`                                    |
| PaymentIQ Configuration File | `GlobalCollectConfig`                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.globalcollect.GlobalCollectConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>PREPROD_N3DS</string>
            <account>
                <merchantId>???</merchantId>
                <secretKey>???</secretKey>
                <authType>FINAL_AUTH</authType> <!-- FINAL_AUTH = Authorization. AUTH_CAPTURE = sale. -->
                <use3Dsecure>true</use3Dsecure>
                <supportedCurrencies>EUR|GBP</supportedCurrencies>
                <version>v1</version>
                <transactionChannel>ECOMMERCE</transactionChannel>
                <apiKey>???</apiKey>
                <useTokenId>true</useTokenId>
                <pspPrivateKey>???</pspPrivateKey>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
    <container>iframe</container>
</com.devcode.paymentiq.integration.globalcollect.GlobalCollectConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                                                                                |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId          | Merchant ID issues by GlobalCollect.                                                                                                                       |
| apiKey              | Api key issued by GlobalCollect. Used together with secretKey to create correct Authorizations that will allow ProductIQ to make requests to GlobalCollect |
| secretKey           | Signature key provided by GlobalCollect used by PaymentIQ for security reasons, together with the apiKey.                                                  |
| authType            | Authorization type.                                                                                                                                        |
| use3Dsecure         | Whether the creditcard operations should prompt the user for 3DSecure authentication. Supports v1 and v2                                                   |
| supportedCurrencies | Currencies supported by GlobalCollect                                                                                                                      |
| version             | GlobalCollect API version. Integration was developed for v1                                                                                                |
| transactionChannel  | Indicates the channel via which the payment is created. Allowed values: ECOMMERCE, MAIL, MOTO, TELEPHONE                                                   |
| useTokenId          | Whether card operations should be tokenized and tokens used for subsequent, reccuring payments.                                                            |
| pspPrivateKey       | Secret key used in order to validate webhook authenticity. Created by merchant in the GlobalCollect Configuration Center - under Webhooks Keys.            |


## Provider Configuration

1. The above XML template (GlobalCollect) will need to be added via backoffice Admin -> Configuration.
2. Routing needs to be added for Creditcard operations in Routing -> Routing.


## Example Routing Rules
![CreditCard routing](/img/providers/routing/global_collect_routing.png)

## Transaction Flow

1. The end user enters the transaction amount (and creditcard relevant information).
2. PaymentIQ sends the payment request to GlobalCollect.
3. GlobalCollect responds with an initial status + a redirect url (in case of 3DS).
4. In case of 3DS, the user is redirected in order to complete authentication.
5. GlobalCollect sends back a webhook notification once the transaction status has changed.

### Webhook Configuration
Since GlobalCollect supports static webhook URLs, a setup must be done in the GlobalCollect Configuration center. The [dashboard](https://preprod.account.ingenico.com/dashboard) can be consulted, under the **webhooks** sections.

Under ***Webhook keys*** a webhook Secret Key can be generated. It is necessary in order to validate webhooks being sent by Global Collect.
The Secret Key value needs to be set in the account config ***pspPrivateKey*** as described in the xml above. The Key ID accompanying it, in the Configuration Center, can be ignored.

Under ***Webhook***, a proper callback URL needs to be set. Appropriate endpoints needs to be added and **activated**. Activation logic on PaymentIQ side is implemented and should happen automatically once the endpoint is added in the Config Center.
All webhook events are currently supported, although most - irrelevant - statuses will be ignored.

Test Callback URL: https://test-api.paymentiq.io/paymentiq/api/globalcollect/callback      
Prod Callback URL: https://api.paymentiq.io/paymentiq/api/globalcollect/callback

## Test Information

### Creditcard

| Card Number      | Expected Status  | 3DS                             |
|------------------|------------------|---------------------------------|
| 4000000000000002 | PENDING_APPROVAL | v1                              |
| 4000000000000010 | REJECTED         | v1                              |
| 4012000033330026 | PENDING_APPROVAL | v2 frictionless                 |
| 4567350000427977 | PENDING_APPROVAL | v2 frictionless with method url |
| 4012007153923001 | PENDING_APPROVAL | v2 with challenge               |

For a full table of test data, the following [link](https://epayments.developer-ingenico.com/best-practices/services/3dsv2/test-cases/) can be accessed.
