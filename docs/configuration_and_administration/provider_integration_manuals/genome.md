--- 
id: "genome" 
title: "Genome"
hide_title: "true"
---
 
![](/img/providers/logos/genome.png)

# Genome

## About
Genome is a financial ecosystem for real-time payment processing.

PaymentIQ support 4 Genome flows:
1. SEPA payouts (`GenomeBankIBANWithdrawal`) allows possibility to withdraw funds from Genome account.
2. H2H: Host to host API (`CreditcardDeposit`, `Refund`, `Void`, `Capture`). Full card integration with 2D and 3DS flows and authorization options.
3. HPP: Hosted payment pages (`WebRedirectDeposit`, `Refund`). Allows possibility to deposit account using Genome Payment form.  
4. Credit card withdrawals (`CreditcardWithdrawal`) allows possibility to withdraw funds from Genome account.  

| Provider Name                | Genome                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://genome.eu/](https://genome.eu/)                                                                                                           |
| Classification               | Wallet                                                                                                                                             |
| Regions                      | `International`                                                                                                                                    |
| Currencies                   | `EUR`, `USD`, `GBP`                                                                                                                                |
| Methods/PaymentTxTypes       | `GenomeBankIBANWithdrawal`<br/> `WebRedirectDeposit`<br/> `CreditcardDeposit`<br/> `Refund`<br/> `Void`<br/> `Capture`<br/> `CreditcardWithdrawal` |
| PaymentIQ Configuration File | `GenomeConfig`                                                                                                                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.genome.GenomeConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>SEPA</string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <username>???</username>
        <password>???</password>
        <secretKey>???</secretKey>
      </account>
    </entry>
    <entry>
      <string>OCT</string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <useTokenId>???</useTokenId>
        <username>???</username>
        <password>???</password>
        <secretKey>???</secretKey>
      </account>
    </entry>
    <entry>
      <string>H2H</string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <useTokenId>true</useTokenId>
        <username>???</username>
        <password>???</password>
        <secretKey>???</secretKey>
      </account>
    </entry>
    <entry>
      <string>HPP</string>
      <account>
        <productName>name_to_display</productName>
        <supportedCurrencies>EUR</supportedCurrencies>
        <secretKey>???</secretKey>
        <pspPublicKey>???</pspPublicKey>
        <refundSecretKey>???</refundSecretKey>
        <container>window</container>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.genome.GenomeConfig>
```

</details>

### Attributes

| Attribute            | Description                                                                                                                                                                                |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username             | merchant account(Provided by Genome)                                                                                                                                                       |
| password             | merchant password(Provided by Genome)                                                                                                                                                      |
| secretKey(SEPA, H2H) | secret key(Provided by Genome). Used for callback signature validation. If blank - signature validation will be skipped                                                                    |
| useTokenId           | boolean that allows payment by token for stored user accounts. When set to ```true``` value could be that in case successful 3DS payment next payment will be by token without 3DS actions |
| productName          | name of product that will be displayed on payment form. If blank - defaults to transaction ID                                                                                              |
| secretKey(HPP)       | secret key(Genome Merchant Portal: ```Payment Pages>Payment Page>General```). See below detailed ```HPP setup``` instruction                                                               |
| pspPublicKey         | public key(Genome Merchant Portal: ```Payment Pages>Payment Page>General```). See below detailed ```HPP setup``` instruction                                                               |
| refundSecretKey      | secret key for refunds (Genome Merchant Portal: ```Payment Pages>Payment Forms>Edit (Embed Code section)```). See below detailed ```HPP setup``` instruction                               |
| transactionLength    | period after transaction will be settled on Genome side. Applyible for HPP Authorization API. Value is in ```Days```. Defaults to 1. More info under ```HPP setup``` instruction           |
| pspServiceMapping    | contains psp service mapping, values are provided by Genome                                                                                                                                |


## Example Routing Rule
### SEPA
![](/img/providers/routing/genome.png)

### H2H
![](/img/providers/routing/genome_h2h.png)

### HPP
![](/img/providers/routing/genome_hpp.png)

## HPP setup
Note: HPP works with```<container>window</container>```. 
1. To use HPP merchants have to be registered on Genome Merchant portal https://merchant.genome.eu/.
2. Navigate to Payment pages section and create new instance
3. Under Settings populate all required fields. Important: Callback URLs should be ```${baseCallbackUrl}/api/genome/hpp/callback```, redirect URL's ```${baseRedirectUrl}/api/genome/redirect```
4. On this page will be generated public and secret keys that have to be populated as ```pspPublicKey``` and ```secretKey```in accordance.
5. Navigate to Payment forms and create a new one. Here you can configure view of Payment form
6. Under ```EMBED CODE``` section you will find signature that has to be set as ```refundSecretKey```

Note: HPP uses custom product API (product name can be configured using ```productName```) with possibility to enable Authorization API by ```authType``` property .
Due to limitations (not possible to get updates from Genome side about next SETTLE/VOID actions) Authorization API allows only SETTLE that will happen after ```transactionLength```.
In case of success transaction using Authorization API PIQ will consider transaction as successful and finalized. Genome is responsible for transaction ```SETTLE``` after ```transactionLength```
Refunds, using Authorization API, will be possible only from Genome Merchant portal as PIQ won't have info about settled transaction ID.

## APMs via HPP
Genome supports various APMs via HPP. Full list can be found on https://genome.eu/docs/#alternative-methods-list. <br/>
If merchants want to request HPP, calling particular APM, ```pspServiceMapping``` should be configured in PaymentIQ using psp services as shown bellow.

<details>
<summary>Click to view example configuration</summary>
<br/>

```
<com.devcode.paymentiq.integration.genome.GenomeConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <pspServiceMapping>
    <entry>
      <string>???</string><!--PIQ_SERVICE-->
      <string>???</string><!--GENOME_SERVICE-->
  </entry>
  </pspServiceMapping>
  <accounts>
   ....
  </accounts>
