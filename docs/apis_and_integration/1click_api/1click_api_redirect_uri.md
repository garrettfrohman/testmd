---
id: "1click_api_redirect_uri"
---

# Redirect URI

This is the redirect URI that is sent to the call `/oauth/authorize`.
This needs to be hosted and implemented by the merchant.

The URL needs to be able to receive the querystring parameters 
`code` and `state`.

## Example

`https://www.example.com/callback?code=1234&state=WAITING_INPUT`

The `code` parameter contains the one-time authorization_code that is needed for getting token from the PaymentIQ endpoint `/oauth/token`.

The merchant needs to answer HTTP status 200 on this call.

Remember to update the merchants API client with this redirect URI.