---
id: "cashier_specify_version"
---

# Specify Cashier Version

There is an option to specify a specific version for a slow rollout and/or to test new features by applying the following setting in the MerchantConfig-file:

```xml
<cashierConfig>
  <version>{branch_or_version}</version> // branch name or deployed version
</cashierConfig>
```

A branch can also be specified in the URL:

`[https://pay.paymentiq.io/cashier/{branch_or_version}`