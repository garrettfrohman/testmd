---
id: "cashier_javascript_api"
---

# Javascript API

* [Callbacks](#callbacks---on-event)
* [Inject/update data](#injectupdate-data)

# Callbacks - [on() event]
The cashier contain a build in API that provides callbacks for some key events:

* [cashierInitLoad](#cashierinitload)
* [update](#update-data)
* [success](#success-data)
* [failure](#failure-data)
* [pending](#pending-data)
* [unresolved](#unresolved-data)
* [isLoading](#isloading)
* [doneLoading](#doneloading)
* [newProviderWindow](#newproviderwindow-type)
* [paymentMethodSelect](#paymentmethodselectmethodobject)
* [paymentMethodPageEntered](#paymentmethodpageenteredmethodobject)
* [navigate](#navigate-route)
* [isHidden](#ishidden)
* [isVisible](#isvisible)
* [cancelledPendingWD](#cancelledpendingwd)
* [validationFailed](#validationfailed)
* [cancelled](#cancelled)
* [onLoadError](#onloaderror)
* [transactionInit](#transactioninit)

Each of these can be hooked up by using the ```_PaymentIQCashier``` located on the global window object.

**Add callback hooks**

NOTE: If your JS code is not being compiled with babel for example- and are directly injected to a static HTML file,
your IE11 users and below will face issues if you use arrow functions or literal strings, if that's the case, use only standard javascript functions and standard string syntax to make sure it works in all browsers.

NOTE: `API` in the following example is a reference to the hooked callback parameter.

```
API.on({
  cashierInitLoad: () => console.log('Cashier init load'),
  update: data => console.log('The passed in data was set', data),
  success: data => console.log('Transaction was completed successfully', data),
  failure: data => console.log('Transaction failed', data),
  pending: data => console.log('Transaction is pending', data),
  unresolved: data => console.log('Transaction is unresolved', data),
  isLoading: data => console.log('Data is loading', data),
  doneLoading: data => console.log('Data has been successfully downloaded', data),
  newProviderWindow: data => console.log('A new window / iframe has opened', data),
  paymentMethodSelect: data => console.log('Payment method was selected', data),
  paymentMethodPageEntered: data => console.log('New payment method page was opened', data),
  navigate: data => console.log('Path navigation triggered', data),
  cancelledPendingWD: data => console.log('A pending withdrawal has been cancelled', data),
  validationFailed: data => console.log('Transaction attempt failed at validation', data),
  cancelled: data => console.log('Transaction has been cancelled by user', data),
  onLoadError: data => console.log('Cashier could not load properly', data),
  transactionInit: data => console.log('A new transaction has been initiated', data)
});
```
## cashierInitLoad
**Available from Cashier version 1.0.16 and [Bootstrap-script 1.0.17](cashier_init_bootstrapper)**

A callback that gets triggered when the cashier was loaded.

## update (`data`)
Callback will be called when an update is done using the ```api.set``` method.

Response object: `data`

For example, when setting amount, the callback.update would be:

```
{
    "type": "UPDATE",
    "data": {
        "config": {
            "amount": 200
        }
    }
}
```
## success (`data`)
Callback will be called when a transaction is done successfully.
One parameter containing data about the transactions.

Response object: `data`

Example:

```
{
  "status": "SUCCESSFUL",
  "payload": {
    "txRefId": "1499992",
    "amount": "12.00 SEK",
    "txAmount": "12.00",
    "txAmountCy": "SEK",
    "fee": "0.00 SEK",
    "pspReferenceId": "2150317174",
    "psp": "Payvision",
    "pspAccount": "3DS",
    "success": true,
    "pspStatusCode": "0_00",
    "merchantTxId": "2d2ab036-9c60-4b9a-86a0-a40383e995bd",
    "method": "deposit"
  }
}
```

## failure (`data`)
Callback will be called when a transaction failed (only when the cashier ends up on the failed page.
A transction can fail to validate (e.g invalid creditcardnumber) without the failure-callback beeing called since the payment flow stil still be resumed by the user. The callback will only be triggered when the flow is disprupted and the user can not continue with the payment.

Response object: `data`

Example:

```
{
  "status": "FAILED",
  "statusCode": "ERR_DECLINED_OTHER_REASON",
  "txRefId": "1499985",
  "method": "deposit",
  "psp": "Payvision",
  "pspAccount": "3DS",
  "success": false,
  "pspStatusCode": "3000_05",
  "merchantTxId": "1499985"
}
```

## pending (`data`)
Callback will be called when a transaction is pending, you will end up on the status page.

A transaction can be pending when there is a delay of processing the transaction or there are some more
user feedback required for completing the transaction.

Response object: `data`

Example:

```
{
  "tx_status": "Pending",
  "status": ...
  "statusCode": ...
  "txRefId": ...
  "method": ...
  "psp": ...
  "pspAccount": ...
  "success": false,
  "pspStatusCode": ...
  "merchantTxId": ...
}
```

## unresolved (`data`)
Callback will be called when a transaction is unresolved, you will end up on the status page.

Response object: `data`

Example:

```
{
  "tx_status": "Unresolved",
  "status": ...
  "statusCode": ...
  "txRefId": ...
  "method": ...
  "psp": ...
  "pspAccount": ...
  "success": false,
  "pspStatusCode": ...
  "merchantTxId": ...
}
```

## isLoading
Will trigger when something is loading, for example paymentmethods, a new page/tab etc..

## doneLoading
Will trigger when some content has done loading and has been parsed to the DOM.

## newProviderWindow (`type`)
Will trigger when a new iframe or window is being opened from the cashier.

type: `window` | `iframe`

## paymentMethodSelect(`methodObject`)
When a user clicks a payment method, i.e selects it in the list/grid.
Takes one parameter which is the payment method object:

Response object: `data`

Example:

```
{ 
  "txType":"SkrillDeposit",
  "accountSettings":null,
  "accounts":[],
  "limit":{ 
    "max":"5000.00",
    "min":"10.00"
  },
  "fees":[],
  "pspToUserCurrencyBuyRate":0.0,
  "providerType":"SKRILL",
  "service":null,
  "pspCurrency":"",
  "canAddAccount":true,
  "maintenanceInfo":{ 
    "maintenance":false
   },
   "txTypeInput":{ 
      "txType":"SkrillDeposit",
      "header":null,
      "container":null,
      "inputs":[]
      "storeAccounts":true,
      "thirdPartyContainerWidth":0,
      "thridPartyContainerHeight":0,
      "showTransactionDetails":false,
      "showInProgressExtraMsg":false,
      "inputHtml":null,
      "authorizePaymentScript":null,
      "amountRequired":true,
      "hideSetAmount":false,
      "hideSubmit":false
   },
   "toUserCurrencyBuyRate":0.0
}
```

## paymentMethodPageEntered(`methodObject`)
When the app navigates to the detail page of a payment method.
Takes one parameter which is the payment method object.

Response object: `data`

Example:

```
{ 
  "txType":"SkrillDeposit",
  "accountSettings":null,
  "accounts":[],
  "limit":{ 
    "max":"5000.00",
    "min":"10.00"
  },
  "fees":[],
  "pspToUserCurrencyBuyRate":0.0,
  "providerType":"SKRILL",
  "service":null,
  "pspCurrency":"",
  "canAddAccount":true,
  "maintenanceInfo":{ 
    "maintenance":false
   },
   "txTypeInput":{ 
      "txType":"SkrillDeposit",
      "header":null,
      "container":null,
      "inputs":[]
      "storeAccounts":true,
      "thirdPartyContainerWidth":0,
      "thridPartyContainerHeight":0,
      "showTransactionDetails":false,
      "showInProgressExtraMsg":false,
      "inputHtml":null,
      "authorizePaymentScript":null,
      "amountRequired":true,
      "hideSetAmount":false,
      "hideSubmit":false
   },
   "toUserCurrencyBuyRate":0.0
}
```

## navigate (`route`)
When the app navigates - this callback is triggered.

Response string: `path`

Example: `/payment-method`


## isHidden
Callback when the app toggles to be hidden. Happens when the cashier is configured to [autoProcess](cashier_parameter_details#autoprocess)

## isVisible
Callback when the app toggles to be visible, when the provider has loaded when using [autoProcess](cashier_parameter_details#autoprocess) or when an [autoProcess](cashier_parameter_details#autoprocess) was unable to be made.

## cancelledPendingWD
Callback will be triggered when a pending withdrawal has been cancelled. Cancel withdrawal option will appear when you have
`allowCancelPendingWithdrawal` flag set to true.

Example:

```
{ 
  accountId: ...,
  amount: ...,
  continueLink: ...,
  created: ...,
  fee: ...,
  state: ...,
  status: ...,
  transactionId: ...,
  txAmount: ...,
  txId: ...,
  txType: ...,
  tx_status: ...
}
```

## validationFailed
Callback will be triggered when a transaction has failed at validation step, before it has been processed.

Callback will also be triggered in some cases when validation succeeds but process fails and you have not been redirected to a new page, such as status page, which means the flow has not been interrupted and the user can still continue with the payment.

Available from:
Cashier version: `1.1.10`
Bootstrap script version: `1.2.4`

Response object: `data`

Payload example:

```
{ 
  accountId: ...,
  amount: ...,
  method: ...,
  psp: ...,
  pspRefId: ...,
  status: ...,
  txRefId: ...,
  txState: ...
}
```

## cancelled
Callback will be triggered when a transaction flow has been cancelled by the user.

Available from:
Cashier version: `1.1.14`
Bootstrap script version: `1.3.2`

Response object: `data`

Payload example:
```
{
  accountId: ...
  amount: "500,00 kr"
  merchantTxId: "123456"
  method: "deposit"
  psp: "Provider"
  pspAccount: "default"
  status: "CANCELLED"
  statusCode: "ERR_CANCELLED_BY_USER"
  success: false
  txRefId: "999999"
  tx_status: "Cancelled by user"
}
```

## onLoadError

Callback will be triggered when cashier failed to load due to wrong credentials or other init error.

Available from:
Cashier version: `1.1.14`
Bootstrap script version: `1.3.2`

Response object: `data`

Payload example:
```
{
  merchantId: "19800311",
  status: "Failed to get payment methods",
  userId: "PayTestSE"
}
```

## transactionInit

Callback will be triggered once a transaction has been initiated.
Available from:
Cashier version: `1.2.5`
Bootstrap script version: `1.3.7`

Response object: `data`

Payload example:
```
{
    "psp": "creditcard",
    "method": "deposit",
    "locale": "en",
    "amount": "200",
    "txAmountCy": "SEK",
    "accountId": null,
    "txRefId": 1111111
}
```

# Inject/update data

During runtime, you can pass in data to the cashier. It can be to update any given configuration or set data for the current user (e.g email, phonenumber needed for the payment method).

You can also pass in your custom css as a string.

## set

You can also pass in new data to the cashier, for example update the amount or pass in new information about the user.
This is done using the api-object returned in the callback.

```js
new _PaymentIQCashier('#cashier', { ...config }, (api) => {
  api.set({
    config: {
      amount: 120, // new amount
      listType: 'list',
      mode: 'ecommerce',
      // can add most cashier configs to this object
    },
    user: {
      name: 'Admiral Ackbar',
      email: 'it.is.a.trap@example.com'
    },
    attributes: {
      bonusCode: 'some-bonus-code',
      foo: 'bar'
    }
  })
}
```

The cashier will react to the change event and update the information displayed.

## css

You can also pass in your custom css via the API. Do this by sending a string of ```css```.

```js
api.css(`
   #someDiv {
      margin: 10px;
   }
`)
```
