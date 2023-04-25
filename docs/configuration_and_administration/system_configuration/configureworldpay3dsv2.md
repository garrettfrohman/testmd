---
id: "configureworldpay3dsv2"
---

# Configure Worldpay For 3DS2

## Required actions before implementation

The merchant should contact Worldpay and request the Acquirer Merchant ID values for their processing currencies that relate to the merchants Worldpay merchantCode (from the WorldpayConfig). You must also request that Worldpay **enable the third party MPI** for this merchantCode. There will be different acquirerMerchantId values for each processing currency. For example;

- SEK: 1845xxxx
- EUR: 1853xxxx
- CAD: 1853xxxx
- USD: 1853xxxx
- GBP: 1853xxxx

Mapping for these values needs to be added to the Worldpay config in the PSP account that you'll use for 3DS2 transactions, as explained below.

Clarify the actual name of the entity who contracts with Worldpay. This will usually be the name on your Worldpay contract and will also be entered into the config as `<threeDSRequestorName>`, detailed below.

## Implementation walkthrough

<video src="/video/3ds2/3ds2_settingupworldpay.mp4" controls muted preload/>

### Implementation Steps from the walkthorugh

- Configure the WorldpayConfig by following the documentation portal
- Clone the current 3DS pspAccount and rename it 3DS2

<video src="/video/3ds2/3ds2_cloninganentryinthepspconfig.mp4" controls muted preload/>

- Add the additional parameters below to the config

```xml
				<!-- 3DS2 mapping -->
    <acquirerMerchantId>${ptx.txAmount.currencyCode;map(SEK->1845xxxx,EUR->1853xxxx,CAD->1853xxxx,GBP->1853xxxx,USD->1853xxxx)}</acquirerMerchantId>    <!-- Might be simple, can be complex like here -->
    <mcc>7995</mcc> <!-- the MCC code, 7995 for gambling -->
    <merchantCountry>MLT</merchantCountry> . <!-- The registered country of the processing entity (merchant) -->
    <merchantUrl>http://www.yourbrand.com</merchantUrl> . <!-- The URL that processes on this MID -->
    <merchantName>MerchantName</merchantName>
    <threeDSRequestorName>The actual name that Worldpay use for the merchant</threeDSRequestorName> .    <!-- This could be ContractualEntity Ltd.  etc. -->
				<!-- End of 3DS2 mapping -->
```

- Edit the additional parameters to reflect the actual merchant info, and save
    - Note that the `<acquirerMerchantId>` value will need to be mapped according to the values that you have obtained from Worldpay, following the example format above, but deleting any currencies not required, or adding others that are missing. Enter the numeric values in place of the example values above.
    - The `<threeDSRequestorName>` is the contractual entity from your Worldpay contract that you have previously clarified when contacting Worldpay.
- Create a routing rule that sends a live 'test' user to the new 3DS2 account
- Create a 3DS2 Provider routing rule to Ingenio>default for the live 'test' user


- 3DS2 is now live for the live 'test' user.
- Make some test transactions using real cards on the production site
    - Revolut and Transferwise cards are known to be 3DS2 enabled

Once testing of both Visa and Mastercard is completed, move to real transaction testing.
