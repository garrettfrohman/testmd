---
id: "devcode_identity_configuration"
---

# Devcode Identity Configuration

For DevCode Identity setup, you need to request an account (username and password) from DevCode Identity. These will be configured in your DiDKycConfig.

### Example KYC Routing Rule

![](/img/fraudrisk/devcodeidentity01.png)

### Example KYC Block Rule

![](/img/fraudrisk/devcodeidentity02.png)

### Example Configuration

```xml
<com.devcode.paymentiq.integration.didkyc.DiDKycConfig>
<enabled>true</enabled>

 <didClients>
    <didClient>
      <clientId>bambora-demo</clientId>
      <clientSecret>???</clientSecret>
      <piqClientId>???</piqClientId>
    </didClient>
  </didClients>

  <accounts>
  <entry>
    <string>default</string>
      <kycAccount>
        <username>??</username>
        <password>??</password>
        <scope>profile,pep,sanction</scope> <!-- openid value should be used for some providers such as Sum&Sub, FinTec, and EutellerID.-->
        <piqClientId>???</piqClientId> <!-- optional and shall be used for some providers such as BankId, Sum&Sub, FinTec and EutellerID.-->
        <container>window</container> <!-- optional and can be used for some providers such as BankId and Sum&Sub. Possible values are iframe or window-->
        <display>popup</display> <!--Either page (default), popup or inline-popup. popup and inline-popup will adapt the login UI for iframe/popup. It is recommended to use popup for BankId-->
        <extraReqParam><!--extra params to be submitted to the DiD-->
          <entry>
            <string>key</string>
            <string>value</string>
          </entry>
        </extraReqParam>
      </kycAccount>
    </entry>
</accounts>
<idStatusMapping>7 TO 10->ERROR, 0 TO 6->ERROR, LESS 0->ERROR, GREATER 10->ERROR</idStatusMapping>
<ageStatusMapping>0 TO 17->UNDER_AGE, LESS 1->NOT_VERIFIED, GREATER 18->VERIFIED</ageStatusMapping>
<overAllStatusMapping>EQUAL -5->UNDER_AGE, 0 TO 19->NOT_VERIFIED , 20 TO 25->VERIFIED_AGE_ONLY, GREATER 29->VERIFIED_AGE_AND_ID, LESS -5->ERROR</overAllStatusMapping>
<resultTemplate>did-kyc</resultTemplate>
</com.devcode.paymentiq.integration.didkyc.DiDKycConfig>
```

Some tags can be configured at the account level such as: idStatusMapping, overAllStatusMapping, and overAllStatusMapping.

The tags **didClients** are used for BankId and Sum&Sub. **clientId** and **clientSecret** are provided by DiD. The tag **piqClientId** should have a UUID and should be mapped to the right account config by setting the same value for **piqClientId**.

### Sum&Sub specific details

To activate address verification at DiD's side, the merchant should add match to the scope as follows: `<scope>profile,match</scope>`.

To force a photo ID verification, the merchant needs to add the following entry `sumsub-flow` in the account configuration. Also, to simulate receiving a callback notificaiton regarding Sum&Sub verificaiton of uploaded document, `sumsub-test-review` can be configured with either `green` or `red` values.

```xml
<extraReqParam>
  <entry>
    <string>sumsub-flow</string>
    <string>Bambora_Photo_ID</string>
  </entry>
  <entry>
    <string>sumsub-test-review</string>
    <string>green</string>
  </entry>
</extraReqParam>
```

### FinTec specific details

To force a specific scenario of verification, the merchant needs to add the following entry in the account configuration:

```xml
<extraReqParam>
  <entry>
    <string>fintec-scenario</string> 
    <string>gambling</string> <!--fintec-scenario can have either of gambling or gambling-extended value-->
  </entry>
</extraReqParam>
```

### Giropay specific details

To force a specific scenario of verification, the merchant needs to add the following entry in the account configuration:

```xml
<extraReqParam>
  <entry>
    <string>giropay-scenario</string> 
    <string>age-account</string> <!--giropay-scenario can have either of age-account or age value-->
  </entry>
</extraReqParam>
```

