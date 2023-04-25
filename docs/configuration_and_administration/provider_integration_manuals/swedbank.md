--- 
id: "swedbank" 
title: "Swedbank"
hide_title: "true"
---
 
![](/img/providers/logos/swedbank.png)

# Swedbank

## About
Swedbank is a international bank.

| Provider Name                | Swedbank                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Product                      | Swedbank                                                                        |
| Link                         | [https://www.swedbank.com/](https://www.swedbank.com/)                          |
| Classification               | Bank                                                                            |
| Regions                      | `International`                                                                 |
| Supported countries          | `SWE`, `LVA`                                                                    |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `BankLocalWithdrawal`, `BankIBANWithdrawal`, `BankIntlWithdrawal`,`BankDeposit` |
| PaymentIQ Configuration File | `SwedbankConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.swedbank.SwedbankConfig>
  <enabled>true</enabled>
  <kafkaTopic>???</kafkaTopic>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <supportedCurrencies>SEK|EUR</supportedCurrencies>
        <originatorBankAccount>???</originatorBankAccount>
        <templateName>???</templateName>
      </account>
    </entry>
    <entry>
      <string>multibanklink_lv</string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <container>window</container>
        <countryCode>LV</countryCode>
        <merchantId>????</merchantId>
        <pspPrivateKey>-----BEGIN RSA PRIVATE KEY-----
        ????
        -----END RSA PRIVATE KEY-----</pspPrivateKey>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>
    PaymentIQ test \${ptx.txRefId} tx id
  </defaultDescriptor>
</com.devcode.paymentiq.integration.swedbank.SwedbankConfig>
```
</details>

### Attributes

| Attribute                  | Description                                                                                                         |
|----------------------------|---------------------------------------------------------------------------------------------------------------------|
| kafkaTopic                 | piq.batch.swedbank.lv (LVA) or piq.batch.swedbank (default)                                                         |
| originatorBankAccount      | The bank account to transfer money from                                                                             |
| templateName               | swedbank_latvia_kafka for example for swedbank latvia (LVA)                                                         |
| defaultDescriptor          | A description of the transaction. Kan include template expressions like ${ptx.txRefId}                              |
| characterConversionEnabled | if invalid characters should be converted                                                                           |
| characterConversionTable   | A table of characters to replace and what to replace it with                                                        |
| pspPrivateKey              | Merchant creates private key and send a public key to Swedbank                                                      |
| merchantId                 | Merchant indentifier at Swedbank (provided by Swedbank SND_ID)                                                      |
| countryCode                | Swedbank country (Right now only LV is supported)                                                                   |
| vkRefFieldMapping          | Mapping of the VK_REF `UNLALV2X->\${ptx.id},*->\${ptx.txRefId}` to send for each bank code. Ex:  (default is empty) |

### Deposit name matching
Name matching between the merchant user name and the name from Swedbank's redirect. If the names don't match the transaction will be set to the state INCONSISTENT and status code ERR_NAME_MISMATCH. The feature is enabled by adding the following setting to top or account level in SwedbankConfig:

`<matchAccountHolderName>true</matchAccountHolderName>`

It's possible to ignore the name matching for specific banks. This feature is used by adding the bank names of the banks to ignore in the config setting `ignoreNameMatchingForBanks`, for example:

`<ignoreNameMatchingForBanks>BANK1|BANK2</ignoreNameMatchingForBanks>`

## Withdrawal batch processing

### Latvia (LVA)
Specific information about Swedbank Latvia.

#### Flow
A user requests a withdrawal.
- The merchant approves the withdrawal
- The withdrawal is published to kafka queue
- The Swedbank Latvia job will fetch all messages in queue and processes them
- The job will produce a txt file of all tx that matches Swedbank Latvias import file format
- The merchant will get this txt file to its selected email address and is ready to be imported into bank

#### Template

Templates are setup in PaymentIQ Backoffice under Admin -> Templates -> MQ Templates.

<details>
<summary>Click to view example template</summary>
<br/>

```json
{
    "merchantId": ${btx.merchantId},
    "txRefId": "${btx.txRefId}",
    "amount": "${btx.amount}",
    "currency": "${btx.currency}",
    "descriptor": "${btx.descriptor}",
    "txType": "${btx.txType}"${if btx.bankAccount},
    "bankAccount": {
        ${if btx.bankAccount.accountHolder}
        "accountHolder": {
          ${if btx.bankAccount.accountHolder.name}"name": "${btx.bankAccount.accountHolder.name}",${end}
          ${if btx.bankAccount.accountHolder.nationalIdentityNumber}"nationalIdentityNumber": "${btx.bankAccount.accountHolder.nationalIdentityNumber}"${end}
          chompLast<<,>>
        },
        ${end}
        ${if btx.bankAccount.bankName}"bankName": "${btx.bankAccount.bankName}",${end}
        ${if btx.bankAccount.accountNumber}"accountNumber": "${btx.bankAccount.accountNumber}",${end}
        ${if btx.bankAccount.bankCode}"bankCode": "${btx.bankAccount.bankCode}",${end}
        ${if btx.bankAccount.iban}"iban": "${btx.bankAccount.iban}",${end}
        ${if btx.bankAccount.bic}"bic": "${btx.bankAccount.bic}"${end}
    },
    ${end}
    ${if btx.originatorBankAccount}
    "originatorBankAccount": {
        ${if btx.originatorBankAccount.accountNumber}"accountNumber": "${btx.originatorBankAccount.accountNumber}"${end}
    }
    ${end}
    chompLast<<,>>
}
```

</details>

#### National identification number
The national identity number is required so it can be provided in the verify user response in the attributes field `nationalIdentificationNumber`.

#### Example Routing Rule
![](/img/providers/routing/swedbank_lv_batch.png)

### Testing
No test information is available.

### BankDeposit (Multibanklink)

#### Certificate
The merchant and the bank has to exchange certificates. The merchant has to generate a private rsa certificate and then generate a public key that must be sent to the bank. 
Contact Swedbank or technical support for more information how to generate the certificate. 

Then text content of the private rsa certificate must then be added to the SwedbankConfig on the pspPrivateKey attribute of the account.

#### Banks
The supported banks right now are two banks. SEB and Swedbank in Latvia.

| Bank     | BankDeposit bankName param value |
|----------|----------------------------------|
| Swedbank | HABALV22                         |
| SEB      | UNLALV2X                         |

#### Flow

1. The user selects one of the two banks and enter the amount
    1. If no bank is selected then Swedbank will be used.
2. The user is redirected to the selected bank
3. The user logs in into bank and enter payment details.
4. When done bank will redirect to PaymentIQ that will check the bank status.
5. The user is redirected to merchants success / failure / cancel pages. 

#### Example Routing Rule
![](/img/providers/routing/swedbank_lv.png)

#### Testing
Can only be tested live.
