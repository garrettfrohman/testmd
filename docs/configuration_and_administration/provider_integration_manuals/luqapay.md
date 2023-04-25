---
id: "luqapay"
title: "LuqaPay (formerly BestPay)"
hide_title: "true"
---

![](/img/providers/logos/luqapay.png)

# LuqaPay (formerly BestPay)

## About
LuqaPay is a bank and card provider that offers a variety of payment methods (deposits and
withdrawals for banking, credit cards, community banks,  cryptocurrencies and crypto wallets).

| Provider Name                | LuqaPay (formerly BestPay)                                                                                                                                                                                                                                                                                                                                                                      |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://luqapay.com/](https://luqapay.com/)                                                                                                                                                                                                                                                                                                                                                    |
| Classification               | Online Banking / Credit Cards / Cryptocurrency                                                                                                                                                                                                                                                                                                                                                  |
| Regions                      | `International`                                                                                                                                                                                                                                                                                                                                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                                                                                                                                                                                 |
| Methods/PaymentTxTypes       | `BestPayDeposit`<br/>`CommunityBankDeposit`<br/>`BestPayWithdrawal`<br/>`BankIBANWithdrawal`<br/>`BankLocalWithdrawal`<br/>`CreditcardDeposit`<br/>`BankDeposit` <br/>`InteracDeposit` <br/> `CryptoCurrencyWithdrawal` <br/> `CryptoCurrencyDeposit` <br/> `BestPayNetbankingWithdrawal` <br/> `BankDirectWithdrawal` <br/> `BestPayNetbankingIdrWithdrawal` <br/> `BestPayBankIBANWithdrawal` |
| PaymentIQ Configuration File | `BestPayConfig`                                                                                                                                                                                                                                                                                                                                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
Not available.
```

</details>

### Attributes
| PaymentIQ Backoffice | Description                                                                                                                                                                           | Types       |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| merchantId           | Provided by LuqaPay to secure payment initialization (Api Key)                                                                                                                        | Bank, Cards |
| secretKey            | Provided by LuqaPay to recreate the signature in callback                                                                                                                             | Bank, Cards |
| transactionChannel   | Optional. Defaults to COMMUNITY_BANK                                                                                                                                                  | Bank        |
| maxAmount            | use to set the max amount on the available amount list                                                                                                                                | Bank        |
| minAmount            | use to set the min amount on the available amount list                                                                                                                                | Bank        |
| bankMappings         | use to bankinfo to request for example: iban to swift                                                                                                                                 | Bank        |
| maxAmountDifference  | Optional. For communtiy bank deposit. Set to limit the amounts shown to the user in percentage from original amount. E.g 0.2 = 20%                                                    | Bank        |
| enableCsvBatchFiles  | Set to true to enable withdrawals through CSV batch files                                                                                                                             | Bank        |
| use3Dsecure          | true / false                                                                                                                                                                          | Cards       |
| method               | CCDIRECT / CREDIT_CARD (default CREDIT_CARD)                                                                                                                                          | Cards       |
| ignoreLocalisation   | Set to true to not send the language parameter to LuqaPay                                                                                                                             | Cards       |
| useCardholderAsName  | true / false (default false). Option to use the cardholder name instead of the merchant user name when sending the firstName and lastName values to Bestpay for credit card deposits. | Cards       |
| piqVersion           | Set PIQ version, which is associated with the payment method codes at LuqaPay. This attributes is used for Voucher via credit card and should have the value CCVOUCHER                | CC-Voucher  |
| account.service      | List of services that the the account will use                                                                                                                                        |             |
| container            | After this extension by BestPay's/Luqapay's request the container for redirections should be set to "window"                                                                          |             |
| languageMapping      | Provides a language mapping from the one sent in your locale to the language that is specified in the mapping. More on that below the table.                                          |             |

Note:
- LuqaPay is configured using BestPayConfig.
- Some of the attributes  only used for banking and some only for credit cards.

To configure a LuqaPay account you should contact LuqaPay Support to request:

- Request API key and Secret key.
- Ask them to configure the URLs to:

| Environment | Feature               | URL                                                          |
|-------------|-----------------------|--------------------------------------------------------------|
| Test        | PayIn/PayOut/Callback | https://test-api.paymentiq.io/paymentiq/api/bestpay/callback |
| Production  | PayIn/PayOut/Callback | https://api.paymentiq.io/paymentiq/api/bestpay/callback      |

- Whitelist [PaymentIQ IP addresses](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist).



### Language Mapping
The languageMapping parameter is optional in your configuration. By default, without any configuration added, its value
is: <br/>
`<languageMapping>TR->TR,NO|NB->NO,*->EN</languageMapping>`

The way it works is that it takes a parameter from your locale and maps it to the value specified after the '->' sign. <br/>

Example 1: <br/>
If your locale is 'nb_NO', PaymentIQ takes the 'nb' part and converts it to 'NO' which is specified in the mapping.

Example 2: <br/>
If your locale is 'hi_IN', PaymentIQ takes the 'hi' part and converts it to 'EN' because the wildcard sign `*` has been
mapped to 'EN'. Any value has not been explicitly mapped is being mapped to the language to which the wildcard sign `*`
has been mapped.

As of 2021-11-03 the BestPay methods that utilise the languageMapping parameter are:
- BestPayNetbankingWithdrawal
- BestPayDeposit
- CommunityBankDeposit


### NOTE
The provider should send all the required account details (SANDBOX or LIVE) to the merchant, and the merchant should
contact PaymentIQ tech support in order to configure the requested payment options by sending an email to
technicalsupport@worldline.com. If it is a new merchant, they will need to send a corresponding email to the PaymentIQ
onboarding team using onboardingiq@worldline.com.

### Community Bank Deposit Flow
Community bank deposits are a bit different than regular deposits. The available amounts to deposit must always be requested by the provider before making the actual deposit. This means that the amount will most likely change from the original amount entered in the cashier. The flow goes like this:

1. The user enters the amount they want to deposit in the cashier as usual and a process request is sent to PIQ. Merchant authorize will not be done at this stage, instead it will be requested when the final amount is set.
2. PIQ requests available banks from the provider and responds to the process call with a redirect form with the available banks for the user to choose from.
3. When the user selects the bank, PIQ makes another call to the provider to request the available amounts for that bank. If the original amount is available, step 4 is skipped and the flow continues from step 5.
4. The closest lower and higher amount from the original amount is shown to the user to select from. When selected, the transaction is updated with the new amount and the limit rules in PIQ runs again.
5. Now, the merchant authorize is done which gives the merchant a chance to approve the final amount. If not declined, the transaction proceeds by redirecting the user to the provider where the deposit is finilized.

### Withdrawals through CSV batch files
Withdrawals through API only works with banks connected to community bank. If the bank is not connected the transactions must be sent as a CSV batch files. To use this feature there are some internal configuration needed in PIQ, please contact support.

### Bank Transfers
Bank transfers are used with TxType BankDeposit. There are different kinds of bank transfers on Luqapay's side. To select the one to use you have to either send the value as a service or configure it on account level in BestPayConfig as `<method>`. See Luqapay's documentation for a full list. Example:

```<method>DIRECT_INSTANT_BANK_TRANSFER</method>```

### Indian NetBanking deposit

This method is used to make a bank deposit. <br/>
Please make sure to enable BANK-INDIAN_NET_BANKING in Rules -> Payment Methods for the account that should use this method.


Supported countries: `India`

Supported currencies: `INR`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize payment" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Jeton Cash Card - Redeem Voucher deposit

This method is used to make a deposit from a JetonCash Voucher issued by the provider. <br/>
Please make sure to enable BANK-REDEEM_VOUCHER in Rules -> Payment Methods for the account that should use this method.

Supported countries: `Global`

Supported currencies: `JPY`, `EUR`, `INR`, `BRL`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends a token request to BestPay/Luqapay and gets back a response with a token (used to authorize the next request in headers)
   along with redirectUrl. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above and is asked to enter the JetonCash number which
   the amount should be deposited from with its security code and expiry date.
4. PaymentIQ sends a pay request and gets the transaction status in the response.

### UPI deposit

This method is used to make a bank deposit. <br/>
Please make sure to enable BANK-UPI in Rules -> Payment Methods for the account that should use this method.


Supported countries: `India`

Supported currencies: `INR`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize payment" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### NetBanking IDR deposit

This method is used to make a bank deposit. <br/>
Please make sure to enable BANK-NETBANKING_IDR in Rules -> Payment Methods for the account that should use this method.


Supported countries: `Indonesia`

Supported currencies: `IDR`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize payment" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Manual Papara

This method is used to make a bank deposit. <br/>
Please make sure to enable BANK-MWALLET_PAPARA in Rules -> Payment Methods for the account that should use this method.

Supported countries: `Turkey`

Supported currencies: `TRY`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Manual Peppara

This method is used to make a bank deposit. <br/>
Please make sure to enable BANK-MWALLET_PEPPARA in Rules -> Payment Methods for the account that should use this method.

Supported countries: `Turkey`

Supported currencies: `TRY`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Bank Transfer Voucher

This method is used to make a deposit via bank transfer voucher. <br/>
Please make sure to enable BANK-BTVOUCHER in Rules -> Payment Methods for the account that should use this method.

Supported countries: `Japan`

Supported currencies: `USD`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.


## Interac

This method is used to make a bank deposit.

Option #1 (setup with BankDeposit tx type and INTERAC service):
Set BANK-INTERAC as _Deposit method_ in _Rules -> Payment methods_ for the account that should use this method.

Option #2 (setup with InteracDeposit tx type):
Set INTERAC as _Deposit method_ in  _Rules -> Payment methods_ for the account that should use this method.



Supported countries: `Canada`

Supported currencies: `CAD`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### CryptoPay

This method is used to make a cryptocurrency deposit. <br/>
Please make sure to enable BANK-CRYPTOPAY in Rules -> Payment Methods for the account that should use this method.

Supported countries: `Turkey`, `Germany`, `Ukraine`

Supported currencies: `EUR`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.
5. In case of UNDERPAID/OVERPAID/TIMEOUT status of the transaction, the transaction's status will be set to PROCESSING_MERCHANT.
   A refundUrl will be returned by the PSP which will be appended to the transaction details and also visible in PaymentIQ's
   transactions table under "Info". That url should be used by the merchant to manually finish the transaction (accept or refund the payment)
   Once the merchant has completed the manual process the PSP will return with a callback that fails the transaction, therefore
   in case of accepting the amount, the money should be added to the user's account manually.

#### NOTE
In order to test the UNDERPAID/OVERPAID/TIMEOUT scenarios please use the following amounts:
For UNDERPAID - 444 EUR
For TIMEOUT - 555 EUR
For OVERPAID - 666 EUR

### CCDirect

While CCDirect can be set-up from the config file, there is also the possibility of having a separate CreditCardDeposit tx type with the service set to CCDIRECT. For this new tx type, the method configured on the account level is ignored, it will always take the value of the service.

### Crypto via Credit Card

This method is used to make a deposit using a credit card. <br/>
Please make sure to enable CREDITCARD-CRYPTO in Rules -> Payment Methods for the account that should use this method.

Supported countries: `Global`

Supported currencies: `All`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier along with credit card credentials (number, holder name, expiration
   date and CVV).
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.


### Crypto via Bank Transfer

This method is used to make a deposit via crypto bank transfer. <br/>
Please make sure to enable BANK-BTCRYPTO in Rules -> Payment Methods for the account that should use this method.

Supported countries: `Global`

Supported currencies: `EUR`, `USD`

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Instant QR

This method is used to make a bank deposit. <br/>
Please make sure to enable BANK-INSTANT_QR in Rules -> Payment Methods for the account that should use this method. <br/>

Important! This payment method only accepts amounts that are multiples of 10 and the minimal amount accepted is 20.
Therefore it is essential to configure your fees in the backoffice under Rules -> Fees -> Fee. <br/>
The conditions that you need to set are:
- Methods - set to BANK-INSTANT_QR
- Payment method - set to Deposit


The actions to be set are:
- Mode - set to Deduct
- Percentage fee - set your percentage fee, f.ex 1.0%

Supported countries: `Turkey`

Supported currencies: `TRY`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Instant Cepbank

This method is used to make a bank deposit. <br/>
Please make sure to enable BANK-INSTANT_CEPBANK in Rules -> Payment Methods for the account that should use this method. <br/>

Important! This payment method only accepts amounts that are multiples of 10 and the minimal amount accepted is 20.
Therefore it is essential to configure your fees in the backoffice under Rules -> Fees -> Fee. <br/>
The conditions that you need to set are:
- Methods - set to BANK-INSTANT_CEPBANK
- Payment method - set to Deposit


The actions to be set are:
- Mode - set to Deduct
- Percentage fee - set your percentage fee, f.ex 1.0%

Supported countries: `Turkey`

Supported currencies: `TRY`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Cepbank

This method is used to make a bank deposit. <br/>
Please make sure to enable BANK-CEPBANK in Rules -> Payment Methods for the account that should use this method. <br/>

Important! This payment method only accepts amounts that are multiples of 10 and the minimal amount accepted is 20.
Therefore it is essential to configure your fees in the backoffice under Rules -> Fees -> Fee. <br/>
The conditions that you need to set are:
- Methods - set to BANK-CEPBANK
- Payment method - set to Deposit


The actions to be set are:
- Mode - set to Deduct
- Percentage fee - set your percentage fee, f.ex 1.0%

Supported countries: `Turkey`

Supported currencies: `TRY`


#### Transaction Flow

1. The user enters the amount to deposit in the cashier.
2. PaymentIQ sends "initialize" request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. The user is redirected to the redirectUrl given in the response above with further instructions.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Custody Crypto

This method is used to make a crypto currency deposit. It is based on crypto wallets, so transactions are initiated
from the user's crypto environment. Every crypto wallet is created individually for each pair of the merchant's email
and the user's email. <br/>

Supported countries: `Global`

Supported currencies: `All`

#### Custody Crypto's configuration

This method has to work on a separate, dedicated account for which Luqapay has to provide the credentials.

1. Configure your BestPayConfig:

<details>
<summary>Click to view BestPayConfig</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bestpay.BestPayConfig>
   <enabled>true</enabled>
   ...
   <!-- This field is mandatory for this method and the value has to match the name of the account that uses Custody Crypto (accounts.entry.string)-->
   <cryptoWalletAccountName>BestPayCryptowalletAccount</cryptoWalletAccountName>
   <accounts>
      ...
      <entry>
         <!-- This account should be used to generate crypto wallet addresses only (CUSTODY_CRYPTO) For any other method please use a different account.-->
         <string>BestPayCryptowalletAccount</string>
         <account>
            <merchantId>??</merchantId>
            <apiKey>??</apiKey>
            <secretKey>??</secretKey>
            <email>??</email>
            <password>??</password>
            <service>BTC|BCH|ETH|USDT|USDT.ERC20|XRP|LTC|DOGE</service>
         </account>
      </entry>
   </accounts>
   ...
</com.devcode.paymentiq.integration.bestpay.BestPayConfig>
```
</details>

