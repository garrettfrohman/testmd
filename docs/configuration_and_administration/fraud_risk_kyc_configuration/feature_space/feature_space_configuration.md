---
id: "feature_space_configuration"
---

# Feature Space Configuration

## Back Office configuration

The following sections present detailed information about KYC module functionalities.

### Fraud provider

Using the fraud provider tab, the user will be able to route the transactions to specific Fraud providers. Please note that routing the transaction to specific provider will not affect the transaction unless you have configured the Fraud Provider Block rules (described in the following section).

![](/img/fraudrisk/featurespace01.png)

![](/img/fraudrisk/featurespace02.png)

### Fraud provider block

Specifying Fraud Provider Block rules will allow you control the received response from the Fraud Provider (as you should have had configure them earlier as in previous section). You can access it as in following screenshot.

![](/img/fraudrisk/featurespace03.png)

The following subsections describes how you can configure your rules.

#### Approval

In case of getting an approval response, the decision will be configured as a condition as following:

![](/img/fraudrisk/featurespace04.png)

#### Rejection

In case of rejection, the decision will be configured as a condition as following:

![](/img/fraudrisk/featurespace05.png)

#### Recommended 3DS routing

In case of having a recommendation from FeatureSpace side to do a 3DS transaction, the decision will be configured as a condition as following. 

![](/img/fraudrisk/featurespace06.png)

Please note that you can update the transaction details by adding more information (Actions > info) and the same thing for the PSP status code.

## FeatureSpace Integration Configuration

To use FeatureSpace a configuration file must be set up.

### Example configuration file:

```xml
<com.devcode.paymentiq.integration.featurespace.FeatureSpaceConfig>
  <enabled>true</enabled>
   <jsonDecisionResponsePath>$.approveDeposit</jsonDecisionResponsePath>
   <jsonScorePath>$.score</jsonScorePath>
  <accounts>
    <entry>
      <string>FeatureSpaceFraudAccountCC</string>
      <account>
        <serviceEndpoint>??</serviceEndpoint>
        <templateName>FeatureSpaceCreditCardTemplate</templateName>
        <version>1</version>
      </account>
    </entry>
    <entry>
      <string>FeatureSpaceFraudAccount</string>
      <account>
        <serviceEndpoint>??</serviceEndpoint>
        <templateName>FeatureSpacePaymentTemplate</templateName>
        <version>1</version>
      </account>
    </entry>    
  </accounts>
</com.devcode.paymentiq.integration.featurespace.FeatureSpaceConfig>

```

Also, you should request from the FeatureSpace support team to prepare your own template details as in `<templateName>` since the template is saved at the master merchant side. The template will specify what kind of data will be submitted to FeatureSpace side.

### Example template:

![](/img/fraudrisk/featurespace07.png)

```json

{
 "accountId": "${ptx.merchantUserId}",
 "accountIsVerified": \"${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.AccountIsVerified}\",
  "accumulatedDeposit": 
  { 
      "value": ${if ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.BalTurnover}${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.BalTurnover}${else}0${end},
      "currency": "${if ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.Currency}${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.Currency}${else}${ptx.txAmount.currencyCode}${end}",
      "baseCurrency": "${ptx.amountBase.currencyCode}"
  },
 "amount": { "value": ${ptx.amount.amount}, "currency": "${ptx.txAmount.currencyCode}", "baseValue": ${ptx.amountBase.amount}, "baseCurrency": "${ptx.amountBase.currencyCode}" },
 "balance": { "value": ${ptx.merchantUserBal.amount}, "currency": "${ptx.merchantUserBal.currencyCode}", "baseValue": ${userBalanceBase.amount}, "baseCurrency": "${userBalanceBase.currencyCode}"},
 "brand": \"${if ptx.merchantId=100004001}garbo${else}mrgreen${end}\",
 "channel": "${ptx.attributes.mrg_client}",
 "eventId": "${ptx.id}",
 "eventTime": "${ptx.lastUpdated;date(yyyy-MM-dd'T'HH:mm:ssZ)}",
 "eventType": ${if ptx.method is 'Deposit' }"depositRequest"${else}${ptx.method}Request${end},
 "fee": { "value": ${ptx.fee.amount}, "currency": "${ptx.fee.currencyCode}", "baseValue": ${ptx.feeBase.amount}, "baseCurrency": "${ptx.feeBase.currencyCode}"},
 "idCheckStatus": "${ptx.merchantUser.kycStatus}",
 "ipAddress": "${ptx.ipAddr}",
 "ipCountry": "${ptx.ipCountry}",
 "market": ${if ptx.merchantUserCat='MrGreen'}"INT"${else}"${ptx.merchantUserCat;regexp(^MrGreen|Garbo)}"${end},
 "methodDetails": {
  "methodProvider": ${if ptx.pspService}"${ptx.pspService}"${else}"${ptx.psp}"${end}, 
  "methodType": "${ptx.txType.providerType}", 
  "methodId": "${ptx.userPspAccountDetails.accountUuid}"
  },
 ${if ptx.latestTxCmdMap.CallcreditVerifyUserTxRes.pepAndSanctionWarning}
 "pepsAndSanctions" : "${ptx.latestTxCmdMap.CallcreditVerifyUserTxRes.pepAndSanctionWarning}",
 ${end}
 "quickDeposit": ${if ptx.attributes.type is 'standard' } true ${else} false ${end},
 "schemaVersion": ${accountConfig.version},
 "transactionId": "${ptx.id}",
 "userCountry" : "${ptx.merchantUser.countryCode.twoAlphaCode}"
}
```