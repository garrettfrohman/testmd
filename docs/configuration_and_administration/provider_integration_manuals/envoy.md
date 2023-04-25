--- 
id: "envoy" 
title: "Envoy"
hide_title: "true"
---
 
![](/img/providers/logos/envoy.png)

# Envoy

## About
Envoy is a bank provider with support for Deposits and Withdrawals.

| Provider Name                | Envoy                                                                                                                                      |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | -                                                                                                                                          |
| Classification               | Online Banking                                                                                                                             |
| Regions                      | `International`                                                                                                                            |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                          |
| Methods/PaymentTxTypes       | `EnvoyDeposit`<br/> `EnvoyWithdrawal`<br/> `BankDeposit`<br/> `BankIBANWithdrawal`<br/> `BankIntIBANWithdrawal`<br/> `BankLocalWithdrawal` |
| PaymentIQ Configuration File | `EnvoyConfig`                                                                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.envoy.EnvoyConfig>
  <enabled>true</enabled>
  <width>1000</width>  
  <height>875</height>
  <container>window</container>
  <version></version>
  <liveMode>true</liveMode>
  <liveUrl>https://www.envoytx.com/MerchantAPI.asmx?WSDL</liveUrl>
  <liveUsername>??</liveUsername>
  <livePassword>??</livePassword>
  <testUrl>http://testapi.envoyservices.com/MerchantAPI/MerchantAPI.asmx?WSDL</testUrl>
  <testUsername>??</testUsername>
  <testPassword>??</testPassword>
  <sourceOrTarget>T</sourceOrTarget>
  <oneClickDepositUrl>https://www.envoytransfers.com</oneClickDepositUrl>
  <merchantId>??</merchantId> <!-- Eg 000123ABC -->
  <customerRef>??</customerRef> <!-- Eg MGABC1234567 --> 
  <successRedirectUrl>${successUrl}</successRedirectUrl>
  <failedRedirectUrl>${failureUrl}</failedRedirectUrl>
  <supportedSubServices>EPS|SOFORT|GIROPAY|IDEAL.*|PRZELEWY|EKONTO|TRUSTPAY|INSTADEBIT|USEMYBANK</supportedSubServices>
  <extraParameters>defaultBank->IDEAL:(.*)</extraParameters>
  <envoyAccountCy/>
  <statusCodeMapping>
    <entries>
      <statusCodeEntry>
        <method>.*Withdrawal</method>
        <response>0</response>
        <statusCode>SUCCESS</statusCode>
      </statusCodeEntry>
      <statusCodeEntry>
        <method>.*Withdrawal</method>
        <response>200</response>
        <statusCode>PROCESSING_PROVIDER</statusCode>
      </statusCodeEntry>
      <statusCodeEntry>
        <method>.*Withdrawal</method>
        <response>-513</response>
        <statusCode>ERR_DECLINED_BAD_REQUEST</statusCode>
      </statusCodeEntry>
    </entries>
  </statusCodeMapping>
  <killCallback></killCallback>
</com.devcode.paymentiq.integration.envoy.EnvoyConfig>
```
</details>

### Attributes

| Attribute                        | Default value | Description                                                                                                                                                                                                                                                                                    |
|----------------------------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| verifyNameMatchServicePattern    | Blank         | Configured using service names, for example, SOFORT. When a service name is declared, the name matching will be enabled for the specified service. You can have multiple services separated by pipe sign. Example: ```<verifyNameMatchServicePattern>SOFORT</verifyNameMatchServicePattern>``` |
| nameMatchPercentageThreshold     | 90            | Set to adjust the matching percentage threshold. Example: ```<nameMatchPercentageThreshold>80</nameMatchPercentageThreshold>```                                                                                                                                                                |
| nameMatchIgnoreMiddleNames       | false         | Set to true to ignore all middle names. Example: ```<nameMatchIgnoreMiddleNames>true</nameMatchIgnoreMiddleNames>```                                                                                                                                                                           |
| nameMatchIgnoreIfNameMissing     | false         | Set to true to ignore the name matching if one of the names is missing. Example: ```<nameMatchIgnoreIfNameMissing>true</nameMatchIgnoreIfNameMissing>```                                                                                                                                       |
| nameMatchIgnoreCase              | false         | Set to true to ignore case. Example: ```<nameMatchIgnoreCase>true</nameMatchIgnoreCase>```                                                                                                                                                                                                     |
| nameMatchSwapFirstLastIfMismatch | false         | Set to true to swap first and last name if mismatch. Example: ```<nameMatchSwapFirstLastIfMismatch>true</nameMatchSwapFirstLastIfMismatch>```                                                                                                                                                  |
| nameMatchReplaceDashWithSpace    | false         | Set to true to replace dash with space before matching the names. Example: ```<nameMatchReplaceDashWithSpace>true</nameMatchReplaceDashWithSpace>```                                                                                                                                           |
| nameMatchRemoveDashIfMismatch    | false         | Set to true to remove dash from name without leaving whitespace. Example: ```<nameMatchRemoveDashIfMismatch>true</nameMatchRemoveDashIfMismatch>```                                                                                                                                            |

## Example Routing Rule
![](/img/providers/routing/envoy.png)
## Test Information
No test accounts available. Please contact DevCode for more information.
