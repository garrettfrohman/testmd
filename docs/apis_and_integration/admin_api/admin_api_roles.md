---
id: "admin_api_roles"
---

# Roles Reference

When adding roles to the Admin API Client it is important to first know what features you will be using it for and to limit the access rights of the client according to those as much as possible.

:::info

The roles for the Admin API Client and the PaymentIQ Backoffice users have separate access scope.

:::

## Roles For The Admin API Client

:::danger

Do not assign all available roles to the Admin API Client. Try and limit the access as much as possible to reflect your intended use.

:::

| Role                      | Access                                                                        |
|---------------------------|-------------------------------------------------------------------------------|
| `ROLE_MERCHANT_ADMIN`     | Access to all Payment Methods                                                 |
| `ROLE_MERCHANT_SUPPORT`   | Access to search, approve, deny, onhold, repeat Payment Methods               |
| `ROLE_INVESTIGATOR_ADMIN` | Access to search, approve, deny, onhold, repeat void, capture Payment Methods |
| `ROLE_INVESTIGATOR`       | Access to refund, void, capture Payment Methods                               |
| *no role required*        | Access to all Account Methods                                                 |
| *no role required*        | Access to all KYC Methods                                                     |
| `ROLE_CONFIG_ADMIN`       | Access to all Configuration Methods                                           |
| `ROLE_RULES_ADMIN`        | Access to all Decision Table and Rules Methods                                |
