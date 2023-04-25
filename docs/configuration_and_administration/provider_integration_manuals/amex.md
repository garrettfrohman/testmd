--- 
id: "amex" 
title: "Amercian Express"
hide_title: "true"
---
 
![](/img/providers/logos/americanexpress.png)

# Amercian Express

## About
Direct integration to American Express.

| Provider Name                | American Express                                                                         |
|------------------------------|------------------------------------------------------------------------------------------|
| Link                         | -                                                                                        |
| Classification               | Credit Card Processor                                                                    |
| Regions                      | `International`                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Void`<br/> `Capture` |
| PaymentIQ Configuration File | `AmericanExpressConfig`                                                                  |

## Configuration Information
### Attributes

| PaymentIQ Configuration    | Provider Credential                                                                                                           |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| merchantId                 |                                                                                                                               |
| terminal                   | TerminalId. Unique code that identifies a specific terminal at a Merchant location                                            |
| merchantCode               | Merchant Category Code (MCC)                                                                                                  |
| regionCode                 | Region header                                                                                                                 |
| merchantName               | Card Acceptor Name                                                                                                            |
| merchantAddress            | Card Acceptor Address                                                                                                         |
| merchantZip                | Card Acceptor Postal Code                                                                                                     |
| merchantCity               | Card Acceptor City                                                                                                            |
| merchantRegion             | Card Acceptor Region Code                                                                                                     |
| merchantCountry            | Acquiring Institution Country Code (3 digits)                                                                                 |
| useTokenId                 | Set to true for recurring payments                                                                                            |
| paymentFacilitator         | Set to true for Payment Facilitator/Aggregator. If true, subMerchant data needs to be included in merchant authorize response |
| batchCloseJobEnabled       | Enable closing batches at specific times                                                                                      |
| batchCloseCronInterval     | Set the cron interval of when batches should be closed. Defaults to `0 59 23 * * *` (23:59)                                   |
| batchCloseCronTimezone     | Set the timezone of when batches should be closed. Defaults to UTC                                                            |
| useMerchantTxIdAsInvRefNbr | Set to true to send merchantTxId as invRefNbr in the capture request to Amex                                                  |

### Payment Facilitators/Aggregators
Sub merchant data needs to be included in the merchant authorize response as attributes with the following parameter structure.

| Parameter             | Description                 |
|-----------------------|-----------------------------|
| merchantMcc           | Merchant Catogry Code (MCC) |
| subMerchantName       | Card Acceptor Name          |
| subMerchantAddress    | Card Acceptor Street        |
| subMerchantPostalCode | Card Acceptor Postal Code   |
| subMerchantCity       | Card Acceptor City          |
| subMerchantRegionCode | Card Acceptor Region Code   |
| subMerchantCountry    | Card Acceptor Country Code  |
| subMerchantEmail      | Card Acceptor Email         |
| subMerchantPhone      | Card Acceptor Phone Number  |
| subMerchantId         | Card Acceptor Seller ID     |

## Example Routing Rule
![](/img/providers/routing/amex.png)
![](/img/providers/routing/amex2.png)

## Test Information
### N3DS
| Card            | Amount | CVC | Exp. date | Result  |
|-----------------|--------|-----|-----------|---------|
| 373953192351004 | 1-10   | Any | Any       | Success |
| 373953192351004 | 11-20  | Any | Any       | Failed  |

### 3DS / SafeKey
| Card            | Amount | CVC | Exp. date | Result  |
|-----------------|--------|-----|-----------|---------|
| 374500261001009 | 11-20  | Any | Any       | Success |
| 374500262001008 | 31-40  | Any | Any       | Failed  |
