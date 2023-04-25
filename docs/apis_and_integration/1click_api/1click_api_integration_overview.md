---
id: "1click_api_integration_overview"
title: "Integration Overview"
---

One of the main architectural goals with PaymentIQ is to have it loosely coupled from the operator’s platform so the two systems can evolve independently without affecting each other. For example identity providers can be added, modified or updated without affecting the operator’s platform.


```mermaid
graph TD
    A("Browser (or any client)") -- "Reverse Proxy/ CDN (cloudflare)"  --> B(( ))
    B --- C(PaymentIQ)
    C -- "Process Sign In"--> D(Identity Providers)
    C -- "Integration API"--> E(( ))
    E --- F(Operator Platform)
``` 

In order to achieve the separations of concerns, the integration between the operator’s platform and PaymentIQ is reverted, i.e. PaymentIQ calls the Operator Platform instead of the Operator platform calls PaymentIQ.

Therefore, the operator needs to implement the Integration API as specified in this document.
