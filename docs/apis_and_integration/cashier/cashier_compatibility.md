---
id: "cashier_compatibility"
---

# Compatible Versions Of The Bootstrapper And The Cashier

The PaymentIQ Cashier introduced a security update in version 1.2.0 which is only compatible with the Bootstrapper > 1.3.0.

If an earlier version of the bootstrapper is used together with the Cashier > 1.2.0, certain features of the Cashiers API won't work.

## Compatibility Matrix

| Cashier            | Bootstrap script | Compatible |
|------------------- |------------------|------------|
| 1.2.0 or later     | 1.3.0 or later   | Yes        |
| 1.2.0 or later     | 1.2.3 or earlier | No         |
| 1.1.9 or earlier   | 1.3.0 or later   | No         |
| 1.1.9 or earlier   | 1.2.3 or earlier | Yes        |

## What will happen if we run in-compatible version?

The callbacks and features of the Javascript API will stop working. The cashier will still load and payments can be made, but some features you have implemented that rely on callbacks from the cashier will stop working.
