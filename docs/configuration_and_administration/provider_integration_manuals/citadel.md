--- 
id: "citadel" 
title: "Citadel"
hide_title: "true"
---
 
![](/img/providers/logos/citadel.png)

# Citadel

## About
Citadel Direct offers merchants the ability to receive payments from their customers via bank transfers. Citadel provides both 'Instant Credit' and 'Bank Transfer' methods where the merchant is notified about a payment either upon transfer initiation (instant credit) or upon receipt of funds (bank transfer).

| Provider Name                | Citadel                                                                                      |
|------------------------------|----------------------------------------------------------------------------------------------|
| Link                         | [http://www.citadelcommerce.com/en/](http://www.citadelcommerce.com/en/)                     |
| Classification               | Online Banking                                                                               |
| Regions                      | `International`                                                                              |
| Currencies                   | Please check directly with the provider regarding what currencies are supported              |
| Methods/PaymentTxTypes       | `BankDeposit`<br/> `BankLocalWithdrawal`<br/> `BankIBANWithdrawal`<br/> `BankIntlWithdrawal` |
| PaymentIQ Configuration File | `CitadelConfig`                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.citadel.CitadelConfig>
  <enabled>true</enabled>
    <height>600</height>
  <width>600</width>
  <accounts>
    <entry>
     <string>default</string>
     <account>
       <merchantName>???</merchantName> <!-- Account name-->
       <accountID>???</accountID>  <!-- Store ID -->
       <username>???</username>  <!-- Staff ID    -->
       <password>???</password>  <!-- Password-->
       <successUrl>${successUrl}</successUrl>
       <failureUrl>${failureUrl}</failureUrl>
     </account>
    </entry>
  </accounts>
   <reconcileReportEnabled>false</reconcileReportEnabled>
 <reconcileReportMailTemplate>citadel-recon-report</reconcileReportMailTemplate>
 <reconcileReportEmailRecipients>???</reconcileReportEmailRecipients>
 <reconcileReportExcludeTxPattern>(^(?=.*transaction_type=(SD[^\w]|SDF))(?=.*method=instant_credit).*$)|(^.*transaction_type=(?!SDR|SWR|SD[^\w]).*$)</reconcileReportExcludeTxPattern>
 <reconcileReportCron>0 */5 * * * *</reconcileReportCron>
 <bankMappings>
    <!--CAN BANKS -->
    <bankMapping><branchCode>25039</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}001</clearingNumber><swift>BOFMCAM2XXX</swift><bankName>Bank of Montreal</bankName></bankMapping>
    <bankMapping><branchCode>00109</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}002</clearingNumber><swift>NOSCCATTXXX</swift><bankName>Bank of Nova Scotia</bankName></bankMapping>
    <bankMapping><branchCode>01003</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}003</clearingNumber><swift>ROYCCAT2XXX</swift><bankName>Royal Bank of Canada</bankName></bankMapping>
    <bankMapping><branchCode>80299</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}004</clearingNumber><swift>TDOMCATTXXX</swift><bankName>Toronto-Dominion Bank</bankName></bankMapping>
    <bankMapping><branchCode>01729</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}010</clearingNumber><swift>CIBCCATTXXX</swift><bankName>Canadian Imperial Bank of Commerce</bankName></bankMapping>
    <bankMapping><branchCode>10009</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}016</clearingNumber><swift>HKBCCATTXXX</swift><bankName>HSBC Bank Canada</bankName></bankMapping>
    <bankMapping><branchCode>03039</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}030</clearingNumber><swift>CWBKCA61XXX</swift><bankName>Canadian Western Bank</bankName></bankMapping>
    <bankMapping><branchCode>02781</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}039</clearingNumber><swift>BLCMCAMMXXX</swift><bankName>Laurentian Bank of Canada</bankName></bankMapping>
    <bankMapping><branchCode>16001</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}621</clearingNumber><swift>NRTHUS33XXX</swift><bankName>Peoples Trust Company</bankName></bankMapping>
    <bankMapping><branchCode>17560</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}309</clearingNumber><swift>CTZNCA8VXXX</swift><bankName>Citizens bank of Canada</bankName></bankMapping>
    <bankMapping><branchCode>00109</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}809</clearingNumber><swift>CUCXCATTXXX</swift><bankName>Central Union bank</bankName></bankMapping>
    <bankMapping><branchCode>00109</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}839</clearingNumber><swift>CUCXCATTVAN</swift><bankName>Tignish Credit Union bank</bankName></bankMapping>
    <bankMapping><branchCode>00109</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}889</clearingNumber><swift>CUCXCATTREG</swift><bankName>Affinity Credit Union bank</bankName></bankMapping>
    <bankMapping><branchCode>00109</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}815</clearingNumber><swift>CCDQCAMMXXX</swift><bankName>FEDERATION DES CAISSES DESJ. QUEBEC</bankName></bankMapping>
    <bankMapping><branchCode>07639</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}219</clearingNumber><swift>ATBRCA6EXXX</swift><bankName>Alberta Treasury Branches</bankName></bankMapping>
    <bankMapping><branchCode>05591</branchCode><countryCode>CAN</countryCode><clearingNumber>\\d{5}006</clearingNumber><swift>BNDCCAMMINT</swift><bankName>Banque Nationale</bankName></bankMapping>
    
    <!-- Australia -->
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>03.*|73.*</clearingNumber><swift>WPACAU2SXXX</swift><bankName>Westpac Banking Corporation</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>06.*|76.*</clearingNumber><swift>CTBAAU2SXXX</swift><bankName>Commonwealth Bank of Australia</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>08.*|78.*</clearingNumber><swift>NATAAU3303M</swift><bankName>National Australia Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>10.*</clearingNumber><swift>SGBLAU2SXXX</swift><bankName>BankSA</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>11.*</clearingNumber><swift>SGBLAU2SXXX</swift><bankName>St George Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>12.*</clearingNumber><swift>QBANAU4BXXX</swift><bankName>Bank of Queensland;</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>33.*</clearingNumber><swift>SGBLAU2SXXX</swift><bankName>St George Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>19.*</clearingNumber><swift>SGBLAU2SXXX</swift><bankName>Bank of Melbourne (2011), previously Advance Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>24.*</clearingNumber><swift>CITIAU2XXXX</swift><bankName>Citibank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>30.*</clearingNumber><swift>BKWAAU6PXXX</swift><bankName>BankWest</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>48.*</clearingNumber><swift>METWAU4BXXX</swift><bankName>Suncorp Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>1.*</clearingNumber><swift>ANZBAU3MXXX</swift><bankName>Australia and New Zealand Banking Group Limited</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>633.*</clearingNumber><swift>BENDAU3BXXX</swift><bankName>Bendigo Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>650.*</clearingNumber><swift>ASLLAU2C</swift><bankName>Newcastle Permanent Building Society</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>014664.*</clearingNumber><swift>ANZBAU3MXXX</swift><bankName>ANZ Bank in Mount Isa</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>015595.*</clearingNumber><swift>ANZBAU3MXXX</swift><bankName>ANZ Bank in Keith</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>923.*|936.*</clearingNumber><swift>INGBAU2SXXX</swift><bankName>ING Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>939.*</clearingNumber><swift>AMPBAU2SXXX</swift><bankName>AMP</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>012.*</clearingNumber><swift>ANZBAU2SXXX</swift><bankName>ANZ Bank;</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>013.*|014.*|015.*|016.*|017.*</clearingNumber><swift>ANZBAU3MXXX</swift><bankName>ANZ</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>80.*|81.*</clearingNumber><swift>CUSCAU2SXXX</swift><bankName>Cuscal</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>610.*</clearingNumber><swift>BENDAU3B</swift><bankName>Adelaide Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>183.*</clearingNumber><swift>MACQAU2SXXX</swift><bankName>Macquarie Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>637.*</clearingNumber><swift>ASLLAU2CGBS</swift><bankName>The Greater Building Society Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>638.*</clearingNumber><swift>HBSLAU4T</swift><bankName>Heritage Bank Limited</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>640.*</clearingNumber><swift>ASLLAU2C</swift><bankName>Hume Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>641.*</clearingNumber><swift>ASLLAU2C</swift><bankName>IMB Bank</bankName></bankMapping>
    <bankMapping><countryCode>AUS</countryCode><clearingNumber>944.*</clearingNumber><swift>MEQBAU3M</swift><bankName>ME Bank</bankName></bankMapping>
    
    <!-- New Zealand -->
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>060.*|01.*</clearingNumber><swift>ANZBNZ22XXX</swift><bankName>ANZ</bankName>ANZ</bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>06.*|76.*</clearingNumber><swift>CTBAAU2SXXX</swift><bankName>Commonwealth Bank of Australia</bankName></bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>03.*|09.*|23.*</clearingNumber><swift>WPACNZ2W</swift><bankName>Westpac New Zealand</bankName></bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>12.*|14.*</clearingNumber><swift>ASBBNZ2AXXX</swift><bankName>ASB Bank</bankName></bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>02.*|08.*</clearingNumber><swift>BKNZNZXXX</swift><bankName>Bank Of New Zealand</bankName></bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>02.*|08.*</clearingNumber><swift>RBNZNZXXX</swift><bankName>Reserve Bank Of New Zealand</bankName></bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>31.*</clearingNumber><swift>CITINZ2XXXX</swift><bankName>Citibank Auckland</bankName></bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>31.*</clearingNumber><swift>CITINZ2102W</swift><bankName>Citibank Wellington</bankName></bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>38.*</clearingNumber><swift>KIWINZ22XXX</swift><bankName>Kiwibank Limited</bankName></bankMapping>
    <bankMapping><countryCode>NZL</countryCode><clearingNumber>15.*</clearingNumber><swift>TSBANZ22XXX</swift><bankName>TSB Bank Limited</bankName></bankMapping>

