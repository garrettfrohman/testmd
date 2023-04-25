--- 
id: "neopay" 
title: "NeoPay"
hide_title: "true"
---
 
![](/img/providers/logos/neopay.png)

# NeoPay

## About
NeoPay is an aggregator that offers a number of alternative payment methods using their hosted payment page.

| Provider Name                | NeoPay                                     |
|------------------------------|--------------------------------------------|
| Link                         | [https://neopay.lt/](https://neopay.lt/)   |
| Classification               | Aggregator                                 |
| Regions                      | `International`                            |
| Currencies                   | `EUR`,`PLN`,`SEK`,`NOK`                    |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `BankIBANWithdrawal` |
| PaymentIQ Configuration File | `NeoPayConfig`                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.neopay.NeoPayConfig>
    <enabled>true</enabled>
    <projectId>??</projectId>
    <projectKey>??</projectKey>
    <bankMappings>
        <!--NeoPay LT BANKS -->
        <bankMapping><countryCode>LT</countryCode><bic>HABALT22</bic><bankCode>swedbank</bankCode><bankName>„Swedbank” AB LT</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>CBVILT2X</bic><bankCode>seb</bankCode><bankName>AB "SEB bankas" LT</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>INDULT2X</bic><bankCode>citadele</bankCode><bankName>Citadele</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>AGBLLT2X</bic><bankCode>luminor</bankCode><bankName>Luminor LT</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>REVOLT21</bic><bankCode>revolut</bankCode><bankName>Revolut LT</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>CBSBLT26</bic><bankCode>siauliubankas</bankCode><bankName>Šiaulių bankas</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>MDBALT22</bic><bankCode>medicinosbankas</bankCode><bankName>Medicinos bankas</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>UANFLT21</bic><bankCode>neofinance</bankCode><bankName>NEO Finance, AB</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>LCKULT22</bic><bankCode>lcku</bankCode><bankName>Lietuvos centrinė kredito unija</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>VRKULT21</bic><bankCode>ratounija</bankCode><bankName>RATO</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>JCKULT21</bic><bankCode>kreda</bankCode><bankName>Kreda</bankName></bankMapping>
        <bankMapping><countryCode>LT</countryCode><bic>EVIULT2V</bic><bankCode>paysera</bankCode><bankName>Paysera LT</bankName></bankMapping>

        <!--NeoPay LV BANKS -->
        <bankMapping><countryCode>LV</countryCode><bic>HABALV22</bic><bankCode>swedbank</bankCode><bankName>"Swedbank" AS LV</bankName></bankMapping>
        <bankMapping><countryCode>LV</countryCode><bic>UNLALV2X</bic><bankCode>seb</bankCode><bankName>AS "SEB banka" LV</bankName></bankMapping>
        <bankMapping><countryCode>LV</countryCode><bic>RIKOLV2X</bic><bankCode>luminor</bankCode><bankName>Luminor LV</bankName></bankMapping>
        <bankMapping><countryCode>LV</countryCode><bic>PARXLV22</bic><bankCode>citadele</bankCode><bankName>SC Citadele bank</bankName></bankMapping>
        <bankMapping><countryCode>LV</countryCode><bic>REVOLV21</bic><bankCode>revolut</bankCode><bankName>Revolut LV</bankName></bankMapping>
        <bankMapping><countryCode>LV</countryCode><bic>RTMBLV2X</bic><bankCode>rietumu</bankCode><bankName>Rietumu</bankName></bankMapping>
        <bankMapping><countryCode>LV</countryCode><bic>PAYELV21</bic><bankCode>paysera</bankCode><bankName>Paysera LV</bankName></bankMapping>


        <!--NeoPay EE BANKS -->
        <bankMapping><countryCode>EE</countryCode><bic>HABAEE2X</bic><bankCode>swedbank</bankCode><bankName>"Swedbank" AS EE</bankName></bankMapping>
        <bankMapping><countryCode>EE</countryCode><bic>EEUHEE2X</bic><bankCode>seb</bankCode><bankName>AS "SEB Pank" EE</bankName></bankMapping>
        <bankMapping><countryCode>EE</countryCode><bic>RIKOEE22</bic><bankCode>luminor</bankCode><bankName>Luminor EE</bankName></bankMapping>
        <bankMapping><countryCode>EE</countryCode><bic>PARXEE22</bic><bankCode>citadele</bankCode><bankName>AS Citadele banka Eesti filiaal</bankName></bankMapping>
        <bankMapping><countryCode>EE</countryCode><bic>REVOEE21</bic><bankCode>revolut</bankCode><bankName>Revolut EE</bankName></bankMapping>
        <bankMapping><countryCode>EE</countryCode><bic>LHVBEE22</bic><bankCode>lhv</bankCode><bankName>LHV</bankName></bankMapping>
        <bankMapping><countryCode>EE</countryCode><bic>EKRDEE22</bic><bankCode>cooppank</bankCode><bankName>Coop Pank AS</bankName></bankMapping>
        <bankMapping><countryCode>EE</countryCode><bic>PAYEEE21</bic><bankCode>paysera</bankCode><bankName>Paysera EE</bankName></bankMapping>

        <!--NeoPay NL BANKS -->
        <bankMapping><countryCode>NL</countryCode><bic>ABNANL2A</bic><bankCode>abnamro</bankCode><bankName>ABN Amro</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>RABONL2U</bic><bankCode>rabobank</bankCode><bankName>Rabobank</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>FVLBNL22</bic><bankCode>vanlanschot</bankCode><bankName>F. VAN LANSCHOT</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>INGBNL2S</bic><bankCode>ing</bankCode><bankName>ING</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>ASNBNL21</bic><bankCode>devolksbank</bankCode><bankName>ASN</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>KNABNL2H</bic><bankCode>knab</bankCode><bankName>KNAB</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>RBRBNL21</bic><bankCode>devolksbank</bankCode><bankName>Regiobank</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>SNSBNL2A</bic><bankCode>devolksbank</bankCode><bankName>SNS Bank</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>BUNQNL2A</bic><bankCode>bunq</bankCode><bankName>BUNQNL2A</bankName></bankMapping>
        <bankMapping><countryCode>NL</countryCode><bic>TRIONL2U</bic><bankCode>triodos</bankCode><bankName>Triodos</bankName></bankMapping>

        <!--NeoPay PL BANKS -->
        <bankMapping><countryCode>PL</countryCode><bic>BPKOPLPW</bic><bankCode>pkobp</bankCode><bankName>PKO Bank Polski</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>INGBPLPW</bic><bankCode>ingpl</bankCode><bankName>ING Bank Polska</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>BREXPLPW</bic><bankCode>mbank</bankCode><bankName>mBank</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>PPABPLPK</bic><bankCode>bnpparibas</bankCode><bankName>BNP PARIBAS</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>WBKPPLPP</bic><bankCode>santander</bankCode><bankName>Santander Bank Polska</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>BIGBPLPW</bic><bankCode>millennium</bankCode><bankName>Bank Millennium</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>IBNKPAPA</bic><bankCode>inteligo</bankCode><bankName>Inteligo Bank</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>NESBPLPW</bic><bankCode>nestbank</bankCode><bankName>Nest Bank</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>IEEAPLPA</bic><bankCode>ideabank</bankCode><bankName>Idea Bank</bankName></bankMapping>
        <bankMapping><countryCode>PL</countryCode><bic>LBPPLPW</bic><bankCode>aliorbank</bankCode><bankName>Alior Bank</bankName></bankMapping>

        <!--NeoPay SE BANKS -->
        <bankMapping><countryCode>SE</countryCode><bic>SWEDSESS</bic><bankCode>swedbankse</bankCode><bankName>Swedbank AS SE</bankName></bankMapping>
        <bankMapping><countryCode>SE</countryCode><bic>ESSESESS</bic><bankCode>sebse</bankCode><bankName>SEB SE</bankName></bankMapping>
        <bankMapping><countryCode>SE</countryCode><bic>NDEASESSPGI</bic><bankCode>klarna</bankCode><bankName>Nordea</bankName></bankMapping>
        <bankMapping><countryCode>SE</countryCode><bic>DABASES</bic><bankCode>klarna</bankCode><bankName>Danske Bank</bankName></bankMapping>
        <bankMapping><countryCode>SE</countryCode><bic>AABAFI22XXX</bic><bankCode>klarna</bankCode><bankName>Ålandsbanken</bankName></bankMapping>
        <bankMapping><countryCode>SE</countryCode><bic>HANDSESSMLM</bic><bankCode>klarna</bankCode><bankName>HANDELSBANKEN</bankName></bankMapping>
        <bankMapping><countryCode>SE</countryCode><bic>DNBASES</bic><bankCode>klarna</bankCode><bankName>DNB</bankName></bankMapping>

        <!--NeoPay FI BANKS -->
        <bankMapping><countryCode>FI</countryCode><bic>OKOYFIHH</bic><bankCode>klarna</bankCode><bankName>OP Financial Group</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>DABAFIHH</bic><bankCode>klarna</bankCode><bankName>Danske Bank</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>NDEAFIHH</bic><bankCode>klarna</bankCode><bankName>Nordea</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>OMSAFI2S</bic><bankCode>klarna</bankCode><bankName>OmaSP</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>POPFFI22</bic><bankCode>klarna</bankCode><bankName>POP Pankki</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>ITELFIHH</bic><bankCode>klarna</bankCode><bankName>Säästöpankki</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>HANDFIHH</bic><bankCode>klarna</bankCode><bankName>Handelsbanken</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>AABAFI22TMS</bic><bankCode>klarna</bankCode><bankName>Ålandsbanken</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>SBANFIHH</bic><bankCode>klarna</bankCode><bankName>S-Pankki</bankName></bankMapping>
        <bankMapping><countryCode>FI</countryCode><bic>HELSFIHH</bic><bankCode>klarna</bankCode><bankName>aktia</bankName></bankMapping>

        <!--NeoPay NO BANKS -->
        <bankMapping><countryCode>NO</countryCode><bic>DABANO22</bic><bankCode>klarna</bankCode><bankName>DANSKE BANK</bankName></bankMapping>
        <bankMapping><countryCode>NO</countryCode><bic>DNBANOKC</bic><bankCode>klarna</bankCode><bankName>DNB BANK ASA</bankName></bankMapping>
        <bankMapping><countryCode>NO</countryCode><bic>NDEANOKK</bic><bankCode>klarna</bankCode><bankName>NORDEA</bankName></bankMapping>
        <bankMapping><countryCode>NO</countryCode><bic>SGFSNO21</bic><bankCode>klarna</bankCode><bankName>SPAREBANK 1</bankName></bankMapping>
        <bankMapping><countryCode>NO</countryCode><bic>SPAVNOBB</bic><bankCode>klarna</bankCode><bankName>SPAREBANKEN VEST</bankName></bankMapping>
        <bankMapping><countryCode>NO</countryCode><bic>SBAKNOBB</bic><bankCode>klarna</bankCode><bankName>SBANKEN ASA</bankName></bankMapping>
        <bankMapping><countryCode>NO</countryCode><bic>HANDNOKK</bic><bankCode>klarna</bankCode><bankName>HANDELSBANKEN</bankName></bankMapping>

    </bankMappings>
    <accounts>
        <entry>
            <string>DEFAULT</string> <!--all methods-->
            <account>
                <merchantName>Devcode</merchantName>
                <supportedCurrencies>EUR|PLN|SEK|NOK</supportedCurrencies>
            </account>
        </entry>
        <entry>
            <string>??_BANK</string>
            <account>
                <countryCode>??</countryCode>
                <forceBank>??</forceBank>
                <merchantName>??</merchantName>
                <supportedCurrencies>??</supportedCurrencies>
            </account>
        </entry>
       <entry>
          <string>PAYOUT</string>
          <account>
             <username>??</username>
             <password>??</password>
             <apiKey>??</apiKey>
             <merchantName>??</merchantName>
             <supportedCurrencies>??</supportedCurrencies>
             <beneficiaryAccountNumber>??</beneficiaryAccountNumber>
          </account>
       </entry>
    </accounts>
    <testMode>true</testMode>
   <pspPrivateKey>??</pspPrivateKey>
   <encryptionCertificate>??</encryptionCertificate>
</com.devcode.paymentiq.integration.neopay.NeoPayConfig>
```

</details>

### Attributes

| Attribute                              | Description                                                                                                                                                                                              |
|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.projectId                | Merchant project id on Neopay side                                                                                                                                                                       |
| accountConfig.projectKey               | Merchant project key on Neopay side                                                                                                                                                                      |
| accountConfig.countryCode              | Country code of selected bank                                                                                                                                                                            |
| accountConfig.forceBank                | Bank name that should be forced for account                                                                                                                                                              |
| accountConfig.username                 | Client public ID from created application for payouts                                                                                                                                                    |
| accountConfig.password                 | Client secret ID from created application for payouts                                                                                                                                                    |
| accountConfig.apiKey                   | One-time Authorization code needed for payouts. It is important to run test transaction within a period of 1 minute after code retrieval. The instructions on how to retrieve a code can be found below. |
| config.encryptionCertificate           | SSL certificate generated by merchant. Used for payouts.                                                                                                                                                 |
| config.pspPrivateKey                   | Corresponding private key to the SSL certificate. Used for payouts.                                                                                                                                      |
| accountConfig.beneficiaryAccountNumber | Merchant's IBAN number. Required for payouts.                                                                                                                                                            |

### Callback URL

The callback URLs have to be provided to Neopay.

| Environment | URL                                                               |
|-------------|-------------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/neopay/callback/{mid} |
| Live        | https://api.paymentiq.io/paymentiq/api/neopay/callback/{mid}      |

Where ```{mid}``` = your assigned merchantId

### Payouts configuration
Neopay Payouts is a separate API and so has different prerequisites from the merchant to be able to implement.

#### NeoPay Payouts merchant application setup
1. Generate certificates locally (for later use in the application registration process, in every API call and to be provided to the provider):

   Assuming `openssl` application is installed on your local computer, execute the following commands in the command line tool.

   (Provided are the commands for the `test` provider environment. For `prod` - name of the files could be changed respectively, e.g. `piq_test_server.key` -> `piq_prod_server.key` and so on)

   `openssl genrsa -des3 -out piq_test_server.key 2048`

   `openssl rsa -in piq_test_server.key -out piq_test_server.pem`

   `openssl req -new -nodes -key piq_test_server.pem -out piq_test_server.csr [DO NOT CREATE A challenge password]`

   `openssl rsa -in piq_test_server.pem -out piq_test_server_key.pem`

   `openssl x509 -req -days 730 -in piq_test_server.csr -signkey piq_test_server_key.pem -out piq_test_server_key.crt`

   Generated file `piq_test_server_key.crt` should be given to the provider (for their internal account recognition and authorization)
   The content of `piq_test_server_key.crt` should be set in config parameter `config.encryptionCertificate`

   The content of `piq_test_server_key.pem`should be set in config parameter `config.pspPrivateKey`

2. Register/create an application at the provider side:
   Url (provider prod): [https://ob-api.neofinance.com/developer/portal](https://ob-api.neofinance.com/developer/portal)

   Url (provider test): [https://test-ob-api.neofinance.com/developer/portal](https://test-ob-api.neofinance.com/developer/portal)

   Some hints for the application registration:
   - `Email` - should be the email provided to the provider (so it will be recognized within their internal system)
   - `Redirect url` - callback url - the next URL should be set for staging [https://test-api.paymentiq.io/paymentiq/api/neopay/callback](https://test-api.paymentiq.io/paymentiq/api/neopay/callback) and this one for prod [https://api.paymentiq.io/paymentiq/api/neopay/callback](https://api.paymentiq.io/paymentiq/api/neopay/callback)
   - `Certificate QWAC` - content of the `piq_test_server_key.crt` file generated in the previous step
   - `Access Token Lifetime (sec)` - 3600 (recommended by the provider, could be another value)
   - `Refresh Token Lifetime (sec)` - 7776000 (recommended by the provider, could be another value)
     Other fields are either self-explanatory or could be left default or empty.

   As a result of successful application registration the following data will have been generated.:
   - `Client public ID`
   - `Client secret ID`

#### Getting authorization code.
The code is needed for retrieving of an access/refresh token pair. It is obtained in a browser with the account login. (Could be done once if token expiration is monitored)

   1. The code can be retrieved by prompting next URL in the browser:
   `{env}/oauth/v2/auth?client_id={client_id}&redirect_uri={redirect_uri}&response_type=code&scope=accounts%20payments%20accounts.list%20payments.preconfirmed`
   Where: `{env}` - provider's test [https://test-ob-api.neofinance.com](https://test-ob-api.neofinance.com) or prod url [https://ob-api.neofinance.com](https://ob-api.neofinance.com), `{client_id}` - Client public ID, `{redirect_uri}` - set redirect url during application registration.

   There merchant will be asked to login with his credentials. Merchant should contact the NeoPay in order to get the credentials.

   2. After completing signing in on the previous step, browser will be redirected to the URL with the authorization code. It will look like this:
   `{redirect_uri}?state=&code={code}`
   Where `{code}` is the authorization code that should be set in the config parameter `accountConfig.apiKey`.

   IMPORTANT: The test transaction should be initiated within the period of 1 minute after the authorization code is obtained. Otherwise, the code will expire and new authorization code will be needed.

## Example Routing Rule

![](/img/providers/routing/neopay.png)

## Test Information

Once the deposit transaction has been initiated, and the user is redirected to the hosted page, you can proceed with the test payment.