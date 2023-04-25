---
id: "kyc"
---

# KYC Rules

Setting rules that relate to the KYC provider used for automated checks are found in the KYC tab.

Rules are created in the same manner as with other categories, with conditions being defined, and actions that define which KYC provider to use as a result.  Conditions available in this rule set are limited to the player rather than any transactions, as it is usually intended that the automated KYC check will take place before any transaction has occurred.

## Constructing KYC Routing rules

Within the KYC tab you will find the ‘Routing’ category and this is where we determine which integrated KYC provider to use.

**Example UK KYC check on unverified users:**

![](/img/rulesettings/RulesKYC/1.png)

As you will note it is not necessary to construct elaborate rules for KYC routing, and these are generally quite straightforward.  The above rule acts on New UK customers who are unverified and have initiated a deposit

## Constructing KYC Fallback rules

In the same manner as transaction routing can be configured to allow a fallback solution to act if the primary routing solution fails, this can also be used within the KYC checks to provide a secondary KYC check with a second KYC provider.

**Example Fallback to secondary provider of KYC check fails:**

![](/img/rulesettings/RulesKYC/2.png)

Fallback rules are quite simple in nature and take the premise that if Provider 1 fails then try Provider 2.