##### Note
For this method to work properly, the field `<cryptoWalletAccountName>`
is mandatory and it has to match the name of the
account name that uses Custody Crypto (accounts.entry.string). <br/>
In our example in the BestPayConfig file above, the name of the account dedicated for Custody Crypto is: <br/>
`<string>BestPayCryptowalletAccount</string>`<br/>
Therefore we set: <br/>
`<cryptoWalletAccountName>BestPayCryptowalletAccount</cryptoWalletAccountName>`

2. Configure USDT.ERC20, BTC, USDT, BCH, XRP, ETH, LTC, DOGE in the MerchantConfig

<details>
<summary>Click to view MerchantConfig</summary>
<br/>

```xml
<entry>
   <string>CRYPTOCURRENCY</string>
   <string>...|USDT.ERC20|BTC|USDT|BCH|XRP|ETH|LTC|DOGE</string>
</entry>
```
</details>

3. Enable CRYPTOCURRENCY-USDT.ERC20, CRYPTOCURRENCY-BTC, CRYPTOCURRENCY-USDT, CRYPTOCURRENCY-BCH, CRYPTOCURRENCY-XRP,
   CRYPTOCURRENCY-ETH, CRYPTOCURRENCY-LTC, CRYPTOCURRENCY-DOGE withdrawal option in Rules -> Payment Methods.
