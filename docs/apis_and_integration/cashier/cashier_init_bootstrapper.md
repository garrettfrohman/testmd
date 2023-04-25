---
id: "cashier_init_bootstrapper"
---

# Initialize Using Bootstrapper Script

Include the bootstrapper, using NPM or script-tag.

**NOTE**: You need to initialize the cashier via this bootstrapper-script to have access to the cashier's API.
Solely using the cashiers URL will not give you access to the API.

```html
npm i paymentiq-cashier-bootstrapper
```
or include as script (adds global variable _PaymentIQCashier)

```html
<script type=text/javascript src='https://static.paymentiq.io/cashier/cashier.js'></script>
```

Then initialize the cashier by passing in:

1. Reference to an element in your DOM (id or class)
2. Config object for the cashier
3. Optional callback-handler for when the Cashier has been initialized

```js
import _PaymentIQCashier from 'paymentiq-cashier-bootstrapper'

new _PaymentIQCashier('#cashier',
  {
    merchantId: '1337',
    userId: 'Han Solo',
    sessionId: '66',
    environment: 'test', // if not set, defaults to production
    method: 'deposit' // if not set, defaults to deposit
  },
  (api) => {
     console.log('Cashier intialized and ready to take down the empire')
     
     // register callbacks
     api.on({
      cashierInitLoad: () => console.log('The cashier successfully loaded and is ready'),
      success: data => console.log('Successful transaction completed', data)
     })
  }
)
```