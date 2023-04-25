---
id: "1click_api_create_a_client"
---

# Create A Client

1-Click APIs support OAuth 2.0 flows for different types of client applications.
In all of these flows, the client application requests an access token that is associated with only your client application and the owner of the protected data being accessed.
The access token is also associated with a limited scope that defines the kind of data your client application has access to (for example "Manage your tasks").
An important goal for OAuth 2.0 is to provide secure and convenient access to the protected data, while minimizing the potential impact if an access token is stolen.

## Authorization code flow

Use the authorization code flow to allow the end-user to grant your application access to their protected data on PaymentIQ APIs.
The protocol for this flow is specified in [Authorization Code Grant](https://tools.ietf.org/html/rfc6749#section-4.1).

## Create API Client in PaymentIQ Backoffice

The API Client section is located under "Admin > API clients".
The back-office user must have role MERCHANT_ADMIN enabled to be able to access the view.
To create a client the merchant needs to configure some information.

1. **Client name:**  Name of the client for example bambora_client.
2. **Client type:** Grant type to use and should always be set to authorization_code for 1-Click API.
3. **Redirect URLs:** The redirect_uri in the operator platform. PaymentIQ will redirect the end-user with the one-time code and state. This is used by PaymentIQ to control that the provided url is an official one. PaymentIQ only matches on URL, not query string so the merchant can add their own information with query string. Multiple redirect_uri can be added, you can also use * as wildcard.
4. **Resource ids:** The resource the client is attempting to access. Available resources are backoffice_api and identity_api. Should always be set to identity_api for 1-Click API.
5. **Whitelist IP addresses:** The IP addresses to whitelist for the client. IPs will be checked during server calls e.g token retrieval and check token. If you leave this empty, everyone is able to use this.

![](/img/1clickapi/authorization_code_create_client.png)

It will look something like this:

![](/img/1clickapi/authorization_code_settings.png)

You will need this client id if you want to configure `GIIClientConfig`.