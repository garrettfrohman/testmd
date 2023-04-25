--- 
id: "empeasywire"
title: "EMP EasyWire"
hide_title: "true"
---

![](/img/providers/logos/empeasywire.png)

# EMP EasyWire

## About
EasyWire is a Payment Solution Provided by EMP-CORP in order to provide as solution that is designed to allow clients make Bank payouts.

| Provider Name                | EMP EasyWire         |
|------------------------------|----------------------|
| Link                         | N/A                  |
| Classification               | Banking              |
| Currencies                   | `EUR`                |
| Methods/PaymentTxTypes       | `BankIBANWithdrawal` |
| PaymentIQ Configuration File | `EmpConfig`          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.emp.EmpConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <container>window</container>
    <accounts>
        <entry>
            <string>easywire</string>
            <account>
                <apiKey>???</apiKey>
                <signingCertificate>???</signingCertificate>
                <password>???</password>
                <supportedCurrencies>EUR</supportedCurrencies>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.emp.EmpConfig>
```
</details>

### Configuring PGP
1. Generate PGP key pair using https://pgptool.org/. Please, remember all filled in options, especially "passphrase".
   ![](/img/providers/routing/empeasywire-pgp.png)
2. Download Public and Private key.
3. Send Public key to EMP EasyWire and ask them to set it up.
4. Open Private key in Text Editor and copy whole text. Paste it under "signingCertificate" on account config level. Please be sure to now insert any empty space before or after inserted value. See example.
5. Add passphrase for your Private key under password field.
```xml
<signingCertificate>-----BEGIN PGP PRIVATE KEY BLOCK-----

    xcMGBGP6W0oBCADqG479TraEPS88IwkVXj7Xb+8bDRT3Wc4PF4VPLD2URP7FBxrn
    nZ8Q1zhaq7LyDio7Y6DnDkUBkOWM/UoAXTloCFfNA/3DvlFaWOpT6owC6ERAijIj
    QxhQvIV0WeYO0nVtXgJxFIQ5kKjOUx6nAcKH2MFibR2dtGW2/Cwbdo92bbqBQagN
    5qSGfJxvngWIV4Zc0/4bFNKP8w9P/Zc1C3oEJ44GELe8Lzbyxf0qBcdEsGiZ5adO
    EI2VUD8swBAuoSt6enFqFm3vHrt3m9Qw9s0yibQouTn8o59lTHsF4b1LzrPoNF+D
    q22BGAuNp5qygBJILJmKUXPgG7pExid/Es8BABEBAAH+CQMIL/fOakmWjnVg3bZE
    vG8Gofrstjd2DQ6XIF3whENdRz7eIqdLfoae1v9DriIVHdkNBkRrX1JVY7RpAB+r
    dMyMxs/JTLrslwEZ+
    -----END PGP PRIVATE KEY BLOCK-----</signingCertificate>
<password>123</password>
```
6. Add EASYWIRE service to MerchantConfig under BANKIBAN section. Service EASYWIRE will use only bankIban field (no bic, beneficiaryName needed).
```xml
    <entry>
      <string>BANKIBAN</string>
      <string>EASYWIRE</string>
    </entry>
```
7. Choose payment method as BANKIBAN-EASYWIRE.
   ![](/img/providers/routing/empeasywire1.png)

| Attribute                  | Description                                                                             |
|----------------------------|-----------------------------------------------------------------------------------------|
| account.password           | Corresponds to the PGP private key's passphrase. See instruction below how to generate. |
| account.signingCertificate | Corresponds to the PGP private key. See instruction below how to generate.              |
| account.apiKey             | Corresponds to APIKEY provided by EasyWire.                                             |

## Example Routing Rule
![](/img/providers/routing/empeasywire.png)

## Test Information

For testing Withdrawal method please use any valid IBAN e.g. DE12500105170648489890.
To see your transactions in Emp EasyWire back office, please, use this page [https://easywire.empcorp.com/login](https://easywire.empcorp.com/login).
Press "Forgot Password?" and enter your email address. You will receive email with login anf password.


