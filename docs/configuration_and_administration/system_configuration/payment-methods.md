---
id: "payment-methods"
---

# Payment Method Rules

The payment methods rule category is the section that allows a merchant to configure how the cashier is displayed to an end user on the merchant site.

The main use of these rules is to determine which payments methods are displayed to the end user, and in which order.  Using these rules it is incredibly easy to add or remove payment methods from the player deposit and withdrawal cashiers.

Rules are created in the same manner as with other categories, with conditions being defined, and actions taking place as a result.  The rules can be as general, or as specific as required, and is even capable of showing a different cashier to each individual player.

## Constructing payment methods Rules

As the cashier is displayed to the end user before a transaction takes place the number of available conditions that can be defined is reduced to those that apply to the user themselves.

Note:  It is important to always select ‘Payment method’ within the conditions as this defines whether the displayed cashier will be for Deposits or Withdrawals.

**Example Default Deposit Cashier:**

![](/img/rulesettings/RulesPaymentMethods/1.png)

The order that the payment methods will appear in the cashier is the same as the order in which the ‘Methods’ action is defined, with the exception that if ‘Add last used first’ = yes then the most recently used method will be given top priority in the cashier.

Of course we can further refine the cashier to display different deposit methods according to the country of the user, and any of several other parameters.

**Example Default First Deposit Cashier:**

![](/img/rulesettings/RulesPaymentMethods/2.png)

For first time depositors Neteller and Skrill are not shown, due to the high prevalence of bonus abuse from these deposit method users.

**Example Finland Deposit Cashier Web only:**

![](/img/rulesettings/RulesPaymentMethods/3.png)

You will note that ‘Channel’ = ‘I’ has been added to indicate web only, the mobile ‘M’ cashier would be defined separately.

**Example Default Withdrawal Cashier:**

![](/img/rulesettings/RulesPaymentMethods/4.png)

You will note that some additional actions are included with the withdrawal cashier.

- Exclude if not used  = Yes – Does not display a withdrawal method if it has not already been used to deposit.
- Always enabled – Allows a method to always be displayed, regardless of whether it has been previously used.  Usually bank withdrawal.
- Include hidden accounts = Yes – Allows users to withdraw to depositing accounts even if they have ‘deleted’ them from the deposit cashier through the site.

**Example Test Withdrawal Cashier:**

![](/img/rulesettings/RulesPaymentMethods/5.png)

This is an example of a withdrawal cashier configured for ‘Test’ and that only applies to the test user ‘TEST123’.