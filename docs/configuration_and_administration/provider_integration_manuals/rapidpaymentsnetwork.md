--- 
id: "rapidpaymentsnetwork" 
title: "Rapid Payments Network"
hide_title: "true"
---
 
![](/img/providers/logos/rapidpaymentnetwork.png)

# Rapid Payments Network

## About
RPN is a Payment Solution Providers that has the ability to process China UnionPay (CUP) Debit Card Payments.

| Provider Name                | Rapid Payments Network                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://www.rpnpay.com/](http://www.rpnpay.com/)                                |
| Classification               | Online Banking                                                                  |
| Regions                      | `China`                                                                         |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `ChinaUnionPayDeposit`<br/> `ChinaUnionPayWithdrawal`                           |
| PaymentIQ Configuration File | `RapidPaymentsNetworkConfig`                                                    |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.rapidpaymentsnetwork.RapidPaymentsNetworkConfig>
 <enabled>true</enabled>
 
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <secretKey>??</secretKey>
        <use3Dsecure>false</use3Dsecure>
        <version>1.0</version>
        <merchantId>??</merchantId>
        <supportedCurrencies>JPY</supportedCurrencies>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
 </accounts>

  <chinaUnionPayService>
    <entry><string>1</string><string>ICBC</string></entry>
    <entry><string>2</string><string>ABC China</string></entry>
    <entry><string>3</string><string>Bank Of China</string></entry>
    <entry><string>4</string><string>China Construction Bank</string></entry>
    <entry><string>5</string><string>Bank of Communications</string></entry>
    <entry><string>6</string><string>China Everbright Bank</string></entry>
    <entry><string>7</string><string>SPD Bank</string></entry>
    <entry><string>8</string><string>Bank of Beijing</string></entry>
    <entry><string>9</string><string>CGB china</string></entry>
    <entry><string>10</string><string>Ping An bank</string></entry>
    <entry><string>11</string><string>Industrial Bank</string></entry>
    <entry><string>12</string><string>CMB China</string></entry>
    <entry><string>13</string><string>Shenzhen Development Bank</string></entry>
    <entry><string>14</string><string>POSTAL SAVINGS BANK OF CHINA</string></entry>
    <entry><string>15</string><string>HUAXIA BANK</string></entry>
    <entry><string>16</string><string>China Minsheng Banking</string></entry>
  </chinaUnionPayService>
 
</com.devcode.paymentiq.integration.rapidpaymentsnetwork.RapidPaymentsNetworkConfig>
```

</details>

### Attributes

| Attribute    | Description                                |
|--------------|--------------------------------------------|
| username     | Provided by Rapid Payments                 |
| password     | Provided by Rapid Payments                 |
| merchantId   | Merchant ID, (Provided by Rapid Payments)  |
| secretKey    | Merchant  Key (Provided by Rapid Payments) |
| merchantName | Provided by Rapid Payments                 |
| useWeChat    | Set to true to use WeChat                  |

### Bank ID

| Bank Id | Bank Code | Bank Name (English)                     |
|---------|-----------|-----------------------------------------|
| 1       | ICBC      | INDUSTRIAL AND COMMERCIAL BANK OF CHINA |
| 2       | ABOC      | AGRICULTURE BANK OF   CHINA             |
| 3       | BOC       | BANK OF CHINA                           |
| 4       | CCB       | CHINA CONSTUCTION   BANK                |
| 5       | BOCM      | BANK OF   COMMUNICATIONS                |
| 6       | CEB       | CHIAN EVERBRIGHT   BANK                 |
| 7       | SPDB      | Shanghai Pudong   Development Bank      |
| 8       | BOB       | Bank Of Beijing                         |
| 9       | CGB       | Guangdong   Development Bank            |
| 10      | PAB       | Ping An Bank                            |
| 11      | CIB       | China Industrial   Bank                 |
| 12      | CMB       | China Merchants Bank                    |
| 13      | SDB       | Shenzhen Development   Bank             |
| 14      | PSBC      | Postal Savings Bank Of China            |
| 15      | HXB       | Huaxia Bank                             |
| 16      | CMSB      | China Minsheng Bank                     |
| 17      | CITIC     | CITIC                                   |

## Example Routing Rule
- 

## Test Information

No test information is available for non WeChat transactions.

### WeChat
1. Initiate RPN payment (with WeChat enabled) in WebBrowser. Web Page with QR code will be loaded

![](/img/providers/rapidpaymentsnetwork01.png)

2. Open WeChat application in your mobile device and scan QR code

![](/img/providers/rapidpaymentsnetwork02.png)

3. After code has been scanned additional dialog containing "Pay Now" button will be loaded. Click “Pay Now” to get another page where credit card number should be entered.


![](/img/providers/rapidpaymentsnetwork03.png)