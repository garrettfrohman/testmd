---
id: "1click_api_brite"
---

# Brite Flow And Configuration

## Requirements
The merchant must have an account activated in the Brite platform. The credentials should be added in BriteConfig via PaymentIQ backoffice.

## KYC Data
| Field     | Type   | Example      | Description                        |
|-----------|--------|--------------|------------------------------------|
| personid  | string | 199005011234 | Entity’s person-id                 |
| dob       | string | 1990-05-01   | Entity’s dob in yyyy-MM-dd format. |
| name      | string | John Doe     | Entity’s full name                 |
| firstName | string | John         | Entity’s first name                |
| lastName  | string | Doe          | Entity’s last name                 |
| street    | string | Somestreet 1 | Entity’s street name               |
| zip       | string | 13650        | Entity’s ZIP code.                 |
| city      | string | Stockholm    | Entity’s city.                     |
| country   | string | Sverige      | Entity’s country.                  |