4. Additionally, Cashier Payment Method-settings has to be configured and two html templates have to be added.
Please contact PaymentIQ's tech support for the configuration changes.
5. Make sure that you send the following parameters in the cashier:

   | Parameter        | Value     |
   |------------------|-----------|
   | amount           | 0         |
   | mode             | ecommerce |
   | disableBtnAtZero | false     |
   | showAccounts     | false     |

When using our Cashier, your url should therefore include the following request params:
`amount=0&mode=ecommerce&disableBtnAtZero=false&showAccounts=false`

#### Transaction Flow

1. The user enters the cashier and clicks on the "Deposit" button. It is highly recommended to change the name of the
   button to "Show wallet", as the deposit is being initiated from outside the cashier.
2. PaymentIQ checks whether a wallet address exists for the pair of merchant email - user's email. <br/>
   a) If the wallet address exists in PaymentIQ's vault, it is simply being displayed to the user on a separate html
   page with a QR code. <br/>
   b) If the wallet address does not exist in PaymentIQ's vault, PaymentIQ sends a request to create a wallet address.
   It is done by initaiting a transaction with the amount equal to 0 which will be visible in the backoffice.
   In a successful response, PaymentIQ receives the wallet address, stores it under the user's account and thw wallet
   address is being displayed to the user on a separate HTM page with a QR code. <br/>
