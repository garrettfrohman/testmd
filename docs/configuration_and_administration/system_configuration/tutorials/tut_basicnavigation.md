---
id: "tut_basicnavigation"
---

# Basic Navigation

The tutorials documents are intended to help new users of PaymentIQ familiarize themselves with how it is organized and what options are available. The tutorials requires access to PaymentIQ and/or the PaymentIQ Test environment, and you follow along replicating the steps demonstrated to maximize your learning efforts.

If you have any questions regarding the tutorials, please reach out to our support team.

:::info Prerequisites

To be able to follow along with this tutorial you will need to have access to either the PaymentIQ Test or the PaymentIQ Production environment.

:::

### Login

PaymentIQ has two backoffice systems that you as a merchant can log in to, one test and one production environment. You can log in to either of them to follow this tutorial. When going to the system URL you will be prompted by a login screen and depending on how your system administrator has configured the system an additional two factor authentication verification prompt. Log in to the backoffice system using your credentials.   

![](/img/tutorials/tut00.png)


### Home View

When you have logged in you end up in the **Home** View of PaymentIQ. It has links to the views your PaymentIQ user has access to. You may have access to more or fewer tabs than the below screenshot. An overview of those can be found in the Administrator Navigation Tutorial.

![](/img/tutorials/tut01.png)

The same views/tabs that are accessible from the **Home** view can also be accessed via the the top navigation bar.

At the top right of the navigation bar you will also see your the user details of the user you have logged in with and the MID you are currently logged in to. If you have access to multiple MIDs you will see a dropdown menu from which you can switch between them.

:::tip

A MID or MerchantID is the identifier used in PaymentIQ for the merchant system/brand. A merchant can have multiple MIDs in PaymentIQ.

:::

### Transaction View

Click on the Transaction button to access the **Transaction** view.

![](/img/tutorials/tut02.png)

The **Transaction** view is the main query screen for searching and viewing transaction details.

This is the main query screen for searching for and viewing transaction details. Any transaction from the merchant that interacts with PaymentIQ will be listed here. 

Right click on any of the headers of the columns in the table of transactions to view a select menu for which columns that should be shown for your backoffice user in that view.

![](/img/tutorials/tut07.png)

As you get familiar with the system you may want to modify what columns are shown for you. 

Right click again on any transaction or column in the table of transactions to see a menu of useful options specific to that transaction.

![](/img/tutorials/tut08.png) 

### Searching

At the top of each of the views there is a search bar from where you can do searches relevant to the specific view you are in. Clicking in the Search box brings up a list of categories to use in the search if needed.

To filter transactions select a category and follow the instructions.

Add multiple categories to further refine the search.

Click the search button to start the search.

:::tip
Double-clicking a cell in the results can quick-add add that cell contents to the search terms.
:::

Directly pasting a search parameter and pressing enter or Search will search for that term. e.g.; Player ID, email address, IP address, masked card No. Etc.

Partial searches do not give any results. You must search for full terms (like full email, full masked card No. Etc.).

:::tip
Clicking the star on the right hand side of the search bar will add the current search to your favorite searches for use another time. These are then listed under the number next to the star for quick access again. Use this to help speed up your work.
:::

### Advanced Search alternative

Clicking the down arrow next to the search button will bring up a different format ‘Advanced Search’ option.
In Advanced Search, select your parameters and either display the results by clicking Search, or export to CSV by clicking Export CSV.

:::tip​ TIP
If you are looking to export results, Search first to ensure results displayed are what you expected, before exporting.
:::

:::tip​ TIP
If you are looking to export results, always include a reasonable start date. If you try to export too much data the resulting export might time out. This type of ‘Advanced Search’ cannot be saved for use later.
:::


### Approve View

Click on the Approve button to access the **Approve** view.

The **Approve** view is the place to manage and approve or deny pending transactions.

![](/img/tutorials/tut03.png)

The main use cases for this tab are:
- Approving or denying a player withdrawal.
- Approving or denying a player deposit.

The Approve tab has the same basic characteristics for searching, exporting, reordering columns etc. as the Transactions tab.

Transactions are approved or denied by checking the box to the left of the transaction/s and then using the Action button on the right.

Multiple transactions can be selected for processing at the same time.

Once a withdrawal is actioned, it is sent back to the player account (Deny), or to the PSP for processing (Approve), and the status will update accordingly.

There is a confirmation dialogue before the action is taken.

### Investigate View
Click on the Investigate button to access the **Investigate** view.

![](/img/tutorials/tut04.png)

There are several functions of the Investigate tab:

- Manually force the status of a transaction into another status. The main use of this function is for user queries, when a transaction, for some reason (e.g connection error), has not completed correctly and needs to be adjusted.

- Allow back office users to register refunds, captures, and voids against existing transactions.

- Allow back office users to register manual corrections on existing transactions, such as chargebacks and refunds (only for reporting purposes).

#### Updating a transaction status

![](/img/tutorials/tut09.png) 

It is important to note that there are two types of transaction statuses.  

1. *Finalized* status transactions (the transaction has reached a conclusion). These are `SUCCESSFUL`, `FAILED` and `CANCELLED`.
2. *Pending* status transactions (the transaction is still waiting to move to a final state).  These are `WAITING_INPUT`, `WAITING_APPROVAL`, and `INCONSISTENT` transactions.

