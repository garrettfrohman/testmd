--- 
id: "payex" 
title: "PayEx"
hide_title: "true"
---
 
![](/img/providers/logos/payex.png)

# PayEx

## About
PayEx is a creditcard processor offering Deposits and Withdrawals.

| Provider Name                           | PayEx                                                                                                                                                                   |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                                    | [https://payex.com/](https://payex.com/)                                                                                                                                |
| Classification                          | Debit/Credit Card Processor                                                                                                                                             |
| API                                     | Please contact our technicals support team for information.                                                                                                             |
| Regions                                 | `International`                                                                                                                                                         |
| Currencies                              | Please check directly with the provider regarding what currencies are supported                                                                                         |
| Methods/PaymentTxTypes (PayExConfig)    | `CreditcardDeposit`                                                                                                                                                     |
| Methods/PaymentTxTypes (PayExRestConfig | `CreditcardDeposit`, `CreditcardWithdrawal`, `CreditcardAccountVerification`, `Refund`, `Capture`, `Void`, `BankDeposit`, `WebRedirectDeposit`, `WebRedirectWithdrawal` |
| PaymentIQ Configuration File            | `PayExConfig` or `PayExRestConfig`                                                                                                                                      |

## Configuration Information

### Prerequisites
* PayEx has one deprecated config `PayExConfig` and one current `PayExRestConfig`. To route and use the new `PayExConfig` we will have to add a `Action` called `PSP Version` with the value `REST`.  Example of this can be found in the routing section for the `PayExRestConfig`.
* Card payouts must be enabled from payex side

### PayExConfig
Configuration for PayEx deprecated old api.

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payex.PayExConfig>
    <enabled>true</enabled>
	<useViqProxy>false</useViqProxy>
	<accounts>
		<entry>
			<string>RECURRING</string>
			<account>
			    <use3Dsecure>false</use3Dsecure>
				<merchantId>???</merchantId>
				<secretKey>???</secretKey>
				<redirectUrl>${baseRedirectUrl}/api/payex/deposit/redirect</redirectUrl>
				<useTokenId>true</useTokenId>
			</account>
		</entry>
		<entry>
			<string>MANUAL-N3DS</string>
			<account>
		  	    <use3Dsecure>false</use3Dsecure>
				<merchantId>???</merchantId>
				<secretKey>???</secretKey>
				<redirectUrl>${baseRedirectUrl}/api/payex/deposit/redirect</redirectUrl>
				<useTokenId>false</useTokenId>
			</account>
		</entry>
		<entry>
			<string>MANUAL-3DS</string>
			<account>
			    <use3Dsecure>true</use3Dsecure>
				<merchantId>???</merchantId>
				<secretKey>???</secretKey>
				<redirectUrl>${baseRedirectUrl}/api/payex/deposit/redirect</redirectUrl>
				<useTokenId>false</useTokenId>
			</account>
		</entry>
	</accounts>
	<agreementDescription>Subscription</agreementDescription>
	<confinedDepositUrl>https://confined.payex.com/PxConfined/Pxorder.asmx?WSDL</confinedDepositUrl>
	<intiDepositUrl>https://external.payex.com/pxorder/pxorder.asmx?WSDL</intiDepositUrl>
	<agreementDepositUrl>https://external.payex.com/pxagreement/pxagreement.asmx?WSDL</agreementDepositUrl>  
</com.devcode.paymentiq.integration.payex.PayExConfig>
```
</details>

#### Example Routing Rule
![](/img/providers/routing/payex.png)

### PayExRestConfig
PayEx new Rest api offering more payment methods.

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payex.rest.PayExRestConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>BANK</string>
      <account>
        <supportedCurrencies>???</supportedCurrencies>
        <merchantId>???</merchantId>
        <accessToken>???</accessToken>
        <merchantName>???</merchantName>
        <productCategory>???</productCategory>
      </account>
    </entry>
    <entry>
      <string>N3DS</string>
      <account>
        <supportedCurrencies>???</supportedCurrencies>
        <merchantId>???</merchantId>
        <accessToken>???</accessToken>
        <merchantName>???</merchantName>
      </account>
    </entry>
    <entry>
      <string>3DS</string>
      <account>
        <supportedCurrencies>???</supportedCurrencies>
        <merchantId>???</merchantId>
        <accessToken>???</accessToken>
        <merchantName>???</merchantName>
      </account>
    </entry>
    <entry>
      <string>RECURRING</string>
      <account>
        <supportedCurrencies>???</supportedCurrencies>
        <merchantId>???</merchantId>
        <accessToken>???</accessToken>
        <merchantName>???</merchantName>
        <useTokenId>true</useTokenId>
        <use3Dsecure>false</use3Dsecure>
        <authType>???</authType>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.payex.rest.PayExRestConfig>
```
</details>

### Attributes

| Attribute               | Description                                                                                                                          |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| supportedCurrencies     | Currencies that is supported separated with a \|                                                                                     |
| merchantId              | Id of the merchant (Payee id) in PayEx system (Provided by PayEx)                                                                    |
| accessToken             | Acccess token (Generated from PayEx Backofficec)                                                                                     |
| merchantName            | Name that will be displayed to user on PayEx side                                                                                    |
| useTokenId              | Used when doing recurring deposit. (default false)                                                                                   |
| productCategory         | Product category (used for bank link or BankDeposit)                                                                                 |
| use3Dsecure             | If transaction should be done by 3DS or not. (default false)                                                                         |
| authType                | AUTH_CAPTURE or FINAL_AUTH, use FINAL_AUTH when want to capture the deposit amount manual from Payment IQ BO. (default AUTH_CAPTURE) |
| rejectCreditCards       | true or false if credit cards should be rejected (default false)                                                                     |
| rejectDebitCards        | true or false if deibit cards should be rejected (default false)                                                                     |
| rejectConsumerCards     | true or false if consumer cards should be rejected (default false)                                                                   |
| rejectCorporateCards    | true or false if coparated cards should be rejected (default false)                                                                  |
| useLocaleFromVerifyUser | true or false if locale should be used from verify user before checking for the locale parameter from /process (default is false)    |

#### Example Routing Rule
![](/img/providers/routing/payex_rest_routing.png)

## Test Information
More testing information can be found here [here](https://developer.payex.com/xwiki/wiki/developer/view/Main/ecommerce/resources/test-data/)

### Withdrawal
To do a withdrawal we will have to do a Successful 3DS deposit before.

### Cards

#### Visa
| Card number      | Expiry                  | CVC | Type of test data                    |
|------------------|-------------------------|-----|--------------------------------------|
| 4925000000000004 | After the current month | Any | Loopback only                        |
| 4581097032723517 | After the current month | Any | Loopback only                        |
| 4581099940323133 | After the current month | Any | Loopback only                        |
| 4581096604172848 | After the current month | Any | Loopback only                        |
| 4547781087013329 | 12/20                   | 749 | 3DS ECI 6 NETS & loopback            |
| 4761739001010416 | 12/22                   | 268 | 3DS enrolled, ECI 5, Evry & loopback |
| 4581096477726290 | After the current month | 019 | Swedbank & loopback                  |

#### MasterCard
| Card number      | Expiry                  | CVC | Type of test data                    |
|------------------|-------------------------|-----|--------------------------------------|
| 5226612199533406 | 09/28                   | 602 | 3DS enrolled, ECI 6, Evry & loopback |
| 5413066399580167 | After the current month | Any | Loopback only                        |
| 5226609999109486 | After the current month | Any | Loopback only                        |
| 5226600159865967 | After the current month | Any | Loopback only                        |
| 5226603115488031 | After the current month | Any | Loopback only                        |
| 5226604266737382 | After the current month | Any | Loopback only                        |
| 5226600156995650 | After the current month | Any | Loopback only                        |

#### American Express
| Card number     | Expiry                  | CVC  | Type of test data |
|-----------------|-------------------------|------|-------------------|
| 377601000000000 | After the current month | 5252 | Amex & loopback   |

#### JCB
| Card number      | Expiry                  | CVC |
|------------------|-------------------------|-----|
| 3569990010082211 | After the current month | 123 |

#### Diners
| Card number   | Expiry                  | CVC |
|---------------|-------------------------|-----|
| 6148201829798 | After the current month | 832 |

#### Maestro
| Card number      | Expiry | CVC | Type of test data |
|------------------|--------|-----|-------------------|
| 6764429999947470 | 03/17  | 066 | Evry & loopback   |

#### Dankort
| Card number      | Expiry | CVC | Type of test data |
|------------------|--------|-----|-------------------|
| 5019994016316467 | 10/23  | 375 | NETS & loopback   |
| 5019994001307083 | 05/21  | 615 | NETS & loopback   |

#### Visa/Dankort

| Card number      | Expiry | CVC | Type of test data |
|------------------|--------|-----|-------------------|
| 4571994016401817 | 10/17# | 212 | NETS & loopback   |
| 4571994016471869 | 01/19  | 829 | NETS & loopback   |

#### Amount Error Testing Method

| Number                                         | Error message                           |
|------------------------------------------------|-----------------------------------------|
| 900313                                         | REJECTED_BY_ACQUIRER_INVALID_AMOUNT     |
| 900330                                         | REJECTED_BY_ACQUIRER_FORMAT_ERROR       |
| 900334                                         | REJECTED_BY_ACQUIRER_POSSIBLE_FRAUD     |
| 900343                                         | REJECTED_BY_ACQUIRER_CARD_STOLEN        |
| 900354                                         | REJECTED_BY_ACQUIRER_CARD_EXPIRED       |
| 900351                                         | REJECTED_BY_ACQUIRER_INSUFFICIENT_FUNDS |
| 900359                                         | CARD_DECLINED                           |
| 900362                                         | REJECTED_BY_PAYEX_CARD_BLACKLISTED      |
| 900391                                         | ACQUIRER_HOST_OFFLINE                   |
| 9002xx (xx = 10 = ten seconds, example 900210) | ACQUIRER_TIMEOUT                        |

### BankLink (BankDeposit)
BankLink can not be tested in stage so this has to be tested with live credentials and live environment. 