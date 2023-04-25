---
id: "messages"
---

# Messages

This area of PaymentIQ is used to define custom messages and labels that will be displayed to the end-user during transactions, as well as setting up translations for different locales.

This is a powerful tool and when used in conjunction with custom [PSP status messages](statesandstatuscodes) and can help turn a failed deposit into a future successful deposit by informing the user of a specific reason for the deposit failure.

In the default Messages view you will see many predefined messages that have been set by PaymentIQ and are currently displayed to the customer.

## Reference

| Attribute    | Description                                                           |
| ------------ | --------------------------------------------------------------------- |
| Key          | The key that is referenced in your application to retrieve a message. |
| Category     | The type of message.                                                  |
| Locale       | The country and/or language tag a text should be displayed for.       |
| Value        | The text that will be displayed when the key is referenced.           |
| Description  | A note about the text.                                                |
| Last updated | When the message was last edited.                                     |
| Merchant ID  | Which merchant the message is defined on and/or inherited from.       |

## Creating a New Key

To create a new message key, simply bring up the **New Key** dialogue via the button in the menu. In this dialogue you will be able to define the key name and texts you want to appear, as well as translations.
## Editing an Existing Message

When editing a message, it's a good idea to search for the text that you are looking to replace and open the **Edit Message** dialogue by clicking on a relevant result. In this dialogue, you will be able to change the key name, texts and translations of the message.

It is possible to edit texts that have been inherited from your parent merchant or PaymentIQ - the texts that are greyed-out in the table - as well. These changes will be saved to your current merchant only and be accessible by it and its submerchants, allowing you to edit the texts you want while retaining everything else. 

If you want to edit and share messages across multiple submerchants, make sure to do it at an appropriate parent-level where it can be accessed.
### Advanced Example

In this example, we will replace the message *"This card was denied, please try a different card."* with a message that better indicates the reason the card was denied. The reason, in this example, was because of insufficient funds and we would like to suggest to the user to try a lower amount.

* From a search we see that many existing keys use this generic error message. The result shows multiple keys formatted as `creditcarddeposit.pspcode.xxxxx` where the last bit `.xxxxx` represents a PSP status code.

 ![](/img/settingsandadmin/AdminMessages/2.png)

* On the **Rules/Status Codes** page, we have already defined a custom status code for **Insufficient Funds** as **TryLower**. We will use this custom status code for our new message.

* In the **Messages** menu, use **New Key** to create a new key.

 ![](/img/settingsandadmin/AdminMessages/3.png)

* Create a new key with the name `creditcarddeposit.pspcode.TryLower`, adding other details as appropriate. You can choose to add translations for the key at this point if you have multiple locales defined.

 ![](/img/settingsandadmin/AdminMessages/4.png)

* Click the **Save** button.
  
* You will now find your new message `creditcarddeposit.pspcode.TryLower` in the table for the locales you defined. If you would like to add more translations or change a value, simply click on row to bring up the **Edit Message** dialogue again.

 ![](/img/settingsandadmin/AdminMessages/5.png)

The new decline message is now defined and will apply and is shown to the end-user each time that the **PSP Status** is **TryLower**.

## Adding Locales and Translations

To create a new locale for your messages, open the **Add Locale** dialogue via the button in the menu. In this dialogue you can set a new locale for your messages. The locale must be formatted appropriately, e.g. `en_GB` or `en`.

The locale should be available when you edit or create a message.

## Importing and Exporting Messages

If your user role allows it, you can import and export messages as CSV files.

 ![](/img/settingsandadmin/AdminMessages/6.png)
### How to Export

* Click the **Export** button in the Messages menu.
* A dialogue will open with a field for the CSV separator. The default is `,` if nothing else is configured [here](usersettings).

 ![](/img/settingsandadmin/AdminMessages/7.png)

* Press the **Export** button to download a CSV file of your messages.
### How to Import

* Click the **Import** button in the Messages menu.
* A dialog will now open where you specify the file to import and what CSV separator is used in the document. The default is `,` if nothing else is configured [here](usersettings).

 ![](/img/settingsandadmin/AdminMessages/8.png)

 **Note**, it's important that the following headers are at the top of the CSV file: **category, description, key, locale, value** corresponding to the rest of the contents in the file. All headers and values should be wrapped with `"` and the document should be in `UTF-8` encoding. 

 See example:

 ```
 "category","description","key","locale","value"
 "GUI Text","Amount","amount","en","Amount"
 "GUI Text","Deposit button","deposit.button","en","Press here to deposit"
 "GUI Text","Withdrawal button","withdrawal.button","en","Press here to withdraw"
 ```

* Then click **Import** to import the keys to the current merchant.

 The locales will also be imported if they don't exist. If you import keys that already exists then they will be updated with the data from the imported file.