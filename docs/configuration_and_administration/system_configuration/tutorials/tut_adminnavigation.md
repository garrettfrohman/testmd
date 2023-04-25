---
id: "tut_adminnavigation"
---

# Administrator Navigation

The tutorials documents are intended to help new users of PaymentIQ familiarize themselves with how it is organized and what options are available. The tutorials requires access to PaymentIQ and/or the PaymentIQ Test environment, and you follow along replicating the steps demonstrated to maximize your learning efforts.

If you have any questions regarding the tutorials, please reach out to our support team.

:::info Prerequisites

To be able to follow along with this guide intended for administrators you should first have completed the **Basic Navigation** tutorial.

:::

Log in to PaymentIQ and click the User Accounts button from the navigation bar to access the **User Accounts** view

### User Accounts

The **User Accounts** view gives you access to manually activate, inactivate, delete or simply view customers’ ‘user accounts’.

In this context, a ‘user account’ is a masked credit card number, a bank account number, a Skrill email address etc. The specific account that the player used to deposit or withdraw, if you will.

The main uses of this tab are to search for players and understand what payment accounts they are using, and edit those payment accounts as needed. In this tab you can see the user, the type and specific Account used, as well as some other details.  

:::tip
It is important to note that the ‘Account’ often indicates a partial number, a ‘masked’ credit card number, or bank account, for instance.  For reasons of PCI compliance PaymentIQ is not allowed (and not able) to display complete credit card numbers in the back office.  However this does mean that some card numbers can appear to be used by more than player when in fact the masked (and therefore unavailable) numbers may differ, and this is a different card. 
:::

The ‘Status’ of the account is used to indicate the users ability to make transactions with that user account on the site.

The various meanings of the user account statuses are explained in the following table.

| Field              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Edit Account       | Edit account data, such as bank account number, PayPal email address, credit card expiry date, and cardholder name. The actual credit card number cannot be edited due to PCI regulations.                                                                                                                                                                                                                                                                                                         |
| Activate Account   | Deleted, Blocked or Inactive payment methods can be activated again. They become available to the customer for repeat payments, meaning that when selected in the cashier, the user do not have to re-enter the details.                                                                                                                                                                                                                                                                           |
| Inactivate Account | Removes a payment method from the users saved accounts in the cashier.                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Block Account      | Blocking customer user accounts will ensure that the user account cannot be used by any customer. Used primarily to block user accounts from problem gamblers, or cards that have seen fraudulent use. It is required to specify a reason in order to proceed with blocking. A predefined list of reasons exists and is configurable in MerchantConfig using `<tags>`. Moreover, the agent may specify the users’ block scope based on a specific merchant ID according to the MID hierarchy in PIQ. |
| Show Account       | Hidden payment methods can be made visible in the customer view in the site cashier.                                                                                                                                                                                                                                                                                                                                                                                                               |
| Hide Account       | Payment method details will be removed from the customer view in the site cashier. Users may also hide accounts by deleting them from the cashier themselves.                                                                                                                                                                                                                                                                                                                                      |
| Delete Account     | Deleting payment method details means that the customer will need to enter the entire details again upon their next deposit. However, the account details will not erased and will always be stored in PaymentIQ, but with a status ‘Deleted’.
| Verification       | Toggle between verification statuses **REQUESTED**, **VERIFIFED**, **UNVERIFIED**. The status can be used by the condition **User account verification status** in rules.

#### Updating player ‘User Accounts’

A PaymentIQ back office user is able to manually change the status of a ‘user account’ if required.

Follow these steps regardless of payment method and status. See figure below as example.

1. Search for the customer in the Search field or by using the Advanced Search.
2. Double clicking the customer User ID will list all payment methods used by the customer.
3. Select the Payment Type to be edited. Two or more different payment methods can be selected simultaneously as long as the status selected remains the same.
4. Select the option under the Action button.
5. Confirm your action

If you want to block an account, you should specify the reason category and may specify the block scope. By default, the system will block only the selected user PSP account. If the block scope is specified, the user (for example the cc account) will be blocked over all sub merchants/brands within the selected block scope.


### KYC

Click on the KYC button in the navigation bar to access the **KYC** views.

![](/img/tutorials/tut201.png)

:::tip
The KYC tab consists of sub-tabs used to set parameters, and query and manage the results of integrated KYC checks. Depending on the merchant setup you may have multiple KYC providers offering results.
:::

#### KYC Search Tab

The Search KYC tab has the same basic characteristics for searching, exporting, reordering etc. as the Transactions tab.

The main reasons for Searching within user KYC are;
- Identifying accounts that need further investigation or action, such as those that have an *UNDERAGE* status or appear on the *PEPs and Sanctions* list.
- Verifying the individual KYC status of users.
- To manually update the (verification) Score of a player. Click into the score box for a player, enter a new score, and then use the **Update > Save Changes** button on the right to confirm the new Score.

#### Block Tab

The Block tab is used by PaymentIQ Admins to set rules based blocks on player transactions dependant on the KYC results returned by your integrated KYC provider.

#### Routing Tab

The Routing Tab is used by PaymentIQ Admins to set rules for determining in what circumstances a KYC check is performed, and by which integrated KYC provider.

#### Fallback Tab

The Fallback Tab is used by PaymentIQ Admins to set rules for determining the order that integrated KYC providers are used, if more than one provider is integrated.

### Rules

Click on the Rules button in the navigation bar to access the **Rules** settings.


![](/img/tutorials/tut202.png)


The Rules tab is used to manage the merchant specific rules that apply to a transaction during processing. The rules tab consists of sub-tabs that contain the rule definitions for different categories of rules. Generally speaking, all of the rules can apply to a transaction, and a transaction checks all of the rules until it finds a rule that applies, or reaches the end of the rules. Think of a transaction entering the rules at the top category, and moving through each category of rule until it finds one that applies, top to bottom, and either actions it, or runs out of rules in that category. It then moves down to the next category of rule and looks at those, etc. until it reaches the end of the rules, when the transaction is processed (or not) according to the rules that have been applied.



### Admin

Click on the Admin button in the navigation bar to access the **Admin** settings. If you have the accesses needed on the user you are logged in with you will see one or more of these sections:

![](/img/tutorials/tut203.png)

The Admin tab is used to set the merchant specific configuration of PaymentIQ and has several sub tabs.

- Configuration ​– This area determines specific technical parameters of the merchant, such as integration passwords, and setup configurations. In normal circumstances Configuration should only be changed by Devcode staff, as any errors made may cause transaction processing to STOP.
- Back office Users – This is where an Admin can manage users and user access levels. Further details are provided in the Admin user section.
- Templates – This area allows an Admin user to set up dynamic email templates for any rules that are configured to trigger email sendouts. Further details on email setup are provided in the Admin user section.
- Messages – This area allows an Admin user to specify the messages that will be displayed in the cashier to a site visitor once a transaction has completed. This could be used for dynamic error messaging, for example. Further details on email setup are provided in the Admin user section.
- Forex Rates – This allows an Admin user to look up, change, or add foreign exchange rates that are used by PaymentIQ in the course of transaction processing. Further details on Forex setup are provided in the Admin user section.
- IIN – This area allows for lookup of the card IIN (The first 6 digits of a credit card number are known as the Issuer Identification Number, previously known as bank identification number or BIN). An Admin user can also edit the information stored that relates to card issuers if they wish. Further details on the IIN list are provided in the Admin user section.