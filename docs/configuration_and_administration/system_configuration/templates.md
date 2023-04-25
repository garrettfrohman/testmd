---
id: "templates"
---

# Templates

This area of PaymentIQ is dedicated to the setup of templates that will be used by the merchant.

Although there are five subsections in this category, only the section on Email Templates concerns the merchant user.

The other subsections are for advanced PaymentIQ functions and would generally only be accessed by Devcode staff.

## Email Templates

The email templates category is where a merchant may define specific texts that form the content of the emails that will be initiated by rules triggered in the **Alerts** and **Notification** category of the Rules section explained earlier in the manual.

These templates are generally composed in HTML format, and may contain dynamic elements used to reflect the specifics of the transaction (in the case of a notification) or Alert parameters (in the case of an alert).

### Configuring Email Templates

Email templates are typically composed of a text portion, along with dynamic parameters used to personalize the email to the end user, in an HTML format.

HTML formatting is beyond the scope of this guide, but usually emails to customers can be composed and provided as HTML by a member of your company who has responsibility for copywriting.

To create a new template click on **Add new template +**

![](/img/settingsandadmin/AdminTemplates/1.png)

A new template form will open below. 

This template is to be sent to a customer upon a successful withdrawal, so enter an appropriate Subject line and click the **HTML Body** button to enter the text.

When entering a text you may use one of the available dynamic tags below.

**Commonly used dynamic tags for ‘Notification’ email templates**

| Dynamic Tag                         | Description                                  |
|-------------------------------------|----------------------------------------------|
| ```${ptx.merchantUser.firstName}``` | The merchant user first name                 |
| ```${ptx.merchantUser.lastName}```  | The merchant user last name                  |
| ```${ptx.merchantUser.userId}```    | The merchant userId                          |
| ```${ptx.maskedUserAccount}```      | The masked payment account (e.g credit card) |
| ```${ptx.txAmountAbs}```            | The transaction amount (includes currency)   |

Find all available dynamic tags in the [Email and MQ Parameters](emailparameters) chapter.

A simple withdrawal approval email text might be:

```
Hello ${ptx.merchantUser.firstName}!

Good news!  You recent withdrawal of ${ptx.txAmountAbs} has now been approved and should be with you shortly.

Thanks for playing at our site.

Have a great day!

Regards,

Your customer support team.
```

This would then be entered into the template in a HTML format:

![](/img/settingsandadmin/AdminTemplates/2.png)

Now add a similar text only version to **Email text** (this is the text that will be sent to a user that has email settings that prohibit HTML emails, and is required).

![](/img/settingsandadmin/AdminTemplates/3.png)

Click on the **Save** or **Configure**(i) button at the bottom of the screen. A modal window will open where you can edit the name of the template(that will be used by the rule to specify use of this template). There you can optionally add a Channel, a URL  and a Locale. When you are finished, click on the  **Save** or **Update**(i) button at the bottom of the modal window.

> **_(i):_** This button will replace Save when editing an existing Template.

![](/img/settingsandadmin/AdminTemplates/4.png)

This template is now available and will be sent by any rule that uses the defined **Name** for the Email Template field in that rule.

You may edit this template at any time, and save any changes made by using the **Update** button.

Of course your content department will be able to create much more complex HTML emails that better fit into your merchant brand.  Such emails can also be configured to inform about the latest site promotions, or carry any other information deemed appropriate.

Hint: The site [http://htmledit.squarefree.com/](http://htmledit.squarefree.com/) (not affiliated to Devcode) allows you to see the output from any HTML text rendered in a new window in real-time and is a useful  tool for checking any templates created.

**Dynamic Tags for ‘Alert’ email templates**

| Dynamic Tag             | Description                                        |
|-------------------------|----------------------------------------------------|
| ```${psp}```            | The defined PSP used in the rule.                  |
| ```${threshold}```      | The defined threshold percentage used in the rule. |
| ```${tx_type}```        | The defined Tx Type used in the rule.              |
| ```${psp_service}```    | The defined PSP Service used in the rule.          |
| ```${ALERT_DATE}```     | The time & date the alert was triggered.           |
| ```${unique_users}```   | The No. of unique users.                           |
| ```${minutes_back}```   | The No. of minutes of transactions queried.        |
| ```${percent_failed}``` | The percentage of failed transactions.             |
| ```${merchant_id}```    | The merchant ID that triggered the rule.           |

These tags could be used within an Alert email to give the recipient information regarding the alert generated.

For example, the subject line might read:

Processing ALERT! There have been ```${percent_failed}``` failures in processing ```${tx_type}``` in the last ```${minutes_back}``` !

If informative Alert email templates are constructed, these can help guide the recipient on the steps needed for escalation of the Alert issue.

### Viewing Audit of Template

:::note
This feature has not yet been migrated and is currently only available on <u>[Backoffice version 1.0.191](https://backoffice.paymentiq.io/?version=1.0.191/#)</u>.
:::

The same history function that is available for rules and configuration changes is also applied to templates *Show history*.

![](/img/settingsandadmin/AdminTemplates/6.png)

When clicking the *Show history* link the history of this template will be shown.

![](/img/settingsandadmin/AdminTemplates/5.png)

Just as for rules or configuration you can then select a version to revert to of the template.
