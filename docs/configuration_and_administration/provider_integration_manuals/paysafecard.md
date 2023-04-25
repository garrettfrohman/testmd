--- 
id: "paysafecard" 
title: "PaysafeCard"
hide_title: "true"
---
 
![](/img/providers/logos/paysafecard.png)

# PaysafeCard

## About
PaysafeCards is a voucher solution with support for Deposits and Withdrawals.

| Provider Name                | PaysafeCard                                                  |
|------------------------------|--------------------------------------------------------------|
| Link                         | [https://www.paysafecard.com/](https://www.paysafecard.com/) |
| Classification               | PrePaid Card / Voucher                                       |
| Regions                      | `International`                                              |
| Currencies                   | `EUR`, `CHF`, `AUD`, `CAD`                                   |
| Methods/PaymentTxTypes       | `PaysafecardDeposit`, `PaysafecardWithdrawal`                |
| PaymentIQ Configuration File | `PaysafecardConfig`                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paysafecard.deposit.PaysafecardConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>EUR</string>
      <account>
        <merchantId>??</merchantId>
        <username>??</username>
        <password>??</password>
        <version>SOPG1_0</version>
      </account>
    </entry>
    <entry>
      <string>CAD</string>
      <account>
        <merchantId>1000024030</merchantId>
        <username>psc_devcodeconsultingab_test</username>
        <password>81xLzKwry0Jk5Hl</password>
        <version>SOPG1_0</version>
      </account>
    </entry>
  </accounts>
  <receiveAccountHolderDetails>true</receiveAccountHolderDetails>
  <redirectUrl>https://customer.cc.at.paysafecard.com/psccustomer/GetCustomerPanelServlet</redirectUrl>
  <okUrl>${baseRedirectUrl}/api/paysafecard/deposit/finalize</okUrl>
  <nokUrl>${baseRedirectUrl}/api/paysafecard/deposit/finalize</nokUrl>
  <pnUrl>${baseCallbackUrl}/api/paysafecard/deposit/callback</pnUrl>
  <successRedirectUrl>${successUrl}</successRedirectUrl>
  <failedRedirectUrl>${failureUrl}</failedRedirectUrl>
  <subId>true</subId> <!--Set it to true if merchants needs to use the indentifier or 'reporting criteria' -->
  <brandId>1</brandId> <!-- the subId value, max length 8 characters case sensitive (agreement with Paysafe needed) -->
</com.devcode.paymentiq.integration.paysafecard.deposit.PaysafecardConfig>
```
</details>

### Attributes

| Attribute              | Description                                                                                                               |
|------------------------|---------------------------------------------------------------------------------------------------------------------------|
| merchantId             | The `mid` value, provided by PaysafeCard                                                                                  |
| username               | The `username` value used for basic auth in the requests, provided by PaysafeCard                                         |
| password               | The `password` value used for basic auth in the requests, provided by PaysafeCard                                         |
| subId                  | Set it to true if merchants needs to use the identifier or 'reporting criteria'. Use together with the brandId parameter. |
| brandId                | The subId value, max length 8 characters case sensitive (agreement with Paysafe needed)                                   |
| matchAccountHolderName | Set to true if deposits should be declined if name doesn't match. See details below.                                      |

### Receive my paysafecard account holder details and save as user PSP account

Paysafecard support a feature where they will return the account holder details back to PIQ if the user logged in to it's "my paysafecard" account when making the payment. This feature first has to be enabled on your account by PaysafeCard, and then it also has to be enabled in PIQ by adding the following configuration entry:

`<receiveAccountHolderDetails>true</receiveAccountHolderDetails>`.

Please see the full configuration example below.

When this feature is enabled, PIQ will save a user PSP account with the returned data. This user PSP account can later be used for withdrawals. Important to note is that the saved account can't be used for deposits, and to make sure that saved PaysafeCard accounts do not show up in the cashier for deposits, please add the following configuration entry in the `MerchantConfig` of your MID (best is to contact support to assist with this):

```xml
<ignoredUserPspAccountsByProviderTypes>
  <deposit>PAYSAFECARD</deposit>
</ignoredUserPspAccountsByProviderTypes>
```

### Decline deposit if the account holder name doesn't match
PaymentIQ can decline the deposit before it is processed if the name returned from the provider doesn't match with the name PaymentIQ receives from the verifyUser response. The matching algorithm used is "Levenshtein Distance" and the similarity between the strings must be at least 90% by default. This value can be configured with setting nameMatchPercentageThreshold.

By default the matching will be case sensitive and all middle names will be considered. This can be configured with the settings nameMatchIgnoreMiddleNames and nameMatchIgnoreCase. For example, to ignore all middle names add the following configuration entry:

`<nameMatchIgnoreMiddleNames>true</nameMatchIgnoreMiddleNames>`

The name matching feature is activated by adding the following configuration entry:

`<matchAccountHolderName>true</matchAccountHolderName>`

For Paysafecard to return KYC data the merchant must also set the receiveAccountHolderDetails setting to true.

## Example Routing Rule
![](/img/providers/routing/paysafecard.png)

## Test Information

### Deposits

- Supported currencies: EUR, CAD, AUD, CHF

When making deposits, the user is redirected to the PaysafeCard page. On this page the user has two options, either directly add the voucher code, or log in to their "my paysafecard" account where they can either use already available funds or add a new voucher code to top-up the funds.

The available voucher codes for testing can be found below. If some of the codes are depleted, please contact support so they can be removed and replaced by new ones.

#### Log in to my paysafecard

There are three available accounts you can use to log in to a "my paysafecard" acount.

| username             | password         |
|----------------------|------------------|
| tbWCihOACPiLspsrWfDv | Z30VCoYD1B6hVaA1 |
| TYTzTfjCgWmelEDyFyVi | lGMufW9FIvgTHaA1 |
| nOyrjSUYnumDlnSBOOOC | fNbolM8LLOcz1aA1 |


#### Voucher codes

##### EUR Specific

| PIN              | Face Value  | Currency |
|------------------|-------------|----------|
| 0445432283833284 | 10.00       | EUR      |
| 5525436273948320 | 10.00       | EUR      |
| 9101397148607840 | 10.00       | EUR      |
| 2758033900514210 | 10.00       | EUR      |
| 2294684048634470 | 10.00       | EUR      |
| 5298134916427470 | 10.00       | EUR      |
| 2142994920767120 | 10.00       | EUR      |
| 6295810647942160 | 10.00       | EUR      |
| 2892294345272110 | 10.00       | EUR      |
| 9987175602073640 | 10.00       | EUR      |
| 7934582285562800 | 10.00       | EUR      |
| 133819970769032  | 10.00       | EUR      |
| 8692258225900570 | 10.00       | EUR      |
| 5113506670993940 | 10.00       | EUR      |
| 8802142458426560 | 10.00       | EUR      |
| 3787810779142550 | 10.00       | EUR      |
| 3545171708055640 | 10.00       | EUR      |
| 3276363184829620 | 10.00       | EUR      |
| 60929302319440   | 10.00       | EUR      |
| 5504851526010980 | 10.00       | EUR      |
| 4311474238715040 | 10.00       | EUR      |
| 2820024507222520 | 10.00       | EUR      |
| 1299587011291100 | 10.00       | EUR      |
| 3815969359851910 | 10.00       | EUR      |
| 1809457359546700 | 10.00       | EUR      |
| 5844324679201030 | 10.00       | EUR      |
| 8937008944936620 | 10.00       | EUR      |
| 4522239897795390 | 10.00       | EUR      |
| 5702600928431180 | 10.00       | EUR      |
| 1773813483074770 | 10.00       | EUR      |
| 6843950514936700 | 10.00       | EUR      |
| 1615569606922670 | 10.00       | EUR      |
| 6384230303092150 | 10.00       | EUR      |
| 2330483223712070 | 10.00       | EUR      |
| 4656644024295500 | 10.00       | EUR      |
| 6719536752958340 | 10.00       | EUR      |
| 7138450234822240 | 10.00       | EUR      |
| 8498275386658980 | 10.00       | EUR      |
| 6321079401694840 | 10.00       | EUR      |
| 7484912689987240 | 10.00       | EUR      |
| 9065782162350920 | 10.00       | EUR      |
| 225617705274717  | 10.00       | EUR      |
| 4159302141275040 | 10000000.00 | EUR      |


##### USD, MXN Specific

| PIN              | Serial Number    | Currency |
|------------------|------------------|----------|
| 6413689923760063 | 6413689923760063 | USD      |
| 2094738841200741 | 2094738841200741 | USD      |
| 4680639986169360 | 4680639986169360 | USD      |
| 8988892968927757 | 8988892968927757 | USD      |
| 1298155075524205 | 1298155075524205 | USD      |
| 2937270882093680 | 2937270882093680 | USD      |
| 6479952833424876 | 6479952833424876 | MXN      |
| 8677487464442689 | 8677487464442689 | MXN      |
| 8168948033807861 | 8168948033807861 | MXN      |
| 6905821533618162 | 6905821533618162 | MXN      |
| 1788687673495915 | 1788687673495915 | MXN      |
| 5819130892437051 | 5819130892437051 | MXN      |

##### CHF Specific

| PIN              | Serial No        | Face Value | Currency |
|------------------|------------------|------------|----------|
| 0064121670766279 | 64121670766279   | 10.00      | CHF      |
| 8056656522772463 | 8056656522772463 | 10.00      | CHF      |
| 5335851373221032 | 5335851373221032 | 10.00      | CHF      |
| 5229630039694573 | 5229630039694573 | 10.00      | CHF      |
| 4589079585057115 | 4589079585057115 | 10.00      | CHF      |
| 6250671496687451 | 6250671496687451 | 10.00      | CHF      |
| 6961560915278614 | 6961560915278614 | 10.00      | CHF      |
| 9049562545332764 | 9049562545332764 | 10.00      | CHF      |
| 6732411934411326 | 6732411934411326 | 10.00      | CHF      |
| 6310427894562515 | 6310427894562515 | 10.00      | CHF      |
| 3121481641167066 | 3121481641167066 | 10.00      | CHF      |
| 4526608867202030 | 4526608867202030 | 10.00      | CHF      |
| 3229778832069428 | 3229778832069428 | 10.00      | CHF      |
| 8656885371721261 | 8656885371721261 | 10.00      | CHF      |
| 4754611014808794 | 4754611014808794 | 10.00      | CHF      |
| 6076348321977220 | 6076348321977220 | 10.00      | CHF      |
| 6141114686716574 | 6141114686716574 | 10.00      | CHF      |
| 3195904472089498 | 3195904472089498 | 10.00      | CHF      |
| 0821912190708498 | 821912190708498  | 10.00      | CHF      |
| 6631353185367772 | 6631353185367772 | 10.00      | CHF      |
| 3260059780275048 | 3260059780275048 | 10.00      | CHF      |
| 4825697433933012 | 4825697433933012 | 10.00      | CHF      |
| 5039810012581245 | 5039810012581245 | 10.00      | CHF      |
| 6787502341260932 | 6787502341260932 | 10.00      | CHF      |
| 2418853062601915 | 2418853062601915 | 10.00      | CHF      |

### Withdrawals

For withdrawals, the following values needs to be matched for the user and the Paysafe account:
- email
- firstname
- lastname
- dob(date of birth)

If you have enabled the feature to receive account holder details from deposits, the saved accounts can be used directly to make withdrawals. If there are no saved accounts you have to use the below information to succesfully perform withdrawals.

These are the available test accounts:

| parameter | value                      |
|-----------|----------------------------|
| email     | AgfpFHAeRC@FTwtlCzvXl.mmB  |
| firstname | Test                       |
| lastname  | vuXsEbLOVHYbaNsTmlkDYwvSHD |
| dob       | 1990-06-02                 |

| parameter | value                      |
|-----------|----------------------------|
| email     | tCrcDhdExf@OGCuZekzYD.FHr  |
| firstname | Test                       |
| lastname  | FpyUycKrihqZrSSBvuLtJqVELX |
| dob       | 1990-06-02                 |

| parameter | value                      |
|-----------|----------------------------|
| email     | gvTMQdtRxZ@pAtIDPaQnB.vCT  |
| firstname | Test                       |
| lastname  | hxBKmaNoQGLORVvpbTnhFYUdcG |
| dob       | 1990-06-02                 |
