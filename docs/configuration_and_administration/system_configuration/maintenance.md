---
id: "maintenance"
---

# Maintenance Settings

## Introduction
With any Payment Service Provider there will be times of both planned maintenance and temporary outages. This guide will show you how to deal with maintenance windows for PSPs. It will outline how to prepare for planned maintenance and how to both manually and automatically deal with outages through alerts, fallbacks and rerouting.

After going through the guide and the example chapters you will be able to set up a solution which will minimize service interruption for your customers.

For Credit Card and BANK payments you will be able to set up automatic maintenance failover rules to a secondary PSP.

For Vouchers and EWallets you will be able to temporarily block or remove those payment options from your listed option during the maintenance and notify your customers.

You will be able to deal with notifications of maintenance windows both for when they start and finish.

Most importantly you will benefit from having a prepared clear strategy dealing with PSP maintenance situations. Ultimately this will give you improved acceptance rates.

Please note that you need to have more than one acquirer to set up failovers.

## The Maintenance Area

The Maintenance area can be found from the navigation bar menu in the PaymentIQ back-office by clicking *Admin > Maintenance*.

![](/img/settingsandadmin/AdminMaintenance/0.png)

In this area you can manage entries for when a provider/PSP is having a maintenance window. This page also acts as a log of maintenance windows, giving a complete overview of historical ones, those in progress and those that are upcoming.

The search functionality works the same way as when doing a transaction search. You can search for maintenance windows on *provider type*, *PSP*, *method*, *start date* or *end date* etc. You can also double-click in cells such as PSP or provider to perform a search.

Maintenance windows can be set either by the DevCode team or by the merchant.

![](/img/settingsandadmin/AdminMaintenance/1.png)

* **Merchant-Id** A Payment IQ unique ID to identify a merchant.
* **Id** An ID to identify the maintenance window. Please note that if a transaction is affected by a maintenance rule this ID will be added to the rules column of the transaction.
* **Provider type** The type of provider (Credit card, Neteller etc).
* **PSP** The payment service provider.
* **Service** The PSP service (Ideal, Sofort etc).
* **Method** The method (Deposit, Withdrawal).
* **Mode** The mode of the maintenance. There are currently four different modes:
	* **NO_PLANNED_MAINTENANCE** Default value for when no maintenance is scheduled.
	* **PLANNED_MAINTENANCE** There is an upcoming maintenance window.
	* **DONE** Shows that there was a maintenance window and that it is over.
	* **MAINTENANCE** Shows that a maintenance is in progress.
* **Start date** The date and time for when the maintenance window starts.
* **End date** The date and time for when the maintenance window ends.
* **Excluded user ids** If you would like to exclude some user they are added here. This can be used to test with a specific user if everything works correctly before maintenance has ended.
* **Message key** The message key that the user will get in response when its under maintenance.
* **Message** Will show the translated value of the key in any language (“en” is the default locale for translation). Messages are managed in **Admin** > **Messages**

### Adding a New Maintenance Window
To add a new maintenance window. Select the provider type that you would like to add by checking the checkbox to the left, or right click on the table row.  If you right click, a menu is shown. The same menu will be shown when clicking the **Action** button to the right.

![](/img/settingsandadmin/AdminMaintenance/2.png)

Click on **New [The selected provider type] maintenance.**

![](/img/settingsandadmin/AdminMaintenance/3.png)

A dialog will open where you can enter the conditions for the maintenance. By default we are showing the method (provider type), from date, to date, PSP. You can also add other conditions that can be found under the + sign the same way as when you are adding conditions in the rules section.

For actions there are a few different options, some can be found under the + sign.

* **Message key** This is referring to an existing or new message key that you have defined in the *messages* section.
* **Time** The time value for next live request (only applicable for HALF_OPEN maintenance type).
* **Time unit** The time unit for next live request (only applicable for HALF_OPEN maintenance type)
* **Type of Maintenance**
	* **FIXED (default)** Start date and end date based maintenance. This will not let any traffic to the provider until the end date has passed.
	* **HALF OPEN** Just as with FIXED there is a start and and end date and time. But here regular live requests are made, testing if the PSP/provider is working. This setting has to be combined with an alert rule that will stop the maintenance automatically.

Please note that you should always enter a start date for your maintenance if the provider type is not indefinitely in maintenance. The end date can be left blank if you don’t know when it ends. In that case you will have to add an end date later or delete it when the maintenance is over.

### Editing a Maintenance Window
Editing a maintenance window is done in a similar way as when you add a new maintenance window. Select the maintenance window that you would like to edit by checking the check-box to the left, or right click on the table row. If you right click, a menu is shown. The same menu will be shown when clicking the **Action** button to the right.

