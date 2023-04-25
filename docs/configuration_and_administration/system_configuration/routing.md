---
id: "routing"
---

# PSP Routing Rules

Routing is the way that PaymentIQ determines which PSP will process the transactions as they occur.

Dependent on your merchant setup this may be as simple or as complex as your business requires.

![](/img/rulesettings/RulesRouting/1.png)

**Example**

We will begin with a simple example of rule creation.

We will imagine creating a ‘Catch-all’ rule that will be our default for any Visa deposits that do not hit more specific rules.

It is a good idea to have very general ‘Catch-all’ rules to ensure that all transactions have a default processing route defined in the event previous rules do not apply.

1. Go to Rules > Routing > PSP Routing.
2. Click on New?

![](/img/rulesettings/RulesRouting/2.png)

This will generate a new blank rule in a new Rule category.

![](/img/rulesettings/RulesRouting/3.png)

3. Deselect the check box next to the rule number in the top left to inactivate the rule whilst composing.  This is good practice while creating rules, to stop any unexpected effect on live processing during rule creation.
4. Enter a name for the new Rule set ‘Catch-all Backup’.
5. Name the Rule ‘Visa Deposit Default Routing’
6. Insert a note that describes what the rule achieves.
7. Add a condition ‘Tx Type’
8. Click within the box and find and click ‘CreditcardDeposit’.
9. Add a condition ‘BIN’
	- The condition ‘BIN’ is a free text Regex field that will act on the credit card ‘BIN’ (sometimes called **I**ssuer **I**dentification **N**umber)
10. In the text box type ```4.*```
	- As we know that all Visa numbers start with a 4 we have created a query in Regex that translates as ‘Begins with 4 and is followed by any number of other characters’ – in Regex ```.*``` indicates any number of wild card characters.

Now that we have created the conditions we must define the actions to be taken when these conditions are true.

11. Click in the ‘PSP’ box, scroll down and select ‘Wirecard’
12. In the ‘PSP Account’ box we must type the code that corresponds to the account within the Wirecard configuration where the transaction will be sent for processing.
13. In this case this is ‘N3DS’ indicating the Non 3D secure MID.
14. Click the Save button to save the new rule.

Our final rule appears thus:

![](/img/rulesettings/RulesRouting/4.png)

Note that the rule is greyed out (not active) because the check box next to the Rule number in the top left of the rule is not selected.  If we now check this box and press the Save button the rule immediately becomes active and begins acting on any matching transactions.

**Example**

To aid in rule creation there is a function to enable copying of an existing rule that can then be modified to create a new rule.

In the second example we will add a similar ‘Catch-all’ rule for MasterCard.

1. On the existing rule just created click ‘Copy?’ in the top right corner. This creates a new rule directly below the copied rule, with the same conditions and actions, but no name.
2. Name this rule ‘MasterCard Deposit Default Routing’.
3. Change the free text comment from Visa to Mastercard.

Since we wish our rule to be the same but for MasterCard and we know that all MasterCard’s begin with a 5 we need only change the ‘BIN’ text box from a 4 to a 5.

4. Place your cursor after the 4, delete this, and replace with a 5
5. Click the Save button to save the new rule.

Now our two rules adding basic default routing for all CreditcardDeposit transactions are created.

You will note that when viewing the rules in a ‘collapsed’ view, a short summary of the conditions and actions is displayed to enable easy understanding of the rules functions before further examining by expanding the rules completely.

![](/img/rulesettings/RulesRouting/5.png)

## Creating more specific Routing rules

The rules created above are very simple, but enable a user to understand how rule creation occurs.  As most transaction parameters are available to the PaymentIQ rule engine, much more specific rules can be created dependent on the merchant requirements.

We must always remember that PaymentIQ will act on the first rule (top to bottom) that matches a transaction, so specific rules that define small groups of transactions should be placed before general rules acting on wider groups of transactions.

Rules can be repositioned within a Rule category by simply click-dragging that rule to a new location among the rule definitions.

For instance; if we now wished to route CreditcardDeposit transactions from Norwegian issued cards to an alternative PSP ‘Ticketsurf’, we would create a new rule.

![](/img/rulesettings/RulesRouting/6.png)

However, we would have to position this rule ‘above’ the other existing rules in order for it to act, otherwise the more general Visa rule ‘Visa Deposit Default Routing’ would act on the transaction instead.

![](/img/rulesettings/RulesRouting/7.png)

When composing Rules we can also test them to see which rules would act on certain transactions.

## Testing a Transaction against a Rule

To test a transaction against your created rules, first note (or copy) an existing transaction ID or TxRefId. If the transaction is on the currently selected merchant it works with both the TxRefId and the TxId. If the transaction is on a sub-merchant you need to provide the TxRefId.

1. Click on the ‘Gear’ icon to the right of the ‘Filter’ box.

![](/img/rulesettings/RulesRouting/8.png)

2. Select the option ‘Match transaction against rules’
3. Enter the TxRefId or TxId of the transaction you noted before.
4. Click the ‘Match’ button.
5. If your transaction would activate one of the rules on current merchant then this will be highlighted in green. See below.

![](/img/rulesettings/RulesRouting/9.png)

6. If your transaction would activate a rule on a different merchant the ID of that rule will be displayed, where the first part is the merchant ID that the rule is configured on (1000 in the example below).

![](/img/rulesettings/RulesRouting/11.png)

Note: Rules must be ‘enabled’ for a transaction to be matched against them.

## Rule Preconditions

You will have noted that just above the first rule in a set is a button to add a precondition that will apply to the whole rule set.

This can be useful if you wish (for instance) to create a set of rules that apply only to Norway, or to CreditcardDeposit, or any other parameter, and can then simplify the individual rules themselves.  

It may also enable better organization of rules, to keep certain rule sets distinct, and ensure their applicability only in the required cases.

![](/img/rulesettings/RulesRouting/10.png)

## Rule Weighting

One other aspect of Rule actions that needs clarification is ‘Weight’, and this can be added to a rule under Actions.

The main use of ‘weighting’ is to balance traffic between two similar PSP’s.

As a rule is evaluated against the defined conditions, and matched, the rule engine looks for a ‘Weight’ action parameter.  If no parameter is found the ‘Action’ progresses as defined.

However, if a ‘Weight’ is found then the rule engine looks for other rules that match the same defined conditions, looks at the weight of those, adds all the ‘Weight’ values together, and then makes a random result choice according to the relevant weights given.

See the following example.

**Example**

Three Rules exist with the same conditions (in a single rule set).

* Rule 1 has Weight 70 and an Action of - Wirecard N3DS
* Rule 2 has Weight 20 and an Action of - Wirecard 3DS
* Rule 3 has a Weight of 10 and an Action of - Payvision N3DS

A single transaction would be evaluated against the conditions for a match, and once matched, would be routed to one of the three possibilities randomly, with a probability of 70% for Wirecard N3DS, 20% for Wirecard 3DS, and 10% for Payvision N3DS.

Over time you would see that the traffic has been split on a 70/20/10 basis in favor of the three results.

This is very useful if there are similar PSP’s that perform the same processing, but to whom we wish to distribute traffic in a certain ratio. perhaps based on pricing or other factors.
