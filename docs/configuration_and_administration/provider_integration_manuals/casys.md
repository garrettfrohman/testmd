--- 
id: "casys" 
title: "CaSys"
hide_title: "true"
---
 
![](/img/providers/logos/casys.png)

# CaSys

## About
CaSys is a payment provider offering creditcard deposit and withdrawal (via web redirection), and also recurring.

| Provider Name                | CaSys                                                |
|------------------------------|------------------------------------------------------|
| Link                         | [http://www.casys.com.mk/](http://www.casys.com.mk/) |
| Classification               | Debit/Credit Card Processor                          |
| Regions                      | North Macedonia                                      |
| Currencies                   | `MKD`                                                |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`<br/>`WebRedirectWithdrawal`     |
| PaymentIQ Configuration File | `CaSysConfig`                                        |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.casys.CaSysConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId>
        <merchantName>??</merchantName>
        <secretKey>??</secretKey><!--Merchant Password-->
        <useTokenId>false</useTokenId><!--true: use card tokenization-->
        <supportedCurrencies>MKD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <failTxIfCardIsRegisteredAlready>-2</failTxIfCardIsRegisteredAlready>
  <container>window</container><!--iframe is not supported for payout redirection-->
  <defaultDescriptor>Invoice: ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.casys.CaSysConfig>
```
</details>

### Attributes
| Attribute                       | Description                                                                                                                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId              | Corresponds to *Merchant ID* from CaSys. It identifies a merchant at CaSys side.                                                                                                                              |
| account.merchantName            | Corresponds to *Merchant Name* from CaSys. It identifies a merchant at CaSys side.                                                                                                                            |
| account.secretKey               | Corresponds to *Merchant Password* from CaSys. It is used to generate a checksum for each payment request.                                                                                                    |
| account.useTokenId              | `true` is used to enable card tokenization and to make a recurring payment using stored card token.                                                                                                           |
| failTxIfCardIsRegisteredAlready | `-1` - will return card token if card is not registered yet or fail payment if card is registered already.<br/>`-2` - will always return card token (will not fail payment if the card is registered already) |

## Example Routing Rule
![](/img/providers/routing/casys.png)


## Transaction Flow

### Deposit Flow

Select Creditcard redirect

![](/img/providers/casys_deposit_01.png)

Specify card details and press **Confirm** button

![](/img/providers/casys_deposit_02.png)

Press **Confirm** button again

![](/img/providers/casys_deposit_03.png)

Then press green button to receive 3DS verification code

![](/img/providers/casys_deposit_04.png)

Once it is pressed you will be redirected to the 3DS authentication dialog where 3DS verification code must be specified

![](/img/providers/casys_deposit_05.png)

Once 3DS verification code was specified and 3DS authentication completed, you will see

![](/img/providers/casys_deposit_06.png)

And payment should be completed.

NOTE: In case of invalid 3DS verification code specified in 3DS authentication dialog you will see

![](/img/providers/casys_deposit_07.png)

### Recurring Flow

If you have "useTokenId=true" in your config and card token was generated, you can make a recurring payment by making a repeated payment

![](/img/providers/casys_recurring_01.png)

Then you will be redirected to

![](/img/providers/casys_recurring_02.png)

Press **Confirm** button to proceed with payment.

### Withdrawal Flow

Withdrawal flow is the same as deposit flow.


## Test Information

| Card Number      | Expiry Date | CVV |
|------------------|-------------|-----|
| 5413330089020029 | 12/25       | 990 |
| 5413330089020037 | 12/25       | 494 |
| 5413330089020011 | 12/25       | 704 |

You can use dummy card number e.g. 5413339999999999 for decline transaction.