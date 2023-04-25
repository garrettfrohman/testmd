---
id: "forex"
---

# Forex Rules

PaymentIQ offers merchants full control over the currency that is used for sending transactions to the processing partner, or PSP.

This rule category allows the merchant to define a currency swap with the additional opportunity to add (or even deduct) an exchange margin.

This has two main uses:

## Currency conversion for deposit processing

In allowing conversion from any player currency into any currency for processing deposits, PaymentIQ allows the merchant to process transactions from a currency that is not normally supported by the payments partner.  For instance, we may pass NOK transactions through a PSP that will only process in EUR, by making a rule to convert the original NOK into EUR.

**Example Swap NOK to EUR for Ticketsurf processing:**

![](/img/rulesettings/RulesForex/1.png)

In this example a 1% Forex margin has been added to the transaction, but this can be adjusted or removed according to the business requirements.

Defining the Forex rates used by PaymentIQ is set using the Admin > Forex section, and is covered in a later part of the manual.

## Currency conversion for withdrawal processing

With PaymentIQ a merchant may identify a user's bank country and trigger a currency exchange to send the correct currency to the player's bank account.  An exchange margin may be added to the transaction if required.

**Example Swap bank withdrawal to SEK for Swedish banks:**

![](/img/rulesettings/RulesForex/2.png)

The above example allows a SEK amount to be sent for bank processing from a EUR denominated player account, and deducts an exchange margin of 1.5%, that the merchant will then see as a foreign exchange profit.
