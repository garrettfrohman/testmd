--- 
id: "pagseguro" 
title: "PagSeguro"
hide_title: "true"
---
 
![](/img/providers/logos/pagseguro.png)

# PagSeguro

## About
PagSeguro is a payment provider offering Creditcard Checkout and bank PIX payment operations and status check.

Transparent checkout is a solution that, through encryption, allows credit card charges to be made without opening an external page that redirects the buyer to a payment environment.

The PagSeguro PIX makes it possible to receive charges immediately, for example, points of sale in physical stores and e-commerce solutions.


| Provider Name                | PagSeguro                                                      |
|------------------------------|----------------------------------------------------------------|
| Link                         | [https://pagseguro.uol.com.br/](https://pagseguro.uol.com.br/) |
| Classification               | Card Processor, Banking                                        |
| Regions                      | Brazil                                                         |
| Currencies                   | BRL                                                            |
| Methods/PaymentTxTypes       | `BankDeposit`<br/>`WebRedirectDeposit`                         |
| PaymentIQ Configuration File | `PagSeguroConfig`                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pagseguro.PagSeguroConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>CHECKOUT</string>
      <account>
        <username>??</username>
        <accessToken>??</accessToken>
        <productId>123</productId>
        <defaultDescriptor>product 123 description</defaultDescriptor>
        <supportedCurrencies>BRL</supportedCurrencies>
        <redirectMethod>GET</redirectMethod>
      </account>
    </entry>
    <entry>
      <string>PIX</string>
      <account>
        <username>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</username>
        <password>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</password>
        <accountID>########-####-####-####-############</accountID><!--chave-->
        <defaultDescriptor>some unique text for the payer</defaultDescriptor>
        <supportedCurrencies>BRL</supportedCurrencies>
        <redirectMethod>GET</redirectMethod>
        <httpClientConfigEntry>
        <viqProxy>false</viqProxy>
        <clientCertPem>-----BEGIN CERTIFICATE-----
MIIE2TC...
-----END CERTIFICATE-----</clientCertPem>
          <clientCertKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQI...
-----END RSA PRIVATE KEY-----</clientCertKey>
          <useClientCert>true</useClientCert>
        </httpClientConfigEntry>
        <container>iframe</container>
        <width>400</width>
        <height>600</height>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Bambora payment ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.pagseguro.PagSeguroConfig>
```
</details>

### Attributes

#### CHECKOUT

| Attribute                 | Description                                                                                                                                                  |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.username          | Corresponds to the `email` that was used to register/access PagSeguro back office. It can be seen at `PERFIS DE INTEGRAÇÃO > Vendedor > Credenciais`.        |
| account.accessToken       | Corresponds to the `token` that can be obtained through your screen logged into your PagSeguro account (at `PERFIS DE INTEGRAÇÃO > Vendedor > Credenciais`). |
| account.productId         | Corresponds to the item identifier (Mandatory)                                                                                                               |
| account.defaultDescriptor | Corresponds to the item description (Mandatory)                                                                                                              |

#### PIX

| Attribute                                   | Description                                                                                                                                                                                                                            |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.username                            | Corresponds to the `Cliend ID` from the PagSeguro in order to request access token.                                                                                                                                                    |
| account.password                            | Corresponds to the `Client Secret` from the PagSeguro in order to request access token.                                                                                                                                                |
| account.accountID                           | Corresponds to the unique merchant account identifier that will receive money.                                                                                                                                                         |
| account.forceCountryCode                    | Optional parameter that can be used to specify a country (3 letters code e.g. `BRA`) in case user's country is not configured or is different from Brazil as payments can be made in Brazil only.                                      |
| account.defaultDescriptor                   | It determines a text to be presented to the payer so that he can enter related information, in free format, to be sent to the recipient. If this field is not configured, a `defaultDescriptor` from the PagSeguroConfig will be used. |
| account.httpClientConfigEntry.clientCertPem | Corresponds to the PEM certificate (free text) that is used to make a secured call from PaymentIQ to PagSeguro.                                                                                                                        |
| account.httpClientConfigEntry.clientCertKey | Corresponds to the PEM certificate key (free text) that is used to make a secured call from PaymentIQ to PagSeguro.                                                                                                                    |

#### Notes

- PIX: Client ID, Client Secret, PEM certificate and its key should be provided by the PagSeguro.
- PIX: Webhook URL can be configured using REST API (see below)
- CHECKOUT: Webhook URL is specified in the `CHECKOUT` request, so it is not required to configure it.
- PaymentIQ status polling: For `CHECKOUT` payment it is not possible to configure status polling in PaymentIQ back office as callback notification is required to execute status API call and complete payment. For `PIX` payment - it is possible to configure status polling.

### TxType to operation mapping

| PaymentIQ Transaction Type | PagSeguro Operation |
|----------------------------|---------------------|
| WebRedirectDeposit         | CHECKOUT            |
| BankDepositInput           | PIX                 |

## Configure PIX webhook URL

Webhook url needs to be configured in order to receive a notification from the provider about tx status change. It will let PaymentIQ to react on such change and handle a transaction in a proper way. \
This URL can be configured either by the merchant or the PaymentIQ tech support. \
Webhook URLs for different environments are listed below:

TEST: https://test-api.paymentiq.io/paymentiq/api/pagseguro/callback<br/>
PROD: https://api.paymentiq.io/paymentiq/api/pagseguro/callback

### Check if PIX webhook is configured already

```
curl -i -X GET \
 'https://test-api.paymentiq.io/paymentiq/api/pagseguro/pix/webhook?merchantId={piqMid}&pspAccount={pspAcc}'
```

### Configure PIX webhook

There are two ways how to specify webhook URL

1). Specify it in the request itself using `webhookUrl` parameter:

```
curl -i -X PUT \
   -H "Content-Type:application/json" \
   -d \
'{
  "webhookUrl": "https://test-api.paymentiq.io/paymentiq/api/pagseguro/callback"
}' \
 'https://test-api.paymentiq.io/paymentiq/api/pagseguro/pix/webhook?merchantId={piqMid}&pspAccount={pspAcc}'
