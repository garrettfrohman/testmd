---
id: "multiple_accounts"
---

# Set Up Multiple Accounts For One Provider

For each payment provider you can only have one configuration file per MID. That is the file that contains all the settings relating to that payment provider for that MID. A common use case is for a merchant to have multiple accounts with the same provider. This can be set up in the configuration file by adding additional account sections.

A typical provider configuration file may look something like this:

```xml
<com.devcode.paymentiq.integration.ProviderNameConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>AccountName</string>
      <account>
        <username>??</username>
        <password>??</password>
        <useTokenId>true</useTokenId>
        <authType>FINAL_AUTH</authType>
      </account>
    </entry>    
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
</com.devcode.paymentiq.integration.ProviderNameConfig>
```

It contains various settings, and the ones specifically relating to accounts are located between `<accounts>` and `</accounts>`

So in this example there is one account called "AccountName" that has settings specified for "username", "password", "useTokenId" and "authType". There are other settings such as "testMode" and "container" but they are not located between the brackets and so will not be specific for the accounts.


To add another account with the provider you simply copy the existing account setting to duplicate it, then add in the new credentials/settings you want and save it. So continuing from the previous example you create:

```xml
<com.devcode.paymentiq.integration.ProviderNameConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>AccountName</string>
      <account>
        <username>??</username>
        <password>??</password>
        <useTokenId>true</useTokenId>
        <authType>FINAL_AUTH</authType>
      </account>
    </entry>
    <entry>
      <string>AccountName2</string>
      <account>
        <username>??</username>
        <password>??</password>
        <useTokenId>true</useTokenId>
        <authType>FINAL_AUTH</authType>
      </account>
    </entry>   
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
</com.devcode.paymentiq.integration.ProviderNameConfig>
```

So here we have now created a new entry in the accounts section which gives the possibility to add more provider account credentials which can be used in the routing rules. There is no limit to how many accounts you can add on for a specific provider.