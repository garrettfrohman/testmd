---
id: "troubleshootemail"
---

# Investigate Email Issues

## Problem Description

PaymentIQ has been configured to trigger one or more emails either to the merchant or the customer, but the emails are not being received.

## Troubleshooting Steps

### Was the rule invoked?

All emails in PaymentIQ require a rule to be triggered. So the first step of troubleshooting should be to check the transaction you think should have triggered for example one of the notification or one of the block rules. (Please note that alert rules will not be listed in the Transaction, so for them you will need to check using the "Match transactions against rule" method listed below).

In the Transaction View in PaymentIQ there is a column **Rules** which lists the rules that were used in the transaction. 

For example here a notification rule was used:

```
1979_NO_01_01, 1000_UP_01_01, 1000_KY_05_01, 1979_PM_01_01, 1979_RO_01_02
```

You can also on each rule section in PaymentIQ press the small cogwheel and click "Match transaction against rules" to check which rules a transaction triggered.

![](/img/troubleshooting/nopaymentmethods.png)

If all cases if your transaction has not triggered a rule with an email action the email will not be sent. Please make sure to check the rule sections to make sure you have constructed the rules correctly.

Please note that sometimes rule construction can be tricky. For example if you are construction a velocity rule with condition "Tx state" set to "Successful" thinking it will only do the velocity check on successful transactions. But as the ongoing transaction checking the rule is not yet successful (since the rules are evaluated before transactions are successful) it may not trigger on the transaction.

![](/img/troubleshooting/statesuccess.png)

In an case the first problem to solve for emails not going out will always be to make sure the rule was triggered.

### Does the template match the rule?

In the rule that triggers the email send out you should specify an "Email template name".

![](/img/troubleshooting/emailtemplatename.png)

And in Admin > Templates > Email Templates you configure your email templates for the send out.

![](/img/troubleshooting/emailtemplatename2.png)

A common mistake is to not match the name from the rule with the name for the email template. They need to match exactly for the email to go out. 

### Is there a template for right locale and channel.

In addition to the name matching, when you configure the email templates you have the option to specify Locale and Channel. As you can imagine if either of these are specified for the template they will need to match with the transaction or there will not be any email to send.

### Are you using allowed template variables?

PaymentIQ allows you to include several different variables in your emails. They are listed [here](/docs/configuration_and_administration/system_configuration/emailparameters).

If you are including parameters that are not listed or if you have misspelled one of the parameters you have included it might cause the email not to go out. If you are doing tests we therefore recommend that you omit parameters in your test emails until you have verified all other settings are working as they should as a way to pinpoint any issues.

### Has email send outs been configured correctly?

If you are sending emails you need to have set up an EmailIntegrationConfig with the account information for PaymentIQ to use:

```xml
<com.devcode.paymentiq.integration.message.email.EmailIntegrationConfig>
  <enabled>true</enabled>
  <emailProviders>
    <entry>
      <string>mailgun</string>
      <com.devcode.paymentiq.service.provider.ProviderAccountConfig>
        <service>smtpProvider</service>
        <port>465</port>
        <serviceEndpoint>smtp.mailgun.org</serviceEndpoint>
        <username>yourusername@yourdomain.com</username>
        <password></password>
      </com.devcode.paymentiq.service.provider.ProviderAccountConfig>
    </entry>
  </emailProviders>
</com.devcode.paymentiq.integration.message.email.EmailIntegrationConfig>
```

And an entry in MerchantConfig

```xml
<userEmailCommunicationConfig>
  <enabled>true</enabled>
  <providerId>mailgun</providerId>
  <fromEmail>no-reply@paymentiq.io</fromEmail>
</userEmailCommunicationConfig>
```

The providerId in MerchantConfig points to the account set up in the EmailIntegrationConfig (<string>mailgun</string>).

If it does not point to an existing account in the config no email will go out.

In addition to this, your username, password, port and serviceEndpoint etc will all need to be configured correctly. PaymentIQ can not assist with this as it is Merchant specific information and there are a lot of email account specific issues that you will need to troubleshoot with your email team from the merchant end.

### If you are using GMail, have you allowed to use less secure apps?

For merchants that are using GMail for their email notifications, you will need to change a setting to allow for PaymentIQ to use the account.

To enable this, first make sure you are logged in to GMail, then go to: [https://myaccount.google.com/lesssecureapps](https://myaccount.google.com/lesssecureapps) and set **Allow less secure apps** to **ON**

### Contacting PaymentIQ Technical Support or Onboarding Support

If you have checked the above listed suggestions to resolve the issue but still can not locate the problem, please reach out to the Onboarding Team if you are currently Onboarding or the Technical Support Team if you are live.

It is helpful for us when troubleshooting to know the MID and transaction you are having issues with and any other related information you have found in your troubleshooting.