```

2). Specify webhook URL in the `pspAcc` account in the PagSeguroConfig e.g. `accountConfig.getCallbackUrl > https://test-api.paymentiq.io/paymentiq/api/pagseguro/callback` and execute:

```
curl -i -X PUT \
   -H "Content-Type:application/json" \
   -d \
'' \
 'https://test-api.paymentiq.io/paymentiq/api/pagseguro/pix/webhook?merchantId={piqMid}&pspAccount={pspAcc}'
```

### Delete configured PIX webhook

```
curl -i -X DELETE \
 'https://test-api.paymentiq.io/paymentiq/api/pagseguro/pix/webhook?merchantId={piqMid}&pspAccount={pspAcc}'
```

> ### Notes
>
> - `piqMid` -- this is a merchant ID in the PaymentIQ (Mandatory).
> - `pspAcc` -- this is an account name from the **PagSeguroConfig** (Mandatory).
> - In order to configure a webhook URL it must be specified either in the request payload or in the account config from the **PagSeguroConfig**.

## Example Routing Rule

![](/img/providers/routing/pagseguro.png)

## Test Information

### Checkout

Please use a WebRedirect deposit transaction type to initiate a Checkout PagSeguro. \
After you specified amount and pressed pay button, you will be redirected to the following page:

![](/img/providers/pagseguro_checkout_01.png)

Please specify all required information and press confirmation button. Then you will be redirected to the receipt page.

![](/img/providers/pagseguro_checkout_02.png)

Please note, payment is not completed yet and must be processed by the PagSeguro.

You can approve, cancel or decline payments from the PagSeguro back office. You can access SANDBOX back office using [this](https://acesso.pagseguro.uol.com.br/sandbox) URL. Go to the transactions list view

![](/img/providers/pagseguro_checkout_03.png)

Select your payment

![](/img/providers/pagseguro_checkout_04.png)

and approve, cancel or decline it

![](/img/providers/pagseguro_checkout_05.png)

After it is done, PaymentIQ will receive a notification and will update a corresponding transaction.

### PIX

First of all you will need to have a webhook configured (see above how to do it).

Please use a Bank deposit transaction type to initiate a PIX payment. Also you will need to provide a `nationalId` (CPF or CNPJ) in the payment initiate request.

PaymentIQ Cashier example:

![](/img/providers/pagseguro_pix_01.png)

Once you initiated payment and pressed a pay button, you will be redirected to the QR code page

![](/img/providers/pagseguro_pix_02.png)

Then you will need to scan that QR code in order to proceed with payment.

To complete payment on SANDBOX environment you will have to trigger a PIX transaction to be PAID (you will just need to send a POST request like is described below).

Once payment is completed, PaymentIQ will receive a notification and update a corresponding transaction.  

#### How to trigger a PIX tx to be PAID?

Please execute this cURL:

```
curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "Authorization:Bearer {token}" \
   -d \
'{
    "status": "PAID",
    "tx_id": "{txId}"
}' \
 'https://sandbox.api.pagseguro.com/pix/pay/{txId}'
```

**Notes:**

1). {token} can be found in the PagSeguro BO: `PERFIS DE INTEGRAÇÃO > Vendedor > Credenciais e.g. Seu token: 29A156601899408284CDE843135E9DA1` \
2). {txId} it is the same id that was used in the PIX "charge" request e.g. `PIX000...000{piqTxRefId}` (26 symbols).