3. The user can copy the wallet address and utilise it in her/his own crypto environment to place a deposit. Please note
   that it is possible for the user not to visit the cashier at all to make a deposit once she/he has saved the wallet address.
4. Once Luqapay has received the deposit request from the user's crypto environment, Luqapay validates it and sends a callback to PaymentIQ
only if the transaction has been processed correctly and the deposit is valid.
5. PaymentIQ receives the callback, checks if the account with the wallet address provided in the callback exists in the
vault, verifies the callback's signature and creates a new transaction.
6. The currency in callbacks will always be EUR, therefore PaymentIQ converts the amount received in the callback to the
user balance's currency using Forex.
7. In case you have your fees set in the configuration, PaymentIQ will take the amount from the callback, deduct the fee
   and increase the user's balance by the amount with the fee deducted. <br/>
   For example, the amount received in the callback is 10 EUR and you have set a 1% fee. After receiving the callback,
   PaymentIQ will deduct 0.10 EUR from the amount (which is 1% of 10 EUR) and increase the user's balance by 9.90 EUR.

### Bank Transfer Withdraw - Turkey

This method is used to make a withdrawal to a specified bank account.<br/>
Please make sure to enable BANKIBAN-BANK_TRANSFER_TK in Rules -> Payment Methods for the account that should use this method.

Additionally, Cashier Payment Method-settings has to be configured. Please contact
our technical support to make changes in this file to enable this method.

Supported countries: `Turkey`

Supported currencies: `TRY`

#### Transaction Flow

1. The user enters the amount to withdraw along with the IBAN number and chooses a BIC code from the dropdown menu in the cashier.
2. PaymentIQ sends a token request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction and its type.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Manual Papara Withdraw

This method is used to make a withdrawal to a specified bank account. <br/>
Please make sure to enable BESTPAY-MWALLET_PAPARA in Rules -> Payment Methods for the account that should use this method.

Additionally, Cashier Payment Method-settings has to be configured. Please contact
our technical support to make changes in this file to enable this method.

Supported countries: `Turkey`

Supported currencies: `TRY`

### Manual Peppara Withdraw

This method is used to make a withdrawal to a specified bank account. <br/>
Please make sure to enable BESTPAYMANUALPEPPARA in Rules -> Payment Methods for the account that should use this method.

