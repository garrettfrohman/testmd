---
id: "hosted_fields"
---

# Hosted Fields

The hosted fields are fields that contains sensitive (ex: credit card number, cvv code) data that will be hosted on our PCI servers. Each hosted field will be shown in an iframe container and can be communicated with by using `window.postMessage`.

## SDK

We have developed a SDK for use with our hosted fields and is located on a public [GitHub repository](https://github.com/devcode-git/hosted-fields-sdk). For more information on how to use it see the `readme.md` file in repo root.

## The Fields

### Credit card number

![](/img/integration_overview/hostedfields/01.png)

The credit card number field supports validation to make sure that it’s a valid card by using the luhn algorithm. The credit card field also supports identification of card types and shows a small icon to the left of the card number. The card number information is encrypted when requested from the hosted field in the `encCreditcard` field.

### Expiry date

![](/img/integration_overview/hostedfields/04.png)

The expiry date field supports validation to make sure that it's a valid month and year and that the expiry date has not passed. The expiry date data will be sent in two fields (`expiryMonth`,`expiryYear`) when requesting the data from the hosted fields.

### CVV

![](/img/integration_overview/hostedfields/02.png)

The CVV field supports validation of the length of the field and that it's only digits. The max length of the CVV is 4 digits. The CVV number will be sent encrypted when requested from the hosted field in the `encCvv` field.

### Other fields

Other fields like number and text can also be hosted but no encryption will be performed.
