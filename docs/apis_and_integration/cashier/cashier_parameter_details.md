---
id: "cashier_parameter_details"
---

# Cashier Parameter Details

| Name                                                              | Type           | M/O | Description                                                                                      |
| ----------------------------------------------------------------- | -------------- | --- | ------------------------------------------------------------------------------------------------ |
| [merchantId](#merchantid)                                         | string         | M   | Merchant id                                                                                      |
| [userId](#userid)                                                 | string         | M   | The user id                                                                                      |
| [sessionId](#sessionid)                                           | string         | M   | Session Id                                                                                       |
| [environment](#environment)                                       | string         | O   | Target test, production or development. Defaults to production                                   |
| [method](#method)                                                 | string         | O   | Kind of transaction (deposit or withdrawal)                                                      |
| [mode](#mode)                                                     | string         | O   | Set a mode for the cashier (gambling or ecommerce)                                               |
| [locale](#locale)                                                 | string         | O   | Set the language (ISO string)                                                                    |
| [country](#country)                                               | string         | O   | Set the country (ISO string "alpha-3 code")                                                      |
| [attributes](#attributes)                                         | object         | O   | Pass in an object of arbitrary attributes                                                        |
| [user](#user)                                                     | object         | O   | Pass in an object of arbitrary user properties                                                   |
| [selectlastusedtxmethod](#selectlastusedtxmethod)                 | boolean        | O   | Auto-select the last used paymentmethod                                                          |
| [providerType](#providertype)                                     | string         | O   | Preselect payment method by type (creditcard, trustly etc)                                       |
| [autoProcess](#autoprocess)                                       | boolean        | O   | Auto-submit transaction. **Requires amount & providerType to be set**                            |
| [storeAccount](#storeaccount)                                     | boolean        | O   | Should the account be saved                                                                      |
| [saveAccountOption](#saveaccountoption)                           | boolean        | O   | Display 'save account' option for new payment methods                                            |
| [showAccounts](#showaccounts)                                     | string         | O   | How/Where should saved accounts be shown?                                                        |
| [accountDelete](#accountdelete)                                   | boolean        | O   | Allow user to delete saved accounts (only deposit)                                               |
| [amount](#amount)                                                 | string         | O   | Pre-set an amount (mandatory if mode is ecommerce)                                               |
| [singlePageFlow](#singlepageflow)                                 | boolean        | O   | Simplified flow, pick payment method, account and amount all in one view                         |
| [showAmountLimits](#showamountlimits)                             | boolean        | O   | Show the amount limits for the selected payment method                                           |
| [scrollToOffset](#scrolltooffset)                                 | boolean        | O   | On mobile, when picking a payment method we scroll to it, set an offset                          |
| [showTransactionOverview](#showtransactionoverview)               | boolean        | O   | Show amount, fee and total amount                                                                |
| [predefinedValues](#predefinedvalues)                             | boolean        | O   | Display predefined amounts                                                                       |
| [predefinedAmounts](#predefinedamounts)                           | Array          | O   | Specify which amounts to be available                                                            |
| [showReceipt](#showreceipt)                                       | boolean/string | O   | Show receipt page. If false a loader is shown instead                                            |
| [showHeader](#showheader)                                         | boolean        | O   | Should the header be visible                                                                     |
| [showFooter](#showfooter)                                         | boolean        | O   | Should the footer be visible                                                                     |
| [tabs](#tabs)                                                     | boolean        | O   | Add tab navigation for payment methods and pages.                                                |
| [dropdownTabs](#dropdowntabs)                                     | boolean        | O   | Display tabs as dropdown instead of buttons.                                                     |
| [pendingTab](#pendingtab)                                         | boolean        | O   | Enable Pending Transactions tab.                                                                 |
| [history](#history)                                               | boolean        | O   | Enable Transaction History tab.                                                                  |
| [kycTab](#kycTab)                                                 | boolean        | O   | Enable KYC tab.                                                                                  |
| [containerHeight](#containerheight)                               | string         | O   | Set a height for the cashier-container (auto, px or %)                                           |
| [containerMinHeight](#containerminheight)                         | string         | O   | Min-height for the surrounding iframe. Only used when displayed using the bootstrapper           |
| [containerWidth](#containerwidth)                                 | string         | O   | Set a width for the cashier-container (px or %)                                                  |
| [bonusCode](#bonuscode)                                           | string         | O   | Pass in a bonus code                                                                             |
| [showBonusCode](#showbonuscode)                                   | boolean        | O   | Show input field for bonus code                                                                  |
| [channelId](#channelid)                                           | string         | O   | Pass in a channel id                                                                             |
| [logoUrl](#logourl)                                               | string         | O   | Url to logo to show in header                                                                    |
| [logoSize](#logosize)                                             | string         | O   | Set size to the passed in logo                                                                   |
| [listRadio](#listradio)                                           | boolean        | O   | Show radio buttons for each payment method (default: true)                                       |
| [amountFirst](#amountfirst)                                       | boolean        | O   | Set amount in a seperate step, before selecting payment method                                   |
| [receiptAmountDisplayStyle](#receiptamountdisplaystyle)           | string         | O   | Should the amount in receipt show as **symbol** e.g € ISO-3 (e.g EUR) or as                      |
| [receiptAmountTransactionStyle](#receiptamounttransactionstyle)   | string         | O   | Show receipt header as either **Amount** or TxAmount                                             |
| [receiptExcludeKeys](#receiptexcludekeys)                         | Array          | O   | Keys which should be excluded on the receipt                                                     |
| [layout](#layout)                                                 | string         | O   | **Vertical** or horizontal layout                                                                |
| [logoFullWidth](#logofullwidth)                                   | boolean        | O   | When combined with a logoUrl, a header containing the logo is shown                              |
| [accountId](#accountid)                                           | string         | O   | Pass in the id of a saved account to pre-select it                                               |
| [autoOpenFirstPaymentMethod](#autoopenfirstpaymentmethod)         | boolean        | O   | Auto-open the first payment method. Default: true                                                |
| [scrollToPm](#scrolltopm)                                         | string         | O   | Scroll behaviour when selecting a payment method                                                 |
| [globalSubmit](#globalsubmit)                                     | boolean        | O   | Display submit button at the bottom, under payment methods                                       |
| [showTermsConditions](#showtermsconditions)                       | boolean        | O   | Show text + link + optional logo for terms&condition                                             |
| [allowCancelPendingWithdrawal](#allowcancelpendingwithdrawal)     | boolean        | O   | Allow user to cancel a pending withdrawal                                                        |
| [showListHeaders](#showlistheaders)                               | boolean        | O   | Show headers in list view, Saved accounts & Payment methods                                      |
| [listType](#listtype)                                             | string         | O   | Display the payment methods in 'list' or 'grid' view.                                            |
| [displayLogoOrName](#displaylogoorname)                           | string         | O   | Display only logo, name or both.                                                                 |
| [pollLimit](#polllimit)                                           | number         | O   | Number of tries to poll for an updated tx status                                                 |
| [errorMsgTxRefId](#errormsgtxrefid)                               | boolean        | O   | Show txRefId in error messages. Defaults to false.                                               |
| [showFee](#showfee)                                               | boolean/string | O   | Display fee in transaction overview                                                              |
| [disableBtnAtZero](#disablebtnatzero)                             | boolean        | O   | Enable submit button without amount entered for all payment methods                              |
| [pmListLimit](#pmlistlimit)                                       | number         | O   | Number of new payment methods in the list to show in the list                                    |
| [alwaysShowSubmitBtn](#alwaysshowsubmitbtn)                       | boolean        | O   | Always show a sticky submit button at the bottom                                                 |
| [showTransactionsOnly](#showtransactionsonly)                     | boolean        | O   | Land on transaction history page on load                                                         |
| [font](#font)                                                     | string         | O   | Configure your custom font                                                                       |
| [customLogoFileName](#customlogofilename)                         | string         | O   | Configure your custom logo.                                                                      |
| [trackingPixels](#trackingpixels)                                 | array          | O   | Set up custom tracking pixels for key events.                                                    |
| [trackingScripts](#trackingscripts)                               | array          | O   | Set up custom tracking scripts for key events.                                                   |
| [hideTxOverview](#hidetxoverview)                                 | boolean        | O   | Show/hide transaction overview.                                                                  |
| [allowMobilePopup](#allowmobilepopup)                             | boolean        | O   | Allow providers to open on a new window on mobiles.                                              |
| [fetchConfig](#fetchconfig)                                       | boolean        | O   | Fetch cashier config from PaymentIQ Backoffice                                                   |
| [blockBrowserNavigation](#blockbrowsernavigation)                 | boolean        | O   | Prevents the user from navigating back and forward via browser navigation.                       |
| [showAmount](#showamount)                                         | boolean        | O   | Display amount options.                                                                          |
| [receiptBackBtn](#receiptbackbtn)                                 | boolean        | O   | Show a back button on receipt page                                                               |
| [pendingTxHeader](#pendingtxheader)                               | boolean        | O   | Show the header with pending withdrawals.                                                        |
| [showtermsAndConditionsTemplate](#showtermsandconditionstemplate) | boolean        | O   | Show a defined terms&conditions template configured in PaymentIQ backoffice                      |
| [autoSetIframeProviderHeight](#autosetiframeproviderheight)       | boolean        | O   | Set provider iframe height based on the provider-config from PaymentIQ Backoffice                |
| [newPaymentBtn](#newpaymentbtn)                                   | boolean        | O   | Display a Make new payment-button on the status page                                             |
| [initLoadErrorTimeout](#initloaderrortimeout)                     | number         | O   | Timeout before the onLoadError callback is triggered if the cashier hasn't loaded.               |
| [showCookiesWarning](#showcookieswarning)                         | number         | O   | Show a warning notice that third-party-cookies are disabled.                                     |
| [checkWithdrawalBalance](#checkwithdrawalbalance)                 | boolean        | O   | Client validation if a withdrawal is allowed based on user balance.                              |
| [lastUsedDepositAmount](#lastuseddepositamount)                   | boolean        | O   | Set the amount to the amount from the last successful deposit                                    |
| [historyDateOptions](#historydateoptions)                         | boolean        | O   | Time range options when viewing the transaction history                                          |
| [showBackAtInitPath](#showbackatinitpath)                         | boolean        | O   | Display back button when there is a previous route and current route is the landing route        |
| [allowWindowClose](#allowwindowclose)                             | string         | O   | List of string who has a window flow that needs a manual close of that window once finished.     |
| [enableTermsTemplateFor](#enabletermstemplatefor)                 | string         | O   | Restrict displaying terms & conditions template to only a list of string with selected providers |
| [fixedProviderType](#fixedprovidertype)                           | boolean        | O   | Limit to only render providers set in providerType, even when navigating away from the provider. |
| [hardClose](#hardclose)                                           | boolean        | O   | Close potential provider windows when cashier tab/window is closed.                              |
| [prefillCreditcardHolder](#prefillcreditcardholder)               | boolean        | O   | Populate cardHolder name.                                                                        |

---------------

## merchantId
**Type**: ```String```

**Required**

merchantId in PaymentIQ

---------------

 ## userId
**Type**: ```String```

**Required**

userId in PaymentIQ

---------------

 ## sessionId
**Type**: ```String```

**Required**

sessionId in PaymentIQ

---------------

 ## environment
**Type**: ```String```

**Default**: ```production```

Environment of PaymentIQ you want to target.

Available values: ```production```, ```development```, ```test```

---------------

 ## method
**Type**: ```String```

**Default**: ```deposit```

Available values: ```deposit```, ```withdrawal```

---------------

 ## mode
**Type**: ```String```

**Default**: ```gambling```

Available modes are ```gambling```, ```ecommerce```, ```accountVerification```.

`gambling` - Amount can be changed by user.

`ecommerce` - Amount should be predefined and can not be changed by user.

`accountVerification` - Amount is unavailable. Available from Cashier `version 1.2.0`.

---------------

 ## locale
**Type**: ```String```

**Default**: ```null``` (will fallback to en_GB if none is resolved from PIQ user)

If no locale is specified during setup, the locale set for the userId will be used, but only when it has been received. Until then fallback will be `en_GB`. We recommend you set a locale during setup.

**NOTE** locale can not be set in PaymentIQ Backoffice config via merchantCashierConfig. If you wish to specify locale (and not take it automatically from the PIQ-user), you must do so during setup.

Available values: `sv_SE`, `en_US`, `en_GB`, `no_NO`, `fi_FI`, `pt_BR` (more available)

---------------

---------------

 ## country
**Type**: ```String```

**Default**: ```swe```

This flag is being used when fetching configurations via backoffice (fetchConfig=true). By default this is set to `swe` but you can change this
to the country you want. This can be used in backoffice for rules or for filtering the inputs that are set for a specific market.

---------------

| [country](#country)                         | string   | O | Set the country (ISO string "alpha-3 code")                   |

## attributes
**Type**: ```Object```

**Default**: ```{}```

Pass in custom attributes you want to include in the transaction.

If targeting the cashier directly via url, attribute-properties are passed in using dot-annotation:

```
https://pay.paymentiq.io/cashier/master/?environment=test&attributes.foo=bar
```

---------------

## user
**available from**: `bootstrap-script version 1.0.18` + `cashier version 1.0.16`
 
**Type**: ```Object```

**Default**: ```{}```

Pass in information about the user that can be used to pre-populate input fields.

```
...configuration,
user: {
  phonenumber: '08080808',
  email: 'jane.doe@example.com
}
```

Please note that Creditcard fields can not be prepopulated

If you pass in this user object, any input field that has a name-attribute that matches the passed in property will get prefilled.

```
<input data-v-54df90cb="" pattern=".+@globex.com&quot;" id="payPalEmail" name="email" type="email" inputmode="email" class="input w-full">
```

Since this input has `name="email"` it will get prefilled.

Plese note that some payment methods use specific field-names, meaning in order to pre-populate certain fields might require you to pass in a specific key+value for that specific payment method to get pre-populated. Please consult support in these cases.

If targeting the cashier directly via url, user-properties are passed in using dot-annotation:

```
https://pay.paymentiq.io/cashier/master/?environment=test&showAccounts=false&user.email=email@example.com
```

---------------

 ## selectlastusedtxmethod
**Type**: ```Boolean```

**Default**: ```false```

Auto-select the last used payment method account

---------------

 ## providerType
**Type**: ```String```

**Default**: ```null```

Pre-select a payment method by specifying its name. For example: ```creditcard```, ```trustly```

Can also be matched against the `service` used for the payment method.

---------------

 ## autoProcess
**Type**: ```Boolean```

**Default**: ```false```

Option to automatically submit a transaction.
Will only be triggered if all the necessary information is provided 

Usally means when **amount** and **providerType** is provided.
For payment methods that require additional information (email, phonenumber for example), that has to be provided as well.
Pass this in using the [user](#user) property.

---------------

 ## storeAccount
**Type**: ```Boolean```

**Default**: ```true```

Set if account should be stored as visible after a transaction is done.

---------------

 ## saveAccountOption
**Type**: ```Boolean```

**Default**: ```false```

Display a 'Save account' checkbox for new payment methods, this toggles [storeAccount](#storeaccount)

---------------

 ## showAccounts
**Type**: ```String```

**Default**: ```list-first```

**Available options**: ```list-first```, ```list-with-pm```, ```inline```, ```false```

| Value            | Description                                                                                                                                                                                                                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **list-first**   | Displays all saved accounts at the top of the list.                                                                                                                                                                                                                                              |
| **list-with-pm** | Displays all saved accounts next to its payment method, i.e all saved credit cards will be                                              shown next to the creditcard payment method.                                                                                                             |
| **inline**       | Displays the saved accounts in a dropdown inside the payment method. For example: When you                                              toggle open creditcard a dropdown will be displayed containing all saved accounts + option to                                            add a new card. |
| **false**        | No saved accounts will be displayed.                                                                                                                                                                                                                                                             |

---------------

 ## accountDelete
**Type**: ```Boolean```

**Default**: ```true```

Only available for `deposit`

Allow users to delete saved accounts

---------------

 ## amount
**Type**: ```String```

**Default**: ```null```

Predefine an amount for the transaction. If mode is set to 'ecommerce' this is **mandatory** and can't be changed by the user.

---------------

 ## singlePageFlow
**Type**: ```Boolean```

**Default**: ```false```

Boolean value that if set to true will present a simplified flow, a single view where the user makes all the options in regards to the payments (before routed to the provider)

---------------

 ## showAmountLimits
**Type**: ```Boolean```

**Default**: ```false```

Every payment method can have amount limits configured, min and max values for what they accept. If set to true, these will be shown in the amount input (only viable for mode = 'gambling')

---------------

 ## scrollToOffset
**Type**: ```number```

**Default**: ```0```

When a payment method is selected, [scrollToPm](#scrolltopm) can be offset by a given px-value.

On mobiles the selected payment method will be scrolled to be shown at the top of the screen. This can also be offset.

---------------

 ## showTransactionOverview
**Type**: ```Boolean```

**Default**: ```true```

Boolean value that if set true shows an overview of the amout, fee amount and total.

---------------

 ## predefinedValues
**Type**: ```Boolean```

**Default**: ```true```

Should predefined amount values be shown? They default to show ```200```, ```500```, ```1000``` but can be manually set using [predefinedAmounts](#predefinedamounts)

---------------

 ## predefinedAmounts
**Type**: ```Array<number>```

**Default**: ```[200, 500, 1000]```

Set your custom predefined amounts to allow the user to quick-select.

---------------

 ## showReceipt
**Type**: `Boolean | string`

**Default**: ```true```

**Available values**: `true`, `false`, `only`

Should the app display a receipt page upon a successful transaction? 

If set to false, the app will instead display a loading screen saying "Taking you back to merchant".
The idea here is that the merchant will react on the success-callback from the Javascript-API and close the cashier.

If set to `only`, and if a txRefId is passed in, then the app will only display the receipt for the given transaction.

---------------

 ## showHeader
**Type**: ```Boolean```

**Default**: ```true```

In some views, a header can be shown, containing a back button, the current payment method name and icon.

Will be shown in: Payment method detail view, singlePageFlow-view, setAmount-view.

---------------

 ## showFooter
**Type**: ```Boolean```

**Default**: ```true```

Display a footer, can contain a backbutton in the views where back is availble. 
Can also dispaly a sticky Terms&Condition (or some other message) when combined with [showTermsConditions](#showtermsconditions)

---------------

 ## tabs
**Type**: ```Boolean```

**Default**: ```false```

**Requires**: [`mode: gambling`](#mode)

Adds a tab navigation for payment methods and pages. Default pages are **Deposit** and **Withdrawal** but [Pending Transactions](#pendingtab), [Transaction History](#history) and [KYC](#kyctab) can be added as well.

Tabs can also be displayed as a [dropdown menu](#dropdowntabs).

 ### dropdownTabs
**Available from**: `version 1.1.8`

**type**: `boolean`

**Default**: `false`

**Requires**: [`tabs: true`](#tabs)

Displays tabs as a dropdown menu instead of buttons.

 ### pendingTab
**Available from**: `version 1.1.8`

**type**: `boolean`

**Default**: `false`

**Requires**: [`tabs: true`](#tabs)

Enables **Pending Transactions** in the tab menu.

 ### history
**type**: `boolean`

**Default**: `false`

**Requires**: [`tabs: true`](#tabs)

Enables **Transaction History** in the tab menu.

 ### kycTab
**Available from**: `version 1.3.11`

**type**: `boolean`

**Default**: `false`

**Requires**: [`tabs: true`](#tabs)

Enables **KYC** in the tab menu.

---------------
 ## containerHeight
**Type**: ```String```

**Default**: ```auto```

If set to auto, the application iframe will adjust its height to the content being displayed - taking up as much height as needed.

If you wish to limit the height, just set a fixed height.

---------------

 ## containerMinHeight
**Type**: ```String```

**Default**: ```0```

**Example**: ```600px```

Set a minHeight to the iframe around the application.

From PIQ Cashier Integration version `1.3.9` (only the npm-package) containerMinHeight will also be set to the outer container of the cashier in the iframe.

---------------

 ## containerWidth
**Type**: ```String```

**Default**: ```'100%'```

Set a width for the cashier, either in `px` or `%`

**Example**: ```'600px' or '80%'```

---------------

 ## bonusCode
**Type**: `String`

**Default**: ```null```

Pass in a bonus code to PaymentIQ as an attribute.

This value can also be set during runtime via the [javascript api](cashier_javascript_api#set)

```
api.set({
  config: {
    bonusCode: 'foobar'  
  }
})
```

---------------

 ## showBonusCode
**Type**: ```Boolean```

**Default**: ```false```

If set to true, an input field will be shown under amount where the user can set a bonus code.

The value will be passed into PaymentIQ.
No validation of the bonusCode will be made in the cashier - it will only pass it along.

If validation is required to be made before the transaction is being handled the bonus code input must be placed outside the cashier - validated and then injected to the cashier using the JavascriptAPI.set()

If the amount should be updated with the bonus code, the same approach can be used with JavascriptApi.set() in order to updated the amount displayed in the cashier.

---------------

 ## channelId
**Type**: `String`

**Default**: ```Mac | Window | iOS | Android``` (value based on your device)

Pass in a channelId to PaymentIQ. Can also be set to a fixed custom value.

---------------

 ## logoUrl
**Type**: `String`

**Default**: ```null```

Set a url to a logo to show in a header (header above the "showHeader")

---------------

 ## logoSize
**Type**: `number`

**Default**: ```120```

Set a width for the logo

---------------

 ## listRadio
**Type**: ```Boolean```

**Default**: ```true```

Display a radio select next to each paymentMethod. When selected, the radio will be marked as selected

---------------

 ## amountFirst
**Type**: ```Boolean```

**Default**: ```false```

An alternative flow where the user must select amount first in a seperate view, before picking a payment method

---------------

 ## receiptAmountDisplayStyle
**Type**: `String`

**Default**: ```symbol```

Available values: ```symbol```, ```ISO-3```

If set to symbol, the receipt will show the amount with, e.g 10 € or $10, 10 Kr

If set to ISO-3 it will show as 10 EUR, 10 USD or 10 SEK

---------------

 ## receiptAmountTransactionStyle
**Type**: ```String```

**Default**: ```TxAmount```

Available values: ```TxAmount```, ```Amount```

If set to TxAmount, the receipt will show the actual amount + correct currency the transaction was made with. The user might have selected to deposit 200 SEK, but the actual transaction at the provider was made using 18.88 EUR - 18.88 EUR will then be shown.

If set to Amount it will show as 200 SEK.

---------------

 ## receiptExcludeKeys
**Type**: ```Array```

**Default**: ```[]```

Keys which should be excluded on the receipt page.

These keys are coming from the `Check Transaction Status` request in the parameter `messages`. There you have the keys `label`, `keys`, and `value`.

The keys to use here is the values found in `keys` parameter. Take one of them and add it to this array as a string and the key will be excluded in
receipt page. The text being rendered to receipt page are taken from the `label` parameter.

As of ```version 1.3.1``` it's possible to target translations for a specific `service` or `providerType` if they are defined, e.g. `{service}_creditcarddeposit.receiptDepositTxAmount`.

Available values: 

| Value                                                        |
| ------------------------------------------------------------ |
| **creditcarddeposit.receiptDepositTxAmount**                 |
| **receiptDepositTxAmount**                                   |
| **creditcarddeposit.receiptDepositInProgressExtraMsg**       |
| **receiptDepositInProgressExtraMsg**                         |
| **creditcarddeposit.receiptDepositPspRefId**                 |
| **receiptDepositPspRefId**                                   |
| **creditcarddeposit.receiptDepositAccountToCharge**          |
| **receiptDepositAccountToCharge**                            |
| **creditcarddeposit.receiptDepositFee**                      |
| **receiptDepositFee**                                        |
| **receiptDepositTxId**                                       |
| **txRefId**                                                  |
| **creditcardWithdrawal.receiptWithdrawalAccountToCharge**    |
| **receiptWithdrawalAccountToCharge**                         |
| **creditcardWithdrawal.receiptWithdrawalTxAmount**           |
| **receiptWithdrawalTxAmount**                                |
| **creditcardWithdrawal.receiptWithdrawalPspRefId**           |
| **receiptWithdrawalPspRefId**                                |
| **creditcardWithdrawal.receiptWithdrawalInProgressExtraMsg** |
| **receiptWithdrawalInProgressExtraMsg**                      |
| **creditcardWithdrawal.receiptWithdrawalFee**                |
| **receiptWithdrawalFee**                                     |

---------------

 ## layout
**Type**: ```String```

**Default**: ```vertical```

Available values: ```vertical```, ```horizontal```

If set to horizontal, the details of a payment method will be shown side by side with the list of payment methods.

---------------

 ## logoFullWidth
**Type**: ```Boolean```

**Default**: ```false```

If set to true, the container showing the logo set in [logoUrl](#logourl) will be displayed with 100% width.

---------------

 ## accountId
**Type**: `String`

**Default**: ```null```

Preselect a saved account in PaymentIQ by its accountId.

---------------

 ## autoOpenFirstPaymentMethod
**Type**: ```Boolean```

**Default**: ```true```

Automatically open the first paymentMethod in the list.

---------------

 ## scrollToPm
**Type**: ```String```

**Default**: ```nearest```

Available values: `nearest`, `center`, `start`, `end`

Will auto scroll and display the selected payment method at either top, center, end or nearest.

---------------

 ## globalSubmit
**Type**: ```Boolean```

**Default**: ```false```

If set to true, a single submit button will be shown at the bottom and all times instead of under the expanded payment method.

---------------

 ## showTermsConditions
**Type**: ```Boolean```

**Default**: ```false```

If set to true, and messages are added in PaymentIQ for:

termscondition.link.text (text to be displayed)
termscondition.link.url (optional link to the text)
termscondition.link.background (optional image to show)

The footer will always show (sticky) at the bottom of the page.

---------------

 ## allowCancelPendingWithdrawal
**Type**: ```Boolean```

**Default**: ```false```

If set to true, the cashier will display a panel at the top in the payment methods view/singlePageFlow when the current user have a withdrawal(s) that is pending approval, meaning it has been requested but not yet approved and processed. The user can select to cancel the withdrawal(s), putting the transaction in a CANCELLED-state.

---------------

 ## showListHeaders
**type**: `Boolean`

**Default**: `false`

If set to true, a header/section will be shown over the saved accounts and another one over the payment methods.
Message keys used are ```saved_accounts```and ```payment_methods```

---------------

 ## listType
**type**: `string`

**Default**: `list`

**Available values**: `list`, `grid`

If set to `list`, payment methods will appear in a vertical list.

If set to `grid` each payment method will appear as a card in a grid.

---------------

 ## displayLogoOrName
**type**: `string`

**Default**: `both`

Available values: `both`, `logo`, `name`

Meant to be used together with `listType=grid`. `both` shows both logo & name of the payment method, while `logo` only shows the logo and `name` only the name.

---------------

 ## pollLimit
**type**: `number`

**Default**: `5`

Number of retiries when checking transaction status.
When limit is reached without an updated status, a page will be shown saying the transaction is pending.

---------------

 ## errorMsgTxRefId
**type**: `boolean`

**Default**: `false`

Show txRefId in error messages/signs. Defaults to false.

---------------

 ## showFee
**type**: `boolean || string`

**Default**: `true`

Hide or display fee's with false or true, or set to 'deposit' to only display fee's during deposits or 'withdrawal' to only display during withdrawals.

---------------

 ## disableBtnAtZero
**type**: `boolean`

**Default**: `true`

Option to enable or disable the submit button when no or zero amount has been entered.

As of `version 1.3.9` this option is available for all modes. In earlier versions, this only works for [ecommerce mode](#mode).

---------------

 ## pmListLimit
**type**: `number`

**Default**: `20`

Decide how many new payment methods should be displayed, the rest will be collapsed and available 
through the "Show more payment methods" button at the bottom.

---------------

 ## alwaysShowSubmitBtn
**type**: `boolean`

**Default**: `false`

Have the possibility to always display an floating submit bottom at the bottom of the page when the real submit button is out of the screenview.

---------------

 ## showTransactionsOnly
**type**: `boolean`

**Default**: `false`

Set to true if you want to land on transactions history page.

---------------

 ## font
**Available from**: `version 1.0.16`

**Can not be configured from PaymentIQ Backoffice**

**type**: `string` `{source}, {fontName}, optional: {customFileReference}`

**Default**: `null` (Resolves [Gilroy](https://www.myfonts.com/fonts/radomir-tinkov/gilroy/))

#### Google font
Configure your custom font. You can either select a font available on [google fonts](https://fonts.google.com/) or using a custom one.

If you want to use a google font, configure it by passing in:

```
font: 'google, {yourFont}'
```

E.g
```
font: 'google, Roboto'
font: 'font=google,Exo+2:400,500,600'
font: 'font=google,Exo 2:400,500,600'
```

#### Custom
If you want to configure a custom font, e.g if you host it yourself. Keep in mind that fonts are copy-right protected. You must have a licence to use fonts that are copy-right protected.

```
font: 'custom, {yourFont}, {customFileReference}'
```

```
font: 'custom, WookieeFont, wookiee-industries'
```

Where customFileReference will be the name of your company/brand.
The customFileReference will be used to fetch a css-file Devcode will host on [https://static.paymentiq.io/assets/fonts/custom-font-wookiee-industries.css](https://static.paymentiq.io/assets/fonts/custom-font-wookiee-industries.css)

In that file the font will be defined with a url to their source using `@font-face` and the cashier will automatically download and apply it.

---------------

 ## customLogoFileName

**Can not be configured from PaymentIQ Backoffice.**

**type**: `string`

**Default**: `null`

The given value must consist of the image asset file name and extension (e.g. `Worldline-Mint-Horizontal.svg`) and will be retrieved from `static.paymentiq.io` where the asset must be hosted.

---------------
 ## trackingPixels
**Available from**: `version 1.0.17`

**type**: `array of objects`

**Default**: `null`

You can set up your custom tracking pixels for some speicific type of cashier events.

The following cashier event types are available:
**All deposits- `allDeposits`.**
**First deposit, `firstDeposit`.** *
**And all withdrawals, `allWithdrawals`.**

* In order to use and recieve the `firstDeposit` event, you must configure this via the `merchantCashierConfig` XML file in PaymentIQ backoffice
and add the tag `<checkIfFirstDeposit>true</checkIfFirstDeposit>` and also add `fetchConfig=true` to your static configuration of the cashier.

Read more about backoffice configuration [here](cashier_use_merchantcashierconfig)

You can add as many tracking pixels for the same type of event as you like.

Configure this in the following way:

```
var cashierConfigs = {
  ...your-cashier-configs,
  trackingPixels: [
    {
      type: 'allDeposits',
      scriptSrc: 'https://my-script.com',
      scriptAttrs: 'async, type=text/javascript',
      trackingName: 'All deposits',
      imgSrc: 'https://my-tracking-img-pixel.png',
      imgAttrs: 'weareawesome=true, alt=trackingpixel'
    },
    { ... } // Keep adding how many tracking pixel objects as you prefer.
  ]
}
```

**Flag explanations**
`type` # Add one of these event types: 'firstDeposit', 'allDeposits', or 'allWithdrawals'
`scriptSrc` # Optional script source to load when intializing the cashier,
`scriptAttrs` # Optional script tag attributes
`trackingName` # Custom name of this type of event, eg. "All-Deposits"
`imgSrc` # Add a source to the tracking pixel (img) that should be fired when the event occurs
`imgAttrs` # Optional img tag attributes

---------------

 ## trackingScripts
**Available from**: `version 1.2.0`

Requires configuration to be setup in PaymentIQ Backoffice -> configuration -> MerchantCashierConfig

**type**: `array`

**Default**: `null`

Set up custom tracking scripts for key events.

These scripts will trigger once the event occurs.

The following cashier event types are available: `allDeposits`, `firstDeposit`, `allWithdrawals`

You can add as many tracking scripts as you like.

Configure this in MerchantCashierConfig

```
<com.devcode.paymentiq.service.cashier.MerchantCashierConfig>
    <enabled>true</enabled>
    <checkIfFirstDeposit>false</checkIfFirstDeposit>
    <config>
     {
      ...otherConfig,
      "trackingScripts": [
          {
            "event": "allDeposits",
            "src": "https://someorigin.com/?AccountID={userId}&amp;Value={amount}&amp;Currency={currency}",
            "attrs": "async type=text/javacript"
          },
          {
            "event": "allWithdrawals",
            "src": "https://someorigin.com/?AccountID={userId}&amp;Value={amount}&amp;Currency={currency}",
            "attrs": "async type=text/javacript"
          },
          {
            "event": "firstDeposit",
            "src": "https://someorigin.com/?AccountID={userId}&amp;Value={amount}&amp;Currency={currency}",
            "attrs": "async type=text/javacript"
          }
        ]
    }
    </config>
    <css></css>
</com.devcode.paymentiq.service.cashier.MerchantCashierConfig>  
```

**trackingScript properties**

`event` - When should the script be executed: 'firstDeposit', 'allDeposits', or 'allWithdrawals'

`src` - Script src to load. Can be configured to map dynamic values using `{property}`. Reach out to our onboarding agent or PaymentIQ support to configure these values. Note that the `&` needs to be url-encoded as `&amp;`

`attrs` - Optional script attributes

---------------

 ## hideTxOverview
**Available from**: `version 1.0.18`

**type**: `boolean`

**Default**: `false`

Set to true if you want to hide the transaction overview. Default is set to false and will display the transaction overview with total amount and fees.

---------------

 ## allowMobilePopup
**Available from**: `version 1.0.19`

**type**: `boolean`

**Default**: `false`

**Recommend setting this to true.**
**Currently issues with redirecting back to host page on mobile devices - working on resolving this**

Allow providers to be opened as new windows on mobiles. Default value is set to false which will not allow new window popups on mobiles,
but will instead make a reload to the providers page, and redirect back once the transaction is done.

**If set to 'false':**
When redirected back to your page, a url query parameter called `txRefId` will be appended to the url.
If you don't have a unique endpoint on your site that automatically shows the cashier, you will have to use this url query param to determine if the cashier should automatically show in order to handle the redirect properly.

---------------

 ## fetchConfig
**Available from**: `version 1.1.0`

**type**: `boolean`

**Default**: `false`

Cashier configuration can now be fetched and edited from PaymentIQ Backoffice. [More details about setup here](cashier_use_merchantcashierconfig)

This feature needs to be enabled during [bootstrap setup](cashier_init_bootstrapper) - i.e will not be enabled by setting to true inside PaymentIQ Backoffice.

---------------

 ## receiptBackBtn
**Available from**: `version 1.1.7`

**type**: `boolean`

**Default**: `false`

Set to true if you want to display a back/new payment button on receipt page.

Translation for this buttons label is "make_new_payment".

---------------

 ## pendingTxHeader
**Available from**: `version 1.1.8`

**type**: `boolean`

**Default**: `true`

Hide or show the header with pending withdrawals.

Header will be displayed if both pendingTxHeader and allowCancelPendingWithdrawal is true and when there are pending withdrawals in the users account.

---------------

 ## showtermsAndConditionsTemplate
**Available from**: `version 1.1.9`

**type**: `boolean`

**Default**: `true`

If you have added a "terms and condition" template, you can choose to hide or display it with this flag. Defaults to true (display).

Contact our support team if you want to add a new 'terms and condition' template.

---------------

 ## autoSetIframeProviderHeight
**Available from**: `version 1.1.10`

**type**: `boolean`

**Default**: `true`

Provider iframe height will be set based on the {provider}Config from PaymentIQ Backoffice if set.

To turn this behaviour off, just set this flag to false.

---------------

 ## newPaymentBtn
**Available from**: `version 1.1.11`

**type**: `boolean`

**Default**: `false`

Display a "Init new payment" button at status page when transaction was not succesful or cancelled.

This can be when status is PENDING, CANCELLED, or anything else than SUCCESS.

The text of this button is translated with the key `make_new_payment`.

This is a text styled button and can be customized the way you want by targeting the css class of `make-new-payment-text`

---------------

 ## initLoadErrorTimeout
**Available from**: `version 1.1.14`
**Bootstrap script version**: `1.3.2`

**type**: `number`

**Default**: `10 seconds (10000)`

Set an timeout in milliseconds for how long you will wait for cashier to load before triggering the onLoadError callback. 

---------------

 ## blockBrowserNavigation
**Available from**: `version 1.2.0`

**type**: `boolean`

**Default**: `true`

Prevents the user from navigating back and forward via browser navigation options. Defaults to true.

---------------

 ## showAmount
 **Available from**: `version 1.2.0`

**type**: `boolean`

**Default**: `true`

Display amount options. You can hide amount selections and options by setting this to false.

If you want to use this for zero amount transactions. You can combine this with `mode="ecommerce` `disableBtnAtZero=false` and
if you want to hide transaction overview (amount and fees) you can also add `hideTxOverview=false`.

If you are doing this for account verifications. You can simply just use `mode=accountVerification`.

---------------

 ## showCookiesWarning
**Available from**: `version 1.2.0`

**type**: `boolean`

**Default**: `true`

1.2.0 introduced an update where third-party-cookis are no longer required.
The app will however have some features that will be limited with third-party-cookies disabled - therefore the default behaviour is to display a warning notice about this. This warning can be toggled off so that it's not shown.

Features like provider-redirect (transaction is initialized and the top window is redirected to the provider) is not supported without cookies. After the transction is completed and a redirect back is triggered, cookies are used to resume the flow.

We also require enabled cookies for dealing with providers that during the transacion flow, after the provider has been opened in an iframe or window, trigger a second window to be opened. In that case we rely on cookies to trigger a "Please close this window" once the transaction is completed.

---------------

 ## checkWithdrawalBalance
**Available from**: `version 1.2.2`

**type**: `boolean`

**Default**: `false`

A client validation for allowing/not allowing a withdrawal based on the user's balance. If the set amount is higher than the user's balance - the client will block the request for making a withdrawal. PIQ will do this too but this happens without any requests being made.

To use this - ensure that your system sends the user's balance to PIQ.

---------------

 ## lastUsedDepositAmount
**Available from**: `version 1.2.5`

**type**: `boolean`

**Default**: `false`

If set to true, the amount will be set to the same amount as the user's last successful deposit.

---------------

 ## historyDateOptions
**Available from**: `version 1.2.7`

**type**: `boolean`

**Default**: `true`

Time range options when viewing the transaction history.

Options are today, yesterday, last week, and last month.

This is true by default.

---------------

 ## showBackAtInitPath
**Available from**: `version 1.2.8`

**type**: `boolean`

**Default**: `true`

Display back button when there is a previous route and current route is the landing route.

If you for example set `providerType`, the landing route will be `/payment-method` but technically the previous route is `/list-paymentm-methods`.

If you don't want back button to show when you are at landing page, in this case `/payment-method`, then set this property to `false`

---------------

 ## allowWindowClose
**Available from**: `version 1.2.8`

**type**: `string`

Add payment providers to this list of string who has a window flow that needs a manual close of that window once transaction is finished.

Example:
```
allowWindowClose: 'providerOne, providerTwo, providerThree'
```

Now these will not be displayed as cancelled transaction in cashier as it would normally show when a user manually closes a window. 

Some providers requires the user to manually close the window once the transaction is finished. If so.. add that provider to this list.

---------------

 ## enableTermsTemplateFor
**Available from**: `version 1.2.10`

**type**: `string`

Restrict displaying terms & conditions template to only a list of string with selected providers instead of all.

Example:
```
enableTermsTemplateFor: 'paypal, trustly, skrill'
```

In the code example above we have set to only display the terms and conditions template for paypal, trustly and skrill. Providers name are based on the value in `providerType` or `service` value.

---------------

 ## fixedProviderType
**Available from**: `version 1.2.10`

**type**: `boolean`

**Default**: `false`

Limit to only render providers specified in providerType, even when navigating away from the provider.

When providerType is set you end up on a /payment-method route that only displays the selected provider, but when you navigate away from that
we still could display all the other payment methods. If that is unwanted behavior and you only want to limit to display the provider set in providerType,
set this flag to true.

---------------

 ## hardClose
**Available from**: `version 1.3.0`

**type**: `boolean`

**Default**: `false`

Close potential provider windows when cashier tab/window is closed.

---------------
 
 ## prefillCreditcardHolder
**Available from**: `version 1.3.4`

**type**: `boolean`

**Default**: `false`

Populate account name and make it non-editable.
