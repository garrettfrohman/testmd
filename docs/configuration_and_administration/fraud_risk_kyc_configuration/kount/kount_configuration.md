---
id: "kount_configuration"
---

# Kount Confirguration

## Configuration by the Merchant

There are some setup steps that need to be done on the Merchant Site to activate Kount.

Information about this can be found in the Technical Specifications Guide by Kount.

The merchant also needs to send the Kount session-id to PaymentIQ which is then picked up via the risReqTemplate as per the configuration file.

`SESS=${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.kountSessionId}`

Here the Kount Session ID is retrieved by PaymentIQ from the Verify User answer. This session-id is then used to link what is happening on the Merchant site with the call from PaymentIQ to Kount.

## Configuration in PaymentIQ

Please contact our technical support team for assistance with this configuration.

### Example Configuration file

```xml

<com.devcode.paymentiq.integration.kount.KountConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <siteId>DEFAULT</siteId>
        <merchantId>??????</merchantId>
        <apiKey>????????????</apiKey>
      </account>
    </entry>
  </accounts>

  <risReqTemplate><![CDATA[
SESS=${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.kountSessionId}
VERS=0695
MODE=Q
SITE=${accountConfig.siteId}
MERC=${accountConfig.merchantId}
ORDR=${ptx.merchantTxId}
UNIQ=${ptx.merchantUserId}
IPAD=${ptx.ipAddr}
EMAL=${ptx.merchantUser.email}                    
NAME=${ptx.merchantUser.name}
AUTH=A
MACK=Y
${if last4}
PENC=MASK
LAST4=${last4}
${end}
PTOK=${paymentToken}
PTYP=${paymentType}
CVVR=X
AVSZ=X
AVST=X
SPREMISE=
SSTREET=                    
S2EM=${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.fraud_confirmation_email}                    
S2ST=
S2CI=
S2PC=
S2CC=${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.fraud_customer_country_code}
S2PN=${ptx.merchantUser.mobile}
S2A1=
S2A2=
S2NM=                    
BPREMISE=
BSTREET=
B2CI=
B2CC=
B2ST=
B2PN=
B2PC=
B2A1=
B2A2=
CASH=${ptx.txAmount.amountInFractionUnit}
TOTL=${ptx.txAmount.amountInFractionUnit}
CURR=${ptx.txAmount.currencyCode}
PROD_PRICE[0]=${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.fraud_numeric_provider_price_in_euro_cents}
PROD_QUANT[0]=1
PROD_ITEM[0]=${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.fraud_numeric_booking_id}
PROD_TYPE[0]=${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.fraud_mode}
PROD_DESC[0]=
]]></risReqTemplate>

  <testMode>true</testMode>  
</com.devcode.paymentiq.integration.kount.KountConfig>

```

### Attributes

| Attribute  | Description                    |
|------------|--------------------------------|
| siteId     | Should be set to default.      |
| merchantId | Kount-issued Merchant ID (MID) |
| apiKey     | SDK_Config_Key                 |



Any extra Kount response param can be included in the integration API by adding following config in MerchantConfig

```xml

<extraAttributes>
  <entry>
    <string>fraudScore</string>
    <string>${ptx.latestTxCmdMap.KountRisTxRes.param.SCOR}</string>
  </entry>
</extraAttributes>

```