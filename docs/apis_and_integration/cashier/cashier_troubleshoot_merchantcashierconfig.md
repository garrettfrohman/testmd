---
id: "cashier_troubleshoot_merchantcashierconfig"
---

# Troubleshooting MerchantCashierConfig Issues

Make sure you are passing in a valid JSON inside your `MerchantCashierConfig` by validating it at [jsonlint.com](https://jsonlint.com). Note that you should only validate the JSON-part of your configuration, meaning everything within **and** including the curly brackets `{}`.

For example, this is valid

```json
{
  "singlePageFlow": "true",
  "theme": {
    "buttons": {
      "color": "#8cd600"
    }
  }
}
```

While this is invalid, due to a missing curly bracket

```json
{
  "singlePageFlow": "true",
  "theme": {
    "buttons": {
      "color": "#8cd600"
    
  }
}
```