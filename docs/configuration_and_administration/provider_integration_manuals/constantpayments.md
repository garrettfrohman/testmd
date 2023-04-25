--- 
id: "constantpayments"
title: "ConstantPayments"
hide_title: "true"
---

![](/img/providers/logos/constantpayments.png)

# ConstantPayments

## About
ConstantPayments is an aggregator provider supporting creditcard deposits, withdrawals, refunds, voids and captures.<br/>
ConstantPayments also supports the following alternative payment methods (APMs):

**Deposit**<br/>
UPI, PayTM, Netbanking, Mobikwok, PayZapp, Jio Money, Freecharge, PhonePe, Ola Money

**Payout**<br/>
Direct Bank Payout (UPI, IMPS)

| Provider Name                | ConstantPayments                                                                                                                                                                                                                   |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://docs.constantpos.com/](https://docs.constantpos.com/)                                                                                                                                                                     |
| Classification               | Aggregator                                                                                                                                                                                                                         |
| Regions                      | `International`                                                                                                                                                                                                                    |
| Currencies                   | `INR`, `USD`, `EUR` and others (please check with ConstantPayments)                                                                                                                                                                |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawal` <br/> `Capture` <br/> `Refund` <br/> `Void` <br/> `WebRedirectDeposit` <br/> `BankDomesticDeposit` <br/> `BankDeposit` <br/> `BankLocalWithdrawal` <br/> `BankDomesticWithdrawal` |
| PaymentIQ Configuration File | `ConstantPaymensConfig`                                                                                                                                                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```
<com.devcode.paymentiq.integration.constantpayments.ConstantPaymentsConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <liveServiceEndPoint>https://gateway.constantpos.com</liveServiceEndPoint>
  <testServiceEndPoint>https://gateway.constantpos.com</testServiceEndPoint>
  <liveApmServiceEndPoint>https://api.constantpos.com</liveApmServiceEndPoint>
  <testApmServiceEndPoint>https://api.constantpos.com</testApmServiceEndPoint>
  <testMode>true</testMode>
  <defaultDescriptor>Test Payment ${ptx.txRefId}</defaultDescriptor><!--Description of the transaction shown to the Customer-->
  <accounts>
    <entry>
      <string>account</string>
      <account>
        <merchantId>??</merchantId>    <!-- shop id     -->
        <merchantSecret>??</merchantSecret>    <!-- Secret key -->
        <pspPublicKey>??</pspPublicKey>  <!-- Public key  -->
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
    <entry>
      <!-- You have to setup default account with gatewayNo if you want to use NetBanking -->
      <string>default</string>
      <account>
        <merchantId>??</merchantId>    <!-- shop id     -->
        <merchantSecret>??</merchantSecret>    <!-- Secret key -->
        <pspPublicKey>??</pspPublicKey>  <!-- Public key  -->
        <gatewayNo>??</gatewayNo>  <! -- Gateway ID -->
        <method>??</method>  <! -- APM Method -->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.constantpayments.ConstantPaymentsConfig>
