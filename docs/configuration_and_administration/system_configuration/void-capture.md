---
id: "void-capture"
---

# Void / Capture Rules

The void / capture rule category is used to define parameters for the automated void or capture of deposits.

Void and capture rules are configured in much the same way as other rule sets in PaymentIQ, with conditions defining when the appropriate actions are triggered.  There are almost 50 transaction and player condition parameters available for these rules, and this allows a great deal of flexibility.

The actions allowed are ‘Time unit’ (either seconds, minutes, or hours), ‘Time’ the number of units until the action is taken, and ‘Capture method' (either manual or automatic), and ‘Action' (either void or capture).  This enables the merchant to set a specified delay until a void or capture is processed.

## Constructing Void / Capture rules
### Forcing a manual capture / void

While it is possible to set rules defining when automated capture are triggered, it is also possible to set rules that specify that certain categories of user always have their transactions captured manually. This is useful in ensuring that internal users do not have captured automatically, or for forcing a manual review of any UK users who are not yet age verified.  It can also be used to exclude certain users from the auto capture process, if desired.

**Example Force Deposit Manual Capture with merchant email address:**

![](/img/rulesettings/RulesVoidCapture/1.png)

### Forcing an automatic capture / void

**Example Automated capture KYC verified customers:**

![](/img/rulesettings/RulesVoidCapture/2.png)