Also, please make sure to configure MWALLET_PEPPARA in MerchantConfig:
<details>
<summary>Click to view MerchantConfig</summary>
<br/>

```xml
<entry>
   <string>BESTPAYMANUALPEPPARA</string>
   <string>...|MWALLET_PEPPARA</string>
</entry>
```
</details>

Additionally, Cashier Payment Method-settings has to be configured. Please contact
our technical support to make changes in this file to enable this method.

NOTE! The account has to be in the format of 9 digits - 4 digits, eg. 123456789-1234.
For the best user experience, please configure the frontend message appearing when the account number proves to be invalid - in Admin → Messages add the following keys:

- manualPeppara.accountNumber.invalid

- manualPeppara.accountNumber.required

The messages should inform the user about the account number format that needs to be entered, eg. "The account number has to be in format 9 digits - 4 digits, for example: 123456789-1234. Please try again."

Supported countries: `Turkey`

Supported currencies: `TRY`

#### Transaction Flow

1. The user enters the amount to withdraw along with the bank account number and chooses a BIC code from the dropdown menu in the cashier
   - for convenience only PAPARA is available as per the provider's request.
2. PaymentIQ sends a token request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction and its type.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Crypto Withdraw

This method is used to make a cryptocurrency withdrawal to a specific wallet address <br/>
Please make sure to enable CRYPTOCURRENCY in Rules -> Payment Methods for the account that should use this method.

Additionally, Cashier Payment Method-settings has to be configured. Please contact
our technical support to make changes in this file to enable this method.

Supported countries: `All`

Supported currencies: `EUR`

Supported cryptocurrencies: `BTC`, `BCH`, `XDG`, `ETH`, `LTC`, `USDT`, `XRP`


#### Transaction Flow

1. The user enters the amount to withdraw, the wallet address and additionally the destination tag (requred for XRP only) and selects the cryptocurrency in the cashier.
2. PaymentIQ sends a token request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction and its type.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

#### NOTE
The amounts can not be lower than: <br/>
ETHERIUM: 0.01 ETH <br/>
BITCOIN: 0.006 BTC <br/>
TETHER:15 USDT <br/>
RIPPLE: 30 XRP <br/>
LITECOIN: 0.01 LTC <br/>
BITCOIN CASH: 0.001 BTC <br/>
DOGE: 50 <br/>

### Indian NetBanking Withdraw

This method is used to make a bank withdrawal to a specific account number. <br/>
Please make sure to enable BESTPAYNETBANKING in Rules -> Payment Methods for the account that should use this method.

Additionally, Cashier Payment Method-settings has to be configured. Please contact
our technical support to make changes in this file to enable this method.

Supported countries: `India`

Supported currencies: `INR`

#### Transaction Flow

1. The user enters the amount to withdraw along with the account number and IFSC Code.
2. PaymentIQ sends a token request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction and its type.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched if the transaction
   was not automatically approved or declined in the PSP response mentioned in point 3.

### Interac Withdraw

This method is used to make a bank withdrawal to a specific account number. <br/>
You will need to use `BankDirectWithdrawal` tx type and to do so, you will need to have `BANKDIRECT` enabled in the Rules -> Payment Methods for the account that should use this method.

Additionally, Cashier Payment Method-settings has to be configured. Please contact
our technical support to make changes in this file to enable this method.

Supported countries: `Canada`

Supported currencies: `CAD`

#### Transaction Flow

1. The user enters the amount to withdraw along with the national id, account number, account transit number
   and financial institution number.
2. PaymentIQ sends a token request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction and its type.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched if the transaction
   was not automatically approved or declined in the PSP response mentioned in point 3.

### NetBanking IDR Withdraw

This method is used to make a bank withdrawal to a specific account number. <br/>
Please make sure to enable BESTPAYNETBANKINGIDR in Rules -> Payment Methods for the account that should use this method.

Additionally, Cashier Payment Method-settings has to be configured. Please contact
our technical support to make changes in this file to enable this method.

Supported countries: `Indonesia`

Supported currencies: `IDR`

It is also necessary to populate the Bank Mapping table in Admin -> Bank Mapping in PaymentIQ's backoffice
for the merchant using this method with the values below.
The bank codes can be found under https://developers.luqapay.com/docs/netbanking-idr-withdraw and branch code will
always be set to "Asia" for this method.
Please contact our technical support to configure the mapping if you want to enable this method.

<details>
<summary>Click to view bank_mappings.xml</summary>
<br/>

