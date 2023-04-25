---
id: "pagsmile"
title: "Pagsmile"
hide_title: "true"
---

![](/img/providers/logos/pagsmile.png)

# Pagsmile

## About
Pagsmile is a payment provider offering payment solutions for Latin America countries.

### Payin

- Brazil - Boleto, PIX, DepositExpress, Loterry, Wallets (PicPay, AME, PayPal), BankTransfer*, Cash*
- Mexico - OXXO, SPEI, Wallets (ToditoCash), BankTransfer*, Cash 
- Colombia - PSE, Efecty, BankTransfer*, Cash*
- Chile - BankTransfer, Cash*
- Peru - BankTransfer*, Cash*
- Ecuador - BankTransfer*, Cash

\* - it is possible to trigger such operations in PaymentIQ, but they are not allowed at provider side yet.

### Payout

- Brazil - PIX, BankTransfer
- Mexico - SPEI
- Colombia - BankTransfer, Wallet Tpaga
- Chile - BankTransfer, Wallet Vita
- Peru - BankTransfer
- Ecuador - BankTransfer 

| Provider Name                | Pagsmile                                                                                                                                                                                                                          |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.pagsmile.com/](https://www.pagsmile.com/)                                                                                                                                                                            |
| Classification               | Aggregator of different payment options: Online/Manual Banking, Cash, Wallet                                                                                                                                                      |
| Regions                      | Brazil, Chile, Colombia, Ecuador, Mexico, Peru                                                                                                                                                                                    |
| Currencies                   | `USD`,`PEN`,`CLP`,`COP`,`MXN`,`PEN`,`PEN`                                                                                                                                                                                         |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`<br/>`BoletoDeposit`<br/>`PixDeposit`<br/>`LotericaDeposit`<br/>`OxxoDeposit`<br/>`BankLatamDeposit`<br/>`WalletLatamDeposit`<br/>`CashLatamDeposit`<br/>`BankDomesticWithdrawal`<br/>`WalletLatamWithdrawal` |
| PaymentIQ Configuration File | `PagsmileConfig`                                                                                                                                                                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pagsmile.PagsmileConfig>
    <enabled>true</enabled>
    <useViqProxy>false</useViqProxy>
    <accounts>
        <entry>
            <string>BRAZIL</string>
            <account>
                <accountID>??</accountID><!--app_id for Brazil-->
                <secretKey>??</secretKey><!--security_key-->
                <defaultDescriptor>??</defaultDescriptor><!--Product Name or Payment Reason-->
                <supportedCurrencies>BRL</supportedCurrencies>
                <targetCurrency>USD</targetCurrency><!--Merchant Account Currency-->
            </account>
        </entry>
        <entry>
            <string>CHILE</string>
            <account>
                <accountID>??</accountID><!--app_id for Chile-->
                <secretKey>??</secretKey><!--security_key-->
                <defaultDescriptor>??</defaultDescriptor><!--Product Name or Payment Reason-->
                <supportedCurrencies>CLP</supportedCurrencies>
                <targetCurrency>USD</targetCurrency><!--Merchant Account Currency-->
            </account>
        </entry>
        <entry>
            <string>MEXICO</string>
            <account>
                <accountID>??</accountID><!--app_id for Mexico-->
                <secretKey>??</secretKey><!--security_key-->
                <defaultDescriptor>??</defaultDescriptor><!--Product Name or Payment Reason-->
                <supportedCurrencies>MXN</supportedCurrencies>
                <targetCurrency>USD</targetCurrency><!--Merchant Account Currency-->
            </account>
        </entry>
        <entry>
            <string>COLOMBIA</string>
            <account>
                <accountID>??</accountID><!--app_id for Colombia-->
                <secretKey>??</secretKey><!--security_key-->
                <defaultDescriptor>??</defaultDescriptor><!--Product Name or Payment Reason-->
                <supportedCurrencies>COP</supportedCurrencies>
                <targetCurrency>USD</targetCurrency><!--Merchant Account Currency-->
            </account>
        </entry>
        <entry>
            <string>PERU</string>
            <account>
                <accountID>??</accountID><!--app_id for Peru-->
                <secretKey>??</secretKey><!--security_key-->
                <defaultDescriptor>??</defaultDescriptor><!--Product Name or Payment Reason-->
                <supportedCurrencies>PEN</supportedCurrencies>
                <targetCurrency>USD</targetCurrency><!--Merchant Account Currency-->
            </account>
        </entry>
        <entry>
            <string>ECUADOR</string>
            <account>
                <accountID>??</accountID><!--app_id for Ecuador-->
                <secretKey>??</secretKey><!--security_key-->
                <defaultDescriptor>??</defaultDescriptor><!--Product Name or Payment Reason-->
                <supportedCurrencies>USD</supportedCurrencies>
                <targetCurrency>USD</targetCurrency><!--Merchant Account Currency-->
            </account>
        </entry>
    </accounts>
    <testMode>false</testMode>
    <container>window</container>
    <defaultDescriptor>??</defaultDescriptor><!--Product Name or Payment Reason-->
</com.devcode.paymentiq.integration.pagsmile.PagsmileConfig>
```
</details>

### Attributes

| Attribute         | Description                                                                                                                                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountID         | Corresponds to the `app_id` at provider side. For each country/currency a unique `app_id` is set. Due to this, it make sense to have a separate account defined in the PagsmileConfig in PaymentIQ back office.                  |
| secretKey         | Corresponds to the unique secret key at provider side.                                                                                                                                                                           |
| defaultDescriptor | Corresponds to the product name or payment reason at provider side. It is possible to use either account level or config level default descriptor and the higher priority has the account level parameter.                       |
| targetCurrency    | Corresponds to the specific merchant account currency. For withdrawals we must have a targetCurrency named as `source_currency`. Should be one of: `USD`, `EUR`, `GBP`, `BRL`.                                                   |
| container         | Corresponds to the way how the user will be redirected to the checkout URL (`iframe` not supported for Wallet payment method).                                                                                                   |
| feePayer          | Config level parameter, that is used for BankTransfer, Wallet (Vita, Tpaga), PIX and SPEI operations in order to specify who should pay a fee. Possible values are: `merchant` or `beneficiary` (`merchant` is used by default). |

## Provider Configuration

1. The above XML template (PagsmileConfig) will need to be added via PaymentIQ back office **Admin -> Configuration**.
2. Routing needs to be added for all payment methods used in **Routing -> Routing**.

### BankTransfer Payout in Peru
Region is required for BankTransfer payout in Peru, and it can be taken either from `user.state` or from the `region` attribute in the verify user response of the Integration API:

```json
{
  "success": true,
  "userId": "user_123",
  "firstName": "John",
  "lastName": "Doe",
  ...
  "attributes": {
    "region": "Amazonas"
  },
  ...
}
```

### Payment Method Mapping

| Country  | Payment Method    | Payment Type | PaymentIQ Service      | PaymentIQ tx type      | Comment                                                                           |
|----------|-------------------|--------------|------------------------|------------------------|-----------------------------------------------------------------------------------|
| -        | -                 | Deposit      | -                      | WebRedirectDeposit     | It is used to redirect a user to all allowed payment methods                      |
| -        | BankTransfer      | Deposit      | blank or BANK_TRANSFER | BankLatamDeposit       | Generic BankTransfer deposit in Brazil, Mexico, Colombia, Chile, Peru, Ecuador    |
| -        | Cash              | Deposit      | blank or CASH          | CashLatamDeposit       | Generic Cash deposit in Brazil, Mexico, Colombia, Chile, Peru, Ecuador            |
| Brazil   | DepositExpress    | Deposit      | DEPOSIT_EXPRESS        | BankLatamDeposit       | Local bank transfer deposit in Brazil                                             |
| Brazil   | Boleto            | Deposit      | -                      | BoletoDeposit          | Cash payments in Brazil                                                           |
| Brazil   | PIX               | Deposit      | -                      | PixDeposit             | Online banking in Brazil                                                          |
| Brazil   | Lottery           | Deposit      | -                      | LotericaDeposit        | Cash payments in Brazil                                                           |
| Brazil   | PicPay Wallet     | Deposit      | PICPAY or PIC_PAY      | WalletLatamDeposit     | Wallet payments in Brazil                                                         |
| Brazil   | AME Wallet        | Deposit      | AME                    | WalletLatamDeposit     | Wallet payments in Brazil                                                         |
| Brazil   | PayPal Wallet     | Deposit      | PAYPAL                 | WalletLatamDeposit     | PayPal Wallet payments in Brazil                                                  |
| Mexico   | OXXO              | Deposit      | -                      | OxxoDeposit            | Voucher/Cash payments in Mexico                                                   |
| Mexico   | SPEI              | Deposit      | SPEI                   | BankLatamDeposit       | Online banking deposit in Mexico                                                  |
| Mexico   | ToditoCash Wallet | Deposit      | TODITO or TODITO_CASH  | BankDomesticWithdrawal | ToditoCash Wallet payments in Mexico                                              |
| Colombia | PSE               | Deposit      | PSE                    | BankLatamDeposit       | Real-time online bank transfers in Colombia                                       |
| Colombia | Efecty            | Deposit      | EFECTY                 | CashLatamDeposit       | Cash/Voucher payment in Colombia                                                  |
| -        | BankTransfer      | Withdrawal   | blank or BANK_TRANSFER | BankDomesticWithdrawal | Generic BankTransfer withdrawal in Brazil, Mexico, Colombia, Chile, Peru, Ecuador |
| Brazil   | PIX               | Withdrawal   | PIX                    | BankDomesticWithdrawal | Local bank transfer withdrawal in Brazil                                          |
| Mexico   | SPEI              | Withdrawal   | SPEI                   | BankDomesticWithdrawal | Online banking withdrawal in Mexico                                               |
| Colombia | Tpaga Wallet      | Withdrawal   | TPAGA                  | WalletLatamWithdrawal  | Tpaga Wallet withdrawal in Colombia                                               |
| Chile    | Vita Wallet       | Withdrawal   | VITA                   | WalletLatamWithdrawal  | Vita Wallet withdrawal in Chile                                                   |

## Example Routing Rule
![](/img/providers/routing/pagsmile.png)

## Transaction Flow

1. The end user enters the transaction amount (and banking relevant information for banking withdrawals).
2. PaymentIQ sends the deposit/withdrawal request to Pagsmile.
3. Pagsmile responds with an initial status + a redirect url (for deposits) acknowledging they have received the PaymentIQ request and begin processing.
4. In case of deposit, the user is redirected in order to complete the payment.
5. Pagsmile sends back a callback notification once the transaction status has changed.

## Test Information

### BankTransfer Payout in Brazil
Account for BankTransfer payout should contain `account digit` as a last digit e.g `{account}{account_digit}` - "xxxxxxxn" (we assume the last digit of the bank  account is the `account_digit`).

## Relevant data to test for each country

| Region   | ID Type | ID Number     | Account type                                         | Currency |
|----------|---------|---------------|------------------------------------------------------|----------|
| Brazil   | CPF     | 50284414727   | CPF, CNPJ, EVP, PHONE, EMAIL                         | BRL      |
| Mexico   | RFC     | MAMB780915969 | debit, phone, clabe                                  | MXN      |
| Colombia | NIT/CC  | 502844147     | PHONE(Wallet), CHECKING, SAVINGS                     | COP      |
| Chile    | RUT/RUN | 502844147     | EMAIL(Wallet), CHECKING, SAVINGS, VISTA, RUT, SALARY | CLP      |
| Peru     | DNI/RUC | 5028441472726 | CHECKING, SAVINGS                                    | PEN      |
| Ecuador  | RUC     | 502844        | CHECKING, SAVINGS, VIRTUAL                           | USD      |

## Available banks

| Region   | Link with bank name and bank code                                                                                          |
|----------|----------------------------------------------------------------------------------------------------------------------------|
| Brazil   | [https://docs.pagsmile.com/payout/bank-code/bank-in-brazil](https://docs.pagsmile.com/payout/bank-code/bank-in-brazil)     |
| Mexico   | [https://docs.pagsmile.com/payout/bank-code/bank-in-mexico](https://docs.pagsmile.com/payout/bank-code/bank-in-mexico)     |
| Colombia | [https://docs.pagsmile.com/payout/bank-code/bank-in-colombia](https://docs.pagsmile.com/payout/bank-code/bank-in-colombia) |
| Chile    | [https://docs.pagsmile.com/payout/bank-code/bank-in-chile](https://docs.pagsmile.com/payout/bank-code/bank-in-chile)       |
| Peru     | [https://docs.pagsmile.com/payout/bank-code/bank-in-peru](https://docs.pagsmile.com/payout/bank-code/bank-in-peru)         |
| Ecuador  | [https://docs.pagsmile.com/payout/bank-code/bank-in-ecuador](https://docs.pagsmile.com/payout/bank-code/bank-in-ecuador)   |

## Withdrawals

To initiate a withdrawal the end-user should specify all the required parameters (e.g. see this Chile example from our cashier below).
BranchName is only mandatory for Brazil.

![](/img/providers/pagsmile_withdrawal_bank.png)