```
</details>

### Attributes

| Attribute                 | Description                                                                                         |
|---------------------------|-----------------------------------------------------------------------------------------------------|
| account.merchantId        | ShopID provided by ConstantPayments                                                                 |
| account.merchantSecret    | Secret key provided by ConstantPayments                                                             |
| account.pspPublicKey      | Public key provided by ConstantPayments                                                             |
| account.method            | APM System. Available values: paytm, phone_pe, mobikwik, pay_zapp, jio_money, freecharge, ola_money |
| account.gatewayno         | Gateway ID provided by ConstantPayments. Have to use only for NetBanking                            |
| account.defaultDescriptor | Can be used to define a transaction description shown to the customer                               |
| defaultDescriptor         | Can be used to define a transaction description shown to the customer                               |

### Configure APMs in PaymentIQ Back Office

Please make sure ConstantPaymens is enabled in PaymentIQ. It can be done in the **MerchantConfig** by adding "ConstantPaymens" to the `<psps>` section:
```xml
<psps>ConstantPaymens|...</psps>
```

#### Payment Method to Tx Type Mapping
| Payment Method                                                     | Service or Method                                                 | PaymentIQ Tx Type      | Currencies | Method attribute                                                      |
|--------------------------------------------------------------------|-------------------------------------------------------------------|------------------------|------------|-----------------------------------------------------------------------|
| Withdrawal: UPI                                                    | UPI                                                               | BankDomesticWithdrawal | INR        | upi                                                                   |
| Withdrawal: IMPS                                                   | IMPS                                                              | BankLocalWithdrawal    | INR        | imps                                                                  |
| Deposit: UPI                                                       | UPI                                                               | BankDomesticDeposit    | INR        | upi                                                                   |
| Deposit: Net_Banking                                               | NET_BANKING                                                       | BankDeposit            | INR        | net_banking                                                           |
| PayTM, PhonePee, Mobikwik, PayZapp, JioMoney, Freecharge, OlaMoney | PAYTM, PHONEPE, MOBIKWIK, PAYZAPP, JIOMONEY, FREECHARGE, OLAMONEY | WebRedirectDeposit     | INR        | paytm, phone_pe, mobikwik, pay_zapp, jio_money, freecharge, ola_money |

#### UPI Withdrawal

Account attribute:
- method=upi

1). **MerchantConfig**: configure a specific service for `BANKDOMESTIC`:
```xml
<entry>
  <string>BANKDOMESTIC</string>
  <string>UPI|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `BANKDOMESTIC_UPI` as a withdrawal payment option<br/>
3). Create/Update routing rule by specifying `BankDomesticWithdrawal` transaction type.

#### IMPS Withdrawal

Account attribute:
- method=imps

1). **MerchantConfig**: configure a specific service for `BANKDOMESTIC`:
```xml
<entry>
  <string>BANKLOCAL</string>
  <string>IMPS|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `BANKLOCAL-IMPS` as a withdrawal payment option<br/>
3). Create/Update routing rule by specifying `BankLocalWithdrawal` transaction type.

#### UPI Deposit

Account attribute:
- method=upi

1). **MerchantConfig**: configure a specific service for `BANKDOMESTIC`:
```xml
<entry>
  <string>BANKDOMESTIC</string>
  <string>UPI|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `BANKDOMESTIC-UPI` as a deposit payment option<br/>
3). Create/Update routing rule by specifying `BankDomesticDeposit` transaction type.

#### NET_Banking

Account attribute:
- method=net_banking

1). **MerchantConfig**: configure a specific service for `BANKDOMESTIC`:
```xml
<entry>
  <string>BANK</string>
  <string>NET_BANKING|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `BANK-NET_BANKING` as a deposit payment option<br/>
3). Configure PaymentIQ Cashier UI:

![](/img/providers/constantpayments-paymentmethod.png)

4). Create/Update routing rule by specifying `BankDeposit` transaction type.

#### PayTM, PhonePee, Mobikwik, PayZapp, JioMoney, Freecharge, OlaMoney

Account attribute:
- method=paytm
  (others: phone_pe, mobikwik, pay_zapp, jio_money, freecharge, ola_money)

1). **MerchantConfig**: configure a specific service for `WEBREDIRECT`:
```xml
<entry>
  <string>WEBREDIRECT</string>
  <string>PAYTM|PHONEPE|MOBIKWIK|PAYZAPP|JIOMONEY|FREECHARGE|OLAMONEY</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `WEBREDIRECT-PAYTM` (-PHONEPE, -MOBIKWIK...) as a deposit payment option<br/>
3). Create/Update routing rule by specifying `WebRedirectDeposit` transaction type.

## Test Information

### Without 3DS

| PAN for N3DS / 3DS testing | CVC | Exp. date | Transaction status |
|----------------------------|-----|-----------|--------------------|
| 4200000000000000           | Any | Any       | successful         |
| 4005550000000019           | Any | Any       | declined           |

### 3DS

| PAN for 3DS testing | CVC | Exp. date | Transaction status                               |
|---------------------|-----|-----------|--------------------------------------------------|
| 2201382000000013    | Any | Any       | successful (Frictionless flow)                   |
| 2201382000000047    | Any | Any       | successful (Challenge flow). OTP code is 1qwezxc |
| 2201382000000039    | Any | Any       | successful                                       |
| 2201382000000021    | Any | Any       | failed                                           |
