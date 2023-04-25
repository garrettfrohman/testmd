---
id: "cashier_show_custom_provider_information"
---

# Show Custom Provider Information

Each provider can be configured to show a block of custom information. An arbitrary html-document can be configured in PaymentIQ Backoffice and set to be shown for a specific provider.

Suggested usecases:

* Provide explanation/requirements for the payment method
* Legal texts/links for the payment method
* Include custom form fields, to gather more info from your end user (check with your support agent for more info) 
* Cosmetics

## Steps To Implement

1. Add a new HTML template in `PaymentIQ Backoffice -> Admin -> Templates -> HTML Templates` with the specified name, f.ex: `trustly-input-template`. Then add the HTML you want to display. Reach out to PaymentIQ Technical Support to get more detailed information about supported features and predefined components available in PaymentIQ input templates.

2. Reach out to PaymentIQ Technical Support and ask them up update your PaymentIQ Mid to show the input template. Specify MerchantId, template name and provider.
