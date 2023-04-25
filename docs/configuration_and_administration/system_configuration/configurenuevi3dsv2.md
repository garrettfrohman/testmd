---
id: "configurenuevi3dsv2"
---

# Configure Nuevi for 3DS2

## General

SafeCharge have rebranded to Nuvei but for ease of reference and as they are still listed in PIQ as SafeCharge, they will be referred to as SafeCharge here.

## Required actions before implementation

- The merchant needs to obtain certain values from the SafeCharge back office that will be used in the setup of the REST config
    - `<merchantId>`, `<secretKey>`, `<siteId>`
- These are sourced from the values found within the Safecharge back office at  CPanel->Settings->MyAccount.

![](/img/3dsv2/safechargebo1.png)

![](/img/3dsv2/safechargebo2.png)

For Safecharge we also need to set the parameter `<acquirerMerchantId>` in the 3DS2 config

This parameter is a numerical value and relates to the specific processing MID, but Safecharge need to provide it.

- Contact Safecharge quoting your processing account `<merchantId>` and `<siteId>` and ask them for the  `<acquirerMerchantId>` that relates to this account and that you need it for use of an external MPI.  **It is important that this  `<acquirerMerchantId>` is confirmed as registered for 3DS with Mastercard**, so verify that this is the case with SafeCharge.
- Also **ask SafeCharge to enable 'payment option cards even when country field in the request is empty' for the specific processing MID** `<siteId>`
    - If this is not done then 3DS2 validations can get the error "Your request parameters didn't validate."

## Implementation walkthrough

- Add 3DS2 details below to the SafeChargeRestConfig in the desired PSP account.

```xml
<!--- 3DS2 parameters -->
<acquirerMerchantId>xxxxxxxxxxxxxxxx</acquirerMerchantId> <!-- From SafeCharge -->
<mcc>7995</mcc>
<merchantCountry>YourRegisteredCountry</merchantCountry> <!-- 3-letter iso -->
<merchantUrl>http://www.yourUrl.com</merchantUrl>
<merchantName>YourMerchantsContractualName</merchantName>
<!-- End 3DS2 parameters -->
```

- Edit the additional parameters to reflect the actual merchant info, and save
- Save the new configuration in the SafeChargeRestConfig
- Create a routing rule that sends a live 'test' user to the new 3DS2 account
- Create a 3DS2 Provider routing rule to Ingenio>default for the live 'test' user


- 3DS2 is now live for the live 'test' user.
- Make some test transactions using real cards on the production site
    - Revolut and Transferwise cards are known to be 3DS2 enabled

Once testing of both Visa and Mastercard is completed, move to real transaction testing.
