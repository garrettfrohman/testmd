---
id: "cashier_reset_bootstrapper"
---

# Reset Using Bootstrapper Script

In a single page application you might need to reset the cashier before re-rendering it in order to make sure that the user always gets the initial view of the cashier.

From version `1.2.2` of the paymentiq-cashier-bootstrapper there is a reset method available

You can call this reset method every time before you run your setup to make sure you always get a fresh cashier.

```
window._PaymentIQCashierReset()
```

This will remove the rendered iframe from the DOM tree.






