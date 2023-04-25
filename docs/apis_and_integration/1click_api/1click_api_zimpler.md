---
id: "1click_api_zimpler"
---

# Zimpler ID Flow And Configuration

## Requirements

The merchant must have an account activated in the Zimpler platform. The credentials should be added in ZimplerConfig via PaymentIQ backoffice.

[SignIn](../../apis_and_integration/integration_api/signin) must be implemented for Zimpler to work.

## Configuration

Only one account is needed for both sign in and sign up with deposit.

```xml
<com.devcode.paymentiq.integration.zimpler.ZimplerConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>test-account</merchantId>
        <apiKey>test-account-key</apiKey>
        <version>4</version>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
  </accounts>
  <height>700</height>
  <width>600</width>
</com.devcode.paymentiq.integration.zimpler.ZimplerConfig>
```

## Parameters to Authorize

The parameter `country` is mandatory when calling `/oauth/authorize`

## Testing

Person number / national identification number
* Sweden: 19810101-0000
* Finland: 180265-019L

## Presentation Layer

For ZimplerID flow, PaymentIQ can either return a JSON containing an URL or do a 303 Redirect to the same URL. 
JSON is returned when `iframe=true`, a redirect is performed when `iframe=false`, see [Authorization Endpoint](1click_api_authorization).


Example JSON response:

```json
{
    "redirectOutput": {
        "html": null,
        "url": "https://checkout.zimpler.net/v4#034985535874357",
        "method": "POST",
        "container": "iframe",
        "parameters": {},
        "height": null,
        "width": null
    },
    "messages": [],
    "links": {
        "statusUrl": "http://localhost:8080/paymentiq/identity/api/signin/status?token=uNiuiygbUybYubUybUybkujnhJyihUygvUJyvJHvbJUygvKJKUULklFDjN"
    },
    "success": true
}
```

## KYC Data

:::info
The fields may not return in the same attribute name and format as displayed below e.g address_country is mapped as country with SWE as format. This is to ensure consistency when using multiple identity providers.
:::

| Field                          | Type    | Example       | Description                                                                    |
|--------------------------------|---------|---------------|--------------------------------------------------------------------------------|
| full_name                      | string  | John Doe      | The User's full name including given name(s), middle name(s) and last name(s). |
| first_name                     | string  | John          | The User's first name                                                          |
| last_name                      | string  | Doe           | The User's last name                                                           |
| date_of_birth                  | string  | 1990-07-29    | The User's date of birth in ISO 8601 format.                                   |
| pep                            | boolean | false         | This User is a Politically Exposed Person.                                     |
| national_identification_number | string  | 19900729-3124 | This User's national identification number (eg Personal Number in Sweden).     |
| address_line_1                 | string  | Gulgatan 3    | The User's registered address, first line.                                     |
| address_line_2                 | string  | lgh 1205      | The User's registered address, second line if present.                         |
| address_postcode               | string  | 49123         | The User's registered address, postcode.                                       |
| address_city                   | string  | Stockholm     | The User's registered address, city.                                           |
| address_country                | string  | Sweden        | The User's registered address, country.                                        |


## User Sign Up & Deposit Flow
Sign in/up can be done with or without a deposit. When not doing a deposit, the flow is shorter and only contains the authentication steps.


##Example of Sign Up & Deposit flow:

1. The first step is for the user to choose the bank.

![](/img/1clickapi/zimpler_1.png)

2. Depending on the market, different identification methods are used

![](/img/1clickapi/zimpler_2.png)

3. The user is prompted to perform authentication

![](/img/1clickapi/zimpler_3.png)

4. The account is chosen by the user

![](/img/1clickapi/zimpler_4.png)
