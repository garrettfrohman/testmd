---
id: "alerts"
---


# Alert Rules

The alert Rule category allows the merchant to set rules that will trigger Alert emails to defined email addresses when an event occurs.

The primary use of these rules is to provide transaction based early warning emails to alert the merchant in the event of outages or processing issues.  This means that action can be taken to mitigate any such issues and ensure the best continuity of transaction processing.

## Constructing Alerts rules

Email alerts are configured in much the same way as other rule sets in PaymentIQ, with conditions defining when the appropriate actions are triggered.

The nature of transaction based notification alerts is such that the conditions contain different values to the single transaction based rules.

Rules are constructed on the basis of looking back at the transactions in the last (merchant defined) minutes, and if the threshold of fails is greater than a percentage (that the merchant defines), then send an email.  Also included is the number of unique users (to try to prevent false positives due to one or two users continually failing).

Rules are set to check on a defined schedule, configured in the **Time interval** condition. The **Time interval** is a **‘Cron’** expression.

Note: **Cron** is a time interval construction, and while a full explanation of Cron expressions is beyond the scope of this guide, there are many online resources that can provide such an explanation.

However, the following hints are most useful when constructing a Cron expression for use in Alerts Rules.

`0 */5 * * * *` = Every 5 minutes

`0 */15 * * * *` = Every 15 minutes

`0 */30 * * * *` = Every 30 minutes

**Example Global card deposits alert:**

![](/img/rulesettings/RulesAlerts/1.png)

You will note that this rule looks at the last 15 minutes worth of transactions, but does so every 5 minutes. If ‘Fails’ are greater than 40% of all credit card deposit attempts and there are at least 5 unique users then the email template is triggered, and is sent to the email addresses specified.

Email addresses must be separated by a comma, with no spaces. The Email template to be sent is defined in the Admin section for Email templates and is covered later in this guide.

## Creating more specific Alerts rules

The alerts rule engine is a powerful tool and the defining of alerts can be made quite specific. It is possible to define rules for all payment methods, across all markets, and all channels.  It is up to the merchant to decide how granular the definition of alerts become, and it is usual to refine these alerts over time to be more and more useful.

Combined with the correct email template content specifying the definitive actions to be taken in the event of an outage, and ensuring these are received by the correct persons, means that the merchant can become very reactive to developing processing issues, and often identifies these before the processor themselves realizes that a problem is occurring.

### Set or stop provider maintenance on alert triggering

![](/img/rulesettings/RulesAlerts/2.png)

By setting the **Set to Maintenance** action to a value, a maintenance will be started or ended for the given PSP when the alert is triggered.

#### Setting provider to “fixed” maintenance on alert triggering

By setting the **Set to Maintenance** to **Fixed** a fixed maintenance window will be created. By setting the **time** and **time unit** actions we can set for how long the maintenance window last. (This can also be combined by sending mail when the PSP is set to maintenance)

![](/img/rulesettings/RulesAlerts/3.png)

*When the following rule triggers it will create a maintenance window that will last 10 minutes then it will be revoked. If the alert is still triggering a new maintenance window will be created and so on.*

#### Setting provider to “half open” maintenance on alert triggering

By setting the “Set to Maintenance” to **Half open** a half open maintenance window will be created. By setting the **time** and **time unit** actions we can set when a new live try for this provider will be tried. The tries will be logged to the transaction. This type of alert should be combined with a rule with the **Set to Maintenance** to **stop** so that the maintenance will be revoked by automatic when the PSP is online. (This can also be combined by sending mail when PSP is set to maintenance)

![](/img/rulesettings/RulesAlerts/4.png)

*When the following rule triggers it will create a maintenance window that will try a live request each minute.*

#### “Stop” provider maintenance on alert triggering

By setting the **Set to Maintenance** to **Stop** the maintenance window for that PSP will stop when triggering. (This can also be combined by sending a mail when maintenance is stopped)

![](/img/rulesettings/RulesAlerts/5.png)

*When the following rule will trigger the following rule will stop the maintenance for the PSP.*
