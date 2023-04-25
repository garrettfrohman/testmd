--- 
id: "payper" 
title: "Payper"
hide_title: "true"
---

![](/img/providers/logos/payper.png)

# Payper

## About
Payper is a leading payment option for Canadian players. The Deposit and withdrawal options include Interac e-Transfers, Interac Online, real-time bank payments, EFTs, OCT (Visa Direct, MasterCard Send), and a Digital Cash Card option.

Payper’s exclusive Interac e-Transfer option allow merchants to customize the customer payment experience.  Online banking payment provides real-time open banking payments and withdrawals.  Digital Cash Card is used to send digital cash for immediate e-gift card redemption.

| Provider Name                | Payper                                                                                                    |
|------------------------------|-----------------------------------------------------------------------------------------------------------|
| Link                         | [https://payper.ca/](https://payper.ca/)                                                                  |
| Classification               | Aggregator                                                                                                |
| Regions                      | `Canada`                                                                                                  |
| Currencies                   | `CAD`                                                                                                     |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `WebRedirectWithdrawal` <br/> `BankDirectDeposit` <br/> `BankDirectWithdrawal` |
| PaymentIQ Configuration File | `PayperConfig`                                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.payper.PayperConfig>
  <enabled>true</enabled>
  <validCallbackIpAddresses>??|??</validCallbackIpAddresses>
  <useViqProxy>true</useViqProxy>
  <container>window</container>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <productName>??</productName>
        <apiToken>??</apiToken>
        <pspPublicKey>-----BEGIN PUBLIC KEY----- 
        XXXXXXXXXXXXX 
        -----END PUBLIC KEY-----</pspPublicKey>
        <encryptionKeysId>??</encryptionKeysId>
        <supportedCurrencies>CAD</supportedCurrencies>
        <secretKey>??</secretKey>
        <sessionId>??</sessionId>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.payper.PayperConfig>
```

</details>

### Attributes

| Attribute                              | Description                                                                                                                                                                                                                                                                     |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| validCallbackIpAddresses               | Mandatory. The list of Payper IP addresses from which the callbacks are expected separated by '&#124;' (pipe character) - f.ex. <validCallbackIpAddresses>127.0.0.1&#124;127.0.0.2</validCallbackIpAddresses>. The list of IPs should be provided by Payper                     |
| useViqProxy                            | Mandatory set to true. It is used to make sure that the credit card details are properly decrypted/encrypted in VaultIQ before sending the request to Payper                                                                                                                    |
| container                              | Mandatory - should be set to 'window' for the best user experience (recommended by Payper)                                                                                                                                                                                      |
| account.productName                    | Mandatory. Your product description that will be visible in Payper's system and in the user's bank statements                                                                                                                                                                   |
| account.apiToken                       | Mandatory. It is used to secure the requests sent to Payper and provided by Payper to populate in your configuration                                                                                                                                                            |
| account.pspPublicKey                   | Mandatory. It is used to secure the requests sent to Payper. To get it, please follow section 'Obtaining public key and encryption key id' in this manual                                                                                                                       |
| account.encryptionKeysId               | Mandatory. It is used to secure the requests sent to Payper. To get it, please follow section 'Obtaining public key and encryption key id' in this manual                                                                                                                       |
| account.supportedCurrencies            | Payper only works with CAD, therefore please make sure to set this param to CAD or convert your transaction amount to CAD beforehand                                                                                                                                            |
| account.secretKey                      | Mandatory. It is used to secure the requests sent to Payper and provided by Payper to populate in your configuration                                                                                                                                                            |
| account.sessionId                      | Mandatory. It is used to secure the requests sent to Payper and provided by Payper to populate in your configuration                                                                                                                                                            |
| account.testMode                       | Should be set to true only for test environment                                                                                                                                                                                                                                 |
| account.shouldUseInternalBankSelection | Optional. It works with eTransfer deposits and can be enabled if you wish the user to be redirected to a PaymentIQ html page with a bank selection - if it's not set or set to false the user will get redirected to a hosted Payper page where the bank selection is available |

### Obtaining public key and encryption key id

Obtaining public key and encryption key id should be the first step of enabling Payper as your payment service provider, 
as these fields have to be populated in your PayperConfig file in order for the integration to work properly.

In order to retrieve these credentials, please follow these steps:

1. Make sure you know your merchantId in PaymentIQ - you need to place it in your request where `{merchantId}` is located.
2. Make sure that you get your apiToken from Payper - it has to be placed in the header of the request where `{apiToken}` is located.
3. Send the following request to your respective environment:

For test environment (make sure that isTest=true):

```
curl --request GET \
     --url https://test-api.paymentiq.io/paymentiq/payper/rsa?isTest=true&merchantId={merchantId} \
     --header 'Accept: application/json' \
     --header 'Authorization: Bearer {apiToken}'
```

For live environment (make sure that isTest=false):

```
curl --request GET \
     --url https://api.paymentiq.io/paymentiq/payper/rsa?isTest=false&merchantId={merchantId} \
     --header 'Accept: application/json' \
     --header 'Authorization: Bearer {apiToken}'
```

4. In case of a successful request you will receive the following response:

```
{
  "errors": [],
  "key_id": 1000,
  "public_key": "-----BEGIN PUBLIC KEY-----\nMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCcwFaDLXSDn63b5RbLUk6M77pP\nDB8iGk0vxdnoujprEYzzeE5ehtItdmOQyogscf+AVAEL8LpKdgst7LLWR39rdfud\ngpOdj0t0LA5bFpufv8S1e8UrQF9XvZlSPa5wzFvo0SD7B1eLF4AHojFyM37ASg2t\nknPpCG8icxk+GjY3xQIDAQAB\n-----END PUBLIC KEY-----",
  "status": true
}
```

A failed response would result in a 4XX or 5XX server response - in case that happens please contact PaymentIQ tech support.

5. Grab the "key_id" field value and populate it as the "encryptionKeysId" parameter in your PayperConfig.
6. Grab the "public_key" field value and populate it as the "pspPublicKey" parameter in your PayperConfig. Please make sure
that you replace every `\n` with a new line (enter). <br/>
A properly populated "pspPublicKey" parameter using the "public_key" from the example above should look exactly like this:

```
<pspPublicKey>-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCcwFaDLXSDn63b5RbLUk6M77pP
DB8iGk0vxdnoujprEYzzeE5ehtItdmOQyogscf+AVAEL8LpKdgst7LLWR39rdfud
gpOdj0t0LA5bFpufv8S1e8UrQF9XvZlSPa5wzFvo0SD7B1eLF4AHojFyM37ASg2t
knPpCG8icxk+GjY3xQIDAQAB
-----END PUBLIC KEY-----</pspPublicKey>
```

## Provider Configuration

For all the payment methods, please make sure to follow these steps to configure Payper:

1. Run PaymentIQ and add the aforementioned PayperConfig under Admin -> Configuration.
2. Add Payper to the `<psp>` section in MerchantConfig under Admin -> Configuration.

The additional steps that are required for each method will be described further on in this manual.

### e-Transfer Payment
This method is used to receive deposits.

#### Configuration
Additional configuration:

1. Enable WEBREDIRECT-ETRANSFER deposit method in Rules -> Payment methods.
2. If your accountConfig.shouldUseInternalBankSelection is present and set to true, a `payper-etransfer-select-bank` html template is required - please contact PaymentIQ
tech support to make sure it is available for your MID. By default it is not required, as the user will be redirected to a hosted Payper page where the bank selection takes place.

#### Transaction flow

#### With accountConfig.shouldUseInternalBankSelection present and set to true
1. The user enters the amount to be deposited in the cashier and clicks on "deposit".
2. PaymentIQ sends a request to Payper to obtain a list of banks available for that method.
3. On a successful response from Payper, PaymentIQ redirects the user to a PaymentIQ html page with all the available banks displayed. The user then 
chooses clicks on a chosen bank.
4. PaymentIQ sends a deposit request to Payper and expects a response with an url that the user should proceed to.
5. Once the user has completed the flow, PaymentIQ awaits for a callback from Payper with a transaction status - after that
the status check is being performed against Payper API and the transaction gets updated accordingly to the result.

#### With accountConfig.shouldUseInternalBankSelection not populated (default setting) or set to false
1. The user enters the amount to be deposited in the cashier and clicks on "deposit".
2. PaymentIQ sends a request to Payper to obtain a list of banks available for that method.
3. On a successful response from Payper, PaymentIQ redirects the user to a Payper hosted page with all the available banks displayed. The user then
   chooses clicks on a chosen bank.
4. PaymentIQ sends a deposit request to Payper and expects a response with an url that the user should proceed to.
5. Once the user has completed the flow, PaymentIQ awaits for a callback from Payper with a transaction status - after that
   the status check is being performed against Payper API and the transaction gets updated accordingly to the result.

### e-Transfer Payout
This method is used to send withdrawals.

#### Configuration
Additional configuration:

1. Enable WEBREDIRECT-ETRANSFER withdrawal method in Rules -> Payment methods.

#### Transaction flow

1. The user enters the amount to be withdrawn in the cashier and clicks on "withdraw".
2. Once the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends a payout request to Payper. 
3. In case of a successful or pending response, PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION
   and the transfer will be made to deduct the amount from the user's balance.
4. PaymentIQ awaits for a callback from Payper regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the
   user's balance.

### Online Banking Payout
This method is used to send withdrawals.

#### Configuration
Additional configuration:

1. Enable WEBREDIRECT-OB withdrawal method in Rules -> Payment methods.

#### Transaction flow

1. The user enters the amount to be withdrawn in the cashier and clicks on "withdraw".
2. After the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends a payout request to Payper.
3. In case of a successful or pending response, PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION
   and the transfer will be made to deduct the amount from the user's balance.
4. The user receives an email sent by PaymentIQ with an url provided in a successful Payper response to the payout request
   mentioned in point 2 - the user can complete the flow there.
5. PaymentIQ awaits for a callback from Payper regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the
   user's balance.

### Online Banking Payment
This method is used to send deposits.

#### Configuration
Additional configuration:

1. Enable WEBREDIRECT-OB deposit method in Rules -> Payment methods.

#### Transaction flow

1. The user enters the amount to be deposited in the cashier and clicks on "deposit".
2. PaymentIQ sends a deposit request to Payper.
3. On a successful response from Payper, PaymentIQ redirects the user to the url provided in the response to the deposit API call.
4. Once the user has completed the flow, PaymentIQ awaits for a callback from Payper with a transaction status - after that
   the status check is being performed against Payper API and the transaction gets updated accordingly to the result.

### Digital Cheque
This method is used to send deposits.

#### Configuration
Additional configuration:

1. Enable BANKDIRECT-DIGITALCHEQUE deposit method in Rules -> Payment methods.
2. Make sure to provide the following fields in the cashier / via Front API:
- beneficiaryName
- accountNumber
- financialInstitutionNumber
- transitNumber

#### Transaction flow

1. The user enters the amount to be deposited as well as the beneficiary Name, account number, financial institution number and transit number
   in the cashier and clicks on "deposit".
2. PaymentIQ sends a deposit request to Payper.
3. After a response from Payper PaymentIQ proceeds with the status check and updates the transaction status accordingly.
4. In case when after the status check the transaction remains in the WAITING_INPUT state, PaymentIQ awaits a callback from
Payper after which status check is being executed again and the transaction is being updated accordingly to its result.

### Direct Deposit
This method is used to send withdrawals.

#### Configuration
Additional configuration:

1. Enable BANKDIRECT-DIRECTDEPOSIT withdrawal method in Rules -> Payment methods.
2. Make sure to provide the following fields in the cashier / via Front API:
- beneficiaryName
- accountNumber
- financialInstitutionNumber
- transitNumber

#### Transaction flow

1. The user enters the amount to be withdrawn as well as the beneficiary Name, account number, financial institution number and transit number
   in the cashier and clicks on "withdraw".
2. After the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends a payout request to Payper.
3. In case of a successful or pending response, PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION
   and the transfer will be made to deduct the amount from the user's balance.
4. PaymentIQ awaits for a callback from Payper regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the
   user's balance.

### Interac Online
This method is used to send deposits.

#### Configuration
Additional configuration:

1. Enable WEBREDIRECT-INTERAC deposit method in Rules -> Payment methods.

#### Transaction flow

1. The user enters the amount to be deposited in the cashier and clicks on "deposit".
2. PaymentIQ sends a deposit request to Payper.
3. On a successful response from Payper, PaymentIQ redirects the user to the url provided in the response to the deposit API call.
4. Once the user has completed the flow, PaymentIQ awaits for a callback from Payper with a transaction status - after that
   the status check is being performed against Payper API and the transaction gets updated accordingly to the result.

### Digital Cash Card
This method is used to send withdrawals.

#### Configuration
Additional configuration:

1. Enable WEBREDIRECT-DIGITALCASH withdrawal method in Rules -> Payment methods.

#### Transaction flow

1. The user enters the amount to be withdrawn in the cashier and clicks on "withdraw".
2. After the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends a payout request to Payper.
3. In case of a successful or pending response, PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION
   and the transfer will be made to deduct the amount from the user's balance.
4. PaymentIQ awaits for a callback from Payper regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the
   user's balance.

### Visa Direct Payout
This method is used to process credit card withdrawals.

#### Configuration
Additional configuration:

1. Enable CREDITCARD-VD withdrawal method in Rules -> Payment methods.

#### Transaction flow

1. The user enters the amount to be withdrawn along with the credit card number in the cashier and clicks on "withdraw".
2. After the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends an initial payout request to Payper.
3. On a successful response, PaymentIQ sends a process payout request to Payper.
4. In case of a successful or pending response, PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION
   and the transfer will be made to deduct the amount from the user's balance.
5. PaymentIQ awaits for a callback from Payper regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the
   user's balance.

### MasterCard Send Payout
This method is used to process credit card withdrawals.

#### Configuration
Additional configuration:

1. Enable CREDITCARD-MCS withdrawal method in Rules -> Payment methods.

#### Transaction flow

1. The user enters the amount to be withdrawn along with the credit card number in the cashier and clicks on "withdraw".
2. After the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends an initial payout request to Payper.
3. On a successful response, PaymentIQ sends a process payout request to Payper.
4. In case of a successful or pending response, PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION
   and the transfer will be made to deduct the amount from the user's balance.
5. PaymentIQ awaits for a callback from Payper regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the
   user's balance.

## Example Routing Rule

![](/img/providers/routing/payper.png)

## Test Information

Please check directly with the provider.
