---
id: "cashier_add_custom_template_for_all_providers"
---

# Custom Template For All Providers

This custom template is called merchantInputTemplate and is a general template displayed below the input fields in the cashier. This feature is meant to be applied for all payment-methods.

Available features:
- Required checkbox. (must be checked before proceeding)
- Required bonus code input. (must be entered before proceeding)
- Set this to be displayed only for withdrawal, deposit, or all methods.
- Alternate between displaying content A and B based on if checkbox is checked or not.

## Steps to implement

1. Add a new HTML template in `PaymentIQ Backoffice -> Admin -> Templates -> HTML Templates`. Suggested name is: `merchant-input-template`. Then add the HTML you want to display.

2. Reach out to PaymentIQ Technical Support to update your PaymentIQ MerchantId to show the merchant input template.
