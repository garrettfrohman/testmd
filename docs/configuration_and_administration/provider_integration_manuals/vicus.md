--- 
id: "vicus" 
title: "Vicus"
hide_title: "true"
---
 
![](/img/providers/logos/vicus.png)

# Vicus

## About
Vicus is a payment provider offering bank deposit and withdrawal operations.

| Provider Name                | Vicus                                                              |
|------------------------------|--------------------------------------------------------------------|
| Link                         | [https://www.vicussolutions.com/](https://www.vicussolutions.com/) |
| Classification               | Online/Manual Banking                                              |
| Regions                      | `Indonesia`, `Thailand`, `Vietnam`,                                |
| Currencies                   | `IDR`, `THB`, `VND`                                                |
| Methods/PaymentTxTypes       | `BankDeposit`<br/> `BankLocalWithdrawal`<br/> `Reversal`           |
| PaymentIQ Configuration File | `VicusConfig`                                                      |

## Availability
Indonesia: Online Banking deposit and Virtual Account ATM\
Thailand: Online Banking deposit/withdrawal and QR code deposit\
Vietnam: Online Banking deposit/withdrawal

## Limits
`IDR`\
Min amount: 300000 IDR; Max amount: 100000000 IDR;

`THB`\
Withdrawal: Min amount: 500 THB;\
QR code deposit: Min amount: 100 THB; Max amount: 200000 THB;

`VND`\
Deposit: Min amount: 100000 VND; Max amount: 300000000 VND;\
Withdrawal: Min amount: 100000 VND; Max amount: 100000000 VND;

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.vicus.VicusConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>IDR</string>
      <account>
        <username>??</username>
        <password>??</password>
        <serviceEndpoint>https://idrpays.com/api</serviceEndpoint>
        <accountID>??</accountID>
        <merchantId>??</merchantId>
        <merchantUrl>??</merchantUrl>
        <email>??</email>
        <supportedCurrencies>IDR</supportedCurrencies>
        <apiKey>??</apiKey>
        <service>1</service> <!--4 - Virtual Account; 1 - Online Banking-->
      </account>
    </entry>
    <entry>
      <string>THB</string>
      <account>
        <username>??</username>
        <password>??</password>
        <serviceEndpoint>https://thbpays.com/api</serviceEndpoint>
        <accountID>??</accountID>
        <merchantId>??</merchantId>
        <merchantUrl>??</merchantUrl>
        <email>??</email>
        <supportedCurrencies>THB</supportedCurrencies>
        <apiKey>??</apiKey>
        <service>1</service> <!--1 - Online Banking-->
      </account>
    </entry>
    <entry>
      <string>VND</string>
      <account>
        <username>??</username>
        <password>??</password>
        <serviceEndpoint>https://vndpays.com/api</serviceEndpoint>
        <accountID>??</accountID>
        <merchantId>??</merchantId>
        <merchantUrl>??</merchantUrl>
        <email>??</email>
        <supportedCurrencies>VND</supportedCurrencies>
        <apiKey>??</apiKey>
        <service>1</service> <!--1 - Online Banking-->
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <defaultDescriptor>Bambora payment</defaultDescriptor>
</com.devcode.paymentiq.integration.vicus.VicusConfig>
```

</details>

### Attributes
| Attribute       | Description                                                                                                         |
|-----------------|---------------------------------------------------------------------------------------------------------------------|
| username        | Corresponds to *API_USER_NAME*. Provided by Vicus to make a request                                                 |
| password        | Corresponds to *API_PASSWORD*. Provided by Vicus to make a request                                                  |
| serviceEndpoint | Corresponds to *API URL*. Provided by by Vicus to make a request. It is different for each currency (IDR, THB, VND) |
| accountID       | Corresponds to *Account Name*. Provided by Vicus                                                                    |
| merchantId      | Corresponds to *Merchant ID*. Provided by Vicus                                                                     |
| merchantUrl     | Corresponds to *Website URL*                                                                                        |
| email           | Corresponds to *Business Email*                                                                                     |
| apiKey          | Corresponds to *API Key*. Provided by Vicus                                                                         |
| service         | Corresponds to *Deposit Method* (1 - Online Banking; 4 - Virtual Account)                                           |

## Example Routing Rule
![](/img/providers/routing/vicus.png)

## Test Information

### Virtual Account deposit (Indonesia manual banking deposit)

Please specify amount and select VA PERMATA bank (this bank can only be used for Virtual Account bank payment) as shown below

![](/img/providers/vicus_idr_va_01.png)

After pressing pay button you will be redirected to bank page where you will receive your Bank Code and VA Number:

![](/img/providers/vicus_idr_va_02.png)

In order to complete payment, please go to the Permata bank ATM and deposit there, or some other areas having VA money transfer retail shop:
https://www.domainesia.com/panduan/panduan-virtual-account-permata-bank/

### Online banking deposit (Indonesia)

Please specify amount and select Indonesian bank as shown below

![](/img/providers/vicus_idr_ob_01.png)

After pressing pay button you will be redirected to bank page to complete payment

### Online banking deposit (Thailand)

Please specify amount and select Thailand related bank as shown below

![](/img/providers/vicus_thb_ob_01.png)

After pressing pay button you will be redirected to bank page where you will have to enter login information in order to proceed

![](/img/providers/vicus_thb_ob_02.png)

### QR code deposit (Thailand)

Please specify amount and select Thailand related bank supporting QR code payment (e.g. bank with ID "QR.TH") as shown below

![](/img/providers/vicus_thb_qr_01.png)

After pressing pay button you will be redirected to the page containing payment details and QR code

![](/img/providers/vicus_thb_qr_02.png)

Please scan the QR code in order to make payment

### Online banking deposit (Vietnam)

Please specify amount and select Vietnam related bank as shown below

![](/img/providers/vicus_vnd_ob_01.png)

After pressing pay button you will be redirected to bank page where you will have to enter login information in order to proceed

![](/img/providers/vicus_vnd_ob_02.png)

### Online banking withdrawal (Thailand, Vietnam)

Please specify bank related info like shown below

![](/img/providers/vicus_withdrawal.png)

and press pay button to proceed. Once payment is processed by the bank PaymentIQ will receive a notification from Vicus and will update tx status if required.

## Bank Codes

Please use below "Bank Id" (bank code) as a `service` to make deposit or `bankName` - to make a withdrawal.\
To make **Online Banking** or **Virtual Account** payment you will have to specify "Payment Method Id" as `accountConfig.service`.

### IDR (Deposit)

| No | Bank Id   | Bank Name                       | Payment Method Id | Payment Method  |
|----|-----------|---------------------------------|-------------------|-----------------|
| 1  | VAPERMATA | Virtual Account at Bank Permata | 4                 | Virtual Account |
| 2  | BRI       | Bank Rakyat Indonesia           | 1                 | Online Banking  |
| 3  | BCA       | Bank Central Asia               | 1                 | Online Banking  |
| 4  | BNI       | Bank Negara Indonesia           | 1                 | Online Banking  |
| 5  | BNINEW    | Bank Negara Indonesia M-Secure  | 1                 | Online Banking  |
| 6  | MDR       | Bank Mandiri                    | 1                 | Online Banking  |
| 7  | MDROL     | Bank Mandiri Kupu-Kupu          | 1                 | Online Banking  |

### THB (Deposit & Withdrawal)

| No | Bank Id | Bank Name            | Payment Method Id | Payment Method |
|----|---------|----------------------|-------------------|----------------|
| 1  | QR.TH   | Thai QR Payment      | 1                 | Online Banking |
| 2  | BBL     | Bangkok Bank         | 1                 | Online Banking |
| 3  | KBANK   | Kasikorn Bank        | 1                 | Online Banking |
| 4  | KTB     | Krung Thai Bank      | 1                 | Online Banking |
| 5  | BAY     | Krungsri Bank        | 1                 | Online Banking |
| 6  | SCB     | Siam Commercial Bank | 1                 | Online Banking |
| 7  | TMB     | Thai Military Bank   | 1                 | Online Banking |

### VND (Deposit & Withdrawal)
| No | Bank Id | Bank Name            | Payment Method Id | Payment Method |
|----|---------|----------------------|-------------------|----------------|
| 1  | ACB     | Asia Commercial Bank | 1                 | Online Banking |
| 2  | BIDV    | BIDV Bank            | 1                 | Online Banking |
| 3  | DAB     | DongA Bank           | 1                 | Online Banking |
| 4  | EXIM    | Exim Bank            | 1                 | Online Banking |
| 5  | SCM     | Sacom Bank           | 1                 | Online Banking |
| 6  | TCB     | Techcom Bank         | 1                 | Online Banking |
| 7  | VCB     | Vietcom Bank         | 1                 | Online Banking |
| 8  | VTB     | Vietin Bank          | 1                 | Online Banking |
