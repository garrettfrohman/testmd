---
id: "troubleshootconfigupdate"
---

# Resolve Config-file Update Issues

## Problem Description

When you save an update to a configuration file in PaymentIQ you are met with an error message

![](/img/troubleshooting/configerror.png)

## Troubleshooting Steps

### Is the XML formatted correctly?

When you press the save button PaymentIQ will check that the structure of the XML is correct. So if for example you try and save `<merchantId>PaymentIQ_test</merchantId>>` an error will be shown as you have added an extra `>` at the end of the line.

### Are there any duplicate entries?

Sometimes when you try and add a new entry you may miss that it has already been added further down in the config file. In the below example there is a duplicate entry which will not allow for it to save:

```xml
  <com.devcode.paymentiq.integration.muchbetter.MuchBetterConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>MB</string>
      <account>
        <brandId>??</brandId>
        <supportedCurrencies>USD|EUR|GBP</supportedCurrencies>
        <apiKey>??</apiKey>
        <brandId>??</brandId>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <liveServiceEndPoint>https://w.api.muchbetter.com/merchant</liveServiceEndPoint>
  <defaultDescriptor>???</defaultDescriptor>
  <redirectToWaitingPage>true</redirectToWaitingPage>
</com.devcode.paymentiq.integration.muchbetter.MuchBetterConfig>
```

### Are the entries in the right place?

Some entries are only allowed on the "root" level of the configuration file and some are only allowed in the account configuration level. If you try and add it in the incorrect place you will get an error "Unknown configuration field" next to the save button.

![](/img/troubleshooting/configerror.png)

### Have special characters been bracketed with CDATA?

As mentioned previously the XML in the configuration file needs to be correctly formatted. However sometimes credentials from providers will contain characters that can not be used in XML. For example PaymentIQ will not allow for this password to be saved due to the XML specific characters. 

```<password>[n3ZNCT>^9#5dT:V</password>```

To work around this you need to indicate in the XML that those characters are part of the data and not the document structure. This is done using CDATA.

```<![CDATA[your characters]]>```

So for the example above you would enter:

```<password><![CDATA[[n3ZNCT>^9#5dT:V]]></password>```

### Contacting PaymentIQ Technical Support or Onboarding Support

If you have checked the above listed suggestions to resolve the issue but still can not find it, please reach out to the Onboarding Team if you are currently Onboarding or the Technical Support Team if you are live.

It is helpful for us when troubleshooting to know the MID you are having issues with and any other related information you have found in your troubleshooting.