</bankMappings>
  
</com.devcode.paymentiq.integration.citadel.CitadelConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential |
|-------------------------|---------------------|
| merchantName            | Account name        |
| accountID               | Store ID            |
| username                | Staff ID            |
| password                | Password            |

### Reconcile report
The reconcile report can be enabled to handle offline payments and chargebacks.

The purpose of the reconcile report is that the merchant gets notified via e-mail about any offline payments or chargebacks that have been received against the merchant account, so that these get handled accordingly.

This functionality is a must-have requirement from Citadel and has to be tested by the merchant during the integration process.

Depending on the configuration a reconcile report will be requested automatically from Citadel on pre-defined time intervals. PIQ will process the report and in case of any offline payments or chargebacks present, an e-mail notification will be sent to the configured e-mail address.

*Example configuration:*

```xml
<reconcileReportEnabled>true</reconcileReportEnabled>
<reconcileReportMailTemplate>citadel</reconcileReportMailTemplate> <reconcileReportEmailRecipients>someone@example.com</reconcileReportEmailRecipients>
<reconcileReportExcludeTxPattern>(^(?=.*transaction_type=(SD[^\w]|SDF))(?=.*method=instant_credit).*$)|(^.*transaction_type=(?!SDR|SD[^\w]).*$)</reconcileReportExcludeTxPattern>
<reconcileReportCron>0 */15 * * * *</reconcileReportCron>
```

