---
id: "gb_group_configuration"
---

# GB Group Configuration

For GBGroup, you need to request an account (username and password) as well as a profile ID. These details can be configured in your GbgConfig(below an example).

Like CallCredit, you will need to configure the score result mapping in your GbgConfig according to your profile.

### Example Configuration

```xml

<com.devcode.paymentiq.integration.gbg.GbgConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <defaultTitle>UNKNOWN</defaultTitle>
  <serviceEndpoint>https://pilot.id3global.com/ID3gWS/ID3global.svc/Soap11_Auth</serviceEndpoint>
  <soapAction>http://www.id3global.com/ID3gWS/2013/04/IGlobalAuthenticate/AuthenticateSP</soapAction>
  <username>??</username>
  <password>??</password>
  <company>??</company>
  <resultTemplate>gbg</resultTemplate>
  <ageStatusMapping>-999999 TO -1->UNDER_AGE, 0 TO 1010->NOT_VERIFIED, 1011 TO 999999->VERIFIED, LESS -999999->ERROR, GREATER 999999->ERROR</ageStatusMapping>
  <idStatusMapping>-999999 TO -1->UNDER_AGE, 0 TO 2021->NOT_VERIFIED, 2022 TO 999999->VERIFIED, LESS -999999->ERROR, GREATER 999999->ERROR</idStatusMapping>
  <overAllStatusMapping>-999999 TO -1->UNDER_AGE, 0 TO 1010->NOT_VERIFIED, 1011 TO 2021->VERIFIED_AGE_ONLY, 2022 TO 999999->VERIFIED_AGE_AND_ID , LESS -999999->ERROR, GREATER 999999->ERROR</overAllStatusMapping>
  <accounts>
        <entry>
            <string>??</string>
            <kycAccount>
              <profileId>??</profileId>
            </kycAccount>
        </entry>  
        <entry>
            <string>??</string>
            <kycAccount>
              <profileId>??</profileId>
            </kycAccount>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.gbg.GbgConfig>
```