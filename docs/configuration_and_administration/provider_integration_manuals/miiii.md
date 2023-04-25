--- 
id: "miiii" 
title: "Miiii"
hide_title: "true"
---
 
![](/img/providers/logos/miiii.png)

# Miiii

## About
Wallet platform provides credit card and wallet payment solutions.

| Provider Name                | Miiii                                            |
|------------------------------|--------------------------------------------------|
| Link                         | [https://www.miiii.app/](https://www.miiii.app/) |
| Classification               | Wallet                                           |
| Regions                      | `Argentina`                                      |
| Currencies                   | `ARS`                                            |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                             |
| PaymentIQ Configuration File | `MiiiiConfig`                                    |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.miiii.MiiiiConfig>
    <enabled>true</enabled>
    <validCallbackIpAddresses>3.130.158.171</validCallbackIpAddresses> <!--test server ip-->
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <accessToken>??</accessToken>
                <supportedCurrencies>ARS</supportedCurrencies>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
    <container>window</container>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.miiii.MiiiiConfig>
```

</details>

### Attributes

| Attribute                | Description                      |
|--------------------------|----------------------------------|
| accessToken              | Merchant token provided by Miiii |
| validCallbackIpAddresses | Miiii server IP address          |


## Example Routing Rule

![](/img/providers/routing/miiii.png)

## Test Information

Información de los usuarios

| Name   | Last name      | DNI      | username  | password      | permissions                     |
|--------|----------------|----------|-----------|---------------|---------------------------------|
| Andrés | Nicolás Torres | 32934122 | atorresan | Atorresan_122 | Generador,Aprobador,Confirmador |


### Successful transactions

| Type          | Card             | CVC  | Expiry  |
|---------------|------------------|------|---------|
| MasterCard TC | 5323629993121008 | 123  | 12.2023 |
| VISA TC       | 4507990000000010 | 123  | 12.2023 |
| AMEX TC       | 376411234531007  | 1234 | 12.2023 |
| VISA TD       | 4001020000000017 | 123  | 12.2023 |


### Rejected transactions

| Type          | Card                | CVC  | Expiry  | Outcome               |
|---------------|---------------------|------|---------|-----------------------|
| MasterCard TC | 5323622000000000    | 123  | 12.2023 | Card limit exceeded   |
| MasterCard TC | 5323622220000004    | 123  | 12.2023 | Expired card          |
| MasterCard TC | 5010150000000000010 | 123  | 12.2023 | Invalid card          |
| MasterCard TC | 5323622200000008    | 123  | 12.2023 | Invalid card format.  |
| MasterCard TC | 5323620000000004    | 123  | 12.2023 | Invalid security code |
| VISA TC       | 4507930000000016    | 123  | 12.2023 | Card limit exceeded   |
| VISA TC       | 4507960000000013    | 123  | 12.2023 | Expired card          |
| VISA TC       | 4507910000000018    | 123  | 12.2023 | Invalid card          |
| VISA TC       | 4507950000000014    | 123  | 12.2023 | Invalid card format.  |
| VISA TC       | 4507920000000017    | 123  | 12.2023 | Invalid security code |
| AMEX TC       | 376811234531008     | 1234 | 12.2023 | Expired card          |
| AMEX TC       | 375645646328764     | 1234 | 12.2023 | Invalid card          |
| AMEX TC       | 376911234531006     | 1234 | 12.2023 | Invalid card format.  |
| VISA TD       | 4001020000000025    | 123  | 12.2023 | Invalid card          |

### Miiii wallet account credentials

| Username | Password   |
|----------|------------|
| homostg  | Miiii_2021 |

### Información General
| CVU                    | Token                                  | URL                                        |
|------------------------|----------------------------------------|--------------------------------------------|
| 0000045100000000022039 | MIIII-48a7e5fcc2b14152a704f2d981348728 | https://backoffice.staging.miiii.app/login |