--- 
id: "qaicash" 
title: "Qaicash"
hide_title: "true"
---
 
![](/img/providers/logos/qaicash.png)

# Qaicash

## About
Qaicash is a payment provider offering creditcard, bank and e-wallet deposit and withdrawal. Reversal is also supported for withdrawal operations.

| Provider Name                | Qaicash                                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------------------|
| Link                         | [http://www.qaicash.com/](http://www.qaicash.com/)                                                    |
| Classification               | Aggregator of different payment options: Debit/Credit Card Processor, Online/Manual Banking, E-Wallet |
| Regions                      | China, Thailand, Vietnam, Indonesia, Malaysia, Japan and India                                        |
| Currencies                   | `CNY`, `THB`, `MYR`, `VND`, `KRW`, `JPY`, `USD`, `BTC`, `IDR`, `INR`                                  |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`<br/>`WebRedirectWithdrawal`<br/>`BankLocalWithdrawal`<br/>`Reversal`             |
| PaymentIQ Configuration File | `QaicashConfig`                                                                                       |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.qaicash.QaicashConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <supportedCurrencies>CNY|THB|VND|IDR|MYR|JPY|INR|USD</supportedCurrencies>
        <language>en-Us</language>
        <version>v2.0</version>
        <!--
        It is used to show available banks on UI so user could select any. In case it is 'false' no banks will be shown
        and user will select the banks after redirection to the provider page.
        -->
        <showAvailableBanks>true</showAvailableBanks>
        <!--
        REGULAR: payout should be initiated first (all the bank information is collected at the provider side) and then approved/rejected
        PREAPPROVED: all the bank information is collected at PaymentIQ side and no approval is required to make a payout
        -->
        <withdrawalType>PREAPPROVED</withdrawalType><!--REGULAR or PREAPPROVED-->
        <method>LOCAL_BANK_TRANSFER</method>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Bambora payment ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.qaicash.QaicashConfig>
```
</details>

### Attributes
| Attribute                  | Description                                                                                                                                                                                                                                                                                                                             |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId         | Corresponds to `merchantId` from Qaicash. It is used to build request URL.                                                                                                                                                                                                                                                              |
| account.apiKey             | Corresponds to `merchantApiKey` from Qaicash. It is used to build request and notification `authCode`                                                                                                                                                                                                                                   |
| account.language           | Supported languages: `en-Us`, `zh-Hans`, `th`, `vi`, `ko`, `ja`, `id`                                                                                                                                                                                                                                                                   |
| account.showAvailableBanks | It is used to indicate if banks list will be shown on the UI or not.                                                                                                                                                                                                                                                                    |
| account.withdrawalType     | Indicates a withdrawal type (REGULAR or PREAPPROVED). In case that property is blank or missing, a REQULAR payout will be used by default.                                                                                                                                                                                              |
| account.method             | It can be used to specify a payment method that should be used. In that case user will be redirected to the configured method immediately without showing a page with all available payment methods. The same effect can be achieved when `service` request parameter will be sent to the PaymentIQ e.g. `service=LOCAL_BANK_TRANSFER`. |

#### PaymentIQ Tx Type to service/method mapping
| Operation                | PaymentIQ tx type     | Payment method                                                              | accountConfig.withdrawalType | Comment                                                                                                                                                                                                                                                                                                   |
|--------------------------|-----------------------|-----------------------------------------------------------------------------|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Withdrawal               | WebRedirectWithdrawal | Specified in the `accountConfig.method` or in the `input.service` parameter | can be left blank            | Initiates a REGULAR withdrawal where user will be redirected to the provider's page to specify additional info if needed (e.g. bank details). No available payment options page will be shown.                                                                                                            |
| Withdrawal               | WebRedirectWithdrawal |                                                                             | blank or REGULAR             | PaymentIQ will display all available payment options first. Then user will have to select payment method in order to proceed with payment. In case of some required parameters needs to be specified, user will be redirected to the provider's page to do so (e.g. choose bank or specify user details). |
| Withdrawal (preapproved) | WebRedirectWithdrawal |                                                                             | PREAPPROVED                  | PaymentIQ will display all available payment options first. Then user will have to select payment method in order to proceed with payment. In case of bank withdrawal, user will have to specify bank details at PaymentIQ side.                                                                          |
| Withdrawal (preapproved) | BankLocalWithdrawal   | Specified in the `accountConfig.method` or in the `input.service` parameter | can be left blank            | PaymentIQ will initiate a PREAPPROVED payment option ( e.g. bank withdrawal, where user will have to specify all bank related info at PaymentIQ side).                                                                                                                                                    |
| Deposit                  | WebRedirectDeposit    |                                                                             |                              | PaymentIQ will display all available payment options first. Then user will have to select payment method in order to proceed with payment.                                                                                                                                                                |
| Deposit                  | WebRedirectDeposit    | Specified in the `accountConfig.method` or in the `input.service` parameter |                              | PaymentIQ will initiate a deposit by redirecting a user to a specified payment method (no available payment options page will be shown).                                                                                                                                                                  |

## Example Routing Rule
![](/img/providers/routing/qaicash.png)

## Test Information

On Provider's STG env. everything is configured through MockPay, a mock payment processor that will allow you to select the outcome of a transaction (e.g. whether it succeeds or fails).

### Deposit/Withdrawal Steps
1). Open PaymentIQ Cashier and select WebRedirect payment option (for deposit or withdrawal). \
2). Specify amount and press Pay button. \
3). You will be redirected to the page with all available payment options (Credit Card, Banking, Wallets).

![](/img/providers/qaicash_01.png)

4). If wallet payment option is selected, you will be redirected to the MockPay page where you will be able to simulate payment outcome (SUCCESSFUL or FAILED payment).

![](/img/providers/qaicash_02.png)

5). if banking payment option is selected (with "showAvailableBanks=true") - PaymentIQ will show available banks and user will need to select a bank to proceed with payment.

![](/img/providers/qaicash_03.png)

After "Confirm" button is pressed, user will be redirected to the MockPay page in order to simulate payment outcome (see step "4"). \
if banking payment option is selected (with "showAvailableBanks=false") - user will be redirected to the provider's bank selection page and will be able to proceed with payment in similar way like described above.

![](/img/providers/qaicash_04.png)

6). Once payment is completed, the user will be redirection back to PaymentIQ Cashier.
