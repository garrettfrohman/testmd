---
id: "cashier_init_bootstrapper_typescript"
---

# Typescript - Initialize Using Bootstrapper Script

The bootstrapper is build in Typescript and has exported interfaces you can use during setup.
The interfaces are available from version 1.3.8 of the Bootstrapper in the [NPM package](https://www.npmjs.com/package/paymentiq-cashier-bootstrapper).

## Example

```js
import _PaymentIQCashier, { IPiqCashierConfig, IPiqCashierApiMethods } from 'paymentiq-cashier-bootstrapper'

const config: IPiqCashierConfig = {
  merchantId: '1337',
  userId: 'Han Solo',
  sessionId: '66',
  environment: 'test',
  method: 'deposit'
}

new _PaymentIQCashier('#cashier',
  config,
  (api: IPiqCashierApiMethods) => {
    console.log('Cashier initialized and ready to take down the empire')
    
     // register callbacks
     api.on({
      cashierInitLoad: () => console.log('The cashier successfully loaded and is ready'),
      success: data => console.log('Successful transaction completed', data)
     })
  }
)
```