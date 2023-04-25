---
id: "lps"
title: "LPS"
hide_title: "true"
---

![](/img/providers/logos/lps.png)

# LPS

## About
LPS is a payment provider offering credit card (deposit, refund and withdrawal) and bank (withdrawal) payment options and status check.

| Provider Name                | LPS                                                                                                            |
|------------------------------|----------------------------------------------------------------------------------------------------------------|
| Link                         | [http://www.lateralpaymentsolutions.com/](http://www.lateralpaymentsolutions.com/)                             |
| Classification               | Debit/Credit Card Processor, Online Banking                                                                    |
| Supported Countries          | International                                                                                                  |
| Currencies                   | `AUD`, `USD`, `SEK`, `EUR`                                                                                     |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`Refund`<br/>`CreditcardWithdrawal`<br/>`BankIBANWithdrawal`<br/>`BankLocalWithdrawal` |
| PaymentIQ Configuration File | `LPSConfig`                                                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.lps.LPSConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>false</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <password>??</password>
        <use3Dsecure>true</use3Dsecure>
        <secretKey>??</secretKey>
        <supportedCurrencies>EUR|USD|SEK|AUD</supportedCurrencies>
        <terminalEndpoint>??</terminalEndpoint><!-- our redirect url identifier-->
        <threedsTemplateName>LPS_3DS_Redirect_template</threedsTemplateName>
        <useTokenId>true</useTokenId>
        <authType>FINAL_AUTH</authType><!--AUTH_CAPTURE-->
      </account>
    </entry>
    <entry>
      <string>withdrawal</string>
      <account>
        <defaultDescriptor>operation description goes here...</defaultDescriptor>
        <merchantId>??</merchantId>
        <password>??</password>
        <secretKey>??</secretKey>
        <supportedCurrencies>EUR|USD|SEK|AUD</supportedCurrencies>
        <terminalEndpoint>??</terminalEndpoint><!-- our redirect url identifier-->
        <waitForCallback>true</waitForCallback>
      </account>
    </entry>
  </accounts>
  <notificationIPs>xx.xx.xx.xx|xxx.xxx.xxx.xxx</notificationIPs>
  <notificationSecret>??</notificationSecret>
  <pspTermUrl>??</pspTermUrl>
</com.devcode.paymentiq.integration.lps.LPSConfig>
```
</details>

### Attributes

| Attribute                | Description                                                                                                                                                                                                                                                                                                               |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId       | Corresponds to the `Account` value from LPS used in the requests                                                                                                                                                                                                                                                          |
| account.useTokenId       | Corresponds to the `scsscheck` used in both deposit and withdrawal request. `scsscheck` is a flag to indicate if the transaction will be part of SCSS and it automatically stores the card details and a corresponding token is returned on the response to be used instead of card information in recurring transaction. |
| account.secretKey        | Corresponds to the `pwd` value from LPS for both withdrawal and refund requests                                                                                                                                                                                                                                           |
| account.terminalEndpoint | The redirect URL identifier provided by LPS                                                                                                                                                                                                                                                                               |
| account.waitForCallback  | It is used to identify (if set to `true`) if bank withdrawal confirmation/reversal flow should be triggered. By default (if this property is set to `false` or missing), withdrawal will be declined/approved immediately and all notifications will be skipped. Required for bank withdrawals only.                      |
| validCallbackIpAddresses | It is used to whitelist IPs where notifications will be sent from. Default IP is whitelisted already and all new IPs must be provided by the provider. Required for bank withdrawals only.                                                                                                                                |
| notificationSecret       | It is used to set a notification secret in order to validate during notification processing. It must be configured by the PaymentIQ technical support and sent to the provider. Required for bank withdrawals only.<br/>Please see below how to generate it.                                                              |
| pspTermUrl               | It is used to specify "Term URL" for 3DS payment.                                                                                                                                                                                                                                                                         |

### Note

When creating the account with LPS, be sure to provide the correct URL as the "Back to Merchant URL". For production the correct URL is `https://api.paymentiq.io/paymentiq/api/lps/redirect`.

### Bank Withdrawals

In order to configure bank withdrawals, please follow these steps:

1. Enable **BANKIBAN-WIRES** withdrawal method in **Rules -> Payment methods**.
2. Additional configuration has to be added in TxTypeInput config file. Please contact PaymentIQ tech support to configure that for you.
3. This method utilizes bank mapping table in **Admin -> Bank Mapping** therefore every bank that you intend to use with
   this method has to have a corresponding entry in that table with its details included (swift, bank name etc.)
   Please contact PaymentIQ's tech support to add your bank mappings to the table.

In order to enable bank withdrawal confirmation/reversal flow, please follow these steps:

1. Set `<waitForCallback>true</waitForCallback>` for your account.
2. Generate and set `<notificationSecret>??</notificationSecret>` at config level (not account level).
3. Send a correct notification URL to the provider.
4. Make sure notification IP is whitelisted (please check valid IP(s) with provider and specify in the config using `<validCallbackIpAddresses>..</validCallbackIpAddresses>` if needed).

### Notification Secret

1. Please generate a random UUID e.g. using `uuidgen` from terminal or any other online generator: `UUID = FF84E15C-3485-4223-A915-01F8A79ABE23`;
2. Please take a `secretKey` from your "withdrawal" account config and create a string: `"{secretKey}_{UUID}"`
3. Encode in Base64 using terminal command:
```
echo -n '{secretKey}_{UUID}' | base64
```
As a result you will have: `RWtybUI5bUNDeGhoTjZfRkY4NEUxNUMtMzQ4NS00MjIzLUE5MTUtMDFGOEE3OUFCRTIz`. Please use it as a `notificationSecret` and send it to provider.

### Callback URL

If you have `<waitForCallback>true</waitForCallback>` in your config, you will need to ask provider to configure a merchant specific notification URL:<br/>

TEST: https://test-api.paymentiq.io/paymentiq/api/lps/callback/{piqMid}/batch<br/>
PROD: https://api.paymentiq.io/paymentiq/api/lps/callback/{piqMid}/batch,<br/>

where `piqMid` - is a merchant ID in PaymentIQ back office.

## Example Routing Rule

![](/img/providers/routing/lps.png)

## Test Information

### 3DS/N3DS

| Card Brand | Account          | CVV | Expiry date     | Response type |
|------------|------------------|-----|-----------------|---------------|
| VISA       | 4000000000000002 | Any | Any future date | Approved      |
| MASTERCARD | 5200000000000007 | Any | Any future date | Decline       |

### BankLocalWithdrawal Information

Users should set the BSB code in clearing number input field when making BankLocalWithdrawal transaction in cashier.
