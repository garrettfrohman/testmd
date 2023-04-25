---
id: "cashier_cookies_and_webstorage"
---

# Cashier Cookies And Webstorage

Version 1.2.0 and later does not require third-party cookies enabled. Certain features may be limited though. A warning notice will be displayed to the user, informing him or her about this. The warning notice can be toggle off using [showCookiesWarning](cashier_parameter_details#showcookieswarning).

**For earlier versions**

To be able to use our cashier one needs to have third-party cookies enabled from the browser.

If for some reason cookies are not activated in the browser, the user will end up on a 'Cookies not enabled' page telling the user to enable them
if they want to use the cashier.

Cookies are needed for the cashier in order to process the transaction correctly. Transaction data and id's are stored in webstorage during the transaction process until it's completed. The cashier will not work correctly without this enabled.

By cookies we refer to general web storage such as localstorage and sessionstorage.