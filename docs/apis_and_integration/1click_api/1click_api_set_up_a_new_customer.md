---
id: "1click_api_set_up_a_new_customer"
---

# Set Up A New Customer

## 1 - Update MerchantConfig

In `MerchantConfig` add the following:

```xml
<properties>
    <entry>
      <string>oauthBaseRedirectUrl</string>
      <string>https://test-api.paymentiq.io/paymentiq</string>
    </entry>
</properties>
```

For production you need to use the URL `https://backoffice.paymentiq.io/paymentiq`.

## 2 - Implement Redirect URI

The customer needs to implement [redirect url](1click_api_redirect_uri).

## 3 - Create Client

Create client, according to [this](1click_api_create_a_client), If you want to configure for Devcode Identiy(GII) you need to save the client id for next step.

## 4 - Configure The Identity Provider

Configure the identity provider. If you are configuring `GIIClientConfig`, use the client id from step 3 in `piqClientId`.

It works like this:

![](/img/1clickapi/giiclientconfig.png)

More info [here](1click_api_devcode_identity)

## 5 - Test Manually

Test manually, one good way to test is to use [Postman](https://www.getpostman.com/).
You configure postman like this:

![](/img/1clickapi/postman_example_1.png)

![](/img/1clickapi/postman_example_2.png)

You get `Client ID` and `Client Secret` from the API client in step 3. You will also need to add `https://www.getpostman.com/oauth2/callback` as redirect URL on your API client.

