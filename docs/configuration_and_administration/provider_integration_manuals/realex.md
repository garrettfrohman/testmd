--- 
id: "realex" 
title: "Realex"
hide_title: "true"
---
 
![](/img/providers/logos/realex.png)

# Realex

## About
Realex is a creditcard processor with support for Deposits and Withdrawals.

| Provider Name                | Realex                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.realexpayments.com/](https://www.realexpayments.com/)              |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`                                 |
| PaymentIQ Configuration File | `RealexConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.realex.RealexConfig>
    <enabled>true</enabled>
    <mockResponse>false</mockResponse>
    <useViqProxy>true</useViqProxy>

    <liveMode>true</liveMode>
    <accounts>
        <entry>
            <string>N3DS</string>
            <account>
                <merchantId>??</merchantId>
                <accountID>?? 3ds gbp</accountID>
                <secretKey>??</secretKey>
                <deviceCategory>0</deviceCategory>
                <useTokenId>false</useTokenId>
                <use3Dsecure>true</use3Dsecure>
            </account>
        </entry>
        <entry>
            <string>3DS</string>
            <account>
                <merchantId>??</merchantId>
                <accountID>?? mobile non3ds gbp</accountID>
                <secretKey>??</secretKey>
                <deviceCategory>0</deviceCategory>
                <useTokenId>false</useTokenId>
                <use3Dsecure>false</use3Dsecure>
            </account>
        </entry>
        <entry>
            <string>CFT</string>
            <account>
                <merchantId>??</merchantId>
                <accountID>??</accountID>
                <secretKey>??</secretKey>
                <refundSecretKey>??</refundSecretKey>
                <deviceCategory>0</deviceCategory>
                <useTokenId>false</useTokenId>
                <use3Dsecure>false</use3Dsecure>
            </account>
        </entry>
        <entry>
            <string>OCT</string>
            <account>
                <merchantId>??</merchantId>
                <accountID>??</accountID>
                <secretKey>??</secretKey>
                <refundSecretKey>??</refundSecretKey>
                <deviceCategory>0</deviceCategory>
                <useTokenId>false</useTokenId>
                <use3Dsecure>false</use3Dsecure>
            </account>
        </entry>
    </accounts>
    <mpiMerchantName></mpiMerchantName>
    <mpiMerchantUrl></mpiMerchantUrl>
    <mpiDescribtion></mpiDescribtion>
    <paymentRequestUrl>https://epage.payandshop.com/epage-remote.cgi</paymentRequestUrl>
    <paymentPluginRequestUrl>https://epage.payandshop.com/epage-remote-plugins.cgi</paymentPluginRequestUrl>
    <paymentRequestUrl3d>https://epage.payandshop.com/epage-3dsecure.cgi</paymentRequestUrl3d>

    <process3DSForCardTypes>(VISA|ELECTRON|MASTERCARD|MAESTRO|SWITCH|ENTROPAY)</process3DSForCardTypes>

    <binMappings>
        <binMapping>
            <cardType>VISA</cardType>
            <typeString>VISA</typeString>
        </binMapping>
        <binMapping>
            <cardType>ELECTRON</cardType>
            <typeString>VISA</typeString>
        </binMapping>
        <binMapping>
            <cardType>ENTROPAY</cardType>
            <typeString>VISA</typeString>
        </binMapping>
        <binMapping>
            <cardType>MASTERCARD</cardType>
            <typeString>MC</typeString>
        </binMapping>
        <binMapping>
            <cardType>MAESTRO</cardType>
            <typeString>MC</typeString>
        </binMapping>
        <binMapping>
            <cardType>SWITCH</cardType>
            <typeString>SWITCH</typeString>
        </binMapping>
        <binMapping>
            <cardType>AMEX</cardType>
            <typeString>AMEX</typeString>
        </binMapping>
        <binMapping>
            <cardType>LASER</cardType>
            <typeString>LASER</typeString>
        </binMapping>
        <binMapping>
            <cardType>DINERS</cardType>
            <typeString>DINERS</typeString>
        </binMapping>
    </binMappings>

    <decisionTable>

        <!-- VE_REQ decisions below -->

        <!-- Unable to verify enrollment, no liability switch -->
        <realexDecisionEntry>
            <requestTypePattern>VE_REQ</requestTypePattern>
            <threeDSecureStatusPattern>U</threeDSecureStatusPattern>
            <threeDSecureAction>ABORT_TRANSACTION</threeDSecureAction>
        </realexDecisionEntry>
        <!-- Issuer problems, no liability switch -->
        <realexDecisionEntry>
            <requestTypePattern>VE_REQ</requestTypePattern>
            <realexRCPattern>220</realexRCPattern>
            <cardTypePattern>VISA|ELECTRON|ENTROPAY</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>7</defaultECI>
        </realexDecisionEntry>
        <realexDecisionEntry>
            <requestTypePattern>VE_REQ</requestTypePattern>
            <realexRCPattern>220</realexRCPattern>
            <cardTypePattern>MASTERCARD|MAESTRO|SWITCH</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>0</defaultECI>
        </realexDecisionEntry>

        <!-- Card enrolled, continue -->
        <realexDecisionEntry>
            <requestTypePattern>VE_REQ</requestTypePattern>
            <realexRCPattern>00</realexRCPattern>
            <threeDSecureAction>PROCEED_3D_SECURE</threeDSecureAction>
        </realexDecisionEntry>

        <!-- Card not enrolled, liability switch -->
        <realexDecisionEntry>
            <requestTypePattern>VE_REQ</requestTypePattern>
            <realexRCPattern>110</realexRCPattern>
            <cardTypePattern>VISA|ELECTRON|ENTROPAY</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>6</defaultECI>
        </realexDecisionEntry>
        <realexDecisionEntry>
            <requestTypePattern>VE_REQ</requestTypePattern>
            <realexRCPattern>110</realexRCPattern>
            <cardTypePattern>MASTERCARD|MAESTRO|SWITCH</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>1</defaultECI>
        </realexDecisionEntry>


        <!-- catch all for VE -->
        <realexDecisionEntry>
            <requestTypePattern>VE_REQ</requestTypePattern>
            <threeDSecureAction>ABORT_TRANSACTION</threeDSecureAction>
        </realexDecisionEntry>


        <!-- PA_REQ decisions below -->

        <!-- 3DS ok, liability switch -->
        <realexDecisionEntry>
            <requestTypePattern>PA_REQ</requestTypePattern>
            <realexRCPattern>00</realexRCPattern>
            <threeDSecureStatusPattern>Y</threeDSecureStatusPattern>
            <cardTypePattern>VISA|ELECTRON|ENTROPAY</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>5</defaultECI>
        </realexDecisionEntry>
        <realexDecisionEntry>
            <requestTypePattern>PA_REQ</requestTypePattern>
            <realexRCPattern>00</realexRCPattern>
            <threeDSecureStatusPattern>Y</threeDSecureStatusPattern>
            <cardTypePattern>MASTERCARD|MAESTRO|SWITCH</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>2</defaultECI>
        </realexDecisionEntry>

        <!-- Issuer unable to check, liability switch -->
        <realexDecisionEntry>
            <requestTypePattern>PA_REQ</requestTypePattern>
            <realexRCPattern>00</realexRCPattern>
            <threeDSecureStatusPattern>A</threeDSecureStatusPattern>
            <cardTypePattern>VISA|ELECTRON|ENTROPAY</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>6</defaultECI>
        </realexDecisionEntry>
        <realexDecisionEntry>
            <requestTypePattern>PA_REQ</requestTypePattern>
            <realexRCPattern>00</realexRCPattern>
            <threeDSecureStatusPattern>A</threeDSecureStatusPattern>
            <cardTypePattern>MASTERCARD|MAESTRO|SWITCH</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>1</defaultECI>
        </realexDecisionEntry>

        <!-- Issuer problems with check, no liability switch -->
        <realexDecisionEntry>
            <requestTypePattern>PA_REQ</requestTypePattern>
            <realexRCPattern>00</realexRCPattern>
            <threeDSecureStatusPattern>U</threeDSecureStatusPattern>
            <cardTypePattern>VISA|ELECTRON|ENTROPAY</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>7</defaultECI>
        </realexDecisionEntry>
        <realexDecisionEntry>
            <requestTypePattern>PA_REQ</requestTypePattern>
            <realexRCPattern>00</realexRCPattern>
            <threeDSecureStatusPattern>U</threeDSecureStatusPattern>
            <cardTypePattern>MASTERCARD|MAESTRO|SWITCH</cardTypePattern>
            <threeDSecureAction>PROCEED_WITH_NORMAL_DEPOSIT</threeDSecureAction>
            <defaultECI>0</defaultECI>
        </realexDecisionEntry>

        <!-- catch all for PA -->
        <realexDecisionEntry>
            <requestTypePattern>PA_REQ</requestTypePattern>
            <threeDSecureAction>ABORT_TRANSACTION</threeDSecureAction>
        </realexDecisionEntry>
    </decisionTable>
</com.devcode.paymentiq.integration.realex.RealexConfig>
```

</details>

### Attributes

| Attribute       | Description        |
|-----------------|--------------------|
| merchantId      | Provided by Realex |
| accountID       | Provided by Realex |
| secretKey       | Provided by Realex |
| refundSecretKey | Provided by Realex |

## Example Routing Rule
![](/img/providers/routing/realex.png)

## Test Information

### N3DS Testing Information (SUCCESSFUL)

| Card Brand | Account          | CVV |
|------------|------------------|-----|
| MASTERCARD | 5425230000004415 | Any |
| VISA       | 4263970000005262 | Any |


### N3DS Testing Information (DECLINED)

| Card Brand | Account          | CVV |
|------------|------------------|-----|
| MASTERCARD | 5114610000004778 | Any |
| VISA       | 4000120000001154 | Any |


### 3DS Testing Information (SUCCESSFUL)

| Card Brand | Account          | CVV |
|------------|------------------|-----|
| VISA       | 4012001037141112 | Any |


### 3DS Testing Information (DECLINED)

| Card Brand | Account          | CVV |
|------------|------------------|-----|
| VISA       | 4012001038443335 | Any |


For other test credit cards, please visit:

https://developer.realexpayments.com/#!/resources/test-card-numbers#test-card-numbers-3ds 