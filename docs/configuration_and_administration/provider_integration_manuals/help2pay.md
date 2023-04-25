--- 
id: "help2pay" 
title: "Help2Pay"
hide_title: "true"
---
 
![](/img/providers/logos/help2pay.png)

# Help2Pay

## About
Help2Pay is a banking provider offering Deposits and Withdrawals.

| Provider Name                | Help2Pay                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://help2pay.com/](https://help2pay.com/)                                  |
| Classification               | Online Banking                                                                  |
| Regions                      | `Vietnam`, `Malaysia`, `Indonesia`,`Thailand`                                   |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `BankDeposit` <br/> `BankDomesticWithdrawal`                                    |
| PaymentIQ Configuration File | `Help2PayConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.help2pay.Help2PayConfig>
  <enabled>true</enabled>
  <height>700</height>
  <width>1100</width>
  <container>window</container>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <supportedCurrencies>MYR|THB|VND|IDR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <liveServiceEndPoint>https://api.safepaymentapp.com/MerchantTransfer</liveServiceEndPoint>
  <liveWithdrawalServiceEndpoint>????</liveWithdrawalServiceEndpoint> <!-- Individually assigned per merchant -->
  <liveStatusServiceEndpoint>https://query.safepaymentapp.com</liveStatusServiceEndpoint>
</com.devcode.paymentiq.integration.help2pay.Help2PayConfig>
```
</details>

### Attributes

| PaymentIQ Configuration | Description                        |
|-------------------------|------------------------------------|
| merchantId              | Merchant ID. Provided by Help2Pay. |
| secretKey               | Secret Key. Provided by Help2Pay.  |

### Provider Configuration
To use withdrawals, Help2Pay must [whitelist](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist) the IP address which will make the requests and register a payout verification URL. The payout verification URL should be:
`${baseCallbackUrl}/api/help2pay/withdrawal/verify`

Help2Pay also provides specific withdrawal URLs for merchants, to set this specific URL you can add `<liveWithdrawalServiceEndpoint>` for production and `testWithdrawalServiceEndpoint` for the test environment.

### Deposit Bank Codes

| Currency | Bank Code | Bank Name                                      |
|----------|-----------|------------------------------------------------|
| MYR      | MBB       | Maybank Berhad                                 |
| MYR      | PBB       | Public Bank Berhad                             |
| MYR      | CIMB      | CIMB Bank Berhad                               |
| MYR      | HLB       | Hong Leong Bank Berhad                         |
| MYR      | RHB       | RHB Banking Group                              |
| MYR      | AMB       | AmBank Group                                   |
| MYR      | BIMB      | Bank Islam Malaysia                            |
| THB      | KKR       | Karsikorn Bank (K-Bank)                        |
| THB      | BBL       | Bangkok Bank                                   |
| THB      | SCB       | Siam Commercial Bank                           |
| THB      | KTB       | Krung Thai Bank                                |
| THB      | BOA       | Bank of Ayudhya (Krungsri)                     |
| THB      | GSB       | Government Savings Bank                        |
| THB      | PPTP      | Promptpay                                      |
| THB      | TMB       | TMB Bank Public Company Limited                |
| THB      | CIMBT     | CIMB Thai                                      |
| THB      | KNK       | Kiatnakin Bank                                 |
| VND      | TCB       | Techcombank                                    |
| VND      | SACOM     | Sacombank                                      |
| VND      | VCB       | Vietcombank                                    |
| VND      | ACB       | Asia Commercial Bank                           |
| VND      | DAB       | DongA Bank                                     |
| VND      | VTB       | Vietinbank                                     |
| VND      | BIDV      | Bank for Investment and Development of Vietnam |
| VND      | EXIM      | Eximbank Vietnam                               |
| IDR      | BCA       | Bank Central Asia                              |
| IDR      | BNI       | Bank Negara Indonesia                          |
| IDR      | BRI       | Bank Rakyat Indonesia                          |
| IDR      | MDR       | Mandiri Bank                                   |
| IDR      | CIMBN     | CIMB Niaga                                     |
| PHP      | BDO       | Banco de Oro                                   |
| PHP      | MTB       | MetroBank                                      |

## Example Routing Rule
![](/img/providers/routing/help2pay.png)

## Test Information

| Username | Password |
|----------|----------|
| tester79 | qwe23dsa |

Demo bank account are applicable to all bank except for DAB, BIDV, BCA, MDR, BNI.
