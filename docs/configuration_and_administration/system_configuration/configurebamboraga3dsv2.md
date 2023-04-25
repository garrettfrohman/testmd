---
id: "configurebamboraga3dsv2"
---

# Configure BamboraGa For 3DS2

## Implementation Walkthrough

A video implementation walkthrough of BamboraGa 3DS2 is available

<video src="/video/3ds2/3ds2_settingupbamboraga.mp4" controls muted preload/>

## Implementation Steps from the walkthorugh

- Configure the BamboraConfig by following the guide in the documentation portal
- Clone the current 3DS pspAccount and call it 3DS2 

<video src="/video/3ds2/3ds2_cloninganentryinthepspconfig.mp4" controls muted preload/>


- Add the additional parameters
- Edit the additional parameters to reflect the actual merchants info, and save
- Create a routing rule that sends a live 'test' user to the new 3DS2 account
- Create a 3DS2 Provider routing rule to Ingenio>default for the live 'test' user
- 3DS2 is now live for the live 'test' user.
- Make some test transactions using real cards on the production site
    - Revolut and Transferwise cards are known to be 3DS2 enabled

Once testing of both Visa and Mastercard is completed, move to real transaction testing.