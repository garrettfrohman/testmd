---
id: "block_user_from_master"
---

# Blocking User Accounts From A Master MID

This document outlines how you can set up and block specific user accounts from the Master MID.

## Configuration

The following lines need to be added in both the Master MerchantConfig, and to all Sub-MIDs that are intended to be included:

```xml
<txTypesWithActiveSha256Matching>ALL_TYPES</txTypesWithActiveSha256Matching>
<userPspAccountsBlockWithinScopeEnabled>true</userPspAccountsBlockWithinScopeEnabled>
```

## How to block in Master

Go to the tab ’User accounts’ in PaymentIQ BO. Select the user account you want to block, go to ’Action’ and click ’Block account within scope’.

![](/img/blockingfrommaster/01.png)

The ’Block account’ window will appear:

![](/img/blockingfrommaster/02.png)

**'Are you sure you want to change status to Blocked?’** gives you a selection of reasons for adding the block.

The Reasons can be modified in MerchantConfig by adding the parameters below. You can choose the texts of your preference, and those will appear when you scroll.

### Example:

```xml
<userPspAccountBlockReasons>
    <string>Chargeback</string>
    <string>Business Card</string>
    <string>Confirmed Fraud</string>
    <string>Suspected Fraud</string>
    <string>Customer Request</string>
    <string>Gambling Problem</string>
    <string>Self-exclusion</string>
    <string>Other</string>
  </userPspAccountBlockReasons>
```

**'Block scope MID?'** Shows all MIDs your Backoffice user account has access to. Either you can block a user account in a specific MID, or for all of them by choosing the Master MID.

## Tab UserAccounts in PaymentIQ

When you have blocked a payment method, you will find the information in the tab **User accounts** in to tables **Block reason** and **Block scope**

## Advance Search

You may search for a blocked account within a specific scope by using the advance search.

![](/img/blockingfrommaster/03.png)

