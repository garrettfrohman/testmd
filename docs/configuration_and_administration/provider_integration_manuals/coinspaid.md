--- 
id: "coinspaid" 
title: "CoinsPaid (Crytoprocessing.com)"
hide_title: "true"
---
 
![](/img/providers/logos/coinspaidlogo.png)

# CoinsPaid (Crytoprocessing.com)

## About
CoinsPaid is an organisation providing cryptocurrency payment services. 
They enable businesses to operate worldwide, decrease costs and reach new markets using reliable cryptocurrency processing methods.

| Provider Name                | CoinsPaid                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://coinspaid.com/](https://coinspaid.com/)                                |
| Classification               | Crypto Currency                                                                 |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit`<br/> `CryptoCurrencyWithdrawal`                         |
| PaymentIQ Configuration File | `CoinsPaidConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.coinspaid.CoinsPaidConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantKeyId>???</merchantKeyId> <!-- Key -->
        <secretKey>???</secretKey>  <!-- Secret -->
        <supportedCurrencies>???</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <supportedPrefixCurrencies>BTC</supportedPrefixCurrencies>
</com.devcode.paymentiq.integration.coinspaid.CoinsPaidConfig>'
```

</details>

### Attributes

| Attribute                 | Description                                                                                  |
|---------------------------|----------------------------------------------------------------------------------------------|
| merchantKeyId             | Created in CoinsPaid Backoffice in the Api keys section as key                               |
| secretKey                 | Generated in CoinsPaid Backoffice alongside with the Api key                                 |
| supportedPrefixCurrencies | Cryptocurrencies for which we need to add a prefix on the address to be shown in the QR code |

### Provider Configuration

To be able to test the CoinsPaid Api you need to contact CoinsPaid to create a sandbox merchant account.
Once you have your sandbox account, you will be able to create API keys and authenticate with CoinsPaid API using your credentials.

To create API keys:

1. Navigate to your Merchant dashboard, find section called “API keys” and click "Activate".

  ![](/img/providers/coinspaid01.png)
  
2. In order to activate your API key and see your secret enter 2FA code and click "Activate".

    ![](/img/providers/coinspaid02.png)
    
3. After activation you will see your secret.

  ![](/img/providers/coinspaid02.png)


Add the ApiKey created in your CoinsPaid account as merchantKeyId in the config, the SecretKey as secretKey.

### Callback configuration 

You need to specify the callback URL as well in a "Settings → API" section in your CoinsPaid account and Api_v2 as the API version.

Test callback Url : https://test-api.paymentiq.io/paymentiq/api/coinspaid/callback/

Live callback Url : https://api.paymentiq.io/paymentiq/api/coinspaid/callback/

### Crypto Currency Selection
The crypto currency to use for the transaction must either be sent in the input field `cryptoCurrency` or as a service. A service mapping can be added in CoinsPaidConfig. The default service mapping is:

```xml
<services>
  <entry>
    <string>BITCOIN</string>
    <string>BTC</string>
  </entry>
  <entry>
    <string>ETHEREUM</string>
    <string>ETH</string>
  </entry>
  <entry>
    <string>BITCOIN_CASH</string>
    <string>BCH</string>
  </entry>
  <entry>
    <string>LITECOIN</string>
    <string>LTC</string>
  </entry>
</services>
```

For certain cryptocurrencies such as Ripple, a successful withdrawal requires a destination tag. There are 2 methods of delivering it.
1. Legacy solution > If the user has it in their account details, it will be retrieved from there.
2. Preferred solution > You can set up a transaction type which includes the field destinationTag. You can do so from Admin > Cashier > Payment Methods and Inputs by adding destinationTag in the inputs field.

As the destination tag is only needed for some currencies, to not display the field regardless of chosen cryptocurrency, there is an HTML template (called "coinspaid-withdrawal-cryptocurrency_dropdown") you can use which will show the destinationTag only on certain currencies. 

To use this template, you will have to go to Admin > Cashier > Payment Methods and Inputs. In this file, find the tx displayed in your cashier. From the "inputs" field, remove the cryptocurrency field. Then put "coinspaid-withdrawal-cryptocurrency_dropdown" in the "Input Html Template Name" field.

When using the template, to modify what currencies are shown and what currencies require the destination tag you will have to modify the template. 

## Example Routing Rules
![](/img/providers/routing/coinspaidrouting.png)


## Test Information
### Deposits

After you initiate a deposit transaction,an interface with a Qr code and an address will be shown in order to make a deposit.
Scan the QR code directly into your wallet app, click on the address to open your wallet application automatically with the specified address
or copy the address into your account to make a deposit.

Note that we don't need to generate new addresses for the customer everytime, address can be reused unlimited amount of times, and make a deposit.
We will receive a callback with all the payment informations and create a new transaction in PIQ whenever the customer makes a deposit.

Merchant will need to wait until the transaction is in a final state to know the exact amount of a deposit. Notice also that even a cancelled transaction leads to a creation of a new deposit address for the user.

### Withdrawal
To test withdrawal select CryptoCurrency payment option, choose a crypto currency and add an address.
        
Important: You need to contact CoinsPaid support team to fill your sandbox account with an amount to be able to test.

