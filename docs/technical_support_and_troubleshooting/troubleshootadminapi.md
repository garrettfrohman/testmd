---
id: "troubleshootadminapi"
---

# Resolve Admin API Client Issues

## Problem Description

A merchant is trying to use an API Client to connect with PaymentIQ but is getting a 401 error.

## Troubleshooting Steps

### Are you using the right endpoint?

There are two different endpoints, one for the test and one for the live environment. They can be found [here](/docs/apis_and_integration/admin_api/admin_api_environments)

A common mistake is to point to the live endpoint when trying to use a client set up on test or vice versa.

### Does the client have the right roles?

For a client to work it needs to have roles added on. Ideally you should not add on all roles available, but just the ones you will need. Please check the [roles reference](/docs/apis_and_integration/admin_api/admin_api_environments) documentation.

### Are you calling from a whitelisted IP?

If your client has IPs whitelisted you need to call from one of those IPs. If there are no IPs listed in the whitelisting any IP will work.

So to check that the issue is not IP related, you could try temporarily removing all IPs in the whitelist and see if that resolves the problem.

### Contacting PaymentIQ Technical Support or Onboarding Support

If you have checked the above listed suggestions to resolve the issue but still get a 401 on the call, please reach out to the Onboarding Team if you are currently Onboarding or the Technical Support Team if you are live.

It is helpful for us when troubleshooting to know the MID and Client name you are having issues with and any other related information you have found in your troubleshooting.