![](/img/settingsandadmin/AdminMaintenance/4.png)

Select **View/Edit [Selected Provider type] maintenance.**

![](/img/settingsandadmin/AdminMaintenance/5.png)

An edit/view dialog will open with the conditions that you have for that maintenance window. Edit the information you would like to change and then save your changes.

### Removing a Maintenance Window
This is done in a similar way. Select the maintenance window that you would like to delete by checking the check-box to the left, or right click on the table row. If you right click, a menu is shown. The same menu will be shown when clicking the **Action** button to the right.

![](/img/settingsandadmin/AdminMaintenance/6.png)

Select **Delete [Selected Provider type] maintenance**. The maintenance window will be deleted from the grid. You can also mark multiple maintenance windows and delete all marked at once.

### Manually Starting or Ending a Maintenance Window
The quickest way of ending or starting maintenance is to right click on a provider or provider type and then select start or end maintenance now.

![](/img/settingsandadmin/AdminMaintenance/7.png)

* **Start maintenance now** Creates a maintenance entry with **start date** now with the given provider type and provider.
* **End maintenance now** Ends an ongoing maintenance now by setting the **end date** to now.

### Viewing Audit of Maintenance Window Settings
The same history function that is available for rules and configuration changes is also applied to maintenance settings under *Action* > *Show history*.

![](/img/settingsandadmin/AdminMaintenance/8.png)

## Using Alert Rules to Trigger Maintenance Mode

In the Alert Rules there are options to trigger Maintenance Mode from within a rule. This has many benefits, such as having a quick response on PSP issues and automatically dealing both with rerouting and returning to normal when the maintenance is over. Essentially alert rules can be used to deal with PSP outages in a prepared and predefined way.

The alert settings can be found from the navigation menu under **Rules** > **Alerts**.

Adding conditions to a rule will work just as it would for Routing or any other rule type.

It is in the **Actions** settings with the **Set to Maintenance** option that you can trigger to start or stop a maintenance window for a PSP when an alert is triggered.

![](/img/settingsandadmin/AdminMaintenance/9.png)

There are three options for the **Set to Maintenance** Action which all correspond to the settings you make directly in the maintenance settings.


* **Fixed** Creates a fixed maintenance window when the rule is triggered.
* **Half open** Creates a half-open maintenance window when the rule is triggered.
* **Stop** Stops a maintenance window when the rule is triggered.

### Fixed Maintenance Action on Alert trigger

By setting the **Set to Maintenance** to **Fixed** a fixed maintenance window will be created from when the rule is triggered. By setting the **time** and **time unit** actions we can set for how long the maintenance window last. This can also be combined with other actions such as sending an email for when the PSP is set to maintenance.

Please note that **time** and **time unit** are required values for a fixed maintenance window. If these are not added it will be indefinite.

When the following rule triggers it will create a maintenance window that will last 10 minutes after which it will be revoked. If the alert is still triggering a new maintenance window will be created and so on.

![](/img/settingsandadmin/AdminMaintenance/10.png)



### Half open Maintenance Action on Alert trigger
By setting the **Set to Maintenance** to **Half open** a half open maintenance window will be created. By setting the **time** and **time unit** actions we can set when a new live try for this provider will be tried. The tries will be logged to the transaction. This type of alert should be combined with a rule with the **Set to Maintenance** to **stop** so that the maintenance will be revoked automatically when the PSP is online. This can also be combined with other actions such as sending an email for when the PSP is set to maintenance.


When the following rule triggers it will create a maintenance window that will try a live request each minute.

![](/img/settingsandadmin/AdminMaintenance/11.png)

### Stop Maintenance Action on Alert trigger

By setting the **Set to Maintenance** to **Stop** the maintenance window for that PSP will stop when triggering. This can also be combined with other actions such as sending an email for when the PSP is stopped.


When the following rule is triggered (by meeting the conditions) it will stop any ongoing maintenance for the PSP.

![](/img/settingsandadmin/AdminMaintenance/12.png)


## The Importance of Fallback Rules

When a PSP goes into Maintenance and becomes unavailable either through scheduled maintenance or outages identified by alerts, the temporary solution is to have a fallback PSP available. Without fallback rules there will not be any routing available for the transaction and it will fail.

Fallback rules are set up from the navigation menu under **Rules** > **Routing** > **Fallback**. Instructions for how to set them up are out of scope for this guide (see the backoffice user guide for detailed information).

Please note that fallback rules are especially important to pay attention to when it comes to weighted routing rules. If two PSPs have equal weight and one of them goes into maintenance mode (either scheduled or because of a temporary outage) it does not mean that 100% of the traffic will automatically go into the remaining PSP. For that to work the remaining PSP needs to be set up as a fallback for the failed one.