*reconcileReportEnabled* A flag for enabling / disabling. Can be *true* or *false*

*reconcileReportMailTemplate* A name referring a stored email template (admin -> template -> email template)

*reconcileReportExcludeTxPattern* Regular expression that should match transactions to exclude from the report. For example to exclude transaction type SD and method instant_credit:
```^(?=.*transaction_type=SD)(?=.*method=instant_credit).*$```

*reconcileReportCron* Cron expression defining the fetch interval.  Please note that the first entry is seconds and should preferable be set as 0.  
Example to fetch the report every 15 minutes 0 ```*/15 * * * *```

<details>
<summary>Click to view example email template</summary>
<br/>

```html
<html>
  <body>

    <h3>Citadel Reconcile Report</h3>
    <div>
      <p>
        Dear Merchant,
        <br/><br/>
        The list below provides information about the offline payments (Store deposit) and chargebacks (Revoke store deposit) registered against your merchant account with Citadel since the last execution of the reconciliation job.
        These need to be handled manually on your end. PIQ will not take any automated action.
      </p>
      <br/>
      How to read the file:
      <br/>
      <br/>
      <b>Transaction type:</b>
      <br/>
      <ul>
        <li>SD - Store Deposit. Bank Transfer and Instant Credit payments made by a consumer to the merchant.</li>
        <li>SDR - Revoked Store Deposit. Charge-back against a previously reported �SD� transaction. Reverses a previously recorded �SD� transaction.</li>
        <li>SWR - Returned Store Withdraw. Return of consumer payout. Presumably the payout was undeliverable.</li>
      </ul>
      <p>
        <b>Merchant reference</b> - the value of the Tx-ref-id attribute available in the PIQ backoffice. Note that in case of revokes this will point to the deposit that has been revoked. In case of a Store deposit, this should be used as a reference for finding the user account that made an offline deposit.
      </p>

      If any questions or concers occur, feel free to contact your account manager or technicalsupport@bambora.com

    </div>

    <table>
      <tr>
        <th>Merchant Store Id</th>
        <th>Internal Reference</th>
        <th>Merchant Reference</th>
        <th>Transaction Date</th>
        <th>Transaction Type</th>
        <th>Transaction Subtype</th>
        <th>Method</th>
        <th>Amount</th>
        <th>Currency</th>
        <th>Original Internal Reference</th>
        <th>Country</th>
        <th>Group Id</th>
        <th>Entry Type</th>
      </tr>
      ${foreach transactions tx}
        <tr>
          <td>${tx.merchant_store_id}</td>
          <td>${tx.internal_reference}</td>
          <td>${tx.merchant_reference}</td>
          <td>${tx.transaction_date}</td>
          <td>${tx.transaction_type}</td>
          <td>${tx.transaction_subtype}</td>
          <td>${tx.method}</td>
          <td>${tx.amount}</td>
          <td>${tx.currency_code}</td>
          <td>${tx.original_internal_reference}</td>
          <td>${tx.country}</td>
          <td>${tx.group_id}</td>
          <td>${tx.entry_type}</td>
        </tr>
      ${end}
    </table>

  </body>
</html>
```

