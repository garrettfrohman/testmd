---
id: "troubleshootlogin"
---

# Resolve Login Issues

## Problem Description

A merchant user is unable to log in to their PaymentIQ Backoffice account.

## Troubleshooting Steps

### Error message: Invalid username or password.

![](/img/troubleshooting/noexist.png)

For this error please check:

1. Does the account exist/are you typing the right username? Please reach out to your Backoffice User Administrator to resolve the issue.
2. Is the password correct? Please reach out to your Backoffice User Administrator to have the password reset.
3. If the account has been locked due to too many incorrect login attempts. Please reach out to your Backoffice User Administrator to unlock your account.
4. Are you trying to log in to the right environment? The test and production environments are completely separate with separate backoffice accounts. Please make sure you are not trying to log in with a test account on the live environment or a production account on the test environment. The correct login URLs are:
    - Test: https://test-backoffice.paymentiq.io/
    - Production: https://backoffice.paymentiq.io/

### Error: Your login attempt timed out. Login will start from the beginning.

![](/img/troubleshooting/timeout.png)

This error happens when you are at the login form but do not log in straight away. To resolve please go back to the main login pages and log in again:
    - Test: https://test-backoffice.paymentiq.io/
    - Production: https://backoffice.paymentiq.io/

### Error: Invalid Token

![](/img/troubleshooting/noexist.png)

This error could happen due to a session issue occurring on account creation. To resolve please ask your Backoffice User Administrator to reset your password.

### Does the user have the right roles to log in?

If you are met with an error message directly when logging in to PaymentIQ it likely means your user has been set up without the required roles to log in. Please reach our to your Backoffice User Administrator and ask them to check if the roles for the user has been set up correctly.


### Contacting PaymentIQ Technical Support

If neither of the above steps resolve your login issue, please reach our to technicalsupport@bambora.com for further investigation.

It is helpful for us when troubleshooting to know the MID and the Backoffice User you are having issues with and any other related information you have found in your troubleshooting. 