---
id: "iin"
---

# IIN

IIN is the abbreviation for Issuer Identification Number, which is the first 6 or 8 digits of a credit card number, previously known as Bank Identification Number (BIN number).

This section contains a list of issuer identification number ranges and the associated card details that has been sourced at the IIN service currently in use, and provides further information as to the type of card, actual card issuer, their location, etc.

If the IIN number of credit card matches an IIN range, the respective issuer info details will be used for a transaction where the card is used.

It is possible to search within this list for full or partial card IIN ranges
![](/img/settingsandadmin/AdminIIN/1.png)

### Modifying the IIN list

Occasionally it will become apparent that the IIN list has incorrect details for a certain IIN, and this can potentially cause a customer transaction to fail (if the card is incorrectly identified as US issued, for example).

In this case we are able to edit the card details associated with a specific IIN number range.
П
* Double click any of the fields that require editing.

Some of these fields allow the user to enter a free text value (such as Bank) while other fields present a predefined drop down list of options.
![](/img/settingsandadmin/AdminIIN/2.png)

* Once the new values have been entered, unselect the input area and it will be saved automatically.

The IIN range will now be updated with the new information.

### Modifying the IIN range or creating new range
IIN ranges consist of 11 digits but the back office will only display 6 digits due to security.
To create a new range from the back office, double-click on the "Range start" and "Range end" columns of the existing IIN range, and a new range entry will be created.

Because of that PaymentIQ uses different sources of IIN range information, manual additions, and updates in the back office have the highest priority before all other sources.

