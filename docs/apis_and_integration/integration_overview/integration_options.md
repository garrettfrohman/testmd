---
id: "integration_options"
---

# Integration Alternatives

We offers a variety of ways to connect to and make use of PaymentIQ depending on your requirements. Some merchants will want to use a combination of integration options and we do not have any restrictions to this. Here you can find a list of the main ways to connect to PaymentIQ with some explanatory descriptions.

## Standardized Cashier

Integrating to PaymentIQ using the Standardized Cashier is the recommended option due to the simplicity of using a fully customizable out of the box widget. 

To integrate with this option you will need to:
- Implement the Integration API connecting to the Merchant Operator Platform (this is a requirement for all integrations)
- Configure and add the Cashier widget on your site

## Front API

If you do not wish to use the PaymentIQ Cashier we offer the same functionality via our Front API. It is important to consider when using this option that you miss out on a lot of prebuilt functionality from the cashier and that depending on the payment provider you intend to use different sets of input parameters may be required.

To integrate with this option you will need to:
- Implement the Integration API connecting to the Merchant Operator Platform (this is a requirement for all integrations)
- Implement the FrontAPI that you connect to your interfaces

## 1-Click KYC

The 1-Click API allows for the use of Identity providers for sign in & sign up and/or sign in & deposit flows with stored card information.

To integrate with this option you will need to:
- Implement the Integration API connecting to the Merchant Operator Platform (this is a requirement for all integrations). 
- Implement custom methods in the Integration API specific to the 1-Click communication flow.
- Implement the 1-Click KYC API

# Additional Options

The below listed APIs and configuration options are used in conjunction with the integration options for custom features.

## Admin API

The Admin API is the one you need to implement to access common PaymentIQ Backoffice functionalities. It is commonly used to add  withdrawal approval and other features to the merchant backoffice and is often implemented in combination with the other options.

To integrate with this option you will need to:
- Implement the Admin API and connect it to your admin system or similar

## Payment Facilitator

Setting up a Merchant account as a Payment Facilitator (PF) allows them to offer payment services for sub-merchants. The sub-merchants do not need a PaymentIQ MID configured but uses the MID of the Payment Facilitator. After configuration the PF can add additional sub-merchants without the involvement of PaymentIQ.

Currently BamboraGa can be configured as a Payment Facilitator.

To integrate with this option you will need to:
- Implement the Integration API connecting to the Merchant Operator Platform (this is a requirement for all integrations)
- Provide additional data specific to a PF setup in the Integration API authorize attributes object.
- Implement either of the Cashier/FrontAPI/1-Click API for customers to use.

## Batch Processing

As the name implies we offer batch processing for merchants where this may be beneficial.

To integrate with this option you will need to:
- Reach out to our technical support team to assess if this is a good option for your use case.
- Be able to generate and upload batch files in accordance with our [documentation](batch_processing).

## Hosted Fields

By handing over the responsibility for sensitive fields and have them be be hosted on PaymentIQ's PCI servers you can further increase your security and simplify your customer facing interface.

To integrate with this option you will need to:
- Reach out to our technical support team to assess if this is a good option for your use case.
- Be able utilize the SDK outlined [here](hosted_fields).
