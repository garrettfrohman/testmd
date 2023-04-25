---
id: "1click_api_troubleshooting"
---

# Troubleshooting

If you get HTTP status 401(unauthorized) there is a number of things you should check before reaching out to our Technical Support team:

* Is `oauthBaseRedirectUrl` set in `MerchantConfig`?
* Is the redirect URL registered on the API client?
* Are you using the correct clientId from API client? Remember that you need one API client per brand.
* Are you using a system that requires an `api/signin` call? if yes, check that the provider is configured in `IdentityProviderConfig`

If you are using DID:

* Is it the correct piqClientId in `GIIClientConfig`?
* Is the provider enabled on the DID account? (Contact DevCode identity)
