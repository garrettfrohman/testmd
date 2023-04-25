--- 
id: "point66" 
title: "Point66"
hide_title: "true"
---
 
![](/img/providers/logos/point66.png)

# Point66

## About

| Provider Name                | Point66                                      |
|------------------------------|----------------------------------------------|
| Link                         | [https://point66.com/](https://point66.com/) |
| Classification               | Wallet                                       |
| Regions                      | `Japan`                                      |
| Currencies                   | `USD`                                        |
| Methods/PaymentTxTypes       | `Point66Deposit` <br/> `Point66Withdrawal`   |
| PaymentIQ Configuration File | `Point66Config`                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.point66.Point66Config>
  <enabled>true</enabled>
  <container>window</container>
  <validCallbackIpAddresses>68.183.227.112|68.183.180.191|165.22.101.179|178.128.216.218</validCallbackIpAddresses>
  <accounts>
    <entry>
      <string>Point66TEST</string>
      <account>
        <siteReference>??</siteReference>
        <supportedCurrencies>USD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.point66.Point66Config>
```

</details>

### Attributes

| Attribute                | Description                                                                                                                                               |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| siteReference            | Used as a part of the URL to which PaymentIQ sends requests, provided by Point66 individually for each merchant. Point66 calls this parameter "site code" |
| validCallbackIpAddresses | A list of potential IP addresses from which Point66 send callbacks to PaymentIQ with updated transaction statuses.                                        |
| container                | A container in which the Point66 dashboard should appear after the redirection. Please always use "window".                                               |

## Provider Configuration

1. Run PaymentIQ and add the aforementioned Point66Config under Admin -> Configuration.
2. Add Point66 to the `<psp>` section in MerchantConfig under Admin -> Configuration. 
3. Add routing rules - see example below.
4. Enable POINT66 deposit method and POINT66 withdrawal method in Rules -> Payment methods.
5. Additional configuration has to be added in TxTypeInput config file. Please contact PaymentIQ tech support to configure that for you.
6. An html template has to be added under your MID. Please contact PaymentIQ tech support to 
   place the required template for you.

## Example Routing Rule

![](/img/providers/routing/point66.png)

## Transaction Flow

### Deposits

1. The user enters the amount along with the account number, and the email address in the Cashier.
   The email address as well as the account number should be the same as the ones from the user's Point66 account.
2. PaymentIQ sends an initial deposit request to the PSP.
3. In case the request has been processed successfully, the user gets redirected to the Point66 dashboard where she/he follows
   the instructions to complete the deposit.
4. PaymentIQ receives a callback with the transaction status and sends back a response with the status of the request.
5. If after the callback PaymentIQ has processed the transaction correctly and sends a successful response to Point66,
   the deposit is completed.
   
### Withdrawals

1. The user enters the amount along with the account number that is related to the user's Point66 account.
2. PaymentIQ sends an initial payout request to Point66.
3. If the Point66 response for the initial payout request proved to be successful, PaymentIQ sends a payout request to Point66.
4. After a successful response from Point66 for the payout request, the withdrawal is completed.

## Test Information
For testing, you will need the following credentials:

- siteReference - a.k.a site code provided by Point66 tech support (the one mentioned in the Configuration Information -> Attributes section above)
- Account number - this is assigned individually by Point66 to each user's account and has to be entered in the Cashier
- Email - email account under which the Point66 account is registered, used in the Cashier and to log into the Point66 dashboard after the redirection
- Password - password to the Point66 dashboard, used to log into the Point66 dashboard after the redirection

Please contact Point66 tech support to obtain them.