---
id: "callcredit_configuration"
---

# CallCredit Configuration

For CallCredit, you need to request an account(username and password) as well as an application reference key. These details will be configured in your CallcreditConfig.

Also, according to your configuration of your own configured CallCredit account, you will need to configure the score result mapping in the CallcreditConfig file. For example, if you got the results as following:

![](/img/fraudrisk/callcreditconfig01.png)

The mapping results shall be configured in the respective tags of CallcreditConfig using `<ageStatusMapping>` and `<idStatusMapping>`. The configuration of these details is depicted in the following:

### Example Configuration

```xml
<com.devcode.paymentiq.integration.callcredit.CallcreditConfig>
  <enabled>true</enabled>
  <!--<useViqProxy>true</useViqProxy>-->
  <cardEnhanced>true</cardEnhanced>
  <defaultTitle>UNKNOWN</defaultTitle>
  <serviceEndpoint>https://ct.callcreditsecure.co.uk/callvalidateapi/incomingserver.php</serviceEndpoint>
  <username>??</username>
  <password>??</password>
  <application>??</application>
  <company>??</company>
  <resultTemplate>callcredit</resultTemplate>
  <ageStatusMapping>EQUAL -5->UNDER_AGE, 0 TO 34->NOT_VERIFIED, EQUAL 35->VERIFIED, LESS -5->ERROR, -4 TO -1 ->ERROR</ageStatusMapping>
  <idStatusMapping>EQUAL -5->UNDER_AGE, 0 TO 34->NOT_VERIFIED, EQUAL 35->VERIFIED, LESS -5->ERROR, -4 TO -1 ->ERROR</idStatusMapping>
  <overAllStatusMapping>EQUAL -5->UNDER_AGE, 0 TO 34->NOT_VERIFIED, EQUAL 35->VERIFIED, LESS -5->ERROR</overAllStatusMapping>
</com.devcode.paymentiq.integration.callcredit.CallcreditConfig>
```

Note: whenever you change your Callcredit score mapping, you will only need to update the `<idStatusMapping>` as well as the `<ageStatusMapping>`.