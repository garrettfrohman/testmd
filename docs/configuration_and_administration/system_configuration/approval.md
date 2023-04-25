---
id: "approval"
---

# Approval Rules

The Approval rule category is used to define parameters for the automated approval of player withdrawals.

Approval rules are configured in much the same way as other rule sets in PaymentIQ, with conditions defining when the appropriate actions are triggered.  There are almost 50 transaction and player condition parameters available for these rules, and this allows a great deal of flexibility, and very specific rules may be created to allow the vast majority of withdrawals by regular customers to be automated.

The actions allowed are ‘Time unit’ (either seconds, minutes, or hours), ‘Time’ the number of units until the action is taken, and ‘Approval method' (either manual or automatic).  This enables the merchant to set a specified delay until a withdrawal is processed.  

By specifying automated approval rules correctly, and adjusting these over time as the merchant finds appropriate, it is possible to have more than 75% of withdrawal requests being processed automatically.

## Constructing Approval rules

### Forcing a manual review

While it is possible to set rules defining when automated withdrawals are triggered, it is also possible to set rules that specify that certain categories of user always have their withdrawals manually reviewed. This is useful in ensuring that internal users do not have withdrawals automatically approved, or for forcing a manual review of any UK users who are not yet age verified. It can also be used to exclude certain users from the auto approval process, if desired.

**Example Force Withdrawal Manual Approval with merchant email address:**

![](/img/rulesettings/RulesApproval/1.png)

**Example Force Withdrawal Manual Approval with merchant IP address:**

![](/img/rulesettings/RulesApproval/2.png)

**Example Force Withdrawal Manual Approval for non-verified UK customers:**

![](/img/rulesettings/RulesApproval/3.png)

Another candidate for a forced manual review might be all first time withdrawals and this is defined by setting the additional condition ‘First time withdrawal’ to ‘yes’ within a rule.

Of course rules that force a manual review need to be positioned above any rules that will define automated withdrawals in order to ensure effectiveness.

### Automated approval rules

Automated approval usually require multiple rules acting in conjunction, as users are at different stages of the KYC process, or are new users, or have other conditions that define how comfortable the merchant is with issuing automated withdrawals.

**Example Automated withdrawal FI KYC verified customers:**

![](/img/rulesettings/RulesApproval/4.png)

You will note that other conditions that are usually correct with ‘regular customers’ and may be not correct with possible fraudulent activity, have been included to further refine the rule.

‘First time method used’ is set to ‘no’, indicating that this user has already had a successful withdrawal to this method.

‘First withdrawal’ is set to ‘no’, indicating that the user already had another successful withdrawal.

‘Last deposit method match’ is set to ‘yes’, indicating that the user is withdrawing to the same method that was last used to deposit.

‘Location match’ is set to  ‘IP, BIN, and Registration country’, meaning that all three of these should match (or two, as BIN is ignored if a card is not being used) for the withdrawal to progress.

‘Max amount’ is set to 3000 EUR, meaning the individual withdrawal amount is 3000 EUR or below.

‘Max balance’ is set to 3500 EUR, meaning that the balance of the player account is not more than 3500 EUR (in place to stop a customer making many smaller withdrawals that together form an amount larger than the 3500 EUR limit).

As you can see it is possible to be very specific with what withdrawal the merchant allows to proceed automatically, and as time progresses the merchant will adjust these rules making them more or less strict as the business deems correct.

**Example Automated withdrawal non-verified but previous withdrawal:**

![](/img/rulesettings/RulesApproval/5.png)

This rule is similar to the previous rule but allows withdrawal of up to 100 EUR on maximum balances of 120 EUR for not-verified FI customers with low risk indicators, who have already had a withdrawal manually approved.

Using many of the available conditions it should be possible for the merchant to construct a very good rules set that allows low risk users to be automatically approved for withdrawal, but sends higher risk users to manual review.

### Automatic On-Hold

Creating an approval rule using the action `Approval action` with value `HOLD` allows the matched transactions to be put in the "On-hold" state with status code WAITING_WITHDRAWAL_ON_HOLD_APPROVAL. An agent must then manually either deny the withdrawal or "Unhold" it followed by an Approve, depending on the actions you want to take.

## Preventing users from cancelling Withdrawals using FORBID_CANCELLING_BY_USER

If a merchant wishes to be able to prevent a player from cancelling their withdrawal once it has been submitted (locking or 'flushing' their withdrawal), this can be achieved by application of a specific rule within the Rules>Approval section.

When composing an auto-approval rule, if the Action>ApprovalActionTag value = [FORBID_CANCELING_BY_USER] then the user will receive an error if they try to cancel the withdrawal.
This means that Locking a withdrawal using these rules can only be actioned at the time the user submits the withdrawal request, and so when this rule acts.

Therefore, a condition must be passed from the front end in the API call that will cause this rule to trigger.
This could be specific UserIDs, or a User Category if all withdrawals in this class (or from this user) should be affected, as in the example below.

![](/img/rulesettings/RulesApproval/6.png)

If this decision should be made on a transaction-based level, then a custom 'attribute' class parameter should be passed (such as lockWithdrawal = TRUE/FALSE) along with the withdrawal data in the API call to PIQ, as in the example below.

![](/img/rulesettings/RulesApproval/7.png)

A locked withdrawal will appear in the Approval tab with the Info description ‘Forbid user from cancelling.

![](/img/rulesettings/RulesApproval/8.png)

This withdrawal can be approved or declined by a PaymentIQ user in the normal manner.
