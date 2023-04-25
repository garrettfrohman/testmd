--- 
id: "ppro" 
title: "PPRO"
hide_title: "true"
---
 
![](/img/providers/logos/ppro.png)

# PPRO

## About
The PPRO Group delivers end-to-end financial solutions enabling international electronic payment processes.

Please note that a local license is required for Giropay and Multibanco via PPRO.

| Provider Name                | PPRO                                                                                                                                                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.ppro.com](https://www.ppro.com)                                                                                                                                                      |
| Classification               | Aggregator                                                                                                                                                                                        |
| Regions                      | `International`                                                                                                                                                                                   |
| Currencies                   | `Multiple*`                                                                                                                                                                                       |
| Methods/PaymentTxTypes       | `PProDeposit`<br/> `BankIBANWithdrawal`<br/> `BankLocalWithdrawal`<br/> `QiwiDeposit`<br/> `QiwiWithdrawal`<br/> `PugglePayDeposit`<br/> `OxxoDeposit`<br/> `BoletoBancarioDeposit`<br/> `Refund` |
| PaymentIQ Configuration File | `PPROConfig`                                                                                                                                                                                      |

\*Note: International Pay-out works for currency EUR and all country codes except AF, AL, AO, DZ, EC, GY, ID, IQ, IR, KH, KP, KW, LA, MM, NA, NI, PA, PG, PK, SD, SY, UG, YE, ZW

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ppro.PProConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>??</merchantId> <!-- Login  -->
        <password>??</password>  <!--  Password  -->
        <accountID>??</accountID> <!-- ContractID  -->
        <secretKey>??</secretKey>  <!--  Shared Secret   -->
        <notificationSecret>??</notificationSecret>  <!--  Notification Secret  --> 
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
        <redirectUrl>${baseRedirectUrl}/api/ppro/deposit/redirect/${ptx.txRefId}</redirectUrl>
        <!-- use this tag especially in the case of QiwiDeposit that has currency requirements
        <supportedCurrencies>EUR|USD|SEK|RUB</supportedCurrencies>
        -->
     </account>     
    </entry>
  </accounts>
  <notificationUrl>${baseCallbackUrl}/api/ppro/deposit/callback/${ptx.txRefId}</notificationUrl>
  <services>
    <entry><string>EPS</string><string>eps</string></entry>
    <entry><string>GIROPAY</string><string>giropay</string></entry>
    <entry><string>IDEAL</string><string>ideal</string></entry>
    <entry><string>P24</string><string>p24</string></entry>
    <entry><string>SOFORT</string><string>directpay</string></entry>
    <entry><string>SEPAPAYOUT</string><string>sepapayout</string></entry>
    <entry><string>ASTROPAYCARD</string><string>astropaycard</string></entry>
    <entry><string>ASTROPAYDIRECT</string><string>astropaydirect</string></entry>
    <entry><string>MISTERCASH</string><string>bcmc</string></entry>
    <entry><string>BOLETO</string><string></string>boleto</entry>
    <entry><string>OXXO</string><string>oxxo</string></entry>
    <entry><string>PAYSAFECARD</string><string>paysafecard</string></entry>
    <entry><string>POLI</string><string>poli</string></entry>
    <entry><string>POSTFINANCE</string><string>yellowpay</string></entry>
    <entry><string>PUGGLEPAY</string><string>pugglepay</string></entry>
    <entry><string>QIWI</string><string>qiwi</string></entry>
    <entry><string>SAFETYPAY</string><string>safetypay</string></entry>
    <entry><string>SEPADIRECTDEBIT</string><string>sepadirectdebit</string></entry>
    <entry><string>SKRILL</string><string>skrill</string></entry>
    <entry><string>TELEINGRESO</string><string>teleingreso</string></entry>
    <entry><string>TRUSTLY</string><string>trustly</string></entry>
    <entry><string>TRUSTPAY</string><string>trustpay</string></entry>
    <entry><string>VERKKOPANKKI</string><string>verkkopankki</string></entry>
    <entry><string>PAYU</string><string>payu</string></entry>
  </services>
  
  <liveServiceEndPoint>https://api.girogate.de</liveServiceEndPoint>
  
</com.devcode.paymentiq.integration.ppro.PProConfig>
```

</details>

### Attributes

| Attribute          | Description                                                          |
|--------------------|----------------------------------------------------------------------|
| merchantId         | Corresponds to the `login` value from PPro                           |
| accountID          | Corresponds to the `contractid` value from PPro                      |
| password           | Corresponds to the `password` value from PPro                        |
| secretKey          | The "Shared Secret" value for validating check sum                   |
| notificationSecret | The "Notification Secret" value for validating check sum             |
| consumerRef        | USERID (default) or TXID. Decides which field is sent as consumerref |

### Note
Inside the PProConfig, it is necessary to create additional account configurations to handle certain APM's such as SOFORT, IDEAL and GIROPAY. These APM's only support window as a container in the redirection, as opposed to the standard iframe container.

Setting the following tag inside the account will make sure it opens in a new window: `<container>window</container>`.

### Payment Method Routing PPRO in PaymentIQ
Using `Rules →  Payment Method` will set rules determining which user group will access a certain PPro APM (e.g SOFORT) that will be displayed. The condition will act as filters and the added payment methods (e.g PPRO-SOFORT, PPRO-GIROPAY) will be displayed. In order to add the specific payment methods in the rules, the below mapping entry needs to be added into the MerchantConfig with the wanted PPro services. Please contact the technical support team for assistance.

```xml
<serviceMapping>
    <entry>
        <string>PPRO</string>
        <string>BANCOMER|CARULLA|EFECTY|EMPRESADEENERGIA|SURTIMAX|BANAMEX|WEBPAY|ITAU|BRADESCO|PAYU|ASTROPAYCARD|ASTROPAYDIRECT|MISTERCASH|BOLETO|EPS|GIROPAY|IDEAL|OXXO|P24|PAYSAFECARD|POLI|POSTFINANCE|PUGGLEPAY|QIWI|SAFETYPAY|SEPADIRECTDEBIT|SKRILL|SOFORT|TELEINGRESO|TRUSTLY|TRUSTPAY|VERKKOPANKKI</string>
    </entry>
</serviceMapping>
```

## Example Routing Rule
![](/img/providers/routing/ppro.png)

## Available Services (APM's)

When using the PPro deposit transaction type, the service parameter in the table below is the value that should be sent in the `service` parameter to decide the specific APM to be used.

The tags represent what PIQ will send to PPro and is nothing that the merchant needs to worry about, but can be good to know to which APM they relate to. Where the test tag is called `dumbdummy` the APM does not have it's own test simulation and uses PPro's standard simulation.

| Service parameter | Live tag         | Test tag         |
|-------------------|------------------|------------------|
| ASTROPAYCARD      | astropaycard     | astropaycard     |
| ASTROPAYDIRECT    | astropaydirect   | astropaydirect   |
| BANAMEX           | banamex          | banamex          |
| BANCOMER          | bancomer         | bancomer         |
| BOLETO            | boleto           | boleto           |
| BRADESCO          | bradesco         | bradesco         |
| CARULLA           | carulla          | carulla          |
| EFECTY            | efecty           | efecty           |
| EMPRESADEENERGIA  | empresedeenergia | empresedeenergia |
| EPS               | eps              | eps              |
| GIROPAY           | giropay          | giropay          |
| IDEAL             | ideal            | ideal            |
| INSTANT_TRANSFER  | instanttransfer  | instanttransfer  |
| ITAU              | itau             | itau             |
| MISTERCASH        | bcmc             | bcmc             |
| MYBANK            | mybank           | mybank           |
| OXXO              | oxxo             | dumbdummy        |
| P24               | p24              | p24              |
| PAYU              | payu             | payu             |
| PAYSAFECARD       | paysafecard      | paysafecard      |
| POLI              | poli             | poli             |
| POSTFINANCE       | yellowpay        | yellowpay        |
| PUGGLEPAY         | pugglepay        | pugglepay        |
| ZIMPLER           | pugglepay        | pugglepay        |
| QIWI              | qiwi             | qiwi             |
| QIWI_PAYOUT       | qiwipayout       | qiwipayout       |
| SAFETYPAY         | safetypay        | safetypay        |
| SEPADIRECTDEBIT   | sepadirectdebit  | sepadirectdebit  |
| SKRILL            | skrill           | skrill           |
| SOFORT            | directpay        | directpay        |
| TELEINGRESO       | teleingreso      | dumbdummy        |
| TRUSTLY           | trustly          | trustly          |
| TRUSTPAY          | trustpay         | trustpay         |
| VERKKOPANKKI      | verkkopankki     | verkkopankki     |
| WEBPAY            | webpay           | webpay           |
| SEPAPAYOUT        | sepapayout       | sepapayout       |
| SURTIMAX          | surtimax         | surtimax         |
| MULTIBANCO        | multibanco       | multibanco       |
| BLIK              | blik             | blik             |
| PAYBYBANKAPP      | pbba             | pbba             |

#### Additional notes about specific APMs

* **PAYBYBANKAPP (PbBa)** - An "App to app URL" can be set if the merchant wants to redirect the consumer back to the app which invoked the payment. Added by setting `<appToAppURL>wanted URL</appToAppURL>` in the root level of the PProConfig.

## Test Information
Optional mock user: PPRO

If the specific APM is not present here, there is no specific data required.

| APM               | Test Information                                                                                                                                                                                                          |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Giropay           | BIC: TESTDETT421                                                                                                                                                                                                          |
| Sofort            | **Germany**: First Screen, Bank Name 8888888, Login data: any data, Account: choose one from the list, Tan: 12345 **Belgium**: First Screen bank name: 999, Rest same as Germany **Other**: First Screen bank name: 00000 |
| SEPA Direct debit | Iban: DE12500105170648489890                                                                                                                                                                                              |
| Trustly           | All credentials will be provided during the payment flow.                                                                                                                                                                 |
| SEPA Payout       | IBAN: DE12500105170648489890                                                                                                                                                                                              |
| Instant Transfer  | **Germany**: First Screen, Bank Name 8888888, Login data: any data, Account: choose one from the list, Tan: 12345                                                                                                         |
| Astropaycard      | See [1]                                                                                                                                                                                                                   |

#### [1] AstropayCard test credentials

The following test cards are available in AstropayCard’s Sandbox environment.

| Card number      | CVV  | Expiration | Value | Currency |
|------------------|------|------------|-------|----------|
| 1612708538608684 | 9500 | 09-2018    | 1000  | BRL      |
| 1613595184682272 | 5058 | 04-2017    | 100   | BRL      |
| 1615596647857871 | 3825 | 09-2018    | 1000  | RMB      |
| 1615394714822089 | 7293 | 04-2017    | 100   | RMB      |
| 1614738335984192 | 5111 | 09-2018    | 1000  | TRY      |
| 1614579797475083 | 3897 | 04-2017    | 1000  | TRY      |
| 1616189190064902 | 8625 | 09-2018    | 1000  | USD      |
| 1616310185676837 | 7143 | 04-2017    | 25    | USD      |
