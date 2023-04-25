--- 
id: "alliedwallet" 
title: "AlliedWallet"
hide_title: "true"
---
 
![](/img/providers/logos/alliedwallet.png)

# AlliedWallet

## About
Allied Wallet is a provider of e-commerce merchant services and online payment processing services, enabling business owners to accept credit cards and other payments on their websites.

| Provider Name                | AlliedWallet                                                                    |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.alliedwallet.com/](https://www.alliedwallet.com/)                  |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund`                                               |
| PaymentIQ Configuration File | `AlliedWalletConfig`                                                            |

## Configuration Information

### Attributes

| Attribute  | Description |
|------------|-------------|
| merchantId |             |
| siteId     |             |
| secretKey  | Auth Token  |

## Example Routing Rule
![](/img/providers/routing/alliedwallet.png)

## Test Information

### N3DS

- Amount: 10
- Currency: USD

| Card Brand | Account          | CVV     | Expiry date |
|------------|------------------|---------|-------------|
| VISA       | 4242424242424242 | 123/555 | 12/2024     |