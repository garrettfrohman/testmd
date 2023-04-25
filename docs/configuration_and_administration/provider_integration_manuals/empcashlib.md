--- 
id: "empcashlib" 
title: "EMP CashLib"
hide_title: "true"
---
 
![](/img/providers/logos/empcashlib.png)

# EMP CashLib

## About
Cashlib is a Payment Solution Provided by EMP-CORP in order to provide a solution that is designed to allow a clients to buy a voucher at a Distributor Point Of Sale (POS). Then the client can pay his purchases on affiliated e-merchant web sites with the vouchers he has previously bought.

CASHlib voucher is a paper ticket with a 16 digit Code associated with a Value and an Expiry_date (and other attributes).

After selecting Cashlib payment, the customer journey is the following:

1. User has to enter the 16 digit code on the e-merchant website to make his payment.
2. If the purchase amount is lower than voucher value then the voucher Balance is updated with the remaining value and the user may later make other payments with this voucher.
3. If the purchase amount is higher than user's voucher balance then the user may add other vouchers to reach the payment amount.

There are three types of transactions:
- Voucher Payment
- Voucher Direct Payment
- Voucher Payout

**Voucher Payment** permits to open an iframe on the user’s web browser and entirely processes the payment with the connected customer. After completing the payment process, the customer is returned to the e-merchant URL (either success_url if payment is successful or cancel_url if the payment failed or has been cancelled by customer).

**Voucher Direct Payment** permits to make a payment with the voucher code via a direct server to server communication (no redirect to iframe).

**Voucher Payout** permits to issue a new voucher that can be used by customer to withdraw money.

| Provider Name                | EMP CashLib                                                                     |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.cashlib.com/en/home.html](https://www.cashlib.com/en/home.html)    |
| Classification               | PrePaid Card / Voucher                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CashlibDeposit`<br/> `WebRedirectWithdrawal`                                   |
| PaymentIQ Configuration File | `EMPCashlibConfig`                                                              |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
not available
```

</details>

### Attributes

| Attribute    | Description                           |
|--------------|---------------------------------------|
| merchantId   | Provided by EMP CashLib               |
| secretKey    | Provided by EMP CashLib               |
| posId        | -                                     |
| brandId      | put "0" for non-branded voucher       |
| crosscountry | "Y" for crosscountry voucher else "N" |

### Email template

For payout transactions an email will be sent to the user on the provided email address.

A email template is required for sending out the payment code to the user.
For withdrawals name it emp-cashlib-email-template or set a other name in the EmpConfig file and the ```<emailTemplateName></emailTemplateName>``` attribute.

<details>
<summary>Click to view example email template for withdrawals (emp-cashlib-email-template)</summary>
<br/>

```html
<div class='content-container'>
    <div class='logo-container' >
        <img src="https://cashlib.com/app/uploads/2019/10/logo.png" alt="Cashlib">
    </div>
    <ul class='instruction-list'>
        <li>Use the following code to use voucher</li>
        <li>${code}</li>
        <li>Voucher code is valid until ${expiryDate}</li>
    </ul>
</div>
```
</details>

## Transaction flow

The following is a test from PaymentIQ's test cashier in order to visualize the purchase steps for **Voucher Payment**.


![](/img/providers/cashlib01.png)

![](/img/providers/cashlib02.png)

![](/img/providers/cashlib03.png)

![](/img/providers/cashlib04.png)

## Example Routing Rule

![](/img/providers/routing/cashlib.png)
![](/img/providers/routing/cashlib_payouts.png)

## Test Information

- Please use the lowest amount possible when testing, the vouchers get depleted.

### Voucher Codes

#### Voucher Payment

8038227264490483

7161866837576781

7827917181630896

4004982390748110

1517054099940142

5957017004774326

9254843253070506

#### Voucher Direct Payment

8465544929882070

7837308941662931

9725653115470785