```xml
<list>
   <bankMapping>
      <name>BANK DANAMON</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK DANAMON</bankName>
      <bankCode>011</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BNI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BNI</bankName>
      <bankCode>009</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>MANDIRI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>MANDIRI</bankName>
      <bankCode>008</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BRI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BRI</bankName>
      <bankCode>002</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK WINDU</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK WINDU</bankName>
      <bankCode>036</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>CITIBANK</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>CITIBANK</bankName>
      <bankCode>031</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK OCBC NISP</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK OCBC NISP</bankName>
      <bankCode>028</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK UOB</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK UOB</bankName>
      <bankCode>023</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>CIMB NIAGA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>CIMB NIAGA</bankName>
      <bankCode>022</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK PANIN</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK PANIN</bankName>
      <bankCode>019</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>MAYBANK INDONESIA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>MAYBANK INDONESIA</bankName>
      <bankCode>016</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BCA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BCA</bankName>
      <bankCode>014</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK PERMATA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK PERMATA</bankName>
      <bankCode>013</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK BUMI ARTHA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK BUMI ARTHA</bankName>
      <bankCode>076</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK OF CHINA INDONESIA (BOCI)</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK OF CHINA INDONESIA (BOCI)</bankName>
      <bankCode>069</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>ANZ</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>ANZ</bankName>
      <bankCode>061</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK CAPITAL</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK CAPITAL</bankName>
      <bankCode>054</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>STANCHAR</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>STANCHAR</bankName>
      <bankCode>050</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK DBS</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK DBS</bankName>
      <bankCode>046</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK OF TOKYO</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK OF TOKYO</bankName>
      <bankCode>042</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>HSBC</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>HSBC</bankName>
      <bankCode>041</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK ARTHA GRAHA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK ARTHA GRAHA</bankName>
      <bankCode>037</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>RABOBANK</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>RABOBANK</bankName>
      <bankCode>089</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK ANDA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK ANDA</bankName>
      <bankCode>088</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>EKONOMI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>EKONOMI</bankName>
      <bankCode>087</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK JATIM</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK JATIM</bankName>
      <bankCode>114</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK JATENG</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK JATENG</bankName>
      <bankCode>113</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BPD DIY</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BPD DIY</bankName>
      <bankCode>112</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK DKI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK DKI</bankName>
      <bankCode>111</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK BJB</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK BJB</bankName>
      <bankCode>110</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>MAYAPADA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>MAYAPADA</bankName>
      <bankCode>097</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>JTRUST BANK</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>JTRUST BANK</bankName>
      <bankCode>095</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK IFI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK IFI</bankName>
      <bankCode>093</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK KALTENG</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK KALTENG</bankName>
      <bankCode>125</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BPD KALTIM</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BPD KALTIM</bankName>
      <bankCode>124</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BPD KALBAR</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BPD KALBAR</bankName>
      <bankCode>123</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK KALSEL</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK KALSEL</bankName>
      <bankCode>122</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK LAMPUNG</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK LAMPUNG</bankName>
      <bankCode>121</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK SUMSELBABEL</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK SUMSELBABEL</bankName>
      <bankCode>120</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK RIAU</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK RIAU</bankName>
      <bankCode>118</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK NAGARI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK NAGARI</bankName>
      <bankCode>118</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BPD SUMUT</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BPD SUMUT</bankName>
      <bankCode>117</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK ACEH</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK ACEH</bankName>
      <bankCode>116</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK JAMBI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK JAMBI</bankName>
      <bankCode>115</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK SULTENG</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK SULTENG</bankName>
      <bankCode>134</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK BENGKULU</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK BENGKULU</bankName>
      <bankCode>133</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BPD PAPUA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BPD PAPUA</bankName>
      <bankCode>132</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK MALUKU</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK MALUKU</bankName>
      <bankCode>131</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK NTT</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK NTT</bankName>
      <bankCode>130</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BPD BALI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BPD BALI</bankName>
      <bankCode>129</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK NTB</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK NTB</bankName>
      <bankCode>128</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK SULUT</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK SULUT</bankName>
      <bankCode>127</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK SULSEL</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK SULSEL</bankName>
      <bankCode>126</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK SINARMAS</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK SINARMAS</bankName>
      <bankCode>153</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK MESTIKA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK MESTIKA</bankName>
      <bankCode>151</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK MUAMALAT</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK MUAMALAT</bankName>
      <bankCode>147</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK OF INDIA INDONESIA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK OF INDIA INDONESIA</bankName>
      <bankCode>146</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BNP</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BNP</bankName>
      <bankCode>145</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK SULTRA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK SULTRA</bankName>
      <bankCode>135</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK QNB</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK QNB</bankName>
      <bankCode>167</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK ICBC INDONESIA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK ICBC INDONESIA</bankName>
      <bankCode>164</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK GANESHA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK GANESHA</bankName>
      <bankCode>161</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK MASPION</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK MASPION</bankName>
      <bankCode>157</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK BUKOPIN</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK BUKOPIN</bankName>
      <bankCode>441</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK MEGA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK MEGA</bankName>
      <bankCode>426</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BJB SYARIAH</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BJB SYARIAH</bankName>
      <bankCode>425</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK BRI SYARIAH (BRIS)</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK BRI SYARIAH (BRIS)</bankName>
      <bankCode>422</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK VICTORIA SYARIAH</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK VICTORIA SYARIAH</bankName>
      <bankCode>405</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>KOPERASI INTIDANA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>KOPERASI INTIDANA</bankName>
      <bankCode>333</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BTPN</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BTPN</bankName>
      <bankCode>213</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK WOORI SAUDARA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK WOORI SAUDARA</bankName>
      <bankCode>212</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK BTN</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK BTN</bankName>
      <bankCode>200</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK BYB</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK BYB</bankName>
      <bankCode>490</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>MNC BANK</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>MNC BANK</bankName>
      <bankCode>485</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK HANA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK HANA</bankName>
      <bankCode>484</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK JASA JAKARTA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK JASA JAKARTA</bankName>
      <bankCode>472</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BSM</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BSM</bankName>
      <bankCode>451</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK INA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK INA</bankName>
      <bankCode>513</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BSMI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BSMI</bankName>
      <bankCode>506</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>NOBUBANK</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>NOBUBANK</bankName>
      <bankCode>503</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK ROYAL IND</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK ROYAL IND</bankName>
      <bankCode>501</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK INDOMONEX</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK INDOMONEX</bankName>
      <bankCode>498</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>ATM AGRO</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>ATM AGRO</bankName>
      <bankCode>494</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>B.KES.EKONOMI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>B.KES.EKONOMI</bankName>
      <bankCode>535</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK DINAR</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK DINAR</bankName>
      <bankCode>526</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK BARCLAY</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK BARCLAY</bankName>
      <bankCode>525</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK S.SAMPOERNA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK S.SAMPOERNA</bankName>
      <bankCode>523</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK SYARIAH BUKOPIN</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK SYARIAH BUKOPIN</bankName>
      <bankCode>521</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK PANIN SYARIAH</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK PANIN SYARIAH</bankName>
      <bankCode>517</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK VICTORIA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK VICTORIA</bankName>
      <bankCode>566</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK CNB</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK CNB</bankName>
      <bankCode>559</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK PUNDI</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK PUNDI</bankName>
      <bankCode>558</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK INDEX</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK INDEX</bankName>
      <bankCode>555</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK MAYORA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK MAYORA</bankName>
      <bankCode>553</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK MAS</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK MAS</bankName>
      <bankCode>548</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BTPN SYARIAH</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BTPN SYARIAH</bankName>
      <bankCode>547</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK ARTOS</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK ARTOS</bankName>
      <bankCode>542</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BCA SYARIAH</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BCA SYARIAH</bankName>
      <bankCode>536</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>ARTAJASA/ATMB PLUS</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>ARTAJASA/ATMB PLUS</bankName>
      <bankCode>987</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>COMMBANK</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>COMMBANK</bankName>
      <bankCode>950</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>CTBC INDONESIA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>CTBC INDONESIA</bankName>
      <bankCode>949</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK AGRIS</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK AGRIS</bankName>
      <bankCode>945</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>TELKOMSEL (TCASH)</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>TELKOMSEL (TCASH)</bankName>
      <bankCode>911</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>DOKU</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>DOKU</bankName>
      <bankCode>899</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK EKA BUMI ARTHA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK EKA BUMI ARTHA</bankName>
      <bankCode>867</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>INDOSAT (DOMPETKU)</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>INDOSAT (DOMPETKU)</bankName>
      <bankCode>789</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>SGDOPAY</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>FINNET</bankName>
      <bankCode>777</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>SGDOPAY</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>SGDOPAY</bankName>
      <bankCode>775</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>ALTOPAY</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>ALTOPAY</bankName>
      <bankCode>770</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BPR KS</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BPR KS</bankName>
      <bankCode>688</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>LSB (LEMBAGA SELAIN BANK) /BPR</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>LSB (LEMBAGA SELAIN BANK) /BPR</bankName>
      <bankCode>600</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
   <bankMapping>
      <name>BANK HARDA</name>
      <currencyCode>IDR</currencyCode>
      <countryCode>IDN</countryCode>
      <bankName>BANK HARDA</bankName>
      <bankCode>567</bankCode>
      <branchCode>Asia</branchCode>
   </bankMapping>
</list>
```
</details>

