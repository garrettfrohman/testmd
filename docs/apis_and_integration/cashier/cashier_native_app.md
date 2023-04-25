---
id: "cashier_native_app"
---

# Use In Native APP

The Cashier can be run in a native app - through a webview.

In order to display the cashier you need to run your webview with HTML5 features enabled. Android webview for example defaults to not have window.localStorage enabled.

https://stackoverflow.com/questions/10599739/does-android-webview-browsers-support-html5-features

:::info Requirements for the webview:

* javascriptEnabled
* domStorageEnabled
* canOpenWindowsAutomatically
* supportMultipleWindows
* allowingReadAccess

:::