</details>


## Example Routing Rule
![](/img/providers/routing/citadel.png)
## Test Information

### Citadel Deposit Test

In order to test Citadel deposit, a user login is required to simulate a Citadel user. The first step is to send an amount and call the verifyUser method by PIQ. After that the user will be redirected to an Iframe or window (depending on the merchant needs) presenting a form where the user can continue with the transfer.

1 - Choose your bank. (in test mode you can choose all the alternatives presented.)

![](/img/providers/citadel01.png)

2 - Login to your bank.

User ID: devcode
Password: Welcome_1234

(Account ID : 52497070)
The account ID is not normally required on this recognition.

![](/img/providers/citadel02.png)

3 - Choose the account from which money will be transferred.

![](/img/providers/citadel03.png)

4 - Upon payment confirmation, �Payment Approved� message will be shown

![](/img/providers/citadel04.png)

###	Citadel Withdrawal Test

#### CAN

| Clearing   Number                            | Account Number |
|----------------------------------------------|----------------|
| 01003003(Branch:   01003 + Institution: 003) | 1111222233     |

#### GBR

| BIC      | IBAN                   |
|----------|------------------------|
| NWBKGB2L | GB29NWBK60161331926819 |

#### AUS

| Clearing   Number | Account Number |
|-------------------|----------------|
| 066124            | 30012345       |