This data will be used to assign a bank code and a branch code to the bank name provided by the user in the cashier.

#### Transaction Flow

1. The user enters the amount to withdraw as well as the account number and selects a bank name from the drop-down list.
   Based on the bank name's selection, other input data (bank code and branch code) will be populated by searching the
   aforementioned Bank Mapping table. For example: if the user chooses BANK HARDA, bank code will be set to 567 and branch
   code will be set to "Asia".
2. PaymentIQ sends a token request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction and its type.
4. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched if the transaction
   was not automatically approved or declined in the PSP response mentioned in point 3.

### Bank Transfer Withdraw - Norway

This method is used to make a withdrawal to a specified bank account.<br/>
Please make sure to enable BESTPAYIBAN in Rules -> Payment Methods for the account that should use this method.

Additionally, an html template has to be added in the backoffice. Please contact our technical support to add the template
should you want to enable this payment method.

Supported countries: `Norway`

Supported currencies: `NOK`

#### Transaction Flow

1. The user enters the amount to withdraw along with the IBAN number.
2. PaymentIQ sends a token request to BestPay/Luqapay. Note that the "APPROVED" status in this response does not make the transaction successful.
3. After receiving the token, PaymentIQ sends a request for available banks to the PSP.
4. The user gets redirected to the html page with the available banks listed out and clicks on a bank.
5. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction and its type.
6. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Bank Transfer Withdraw -  Japan

