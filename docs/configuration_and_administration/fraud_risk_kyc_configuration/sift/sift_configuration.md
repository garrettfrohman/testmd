---
id: "sift_configuration"
---

# Sift Configuration

## Configuration by the Merchant

There are some setup steps that needs to be done on the merchant's site to activate Sift. 

## Configuration in PaymentIQ

Please contact our technical support team for assistance with this configuration.

### Example Configuration file

```xml
  <com.devcode.paymentiq.integration.sift.DiDSiftConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
      <accounts>
        <entry>
            <string>default</string>
          <account>
            <serviceEndpoint>https://demo-api.gii.cloud/api/data-sources/userinfo</serviceEndpoint>
            <username>???</username>
            <password>???</password>
          </account>
        </entry>
   </accounts>
  </com.devcode.paymentiq.integration.sift.DiDSiftConfig>
```

### Attributes

| Attribute       | Description                                 |
|-----------------|---------------------------------------------|
| serviceEndpoint | Provider URL                                |
| username        | User name provided by DevCode Identity      |
| password        | Password provided by DevCode Identity       |


### Example Rule setup

In this example three configuration cases will be implemented:

* All deposit transactions with fraud score lower than 2 will be route to the default provider account.
* All deposit transactions with fraud score higher than 2 and lower than 10 will be route to an alternative provider account.
* All deposit transactions with fraud score higher than 10 will be blocked.

**Configure Fraud Provider**

Select Rules -> Routing -> Fraud Provider

![](/img/fraudrisk/sift01.png)

Route all new creditcard deposits to Sift Fraud Provider and to the default Fraud account.

![](/img/fraudrisk/sift02.png)


**Configure Fraud Provider Block**

Select Rules -> Fraud Blocks -> Fraud Provider Block

![](/img/fraudrisk/sift03.png)

Block all transactions with fraud score higher or equal than 10. No re-routing is performed and failed transactions will be assigned a ERR_DECLINED_FRAUD status
Transactions with lower fraud score than 10 are re-routed

![](/img/fraudrisk/sift04.png)


**Configure Routing Rules**

New transactions are routed depending on the fraud score previously received. Transactions that are not new are routed to a third account.

![](/img/fraudrisk/sift05.png)


### API Request

Sample of an API request payload sent from PaymentIQ to Sift for a creditcard transaction:

```json
{
    "scopes": "fraud",
    "data_sources": "sift",
    "name": "Kalle Andersson",
    "given_name": "Kalle",
    "family_name": "Andersson",
    "preferred_username": "Kalle",
    "birthdate": "1981-01-01",
    "postal_code": "12345",
    "street_address": "Storgatan 1",
    "locality": "Storby",
    "region": "Storby",
    "country": "SWEDEN",
    "email": "test@example.com",
    "phone_number": "+46-733805161",
    "enduser_id": "476298",
    "event": {
        "transaction": {
            "transaction_id": "476298",
            "amount": 1000,
            "currency_code": "EUR",
            "payment_method": {
                "bin": "538806",
                "card_last4": "7447",
                "payment_type": "creditcard"
            }
        }
    }
}
```

API response for the previous request

```json
{
  "ssn": "",
  "ssn_type": "",
  "country": "SWEDEN",
  "address": {
    "formatted": "",
    "street_address": "Storgatan 1",
    "locality": "Storby",
    "region": "Storby",
    "postal_code": "12345",
    "country": "SWEDEN",
    "source": "",
    "type": "",
    "is_verified": true
  },
  "addresses": null,
  "screening": {
    "is_pep": false,
    "pep_checked_at": null,
    "pep_risk": 0,
    "pep_details": "",
    "is_sanction": false,
    "sanction_checked_at": null,
    "sanction_risk": 0,
    "sanction_details": "",
    "is_fraud": true,
    "fraud_checked_at": "2021-02-13T10:09:23.530128Z",
    "fraud_risk": 1,
    "details": null
  },
  "is_board_member": false,
  "has_real_estate_data": false,
  "birthdate": "1981-01-01",
  "birthdate_verified": null,
  "preferred_username": "Kalle",
  "name": "Kalle Andersson",
  "given_name": "Kalle",
  "family_name": "Andersson",
  "family_name_prefix": "",
  "family_name_stem": "",
  "initials": "",
  "sub": "bWFudWFsXVhmP2goO2dXeHpiI0ZGOn1tTV05MTIpS+OwxEKY/BwUmvv0yJlvuSQnrkHkZJuTTKSVmRt4UrhV",
  "uuid": "7d9d68cf-f9d4-444a-bbbf-bc1f692c4dfa",
  "email": "test@example.com",
  "email_verified": false,
  "picture": "",
  "gender": "",
  "phone_number": "+46-733805161",
  "phone_number_verified": false,
  "password": "",
  "profile_level": 1,
  "enduser_id": "476298",
  "enduser_id_secure": true,
  "verification_failed": null,
  "verification_failed_reason": "",
  "verification_pending": null,
  "is_foreign_resident": null,
  "is_protected_identity": null,
  "document_number": "",
  "document_type": "",
  "document_country": "",
  "document_valid_from": "",
  "document_valid_until": "",
  "machine_readable_zone": "",
  "age": 40,
  "age_verified": null,
  "is_self_exclusion": null,
  "self_exclusion_checked_at": null,
  "bank_accounts": null,
  "credit_rating": null
}
```
