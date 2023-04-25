---
id: "create_api_client"
---

# Create API Client

To get started with the Admin API you need to create an API client. This is done in the PaymentIQ backoffice under **Admin > API clients**. 

Click **Action** and then **New Client** to begin the setup of a new Admin API Client. Fill out the required fields using the notes listed below.

:::info
Only back office users with the merchant admin role are allowed to create clients.
:::

## Client Name

Set any Client Name to your liking. It is only used for display and can be changed later if wanted.

## Grants

Grant should be set to `client_credentials`.

## Roles

Here you set the user access roles corresponding to those for a regular backoffice user. Please check the [Admin API Roles](admin_api_roles) document to help you chose the roles best for your needs.

## Access Token Validity Seconds  

This shows how many seconds the access token is valid. Standard value for OAuth 2.0 is used. This will be populated automatically, therefore there is no need to add your own value.

## Refresh Token Validity seconds

This shows how many seconds the refresh token is valid. Standard value for OAuth 2.0 is used. This will be populated automatically, therefore there is no need to add your own value.

## IP Address Whitelist

This is an optional Whitelist of Merchant IP-addresses. This can be changed/updated at a later stage.

---

:::info
Once the client has been created additional fields are shown for client settings

![](/img/admin_api/admin07.png)
:::

## Client id                        

The generated Client ID that should be used for the authentication.

## Client secret        

Should be used for the authentication. Use `Show` to display the secret in clear text. Note that the client secret can be regenerated with `New Secret`, which will replace the old secret upon action.

## Scopes

For which scopes the client is for, default values are: `web-origins,address,phone,roles,profile,paymentiq,email`

## Resources

Which "resource" the client is meant for. This will always be `backoffice_api`.
