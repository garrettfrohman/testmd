---
id: "fallback"
---

# PSP Fallback Rules

Fallback Rules can be applied to card transactions that fail with the first PSP. Although any transactions can be resubmitted in this way this is used primarily as a tool to ensure continuity of processing, and ensure that transactions that begin failing through one processor can be automatically retried through a backup processor.  This process is seamless for the customer.

The rules that govern this are formed in the same way as rules for transactions (and indeed all rules).  Conditions are added, with Actions as a result.

Consider the example below that retries failed EMP transactions through Ticketsurf:

![](/img/rulesettings/RulesFallback/1.png)

It is also possible to add further conditions to refine the rule.  For Fallback rules you may also specify PSP status code or Tx status code. Using these conditions it is also possible to exclude transactions from any other fallback rules.

For example the following rules:

![](/img/rulesettings/RulesFallback/2.png)

The Rule FA_02 stops any failed transactions with PSP Status Code 51 (which is Insufficient Funds) from being retried due to the rule FA_01. Of course this rule must be placed above the active fallback rule, as transactions pass through the rule sets from top to bottom.

It should be noted that due to the nature of the authorization process, not all 3D secure transactions can be retried with another provider.

**IMPORTANT:** When configuring fallbacks for PSP accounts used for credit card transactions, all possible fallback accounts need to have the same "authType" as the initial PSP account or else the fallback rule won't match.
