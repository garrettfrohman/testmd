--- 
id: "fonix" 
title: "Fonix"
hide_title: "true"
---
 
![](/img/providers/logos/fonix.png)

# Fonix

## About
Fonix is a mobile billing payment solution. You as a merchant need to add the logo into your cashier.
If the user is using Fonix to get charged for the first time or it has gone more than three months since the last time he used Fonix , the user will get Redirected to a page to enter a code sent to his/her Mobile number.

Fonix only support deposit. The only supported currency is GBP. 

| Provider Name                | Fonix                                            |
|------------------------------|--------------------------------------------------|
| Link                         | [https://www.fonix.com/](https://www.fonix.com/) |
| Classification               | Mobile Payment                                   |
| Regions                      | `United Kingdom`                                 |
| Currencies                   | `GBP`                                            |
| Methods/PaymentTxTypes       | `FonixDeposit`                                   |
| PaymentIQ Configuration File | `FonixConfig`                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.fonixcarrierbilling.FonixConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <width>400</width>
  <height>40</height>
  <container>iframe</container>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <apiKey>??</apiKey>
        <supportedCurrencies>GBP</supportedCurrencies>
        <merchantName>??</merchantName>
        <service>game</service>
        <merchantNumber>??</merchantNumber>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>Gaming payment</defaultDescriptor>
  <smsFallBack>true</smsFallBack>
  <noRetry>true</noRetry>
  <chargeSilent>false</chargeSilent>
  <timeToLive>90</timeToLive>
  <body>you have been charged ${ptx.txAmount} for your selected product of service</body>
  <sendSmsBody><![CDATA[To verify your mobile number and continue to \${accountConfig.service} for ${ptx.txAmount} from \${accountConfig.merchantName}
  enter \${ptx.latestTxCmdMap.FonixGeneratedCodeInput.verificationCode}. Help? \${accountConfig.merchantNumber} 
  ]]></sendSmsBody>
 <originator>Bambora</originator>
 <originatorType>alpha</originatorType>
<verificationHtml><![CDATA[
  <!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
    $("button").unbind().bind('click',function(event){
        event.preventDefault();
        
        $("#fonix-loader").show();
        $.post("${baseRedirectUrl}/api/fonix/codecheck/${ptx.txRefId}",
            {code : $("input").val()},
            function(data,status){
                $("#fonix-loader").hide();
                 if(data === "try-again"){
                 var txt = "The PIN you´ve entered is invalid, please try again.";
                 $("#errortxt").text(txt);
                 }
                  if (data === "successful"||data === "failure"){
                    window.location.href = "${baseRedirectUrl}/api/fonix/proceed/${ptx.txRefId}";
                 }
                 
            });
    });
});


</script>
   <style>
.button {
    background-color: #0B0B61;
    border: none;
    color: #D0D0D0;
    padding: 6px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 12px;
    margin: 3px 2px;
    cursor: pointer;
}
.loader {
    border: 8px solid #f3f3f3; /* Light grey */
    border-top: 8px solid #3498db; /* Blue */
    border-radius: 50%;
    width: 20px;
    height: 20px;
    animation: spin 2s linear infinite;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}
.hidden {
  display: none;
}

.text {
    background-color: #ffffff;
    border: solid;
    border-color: #D0D0D0;
    border-width: 1px;
    color: black;
    padding: 6px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 12px;
    margin: 3px 2px;
    cursor: pointer;
}
::placeholder {
    color: #D0D0D0;
    opacity: 1; /* Firefox */
    font-size: 16px;
}

</style>

</head>
<body bgcolor="#F5F5F5">
<br>
<div><img src ="https://fonix.com/pay_by_mobile/pay_by_mobile_logo_blue.png" alt="phonix" width="60"></div>

<font color = "#696969" size="2" ><b>please confirm your purchase</b></font><br>
<font id="p2" color = "#696969" size="1">we have sent a 4-digits PIN code to your device</font>
<div id="fonix-loader" class="loader hidden"></div><br>
<font id="errortxt" color ="#FF0000" size="2"></font>
<br><br>
<div style="background-color:white;color:white;vertical-align: bottom;padding:20px;border: solid;border-color:#D0D0D0;border-width: 1px;">
<input type = "text" class ="text"  placeholder="PIN-CODE" onfocus="this.value=''" name = "code">
<button class ="button" name = "submit1">ok</button>
</div>
</body>

</html>
  ]]></verificationHtml>
  <liveServiceEndPoint>https://sonar.fonix.io/v2/chargemobile</liveServiceEndPoint>
  <testServiceEndPoint>https://sonar.fonix.io/v2/chargemobile</testServiceEndPoint>
  <sendSmsUrl>https://sonar.fonix.io/v2/sendsms</sendSmsUrl>
</com.devcode.paymentiq.integration.fonixcarrierbilling.FonixConfig>

```
</details>

### Attributes


| Attribute         | Description                                                                                                                                                                                                                                                                                                                                                                          |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apiKey            | It is the API Key that you as a merchant has registered with Fonix. Required.                                                                                                                                                                                                                                                                                                        |
| defaultDescriptor | The bill descriptor of the charge is a mandatory field, although it does not appear on all operator phone bills (yet). The maximum allowed length is 30 characters.                                                                                                                                                                                                                  |
| sendSmsBody       | The body of the SMS which will include the code sent to the user to verify the payment.                                                                                                                                                                                                                                                                                              |
| merchantName      | The merchant name that will be sent in the sendSmsBody.                                                                                                                                                                                                                                                                                                                              |
| merchantNumber    | The merchant customer care Number that will be sent in the sendSmsBody.                                                                                                                                                                                                                                                                                                              |
| service           | The service name that the user will be charged for. It will be sent in the sendSmsBody.                                                                                                                                                                                                                                                                                              |
| smsFallBack       |                                                                                                                                                                                                                                                                                                                                                                                      |
| noRetry           | If `noRetry = true` in combination with `smsFallBack = true`, then PaymentIQ will only attempt to charge the user through a premium SMS message ONCE. <br/><br/>This is useful where you require a quick turn-around of your billing requests, but still want to use SMS fallback. Default is NORETRY=false, meaning we retry to bill the customer thorugh SMS for a period of time. |
| body              | The optional body text of a message accompanying the charge. If you don’t specify it and you requested CHARGESILENT=no, we will use the following:<br/><br/> Default BODY: “You have been charged £nn.nn for your selected product or service.”                                                                                                                                      |
| chargeSilent      | If chargeSilent is false , then the body will be visible to the user. Default is chargeSilent = true.                                                                                                                                                                                                                                                                                |
| timeToLive        | Expiry period of the Charge Mobile request in minutes. If this period expires before a bill attempt was made, then a ‘failed Charge Report’ will be returned to you. Minimum value: 10 minutes, Maximum value: 4320 minutes, Default value: 90 minutes.                                                                                                                              |
| verificationHtml  | Include the HTML template that it will be shown to the user to enter the code.                                                                                                                                                                                                                                                                                                       |

## Example Routing Rule
![](/img/providers/routing/fonix.png)
## Test Information

### Test accounts

- Currency: GBP
- User country: GBR
- Phone number: 447554893154
- Amount: 12, 14 GBP
- (E.g TEST_GBP as mock user)

