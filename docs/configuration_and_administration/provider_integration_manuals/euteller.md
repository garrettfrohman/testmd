--- 
id: "euteller" 
title: "Euteller"
hide_title: "true"
---
 
![](/img/providers/logos/euteller.png)

# Euteller

## About
Euteller is a banking provider for the Finnish market.

| Provider Name                | Euteller                                                                                                          |
|------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Link                         | [http://www.euteller.com](http://www.euteller.com)                                                                |
| Classification               | Online Banking                                                                                                    |
| Regions                      | `Finland`                                                                                                         |
| Currencies                   | `EUR`                                                                                                             |
| Methods/PaymentTxTypes       | `EutellerDeposit`, `EutellerWithdrawal`, `BankDeposit`, `BankIBANWithdrawal`, `SiirtoDeposit`, `SiirtoWithdrawal` |
| PaymentIQ Configuration File | `EutellerConfig`                                                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.euteller.EutellerConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>DP</string>
      <account>
        <customerId>??</customerId>
        <secretKey>??</secretKey>
        <key1>??</key1><!--Merchant API secret = password-->
        <deviceCategoryMapping>I->0,M->1,*->0</deviceCategoryMapping>
      </account>
    </entry>
    <entry>
      <string>WD</string>
      <account>
        <customerId>??</customerId>
        <secretKey>??</secretKey>
        <key1>??</key1><!--Merchant API secret = password-->
        <deviceCategoryMapping>I->0,M->1,*->0</deviceCategoryMapping>
      </account>
    </entry>
  </accounts>
  <!--<container>iframe</container> default is window, force iframe is necessary for merchant (certain banks don't support iframe so if it's used a new window will opened for those banks) --> 
  <height>715</height>
  <width>805</width>
  <!--
  <extraFields>
    <entry>
      <string>TxRefId</string>
      <string>${ptx.txRefId}</string>
    </entry>
    
    /// one can add
    <entry>
      <string>routing</string>
      <string>siirto</string>
    </entry>
    give permission to Euteller to use Siirto for withdrwal.
    If Siirto withdrawal is not available for the user it will fall back to Bank withdrawal.
    ///
    
  </extraFields>
  -->
</com.devcode.paymentiq.integration.euteller.EutellerConfig>
```

</details>

### Attributes
| Attribute                         | Description                                                                                                                                                                                |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| customerId                        | Customer identification, supplied by Euteller                                                                                                                                              |
| secretKey                         | Secret key to calculate the security string, supplied by Euteller                                                                                                                          |
| key1                              | Security key used in the status check against Euteller and to validate account notification callbacks, supplied by Euteller                                                                |
| extraFields                       | Adds the parameter `extra_fields` in the request to provide additional information such as the `siteName`. See configuration example below.                                                |
| deviceCategoryMapping             | Sets the parameter `end_user[device]` in the request. The mapping is based on the `channel` parameter sent to PIQ. <br/> 0 = Desktop <br/> 1 = Mobile browser <br/> 2 = Mobile application |
| useDirectBank                     | Enable the "Direct Bank Selection" mode by setting this to `true`.                                                                                                                         |
| updateStatusOnAccountNotification | Set to true to allow waiting transactions to be updated to success when receiving account notification                                                                                     |

### Example

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.euteller.EutellerConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>DP</string>
      <account>
        <customerId>??</customerId>
        <secretKey>??</secretKey>
        <key1>??</key1><!--Merchant API secret = password-->
        <deviceCategoryMapping>I->0,M->1,*->0</deviceCategoryMapping>
      </account>
    </entry>
    <entry>
      <string>WD</string>
      <account>
        <customerId>??</customerId>
        <secretKey>??</secretKey>
        <key1>??</key1><!--Merchant API secret = password-->
        <deviceCategoryMapping>I->0,M->1,*->0</deviceCategoryMapping>
      </account>
    </entry>
  </accounts>
  <!--<container>iframe</container> default is window, force iframe is necessary for merchant (certain banks don't support iframe so if it's used a new window will opened for those banks) -->
  <height>715</height>
  <width>805</width>
  <!--
  <extraFields>
    <entry>
      <string>siteName</string>
      <string>casino.com</string>
    </entry>

    /// one can add
    <entry>
      <string>routing</string>
      <string>siirto</string>
    </entry>
    give permission to Euteller to use Siirto for withdrwal.
    If Siirto withdrawal is not available for the user it will fall back to Bank withdrawal.
    ///
  </extraFields>
  -->
  <useDirectBank>false</useDirectBank>
  <updateStatusOnAccountNotification>true</updateStatusOnAccountNotification>
</com.devcode.paymentiq.integration.euteller.EutellerConfig>
```
</details>

### Account Notification
Euteller can send a notification the day after the deposit was done with additional information about the account holder. Currently, the provided information is the account holder name and bank name which will be added to the transaction (visible in the Account holder and info column in the transaction view). The Merchant API secret (key1) must be configured on the account config for it to work. The feature must be activated by Euteller who needs the URL to where they will send the request, which is ${PIQ base URL}/api/euteller/account.

### Update Stuck Transactions
In order for transactions to be successful via Euteller customers need to click on the return to merchant button on the Bank's page. Sometimes this does not occur and the transaction remains in WAITING_INPUT state in PIQ. Euteller has added status parameter on the account notification (see above), which PIQ can use to update transactions that are still in WAITING_INPUT.

This feature must be activated by adding the following to EutellerConfig:

`<updateStatusOnAccountNotification>true</updateStatusOnAccountNotification>`

### Saved User Psp Accounts
Euteller can send information about the bank account in the account notification that can be used for withdrawals. If this info is received in the account notification PIQ will save an account of type EUTELLER. This account is then used with the new TxType EutellerWithdrawal. Note that EutellerWithdrawal has no other inputs and can only be used with a saved account.

### Direct Bank Selection
Instead of being redirected to the classic Euteller payment selection page, you can enable the "Direct Bank Selection" mode to be directly redirected to the wanted bank.

To enable this feature you have to add the configuration tag `<useDirectBank>true</useDirectBank>` in the top level of the EutellerConfig. To select the wanted bank you have to send the correct value in the table below as the `service` parameter in either the BankDeposit or EutellerDeposit transaction input.

| service value | bank name     |
|---------------|---------------|
| op            | Osuuspankki   |
| nordea        | Nordea        |
| spankki       | S-Pankki      |
| danske        | Danske Bank   |
| saastopankki  | Säästöpankki  |
| aktia         | Aktia Pankki  |
| pop           | POP Pankki    |
| handelsbanken | Handelsbanken |
| omasp         | OmaSP         |
| alandsbanken  | Ålandsbanken  |

As a merchant you can present the bank selections in multiple ways. The cashier page can contain separate elements for every bank presented in buttons or links or what ever you decide. Or the cashier page can contain a dropdown selection for each bank. The cashier page can also be a hybrid where some banks are presented individually and the classic Euteller selection is also available.

## Example Routing Rule

![](/img/providers/routing/euteller.png)

## Test Information

### Regular Deposit
1.	When redirected, tick the check box next to 'Olen yli 18-vuotias ja hyväksyn sopimusehdot' and click on the Nordea icon.
2.	Click OK in the next step, don't switch tabs or edit the prefilled values marked as dots.
3.	In the next step, the 'Maksu' step, just enter some random chars in the box 'Vahvistustunnus R' and then click 'Vahvista'.
4.	Inside Nordea UI you should select and click 'Palauta hyväksytty maksu' button for simulate PAID transaction or 'Palauta epäonnistunut maksu' button if you wan't to test DECLINED transaction (window should close automatically within 10 sec).

### Direct Deposit
The only difference to a regular deposit test is that you send a valid bank as the `service` parameter. So to test Nordea, send service with value `nordea`, and when you are redirected, follow the same steps as for regular deposit above from step 2.

### Withdrawal
In order to run a test withdrawal, you call the BankIBAN API and send validated BIC and IBAN parameters. The final result of a transaction can take up to one hour before the callback reach PaymentIQ, so the normal state for a transaction is initially ”Waiting Notification” after an agent approve the withdrawal transaction from PIQ back-office.