</com.devcode.paymentiq.integration.genome.GenomeConfig>
```
</details>

Without specifying of service all available payment options will be shown on HPP page. <br/>
In Payment IQ, by default, are configured ```IDEAL``` and ```SOFORT``` in Genome integration. These payment methods can be used without ```pspServiceMapping``` configuration. 

###Step by step instructions how to add APMs via HPP
1. Merchant decides to use particular method that is supported by HPP from the list https://genome.eu/docs/#alternative-methods-list, for ex. ```Latvian Banks```
2. Merchant contacts Genome to configure it or configures this APM for HPP in Genome's portal https://merchant.genome.eu/. Also, at this stage, merchant will get expected by Genome name that should be used during request. For ex. ```Latvian Banks Genome```
3. Now merchant can configure PaymentIQ to support this method by adding ```serviceMapping``` entry to ```MerchantConfig```
```xml
  <serviceMapping>
    <entry>
      <string>WEBREDIRECT</string>
      <string>BANKS_OF_LATVIA</string>
    </entry>
  </serviceMapping>
```
4. Configure ```pspServiceMapping``` mapping in ```GenomeConfig```
```xml
  <pspServiceMapping>
    <entry>
        <string>BANKS_OF_LATVIA</string>
        <string>Latvian Banks Genome</string>
    </entry>
  </pspServiceMapping>
```
5. And add according payment method rule
   ![](/img/providers/routing/genome_hpp_apm_pm.png)
  
6. If merchants already use HPP and APM was added to existing setup on Genome's side, then no need to change anything in existing routing. Otherwise, merchants can add extra routing taking into account ```PSP service```
   ![](/img/providers/routing/genome_hpp_apm.png)

## Test Information

SEPA payout doesn't have test environment

Test cards for HPP and H2H

| Card Brand | Supporting Flow | Card number      | CVV                   | Expiry Date                                 |
|------------|-----------------|------------------|-----------------------|---------------------------------------------|
| Visa       | 2D              | 4111111111111111 | 123 [3 digits random] | MM - [from 01 to 12]; YYYY- 2020 or greater |
| Mastercard | 2D              | 5555555555554444 | 123 [3 digits random] | MM - [from 01 to 12]; YYYY- 2020 or greater |
| Visa       | 3D              | 4012000300001003 | 123 [3 digits random] | MM - [from 01 to 12]; YYYY- 2020 or greater |
| Mastercard | 3D              | 5191330000004415 | 123 [3 digits random] | MM - [from 01 to 12]; YYYY- 2020 or greater |