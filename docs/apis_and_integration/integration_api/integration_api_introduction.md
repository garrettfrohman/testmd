---
id: "integration_api_introduction"
---

# Integration API Introduction

The Integration API handles the communication with the merchant operator platform. All merchants that that use PaymentIQ will need to implement this API, either directly or via a platform provider.

The intended audience for this document is the person responsible for the technical integration. Basic
knowledge of networking programming and monetary transactions are required. Any operating system
and any programming language can be used to implement the Integration API which is needed by
PaymentIQ.

The PaymentIQ Integration API uses JSON, [http://en.wikipedia.org/wiki/JSON](http://en.wikipedia.org/wiki/JSON), for all data
interchange. It is language independent and supported for virtually all programming languages. All
methods are invoked by sending a valid JSON request via HTTPS POST.

Note: The PaymentIQ Integration API expects all requests and responses to be UTF-8 encoded.
Valid currency codes are upper case 3-letter characters according to ISO 4217,
[http://en.wikipedia.org/wiki/ISO_4217](http://en.wikipedia.org/wiki/ISO_4217). Number of digits after the decimal are also defined by the ISO
standard, e.g JPY (Japanese yen) has 0 digits after the decimal.