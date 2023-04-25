--- 
id: "gamersbank"
title: "GamersBank"
hide_title: "true"
---

![](/img/providers/logos/gamersbank.png)

# GamersBank - GamersCard & GamersPay

## About
GamersBank has two products: GamersPay and GamersCard.
GamersPay is dedicated to online banking (PIX Deposit and PIX Withdrawal), whilst GamersCard is a credit card processor (Creditcard Deposit and Creditcard Withdrawal).

| Provider Name                | GamersBank                                                                                         |
|------------------------------|----------------------------------------------------------------------------------------------------|
| Link                         | [https://gamerswallet.com.br/](https://gamerswallet.com.br)                                        |
| Classification               | Online Banking <br/> Debit/Credit Card Processor                                                   |
| Regions                      | `Brazil`                                                                                           |
| Currencies                   | `USD`                                                                                              |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawal` <br/> `PixDeposit` <br/> `BankDomesticWithdrawal` |
| PaymentIQ Configuration File | `GamersBankConfig`                                                                                 |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.gamersbank.GamersBankConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <testMode>true</testMode>
    <container>window</container>
    <accounts>
        <entry>
            <string>gamerscard</string>
            <account>
                <use3Dsecure>false</use3Dsecure>
                <merchantId>???</merchantId>
                <supportedCurrencies>USD</supportedCurrencies>
                <apiKey>???</apiKey>
                <password>???</password>
            </account>
        </entry>
        <entry>
            <string>gamerspay</string>
            <account>
                <merchantId>???</merchantId>
                <supportedCurrencies>USD</supportedCurrencies>
                <forceCountryCode>BR</forceCountryCode>
                <username>???</username>
                <password>???</password>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.gamersbank.GamersBankConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                                                                                                 |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| use3Dsecure         | 3DSecure is not required (mandatory 'false')                                                                                                                                |
| merchantId          | Merchant's id issued by GamersBank                                                                                                                                          |
| supportedCurrencies | GamersBank supported currencies                                                                                                                                             |
| apiKey              | API key provided by GamersBank, needed only for Creditcard Deposit/Withdrawal. It will be a different apiKey for each merchant.                                             |
| forceCountryCode    | Account level parameter that can be used to set non user country code. In case it is blank or missing, user's country will be used.                                         |
| username            | For `gamersbank_pix` it's the client id that together with client secret key would generate the token. It will be provided by provider.                                     |
| password            | For `gamersbank_card` account it is the user password. <br/> For `gamersbank_pix` it's the client secret key needed to retrieve the token. It will be provided by provider. |


## Provider Configuration
1. The above XML template (GamersBankConfig) will need to be added via backoffice Admin -> Configuration.
2. Routing needs to be added for CreditcardDeposit, CreditcardWithdrawal, PixDeposit and BankDomesticWithdrawal in **Routing -> Routing**.

### Payment Method Mapping

| Country | Payment Method | Payment Type | PaymentIQ Service | PaymentIQ tx type      | Comment                                  |
|---------|----------------|--------------|-------------------|------------------------|------------------------------------------|
| BR      | PIX            | Deposit      | -                 | PixDeposit             | Online banking in Brazil                 |
| BR      | PIX            | Withdrawal   | PIX               | BankDomesticWithdrawal | Local bank transfer withdrawal in Brazil |


## Example Routing Rule

![](/img/providers/routing/gamersbank.png)

## Transaction Flow

### Creditcard operations
1. The end user fills in the transaction amount and card details.
2. PaymentIQ sends the deposit/withdrawal request to GamersBank.
3. GamersBank sends a response with the final status of the transaction.

### PIX operations
1. The end user fills in the transaction amount and national id(cpf).
2. PaymentIQ sends the deposit/withdrawal request to GamersBank.
3. GamersBank sends a response with initial status of transaction + redirect url.
4. User is redirected in order to complete the payment(for Pix Deposit just confirming/ for Pix Withdrawal the user also needs to fill in bank account details).
5. GamersBank sends a callback notification once the transaction status is updated on their side.

## Test Information

### Creditcard Operations

| Card number      | CVV | Brand      | Password | Expiry date | Scenario |
|------------------|-----|------------|----------|-------------|----------|
| 5292050400000114 | 123 | MasterCard | PS1234   | 07/23       | Success  |
| 5292050400000080 | 123 | MasterCard | PS1234   | 07/23       | Success  |


### PIX Operations

| Name                                | Email                                   | CPF         | Scenario |
|-------------------------------------|-----------------------------------------|-------------|----------|
| Breno Miguel Marcos Vinicius Araújo | breno-araujo74@portalpublicidade.com.br | 72741715858 | Success  |
| Henrique Bento Murilo Cavalcanti    | henrique-cavalcanti98@openlink.com.br   | 39973394909 | Failure  |

![](/img/providers/gamersbank_pix_deposit.png)
