--- 
id: "interswitch" 
title: "Interswitch"
hide_title: "true"
--- 

![](/img/providers/logos/interswitch.png)

# Interswitch

## About
Interswitch is an Africa-focused integrated digital payments and commerce company. 

| Provider Name                | Interswitch                                                            |
|------------------------------|------------------------------------------------------------------------|
| Link                         | [https://www.interswitchgroup.com/](https://www.interswitchgroup.com/) |
| Classification               | Wallet                                                                 |
| Regions                      | `Nigeria`                                                              |
| Currencies                   | `NGN`, `USD`                                                           |
| Methods/PaymentTxTypes       | `WebPayDeposit`                                                        |
| PaymentIQ Configuration File | `InterswitchConfig`                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.interswitch.InterswitchConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>

  <width>800</width>
  <height>850</height>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>???????</username>
        <password>???</password>
        <secretKey>??</secretKey>
        <supportedCurrencies>NGN|USD</supportedCurrencies>        
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <liveServiceEndPoint>https://webpay.interswitchng.com/collections/w/pay</liveServiceEndPoint>
  <statusCheckUrl>https://webpay.interswitchng.com/collections/api/v1/gettransaction.json</statusCheckUrl>
  <host>webpay.interswitchng.com</host>
</com.devcode.paymentiq.integration.interswitch.InterswitchConfig>
```
</details>

### Attributes

| Attribute | Description                |
|-----------|----------------------------|
| username  | product_id in Interswitch  |
| password  | pay_item_id in Interswitch |
| secretKey | MAC Key in Interswitch     |

## Example Routing Rule

![](/img/providers/routing/interswitch.png)

## Test Information

Please ask the Interswitch for test information.