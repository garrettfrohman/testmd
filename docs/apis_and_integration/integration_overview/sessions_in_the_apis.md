---
id: "sessions_in_the_apis"
---

# Sessions In The APIs

The PaymentIQ Merchant Integration Team are often asked to help clarify where the session-id is coming from to merchants interacting with the APIs.

It is created by the merchant and given in the initial request in the Front API and/or Cashier. PaymentIQ will simply forward it in order for the merchant to verify that it is valid.

So the logic is:

1. The Merchant does a request to PaymentIQ, which will contain a session-id
2. This session-id is then included in the `/verifyuser` request coming from PaymentIQ to the Merchant Operator Platform.
3. The Merchant verifies the end-user, including that the session is valid.

Which means that these sessions are an important part of securing the transaction.


:::warning

The session-id should be a unique session and not reused for several customers.

:::
