---
id: "gdpr"
---

# GDPR Anonymization Requests

Customers will occasionally request data anonymization from Merchants'. For the information stored in PaymentIQ this can be done by backoffice users with both the `ROLE_GDPR_ADMIN` and the `ROLE_USER_PSP_ACCOUNT` roles.

There are a few different ways to anonymize user in PaymentIQ. If you are anonymizing a single user the easiest way is to go to User Accounts and do a search to find the user. Then right click on the user and press **Anonymize user (GDPR)** 

![](/img/gdpr/anonymize_01.png)

and confirm the action.

![](/img/gdpr/anonymize_02.png)

Alternatively, if you are anonymizing multiple users or if you need to anonymize several accounts used for different providers by one user, you can highlight the users in the User Accounts view and press **Action > Anonymize user (GDPR)**  to proceed with the anonymization.

There are a few things you should consider before anonymizing a user.

- Please check that the user does not have transactions under processing before performing a GDPR anonymization request. The user can only be anonymized if there are no transactions in a processing state within the last five months. By processing we mean transactions that are **not** in the final state in PaymentIQ (i.e., `SUCCESSFUL`, `FAILED`, `CANCELLED`, or `INCONSISTENT`), or for Capture based transactions with a waiting for capture status code.

- To anonymize a user that still has transactions under processing you will have to either wait to have the transactions blocking the request finalized, or use the force method to get them into a `SUCCESSFUL`, `FAILED`, `CANCELLED`, Or `INCONSISTENT` state. 

- Triggering GDPR anonymization will prevent you from performing any kind of correction to transactions for anonymized users. This includes refunds, voids etc. Also we will not be able to check if a anonymized user was a fraud or not as their personal data has been removed from PaymentIQ. We therefore recommend that you to action GDPR anonymization requests only after 30 days from the last performed transaction by the user.