Enable BESTPAYTRANSFER withdrawal option in Rules -> Payment Methods<br/>
For routing, use the TxType: `BestPayBankTransferWithdrawal`

Supported countries: `Japan`<br/>
Supported currencies: `JPY`

Please see [Front API](https://docu-portal.paymentiq.io/docs/apis_and_integration/front_api/Banking#luqapay-formerly-bestpay) for necessary parameters.

#### Transaction Flow

1. The user enters the amount to withdraw along with the account number and branch code.
2. PaymentIQ sends a token request to BestPay/Luqapay.<br/>Note that the "APPROVED" status in this response does not make the transaction successful.
3. After receiving the token, PaymentIQ sends a request for available banks to the PSP.
4. The user gets redirected to the html page with the available banks listed out and clicks on a bank.
5. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction and its type.
6. BestPay/Luqapay sends a callback with the transaction status, then the status check chain is launched.

### Bank Transfer VIP Withdraw - Japan

 - **MerchantConfig:**<br/>Add a service named "VIP_WITHDRAWAL_JP" to the "BANKLOCAL" entry in `<serviceMapping>` in MerchantConfig.<br/>
 *This service will be used in _Payment methods_
 - **Payment Methods:**<br/> Set "BANKLOCAL-VIP_WITHDARAL_JP" for the _Withdrawal methods_ in _Actions_ section<br/>
 - **Routing:**<br/> Use the TxType: `BankLocalWithdrawal`<br/>
  _Actions_ section should be enhanced with condition: `PSP version : VIP`

Supported countries: `Japan`<br/>
Supported currencies: `JPY`

Please see [Front API](https://docu-portal.paymentiq.io/docs/apis_and_integration/front_api/Banking#banklocalwithdrawal-2) for necessary parameters.

#### Transaction Flow

1. The user enters the amount to withdraw, bank name, clearing number (combination of 4-digit bank code and 3-digit branch code), bank branch name, account number, full name and full name in local language (Either Hiragana or Katakana, no Kanji).
2. PaymentIQ sends a token request to BestPay/Luqapay.<br/>
3. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction.
4. BestPay/Luqapay sends a callback with the transaction status.

#### Example Routing Rule for Bank Transfer VIP Withdraw - Japan
![](/img/providers/routing/bestpayrules_vip_jp.png)

### Bank Transfer VIP Withdraw - (except of Japan)

- **MerchantConfig:**<br/>Add a service named "VIP_WITHDRAWAL" to the "BANKIBAN" entry in `<serviceMapping>` in MerchantConfig.<br/>
  *This service will be used in _Payment methods_
- **Payment Methods:**<br/> Set "BANKLOCAL-VIP_WITHDRAWAL" for the _Withdrawal methods_ in _Actions_ section<br/>
- **Routing:**<br/> Use the TxType: `BankIBANWithdrawal`<br/>
  _Actions_ section should be enhanced with condition: `PSP version : VIP`

Supported countries (codes): `AE, BG, CH, CZ, DK,GB, HU, KW, NO, PE, PL, RO, SE, TR`<br/>
Supported currencies: `AED, BGN, CHF, CZK, DKK, EUR, GBP, HUF, KWD, NOK, PEN, PLN, RON, SEK, TRY`

Please see [Front API](https://docu-portal.paymentiq.io/docs/apis_and_integration/front_api/Banking#bankibanwithdrawal-2) for necessary parameters.

#### Transaction Flow

1. The user enters the amount to withdraw, bank name, swift code, iban, full name.
2. PaymentIQ sends a token request to BestPay/Luqapay.<br/>
3. Once the transaction has been approved in PaymentIQ's backoffice, a "withdraw" request is sent to the PSP and the PSP returns a response
   with the current status of the transaction.
4. BestPay/Luqapay sends a callback with the transaction status.

#### Example Routing Rule for Bank Transfer VIP Withdraw - (except of Japan)
![](/img/providers/routing/bestpayrules_vip.png)

## Example Routing Rule
![](/img/providers/routing/bestpayrules.png)

## Test Information
### Community Bank Deposit
The user's country code must be TR for Turkey, NO for Norway or JP for Japan. It is also important that the currencies
match the countries, therefore please use TRY for Turkey, NOK for Norway and JPY for Japan.
Only these three counties are enabled to use this payment method.

### Credit Card Deposit
| Card Number      | CVV | Expiry Date | Currency |
|------------------|-----|-------------|----------|
| 4012888888881881 | 123 | 12/25       | EUR      |

### Crypto via Credit Card
| Card Number      | CVV | Expiry Date | Currency |
|------------------|-----|-------------|----------|
| 5500000000000004 | 123 | 12/25       | EUR      |

### Voucher via Credit Card Deposit
CC-Voucher payment method is voucher based credit card solution. It allows end-users to utilised voucher payments by doing deposits through credit cards.

The account config should have the following to activate this solution through LuqaPay: ```<piqVersion>CCVOUCHER</piqVersion>```

### Withdrawal
#### BankIBANWithdrawal
* iban: TR250003200000000052779305
