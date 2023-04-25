---
id: "1click_api_trustly"
---

# Trustly Pay N Play® Flow And Configuration

## Overview

PaymentIQ has a direct integration to Trustly Pay N Play® product. Pay N Play® allows the user to either sign in
or sign up with deposit included in the same flow. It allows the user to play immediately without registration.

![](/img/1clickapi/trustly-flow.png)

## Requirements

1. The merchant must have an account activated in the Trustly platform. The credentials should be added in TrustlyConfig via PaymentIQ Backoffice.
2. The merchant must have a Pay N Play® enabled account. Contact Trustly for more info.

## Configuration

1. The merchant should set up a TrustlyConfig in PaymentIQ Backoffice. Only one account is needed and can be used for both sign in and sign up with deposit.

```xml
<com.devcode.paymentiq.integration.trustly.TrustlyConfig>
  <enabled>true</enabled>
  <defaultDescriptor>PaymentIQ Test</defaultDescriptor>
  <selectAccountUrlTarget>_self</selectAccountUrlTarget>
  <selectAccountFailureUrl>https://www.bambora.com</selectAccountFailureUrl>
  <accounts>
    <entry>
     <string>SignIn</string>
     <account>
       <piqVersion>2</piqVersion>
       <quickDeposit>false</quickDeposit>
       <username>devcode_pnp</username>
       <password>xxxxxxxxxxxxxx</password>
       <version>1.1</version>
       <secretKey>-----BEGIN RSA PRIVATE KEY-----
        XXXXXXXXXXXXX
        -----END RSA PRIVATE KEY-----</secretKey>
        <pspPublicKey>-----BEGIN PUBLIC KEY-----
        XXXXXXXXXXXXX
        -----END PUBLIC KEY-----</pspPublicKey>
        </account>
      </entry>
    </accounts>
    <APIVersion>1.1</APIVersion>
    <depositUrlTarget>_self</depositUrlTarget>
    <withdrawalUrlTarget>_self</withdrawalUrlTarget>
    <quickDeposit>true</quickDeposit>
    <testMode>true</testMode>
    <bankMappings>
      <bankMapping><countryCode>IRL</countryCode><fromClearingHouse>IRELAND</fromClearingHouse></bankMapping>
      <bankMapping><countryCode>DEU</countryCode><fromClearingHouse>GERMANY</fromClearingHouse></bankMapping>
    </bankMappings>
  </com.devcode.paymentiq.integration.trustly.TrustlyConfig>
```

Usually there is three account configurations, one for QuickDeposits, one for RegularDeposits and one for SignIn. The default is that all these account entries use the same Trustly account.

### Mandatory parameters to Authorize

The following query parameters are mandatory when calling `/oauth/authorize`:
* country
* currency

## Presentation Layer

When using `iframe=false` PaymentIQ will return a HTML document, if you use `iframe=true` PaymentIQ will return JSON.

Example JSON response:

```json
{
    "redirectOutput": {
        "html": null,
        "url": "https://test.trustly.com/_/orderclient.php?SessionID=e4862de7-28a3-44df-900e-13a99b69098f&OrderID=1047392075&Locale=",
        "method": "GET",
        "container": "iframe",
        "parameters": {},
        "height": 370,
        "width": 600
    },
    "messages": [],
    "links": {
        "statusUrl": "http://localhost:8080/paymentiq/identity/api/signin/status?token=eyJhbGciOiJIUzI1NiJ9.eyJtZXJjaGFudElkIjoxMDAwLCJleHAiOjE1NTE3NzkzNTksInRva2VuIjoiMTAwMEE2MTIifQ.yoxZkLBolq9X5TOA5nZM8gTSxEoFicaEC_5fP715FXI"
    },
    "success": true
}
```

The HTML response is to big to have as example.

## KYC Data

:::note
The fields may not return in the same attribute name and format as displayed below e.g address_country is mapped as country with SWE as format. This is to ensure consistency when using multiple identity providers.
:::

| Field       | Type   | Example                               | Description                                                       |
|-------------|--------|---------------------------------------|-------------------------------------------------------------------|
| kycentityid | string | 29a750aa-0bad-4a28-a4 2d-ffb9a690d93a | An ID in our system identifying the KYC entity.                   |
| personid    | string | 19900501                              | Entity’s person-id if applicable. This will be null for Germany.  |
| firstname   | string | John                                  | Entity’s first name.                                              |
| lastname    | string | Doe                                   | Entity’s last name.                                               |
| dob         | string | 1990-05-01                            | Entity’s dob in yyyy-MM-dd format.                                |
| street      | string | Entity’s street name.                 | Entity’s street name.                                             |
| zipcode     | string | 13650                                 | Entity’s ZIP code.                                                |
| city        | string | Stockholm                             | Entity’s city.                                                    |
| country     | string | Sweden                                | Entity’s country.                                                 |
| gender      | char   | M                                     | Entity’s gender. Possible values are “M”, “F” or null if unknown. |


## User Sign Up & Deposit Flow

1. User is presented with three options. One option for sign in, a second for sign up the old way, and a third sign up with deposit. In this example, we are demonstrating the third option.

![](/img/1clickapi/trustly-flow-1.png)

2. Once the user initiates the request, the Trustly flow can be presented in an iframe. Here the user should select the bank it wishes to authenticate and deposit with.

![](/img/1clickapi/trustly-flow-2.png)

3. The user is expected to enter his/her ssn. Once completed, the user should authenticate itself via bank-id for example. This is where authentication and KYC verification occurs.

![](/img/1clickapi/trustly-flow-3.png)

4. Once authenticated and verified the user can proceed with deposit. The user should select the bank account he/she wishes to deposit from.

![](/img/1clickapi/trustly-flow-4.png)

5. The flow is finally complete. The user is created, signed in and has money deposited to his/her player account.

![](/img/1clickapi/trustly-flow-5.png)

## Hybrid model and Pure model

There are two options with different feature sets for the Trustly Pay N Play® integration.

- In the **Pure Model / standard** configuration the user is always presented with Trustly as a single payment option. You can deposit funds or use the Trustly resume play feature with balance from a previous session. Users can log in and register accounts either with or without a deposit.

- In the **Hybrid Model** the user is presented with the full cashier, which includes other payment methods apart from Trustly. The Resume Play feature for the Hybrid model is done with a deposit. Because other payment options are available the initial registration must be done with a deposit.

In terms of configuration, for the Pure setup the above outlined steps should be followed exactly with routing done to the Sign-In account (the Pay N Play® Trustly Processing Account).

For the Hybrid setup the initial transaction needs to follow the same steps. However once that is done subsequent transactions (with the full cashier) should be routed to the non Pay N Play® Trustly account. There are several ways to accomplish this. One way is to setup two routing rules, one for the initial SignIn and another for subsequent transactions.

### SignIn routing rule:

![](/img/1clickapi/hybrid_routing.png)

### Subsequent transactions:

![](/img/1clickapi/trustly_hybrid_deposit.png)
![](/img/1clickapi/trustly_hybrid_withdrawal.png)