## Get user's available payment methods (Advanced)

From the front end API you have the possibility to query for available payment methods. In the response there will be information about the maintenance status.

```JSON
"maintenanceInfo": {
                "maintenance":true,
                    "from": "2017-10-05",
                    "to": "2017-11-06",
                    "message":"Credicards are currently under maintenance"
}
```

This information can be useful when building a cashier. For example with if a Voucher solution is not working users can be stopped from using it in the cashier whilst it is under maintenance.

Please also notice that the message returned is set up in **Admin** > **Messages** and linked up with the maintenance window through the **Message key** option in the maintenance settings.

More information about how to interact with the front end API can be found in the PaymentIQ front end API documentation.


## Example Situations

The examples in this section are mean to illustrate some of the combinations of settings that can be used to handle PSP maintenance situations. Do not hesitate to contact the support team if you need more information about a particular situation or if you need help constructing the rules.

### Example 1 - CREDITCARD FAILOVER

A merchant recognizes that a PSP has frequent outages and that they need to have a plan for an automated failover option and a way to stay updated on the status of the situation for when this happens.

The merchant realizes that they need:

1. An alert rule that puts the PSP in maintenance mode and notifies relevant staff
2. A fallback PSP to be used when the original PSP is in maintenance.
3. A notification email
4. An alert rule that re-enables the original setup when the PSP is working again.

#### The Alert - Detecting the issue

This alert rule will check the chosen PSP every five minutes, and if 75% of the transaction has failed (with a minimum of 4 transactions) it will trigger the actions.

The actions are to send an email to staff@merchant.com based on the template PSPOutageAlert. It will check every two minutes if the PSP is working again by allowing for one live transaction.

![](/img/settingsandadmin/AdminMaintenance/13.png)

#### The Alert Email - Notification of the issue

This email will notify which PSP has trigged the alert rule. Use the variable ```${PSP}``` to show the PSP.

![](/img/settingsandadmin/AdminMaintenance/19.png)

#### The Fallback

This fallback rule will, if the PSP that is in maintenance is initiated instead use the one selected under PSP fallback (with the account N3DS).

![](/img/settingsandadmin/AdminMaintenance/14.png)

#### The Alert - Returning to normal

This alert will stop a PSP outage if it is operational again.

This alert rule will check every 5 minutes and look 10 minutes back if more than 77% of the transactions are successful or waiting for input with a requirement of minimum 4 users.

If so it will trigger and stop the maintenance window and send an email to staff@merchant.com based on the email template PSPOutageResolved.

![](/img/settingsandadmin/AdminMaintenance/15.png)

#### The Alert Email - Notification of PSP working properly

This email will notify that the PSP has is back to normal. Use the variable ```${PSP}``` to show the PSP.

![](/img/settingsandadmin/AdminMaintenance/20.png)


### Example 2 - E-WALLET MAINTENANCE

A merchant recognizes that an E-Wallet provider outage is best helped by removing it as a payment option for a given period of time.

The merchant realizes that they need:

1. An alert rule that puts the PSP in maintenance mode and notifies relevant staff
2. A notification email

#### The Alert - Detecting the issue

This alert rule will check for a specific transaction status code. If it appears it will put the PSP in maintenance for 10 minutes. After that it will be available again. Should the status code reappear it will again go into maintenance for the same amount if time and so on.

![](/img/settingsandadmin/AdminMaintenance/16.png)

#### The Alert Email - Notification of the issue

See previous example for how to configure this.


### Example 3 - CREDIT CARD SCHEDULED MAINTENANCE

Devcode has scheduled a maintenance window for a PSP. The Merchant uses the PSP in a weighted routing rule and needs to make sure the maintenance does not cause interruptions of service.

The merchant realizes that they need a fallback rule that triggers on maintenance.

#### The Routing rule

This is an example of how a weighted routing rule looks. Notice that if one of the PSPs go into maintenance 100% of the traffic will not go to the other one unless a fallback rule is set up.

![](/img/settingsandadmin/AdminMaintenance/17.png)

#### The Fallback rule

This fallback rule will reroute all traffic intended for one PSP to a fallback PSP.

![](/img/settingsandadmin/AdminMaintenance/18.png)


## Summary

* Maintenance windows are useful to get a higher acceptance rate by temporarily using alternative routing for when a PSP is not available.
* PSPs can be set to go into maintenance mode on schedule, either by Devcode or by the Merchant through the PaymentIQ Backoffice.
* PSPs can also be set to go in or out of maintenance mode on the triggering of an alert rule.
* If a PSP is in maintenance mode there needs to be a fallback routing rule in place or transactions will fail.
