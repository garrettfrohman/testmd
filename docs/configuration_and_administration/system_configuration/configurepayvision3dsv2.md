---
id: "configurepayvision3dsv2"
---

# Configure Payvision For 3DS2

## Required actions before implementation

The merchant should contact Payvision and request the SchemeId’s that relate to the merchants Payvision memberId. The memberID is a Payvision ID and can be used to link to several scheme MIDs based on a number of conditions. Ensure that Payvision specify what conditions link the memberId to the SchemeIds. As an example, this could be based on currency, like;

- AUD: 750xxx01
- CAD: 750xxx02
- EUR: 750xxx03
- GBP: 750xxx04

Mapping for these values should then be added to the 3DS2 config, as explained below.

- Clarify the actual name of the entity who contracts with Payvision. This will usually be the name on your Payvision contract and will also be entered into the config as `<threeDSRequestorName>`, as explained below.

## Implementation walkthrough

<video src="/video/3ds2/3ds2_settinguppayvision.m4v" controls muted preload/>

### Implementation Steps from the walkthorugh

- Configure the PayvisionConfig by following the documentation portal
- Clone the current 3DS pspAccount and call it 3DS2

<video src="/video/3ds2/3ds2_cloninganentryinthepspconfig.mp4" controls muted preload/>

- Add the additional parameters, copying the below.

    ```xml
    <!-- 3DS2 mapping -->
        <acquirerMerchantId>${ptx.txAmount.currencyCode;map(AUD->750xxx01,EUR->75xxx03,CAD->750xxx02,GBP->750xxx04)}</acquirerMerchantId>  <!-- Might be simple, can be complex like here -->
        <mcc>7995</mcc> <!-- the MCC code, 7995 for gambling -->
        <merchantCountry>MLT</merchantCountry> . <!-- The registered country of the processing entity (merchant) -->
        <merchantUrl>http://www.yourbrand.com</merchantUrl> . <!-- The URL that processes on this MID -->
        <merchantName>MerchantName</merchantName>
        <threeDSRequestorName>The actual name that Payvision use for the merchant</threeDSRequestorName> .    <!-- This could be ContractualEntity Ltd.  etc. -->
        <merchantThreeDSRequestorId>VISA->10066528*${ptx.txAmount.currencyCode;map(AUD->750xxx01,EUR->75xxx03,CAD->750xxx02,GBP->750xxx04)},MASTERCARD->${ptx.txAmount.currencyCode;map(AUD->750xxx01,EUR->75xxx03,CAD->750xxx02,GBP->750xxx04)}</merchantThreeDSRequestorId> .   <!-- Might be simple, can be complex like here -->
    <!-- End of 3DS2 mapping -->
    ```

- Edit the additional parameters to reflect the actual merchants info
    - `<acquirerMerchantId>` is based on the parameters for the schemeId's that Payvision will have provided
        - Note that the `<acquirerMerchantId>` value will need to be mapped according to the values that you have obtained from Payvision, following the example format above, but deleting any currencies not required, or adding others that are missing. Enter the numeric values in place of the example values above.
    - `<merchantThreeDSRequestorId>` is based on the parameters for the schemeId's that Payvision will have provided
        - Note that the `<merchantThreeDSRequestorId>` values will need to be mapped according to the values that you have obtained from Payvision, following the example format above, but deleting any currencies not required, or adding others that are missing. Enter the numeric values in place of the example values above. The values need to be entered twice. Once for Via and once for Mastercard.
    - `<threeDSRequestorName>` is the contractual name of the merchant
    - Other parameters should be edited as appropriate to the merchant
- Save this new 3DS2 configuration
- Create a routing rule that sends a live 'test' user to the new 3DS2 account
- Create a 3DS2 Provider routing rule to Ingenio>default for the live 'test' user
- 3DS2 is now live for the live 'test' user.
- Make some test transactions using real cards on the production site
    - Revolut and Transferwise cards are known to be 3DS2 enabled

Once testing of both Visa and Mastercard is completed, move to real transaction testing.