A transaction that is moved to a final state will trigger a notification in the Integration API, either a cancel or a transfer depending on the status. This notification must be handled by the merchant system in order to force a change in the user account – adding the funds from a successful deposit, or returning pending withdrawal funds to a player account if failed.

1. Use the search function to find the transactions(s) you wish to update.
2. Select the checkboxes of the transactions you would like to update. To select all the boxes at once, click on the uppermost checkbox.
3. Click on the Update button on the far right hand corner and select the Update method.
4. Confirm the option selected.

The table below describes the actions that occur when a transaction status is updated in the specified manner.

| Update Field       | Description                                                                                                                                                                                                                                                                                                                      |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Force Successful   | A customers’ deposit has been debited by the PSP, but the customer account on the merchant website has not been credited for some reason. We can force these transactions into a successful state, which will automatically credit the customer account. An example use would be to credit a customer who has a missing deposit. |
| Force Failed       | Transactions that might be “stuck” in a certain status for some reason can be forced failed and the transaction will be finalized as failed.                                                                                                                                                                                     |
| Force Inconsistent | If you need to change a Failed transaction to Successful, or vice versa, you must first make it inconsistent, before forcing into Failed or Successful. Also, transactions that didn’t complete correctly, and are in an “indefinite” state, can appear with an `INCONSISTENT` state.                                            |

It is important to note that when changing a transaction from failed to successful, or vice versa, a two-step process must be performed.  The transaction must be first moved to `INCONSISTENT` like so; Successful > Inconsistent > Failed or Failed > Inconsistent > Successful.

#### Registering Refund, Capture, and Void

These actions will perform a request against the PSP and create a new transaction in PaymentIQ connected to the original transaction.

| Update Field    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Capture         | Manually capture the amount of an authorized transaction. The transaction must have the status code `SUCCESS_WAITING_AUTO_CAPTURE` or `SUCCESS_WAITING_CAPTURE` in order to be captured.                                                                                                                                                                                                                                                                                                                      |
| Partial Capture | Manually capture a specific amount of an authorized transaction. The transaction must have the status code `SUCCESS_WAITING_CAPTURE` in order to be captured.                                                                                                                                                                                                                                                                                                                                                 |
| Refund          | This will attempt to refund the transaction back to the customer by sending an instruction to the Payment provider. When you make a refund, PaymentIQ does various checks to ensure that the financial institution accepts refund instructions and that the amount to be refunded is still available for that payment. If it is permitted, the refund request is scheduled and sent to the appropriate financial institution. Once a payment is processed, the customer receives the refund amount requested. |
| Partial Refund  | Same as refund but for a specific amount.                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Void            | Credit card transactions can be cancelled (void) before they are captured. If a payment is captured, the customer has been charged and you cannot use this process and should consider making a refund instead.                                                                                                                                                                                                                                                                                               |

#### Registering Manual Corrections

With this function it is possible to register manual corrections on transactions. This will create a new transaction in PaymentIQ that will be associated to the original transaction, but is for information purposes only. No adjustments on the PSP will occur.

These adjustments are mostly useful for reporting purposes, and provide a method for Chargebacks etc. to be included in any reporting generated from the PaymentIQ database.

The table below describes the available correction types.

| Correction Type            | Description                                       |
|----------------------------|---------------------------------------------------|
| Manual Chargeback          | Registers a ManualChargeback transaction          |
| Manual Refund              | Registers a ManualRefund transaction              |
| Manual Partial Refund      | Registers a ManualRefund transaction              |
| Capture                    |                                                   |
| Partial Capture            |                                                   |
| Manual Void                | Registers a ManualVoid transaction                |
| Manual ChargebackWon       | Registers a ManualChargeBackWon transaction       |
| Manual RequestForInfo      | Registers a ManualRequestForInfo transaction      |
| Manual NotificationOfFraud | Registers a ManualNotificationOfFraud transaction |

The user can add a Tag and a Comment for each correction type, with exception for Manual Chargeback and Manual ChargebackWon where you can also add a Notification Date (date when you as a merchant received the chargeback notification), and also for Manual Partial Refund where you have to choose the specific amount. The below example is for when registering a Manual Chargeback.

1. Select a transaction and choose Update > Register Correction.
2. Select the type of correction from the list.
3. Choose Notification Date (optional) \*
4. Choose a tag (optional) \*
5. Enter a Comment (optional) \*

\* If added, this will later appear in the ‘Info’ column of the created transaction.

### Admin Menu

Click on the Admin button to see the **Admin** menu.

![](/img/tutorials/tut06.png)

Depending on your access rights you will see different options in this menu. All users will have access to the **Resource Center** option. The other menu options are covered in the Administrator Navigation Tutorial.

Click on **Resource Center**

The Resource Center contains a link to the PaymentIQ Documentation Portal (this portal)

![](/img/tutorials/tut05.png)

This concludes the basic navigation guide for the most common pages used in day-to-day operations. 

:::tip
If you are an administrator or manage settings in PaymentIQ, please also follow the **Administrator Navigation Tutorial**.
:::