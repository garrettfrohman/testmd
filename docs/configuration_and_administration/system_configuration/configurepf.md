---
id: "configurepf"
---

# Configure Payment Facilitator

Setting up a Merchant as a Payment Facilitator (PF) allows them to offer payment services for sub-merchants. The sub-merchants do not need a PaymentIQ MID configured but uses the MID of the Payment Facilitator. After configuration the PF can add additional sub-merchants without the involvement of PaymentIQ.

Currently BamboraGa can be configured as a Payment Facilitator.

## How to activate a Merchant account as a Payment Facilitator

:::warning
Please make sure that your developer team have made the required IntegrationAPI changes before proceeding
:::

To activate a BamboraGa account as a Payment Facilitator account the following line needs to be added on account level in the BamboraGa configuration file.

```xml
<paymentFacilitator>true</paymentFacilitator>
```

