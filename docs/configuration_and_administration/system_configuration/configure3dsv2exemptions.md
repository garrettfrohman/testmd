---
id: "configure3dsv2exemptions"
---

# Configuring Exemptions for 3DS2

<video src="/video/3ds2/3ds2_limitingthenumberofexemptiontransactionsandusingsca.mp4" controls muted preload/>

## General

Exemptions are requests for a certain action to be performed on a 3DS2 transaction. They are *requests only* and the issuer is not obligated to act on them.

There is usually an associated additional scheme cost with requesting an exemption. This is levied by Visa and Mastercard themselves through your acquirer.

Exemptions are fully supported from 3DS2 v2.2

Some exemptions (Low Value) on authorization are supported from 3DS2 v2.1 (current). 

Note that some acquirers, such as Worldpay, will need to enable exemption support for a merchant MID in their own systems.

## Types of Exemptions

**Low Value Exemption**

This is an exemption on the *authorize* request, and is equivalent to requesting that a transaction be processed Non 3DS

Only used for transactions under €30 value.

*Might* be enacted by default by the card issuer, leaving an exemption request superfluous. 

**How to enable LVA exemptions**

- clone 3DS2 account within the pspConfig
- Rename it 3DS2LVX (or anything you like)
- Add a parameter `<scaExemption>LOW_VALUE_PAYMENT</scaExemption>` within the `<account>` section
- Route transactions to 3DS2LVX to request a low value exemption

**Transaction Risk Analysis Exemption (available from v2.2)**

Used to request a frictionless transaction ostensibly based on a prior risk assessment of the transaction.

Not all acquirers support this. 
There is a sliding scale of allowable transaction values that allow an exemption request, and these are determined by your acquirer. Visa guidelines are;

![](/img/3dsv2/exemption1.png)

Some acquirers have built their own risk analysis engine and require this to be used

- clone 3DS2 account within the pspConfig
- Rename it 3DS2TRX
- Add a parameter `<scaExemption>TRANSACTION_RISK_ANALYSIS</scaExemption>` within the `<account>` section
- Route transactions to 3DS2TRX to request a Risk Analysis exemption
- as of 3DS2 v2.1 this is an exemption request on the authorize transaction, equivalent to a N3DS transaction.

## Fallback to Strong Customer Authentication

If an exemption gets a failure response from the issuer indicating `ERR_DECLINED_SCA_REQUIRED_BY_ISSUER` then this can be used to reprocess the transaction using the full 3DS2 SCA flow.

- Create a routing rule that will redirect these types of transaction back to a full 3DS2 flow
- Create the rule with specific parameters according to the acquirer that the merchant uses
- An example rule for Bambora fallback would look like;

![](/img/3dsv2/exemption2.png)

## Forced Challenge Request

It is also possible to request an SCA (Strong Customer Authentication) challenge during a transaction and try to force the challenge flow.

This is principally used for zero-auth authentication transactions such as are seen in a subscription model business, on the initial transaction when a card is registered.

- clone 3DS2 account within the pspConfig
- Rename it 3DS2SCA
- Add a parameter `<threeDS2TemplateName>3ds2_force_challenge</threeDS2TemplateName>` within the `<account>` section
- Route transactions to 3DS2SCA to request a forced challenge

## Complying with the limitations of Exemptions

PSD2 allows for exemption of SCA on transactions with an amount lower than EUR 30 with the following limitation:

“Transactions up to €30 do not require SCA up to a maximum of 5 consecutive transactions or a cumulative value limit of €100 since the last application of SCA.”

Effectively this means that the merchant should apply SCA at least on every 6th transaction or when a customer transaction would exceed €100 of exemptions in a row.  Unfortunately, PIQ does not support counting the Euro value of transactions since the last SCA challenge but does support doing so based on the number of transactions.  Using this transaction limit, we can approximate the regulatory requirements, while actually being slightly more cautious than necessary to ensure that we do not exceed them.

Using the custom condition ‘Transaction count in a row on PSP account in history’ as in the below rule example we can set the count to a maximum of 3 exempt transactions (max €30 x 3 < €100). When used in combination with the merchants normal routing placed below this rule, this will ensure compliance.

Note that due to the nature of the rule logic, the actual ‘Transaction Count’ value should be one less than the required 3.

This will result in the user hitting the rule after 3 Low Value Exemptions in a row, and then being directed to an SCA MID (configured to Force a challenge, see above)

Of course, the actual values for PSP and PSPAccount may vary according to that which you have configured within the respective PSPConfig that applies.  In the examples above, we have used the recommended terminology.

![](/img/3dsv2/exemption3.png)

This will result in the user hitting the rule after 3 Low Value Exemptions in a row, and then being directed to an SCA MID (configured to Force a challenge, see above).

Your 'standard' Low value exemption rule should be below the exemption rule, to catch those transactions below 30 EUR that you wish to exempt.

![](/img/3dsv2/exemption4.png)

Of course, the actual values for PSP and PSPAccount may vary according to that which you have configured within the respective PSPConfig that applies. In the examples above, we have used the recommended terminology.