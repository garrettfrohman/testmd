---
id: "1click_api_paypal"
---

# PayPal Flow And Configuration

## Requirements

The merchant must have an account activated in the PayPal platform. The credentials should be added in PayPalConfig via PaymentIQ backoffice.

## Configuration

The merchant or Bambora should set up a PayPalConfig in PaymentIQ back-office. Only one account is needed for both sign in and sign up with deposit.

```xml
<entry>
      <string>default</string>
      <account>
        <accountID>??</accountID>
        <username>??</username>
        <password>??</password>
        <secretKey>??</secretKey>
        <serviceEndpoint>https://api-3t.sandbox.paypal.com/nvp</serviceEndpoint>
        <redirectUrl>https://www.sandbox.paypal.com/cgi-bin/webscr?cmd=_express-checkout&amp;token=</redirectUrl>
       <useTokenId>true</useTokenId>
       <billingType>MerchantInitiatedBilling</billingType>  <!-- it is already the default value but can be changed into MerchantInitiatedBilling-->
       <version>121</version>           <!-- the earlier used version is 106 -->
        <container>iframe</container>
      </account>
</entry>

```

## Testing

| CURRENCY | EMAIL           | PASSWORD  |
|----------|-----------------|-----------|
| EUR      | eur@devcode.se  | gmsmotwlB |
| GBP      | gbp1@devcode.se | gmsmotwlB |


## KYC Data

:::info
The fields may not return in the same attribute name and format as displayed below e.g address_country is mapped as country with `SWE` as format. This is to ensure consistency when using multiple identity providers.
:::

## Full response example:

```
TOKEN=EC%2d2KA76408FA7433117&BILLINGAGREEMENTACCEPTEDSTATUS=1&CHECKOUTSTATUS=PaymentActionNotInitiated&TIMESTAMP=2019%2d10%2d18T14%3a04%3a28Z&CORRELATIONID=8100d1cb83986&ACK=Success&VERSION=121&BUILD=53734851&EMAIL=eur%40devcode%2ese&PAYERID=UG8E3HVK7DNN2&PAYERSTATUS=verified&FIRSTNAME=Elias&LASTNAME=Sidenbladh&COUNTRYCODE=FR&ADDRESSSTATUS=Confirmed&CURRENCYCODE=SEK&AMT=200%2e00&ITEMAMT=200%2e00&SHIPPINGAMT=0%2e00&HANDLINGAMT=0%2e00&TAXAMT=0%2e00&INVNUM=1991A1407200&NOTIFYURL=https%3a%2f%2ftest%2dapi%2epaymentiq%2eio%2fpaymentiq%2fapi%2fpaypal%2fmessage%2fipn&INSURANCEAMT=0%2e00&SHIPDISCAMT=0%2e00&INSURANCEOPTIONOFFERED=false&L_NAME0=devCode&L_QTY0=1&L_TAXAMT0=0%2e00&L_AMT0=200%2e00&PAYMENTREQUEST_0_CURRENCYCODE=SEK&PAYMENTREQUEST_0_AMT=200%2e00&PAYMENTREQUEST_0_ITEMAMT=200%2e00&PAYMENTREQUEST_0_SHIPPINGAMT=0%2e00&PAYMENTREQUEST_0_HANDLINGAMT=0%2e00&PAYMENTREQUEST_0_TAXAMT=0%2e00&PAYMENTREQUEST_0_INVNUM=1991A1407200&PAYMENTREQUEST_0_NOTIFYURL=https%3a%2f%2ftest%2dapi%2epaymentiq%2eio%2fpaymentiq%2fapi%2fpaypal%2fmessage%2fipn&PAYMENTREQUEST_0_INSURANCEAMT=0%2e00&PAYMENTREQUEST_0_SHIPDISCAMT=0%2e00&PAYMENTREQUEST_0_SELLERPAYPALACCOUNTID=elias%2esidenbladh%2dfacilitator%40devcode%2ese&PAYMENTREQUEST_0_INSURANCEOPTIONOFFERED=false&PAYMENTREQUEST_0_PAYMENTREQUESTID=1991A1407200&L_PAYMENTREQUEST_0_NAME0=devCode&L_PAYMENTREQUEST_0_QTY0=1&L_PAYMENTREQUEST_0_TAXAMT0=0%2e00&L_PAYMENTREQUEST_0_AMT0=200%2e00&PAYMENTREQUESTINFO_0_PAYMENTREQUESTID=1991A1407200&PAYMENTREQUESTINFO_0_ERRORCODE=0
```

## KYC Data 

- EMAIL
- FullNAME
- FIRSTNAME
- LASTNAME
- PAYERID – personid such as UG8E3HVK7DNN2
- PAYERSTATUS
- ADDRESSSTATUS
- CITY
- STATE
- COUNTRYNAME
- COUNTRY
- STREET
- ZIP

## Example

![](/img/1clickapi/paypal01.png)

![](/img/1clickapi/paypal02.png)

![](/img/1clickapi/paypal03.png)
