--- 
id: "hipay" 
title: "Hipay"
hide_title: "true"
---
 
![](/img/providers/logos/hipay.png)

# Hipay

## About
HiPay as aggregator will give you access to several different payment methods including Credit Card and Alternative Payment Methods. For APMs Deposit, Refund and Partial-Refund is available. And for Credit Card on top of mentioned options Auth, Capture and Void is also available. Yet, merchant should check each method with provider for more details.

| Provider Name                | Hipay                                                                                                                                                                                                                                      |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://hipay.com/en/](https://hipay.com/en/)                                                                                                                                                                                             |
| Classification               | Debit/Credit Card Processor, Aggregator Provider                                                                                                                                                                                           |
| Regions                      | `International`                                                                                                                                                                                                                            |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                            |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `WebRedirectDeposit`<br/> `IdealDeposit`<br/> `BankIBANDeposit`<br/> `BankIBANDeposit`<br/> `QiwiDeposit`<br/> `HiPayDeposit`<br/> `SofortDeposit`<br/> `GiropayDeposit`<br/> `Void`<br/> `Refund`<br/> `Capture` |
| PaymentIQ Configuration File | `HipayConfig`                                                                                                                                                                                                                              |

## Configuration Information

You as merchant need to take following steps to set up HiPay in our system:
1. Log in to HiPay back-office: [http://stage-merchant.hipay-tpp.com/default/auth/login](http://stage-merchant.hipay-tpp.com/default/auth/login)
2. Navigate to Integration / Security Settings.
3. Whitelist the IP addresses [found here](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist),
4. Generate new credentials (or use already existing ones).
5. In account config: 
`<username>` corresponds to Username in HiPay back-office,
`<password>` corresponds to Password in HiPay back-office,
`<merchantKeyId>` corresponds to URL Encoded Secret Passphrase in HiPay back-office.

## Example Routing Rule

-

## Test Information

- Any expiry date in the near future may be used as well as any 3-digit CVV code (4 digits for American Express).
- The Cardholder value is not verified on the TEST platform. Therefore, any value can be used.

| Credit   Card Number | Brand                 |
|----------------------|-----------------------|
| 4111111111111111     | VISA                  |
| 4200000000000000     | VISA                  |
| 4242424242424242     | VISA                  |
| 4000000000000002     | VISA   with 3DS       |
| 4111113333333333     | VISA   always refused |
| 5399999999999999     | Mastercard            |
| 5404000000000001     | Mastercard            |
| 5454545454545454     | Mastercard            |
| 5137009801943438     | Mastercard with 3DS2  |
| 4484120000000029     | CB                    |
| 6766000000000        | Maestro               |
| 67030000000000003    | Bancontact            |
| 374111111111111      | American   Express    |

### 3DS2
For configuration of 3DS2 please refer to this documentation: https://docu-portal-test.paymentiq.io/docs/configuration_and_administration/system_configuration/configure3dsv2  
HiPay 3DS2 is only supported by Internal3DServer. Amounts in EUR between 100-200 will trigger 3DS2 on HiPay's side. 

### SOFORT Überweisung:
Choose "Demo Bank" or enter bank "00000" -> Next.
Account number "00000", PIN "123456789" -> Next.
Choose an account -> Next.
TAN "12345" -> Next.

### Przelewy24
Choose a bank.
Login: sandbox / Password: sandbox
Click on "Pay".

### iDEAL
On the iDEAL simulator, choose the action to test:
Success
Exception
Cancelled
Failure

### ING Home'Pay
On the ING Home'Pay simulator, choose the action to test:
Payment accepted
Cancelled

### Belfius
On the first screen of the Belfius simulator, choose "Yes, I confirm my payment".
Then, on the second screen, choose the action to test:
Payment accepted
Failure
Cancelled

### Giropay
BIC/SWIFT code: TESTDETT421
Bank account/login: sepatest1
PIN: any 5-digit number
TAN: any 6-digit number

### PayPal
For PayPal test payments, use the personal account email address of your PayPal sandbox account.

### PaysafeCard
Use this number to make a valid TEST transaction in EUR:
0000-0000-0260-5213
