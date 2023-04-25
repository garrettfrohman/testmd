---
id: "fraud-blocks"
---

# Fraud Block Rules

This rule category allows a merchant to create rules that will cause PaymentIQ to ‘Block’ (not send for processing to the PSP) any transactions that trigger against the rules that are defined.

The Blocks are split into 6 categories under the ‘Blocks’ tab, allowing merchants to stop transaction processing based on the conditions set, but there is also another ‘Block’ rule under the KYC tab.

There are essentially three different types of block available to be defined.

## Individual transaction based Blocks

These are blocks that will act on an individual transaction and prevent that transaction from being passed for processing based on the data from that transaction.

There are four types of blocks that act in this way, and are all essentially the same, but are defined in separate rule categories for better merchant management.

### IP Block, BIN Block, KYC Block, General Block

Rules are defined using any of the conditions available, and have an action of ‘Accept’ or ‘Decline’.

These are mostly used to block transactions from fraudulent IP addresses, IP addresses assigned to undesirable countries, BINs (credit card identifiers) issued in undesirable countries, or certain categories of KYC results (mostly underage).

Below are examples of each category of block.

**Example Block US IP addresses:**

![](/img/rulesettings/RulesBlocks/1.png)

**Example Block IP addresses with chargeback/fraud:**

![](/img/rulesettings/RulesBlocks/2.png)

The IP Block may also be used to ‘whitelist’ certain IP addresses or ranges by setting the Action to ‘Allow’, if desired (of course any whitelist rule must be at the top of the rule set to be certain of triggering).

Note: The condition `IP address` is a regex input, so to match against e.g dots in an IP you have to escape these, since they are a meta character in regex used to match any character. Escaping example to match IP "192.168.0.17": `192\.168\.0\.17`.

**Example Block US Credit Cards using BIN issuer country:**

![](/img/rulesettings/RulesBlocks/3.png)

**Example Block UK underage players:**

![](/img/rulesettings/RulesBlocks/4.png)

If none of the above block categories are relevant to your use case, you can use the general block rules with use of any conditions and configure your own custom block message with the `Info` action.

**Example of general block usage and block certain users:**
![](/img/rulesettings/RulesBlocks/9.png)

You can also add the actions `Failed status code` and `PSP status code` in order to make your block decline entirely customized with your desired status messages.
![](/img/rulesettings/RulesBlocks/10.png)

## Velocity based blocks

This is a category of block based on the user's previous transaction history, and may be used to limit the number of transactions, or the value of transactions that a user can make in a defined time period.  It can also be used to prevent additional deposits when a user balance is above a certain threshold.

This is mostly used as part of your fraud prevention setup, to pre-emptively decline transactions that fit a fraudulent pattern.

:::tip

By default, all transaction states are counted in the transaction history, and therefore used in the velocity calculation. If you need to narrow down which states of the transactions in the user's history and calculation, say only successful transactions, you need to add the Action `Tx state` (Observe that it's not as a Condition).

:::

**Example Limit Non 3D secure deposits for unverified customers to 1000 EUR per 24 hrs:**

![](/img/rulesettings/RulesBlocks/5.png)

**Example Stop user card deposit when balance is over EUR 200:**

![](/img/rulesettings/RulesBlocks/6.png)

#### Choosing the status code

When a transaction is declined due to a velocity rule, the default transaction status in PIQ will be `ERR_DECLINED_FRAUD`. However, it is possible to choose which status the transactions should end up in. This is done by adding the action `Failed status code` to the rule and selecting the wanted status code from the dropdown menu.


## User psp account blocks

This category of block rule is used to determine the merchant level rules that will apply to the user's ability register multiple payment accounts for one PSP, or control whether a user may share payment accounts with other users.

It is mostly used to stop sharing of user specific payment methods (Paypal, Skrill, Neteller etc.) between players, and prevent multiple accounts from depositing with previously used payment accounts (from other users).  It can also be used to limit the number of payment accounts per PSP.  For instance Paypal requirements are that a users may only use one Paypal account on a site.

**Example Stop sharing of credit cards between different users:**

![](/img/rulesettings/RulesBlocks/7.png)

**Example Set the max number of Paypal accounts to one and prevent sharing.**

![](/img/rulesettings/RulesBlocks/8.png)
