---
id: "cashier_html_example"
---

# HTML Example

```html
<!DOCTYPE html>
  <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Cashier</title>
        <script type=text/javascript src='https://static.paymentiq.io/cashier/cashier.js'></script>
        <style> html, body { margin: 0px; overflow: hidden; } #cashier { height: 100vh; }</style>
    </head>
    <body>
    <div id='cashier'></div>
    <script>
    var CashierInstance = new _PaymentIQCashier('#cashier', {
      merchantId: 1000,
      userId: 123,
      sessionId: 123,
      environment: 'test'
    }, (api) => {    
        api.on({
          cashierInitLoad: () => console.log('Cashier init load'),
          update: data => console.log('The passed in data was set', data),
          success: data => console.log('Transaction was completed successfully', data),
          failure: data => console.log('Transaction failed', data),
          isLoading: data => console.log('Data is loading', data),
          doneLoading: data => console.log('Data has been successfully downloaded', data),
          newProviderWindow: data => console.log('A new window / iframe has opened', data),
          paymentMethodSelect: data => console.log('Payment method was selected', data),
          paymentMethodPageEntered: data => console.log('New payment method page was opened', data),
          navigate: data => console.log('Path navigation triggered', data)
        })
        api.set({
          config: {
            amount: 10
          }          
        })
        api.css(`
          .your-custom-css {
            color: blue;
          }
        `)
      }
    )
  </script>
  </body>
</html>
```