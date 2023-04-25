---
id: "troubleshootruleengine"
---

# Resolve First Velocity Rule Not Matching

## Velocity Rules

### Problem Description

When you have multiple velocity rules and the transaction is matching multiple rules, instead of first matched velocity rule you are seeing result of other matching rule regardless of the order. 

### Solution 

#### Activate "activeFirstVelocityRuleMatching" flag in MerchantConfig

Add `<activeFirstVelocityRuleMatching>true</activeFirstVelocityRuleMatching>>` in the MerchantConfig. This will force rule engine to return the result of first matched order. 

```xml
  <com.devcode.paymentiq.integration.merchant.MerchantConfig>
    ...
    <activeFirstVelocityRuleMatching>true</activeFirstVelocityRuleMatching>
    ...
  </com.devcode.paymentiq.integration.merchant.MerchantConfig>
```
