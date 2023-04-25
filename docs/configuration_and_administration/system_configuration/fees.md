---
id: "fees"
---

# Fee Rules

The Fees rule category is able to define two different classes of fee.

**Fee** is that which will be charged to the end user customer by the merchant, and is added to (or deducted from) the transaction amount.

**Provider Fee** is defined by the merchant according to their PSP contracts, and can be used to calculate the individual fees per transaction that are payable by the merchant to the PSP.  It is for reporting purposes only and does not have an effect on the transaction processed.

## Fee Rule Category

The Fee Rule Category is used to manage the end user fees that may be charged by the merchant to the customer if required.  The fee rules are very flexible and can either add or deduct a fixed fee, or a percentage fee, to deposits or withdrawals.

Rules are constructed in a similar manner within this category, with conditions being defined, and actions occurring when a transaction conforms to these rules.  The range of conditions that can be added enables a great deal of specific rules to be defined if desired.

## Notes

Fee rule **cannot** have more than two decimals and if configured as such the rule will not work.

### Deposit fees

In an example that adds a 2.5% fee to all card transactions up to 300 EUR, but then is free above 300 EUR we would do the following:

Create a first rule as below: This charges a 2.5% fee up to a 299 EUR transaction value.

![](/img/rulesettings/RulesFees/1.png)

Note that for the ‘Fixed fee max’, we must specify the currency along with the amount.  For multiple currencies, you could use a comma as a separator:

E.g. 300 EUR, 3000 SEK, 3000 NOK, 1000 PLN, 8000 CZK

Now a second rule is created:  This specifies a zero fee for 300 EUR and above.

![](/img/rulesettings/RulesFees/2.png)

Using combinations of rules in such a way it is possible to construct very specific fee structures, down to the player level.  If you need help constructing rules, email technicalsupport@bambora.com with your query.

### Withdrawal fees

For an example that deducts a €1 fee from all withdrawals we would construct:

![](/img/rulesettings/RulesFees/3.png)

Again, using combinations of rules it is possible to construct quite complex withdrawal fees.  

To exclude a PSP (or player, or country, or any other parameter) from withdrawal fees you would create a rule that assigns a zero fee to that PSP(or player, or country, or any other parameter), and place it above other rules that define fees.

#### Free withdrawals

It is possible to define a number of free withdrawals with the help of the condition ’Free withdrawals’ and define the required parameters.
The ’Free withdrawals’ condition passes if the player has not made more than N withdrawals in the last X days.
With the below example setup, the player can make 3 withdrawals in 2 days without fees. After that, the player will be charged the fee defined in the next matching rule.

![](/img/rulesettings/RulesFees/free_withdrawal_condition.png)

Also, with the help of the action ‘Next free withdrawal’ you can create a separate rule to display next free withdrawal date in the cashier.
This will automatically work if using the PaymentIQ standardized cashier.
If using your own in-house cashier you should look for the nextFreeDate field within the feeInfo object of the payment method response in the Front API.

![](/img/rulesettings/RulesFees/free_withdrawal_action.png)

Of course any conditions can be used to define the category of player that the rule applies to, even down to specifying the players individually.  

You should note that this rule should be placed above the general rule that specifies actions on larger groups of players.

## Provider Fees Category

In order to give great reporting clarity into the amount that individual transactions are costing the merchant to process it is possible to define a ‘Provider fee’ that will be attached to the transaction data.

This fee, if defined correctly, should allow the merchant to check the amounts being invoiced by PSP’s against the expected amounts to be paid on a transactional level.

It also allows deeper analysis of transactional costs to be performed.  For instance, allocating specific PSP costs to a country or region in the financial accounts, or determining which players, due to their deposit and withdrawal behaviors, have lower profit margins than expected.

Provider fee rules are constructed in much the same way as end user fees.

The below example reflects a PSP whose fee is 1.5%, with a minimum of 0.50 EUR and a maximum of 2.50 EUR.

![](/img/rulesettings/RulesFees/5.png)

Obviously, the PSP in the above rule still needs to be defined.

The second example reflects a PSP who has a fee of 1.5%, and also a fixed fee per transaction of 0.50 EUR.

![](/img/rulesettings/RulesFees/6.png)

Provider fee recording does have certain limitations, as PSP fee schedules can be very varied, and defined outside the scope of a pure transactional basis.

For example, PSP 1 might offer a tiered fee structure, with fees determined against monthly volumes.  In this case, we should use our best estimate of which tier we would be in for the coming month, and define the provider fee accordingly.

Another example PSP 2 might offer a monthly rebate dependent on volumes during the month.  In this case, we have two options; Define the provider fees according to the expected fee after the rebate would be applied, or define the provider fee according to the full fee schedule, knowing that this will provide the invoiced cost before rebate is applied.

Another difficulty arises when there are more than one provider fee applies to a transaction, as only one provider fee rule can act on each transaction. For instance: a payment gateway adds a flat fee to all transactions, or a card transaction attracts a fee from both PSP and acquirer.  In these cases, you may find it useful to combine the two fee schedules when defining the provider fee (PSP + acquirer), or in the case of a gateway fee that is applied to all transactions, omit it altogether, recognizing that this cost does apply, but would distort the payment provider cost in the reporting, and so adding it manually after the fact to any reporting made.

Despite these limitations, adding a provider fee to transactions, while not strictly necessary in order to enable processing, adds a good level of visibility to processing costs that is impossible to obtain otherwise.
