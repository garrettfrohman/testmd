---
id: "1click_api_introduction"
---

# 1-Click API Introduction

The intended audience for this document is the person responsible for the technical integration. Basic knowledge of networking programming and monetary transactions are required. Any operating system and any programming language can be used to implement the 1-Click KYC API which is needed by PaymentIQ.

The PaymentIQ 1-Click KYC API uses JSON, http://en.wikipedia.org/wiki/JSON, for all data interchange. It is language independent and supported for virtually all programming languages. All methods are invoked by sending a valid JSON request via HTTPS POST.

Note: The PaymentIQ 1-Click KYC API expects all requests and responses to be UTF-8 encoded.

Valid currency codes are upper case 3-letter characters according to ISO 4217, http://en.wikipedia.org/wiki/ISO_4217. Number of digits after the decimal are also defined by the ISO standard, e.g JPY (Japanese yen) has 0 digits after the decimal.

## OAuth2 Standard

1-Click API is based on a proven standard. OAuth 2.0 is the industry-standard protocol for authorization.
OAuth 2.0 focuses on client developer simplicity while providing specific authorization flows for web applications, desktop applications, mobile phones, and living room devices.
This specification and its extensions are being developed within the IETF OAuth Working Group.


