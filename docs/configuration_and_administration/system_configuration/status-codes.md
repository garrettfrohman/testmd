---
id: "status-codes"
---

# Status Code Rules

Payment providers often return confusing messages to the merchant in the event of a declined transaction.  By using the Status Codes rule category it is possible to redefine these messages into a coherent reason code.

Rules created in the Status Codes category allow you to form a (Regex) query relating to the PSP generated decline message, and then define your own PSP status message that will be displayed in PaymentIQ along with the transaction.   This custom message has several advantages; it can provide greater clarity into a transactions’ reason for failing to any agents looking at a transaction; it standardizes decline messages to allow meaningful reporting on decline reasons; and in conjunction with the ‘Messages’ function of PaymentIQ, it allows custom decline messages to be displayed to the end user after a transaction failure.


Note:  Regex is a query language that can construct complex query terms and run them against text strings.  A full explanation of Regex is beyond the scope of this guide but there are many online resources that can provide a full explanation.

However, the following hints are most useful when constructing text-based queries on decline messages.

Regex string
* ```.*``` = any number of wild cards
* ```\``` = nullifies the meaning of the following character
* ```|``` = OR and allows a longer query
So ```.*xxx.*``` finds all strings with xxx in them at any point.

So the string
```.*\(51.*|.*insufficient.*```
Finds any text that has (51 or insufficient in it at any point.

(this query helps with identifying ‘Insufficient Funds’ (sometimes error code 51) reasons returned from a PSP)

## Constructing Status Codes Rules

Rules in this category are constructed in a similar fashion to those in other categories, with conditions leading to actions.  There are fewer conditions available due to the nature of the rule, and the most important conditions are the Regex query on PSP ‘Info’ and ‘PSP status code’. This is what we use to determine the exact nature of the decline message.

**Example Defines Insufficient funds as ‘TryLower’:**

![](/img/rulesettings/RulesStatusCodes/1.png)

The above rule redefines the PSP Status Code as ‘TryLower’.  This then appears next to the qualifying transactions as a new ‘PSP status code’.

Initially, by looking into the ‘PSP status codes’ and ‘Info’ that each PSP returns with a transaction, possibly in conjunction with a request to the PSP to provide plain text translations of their decline reason codes, it will be possible to define most decline codes.

The merchant would then construct rules based around a Regex query on each of these codes and standardize these across PSP’s.

Over time this will greatly improve the agents clarity on exactly why a transaction has failed, and will also provide a valuable tool for allowing reporting on decline reasons.
