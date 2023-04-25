---
id: "liveprodtest3dsv2"
---

# Live Production Testing of 3DS2

## Live routing best practices

- Once tested, it is best to 'turn on' 3DS2 for a significant section of customers for some hours, in order to gather data on how 3DS2 is performing.
- A merchant should create a routing rule to send cards to the 3DS2 MID created in the live 'testing' phase
- Once this is enabled, monitor the transactions as they occur.  This can best be done by searching for Type=ThreeDSAuthentication in the Transactions view in PIQ
- There are also Analytics dashboards called;
    - 3DS2 Graphical Overview - Begins to be populated after a day. Set the timeframe correctly.
    - 3DS2 Activity - Pie chart with transaction status breakdown
- If there are more than expected failures, then the merchant can go back and revert the rule that has been routing to 3DS2 using 'History' in the ruleset
- The purpose of this initial testing is to gather data on which BINs or issuing bank perform well with 3DS2, so it is important to have examples of transactions, even if they include failures.
- After a few hours the 'test' rules can be turned off and the merchant should analyse the data.  Usually looking at the data on a BIN level is useful for identifying BINs that perform well with 3DS2, and those that appear to have issues.
- BINs identified as performing well should have a new BIN specific routing rule added so that 3DS2 can be turned on for those BINs
- For non-performing BINs the failure reasons should be analysed to see if these are 'standard' reasons or if there are technical issues with the 3DS2 implementation.
- Report any seeming technical issues to the TechnicalSupport Email ensuring to use 3DS2 in the subject line
- Over time the activation of 3DS2 can be refined and optimised in this way.

Understanding the results of testing - Video Walkthrough

<video src="/video/3ds2/3ds2_understandingtheresultsoftesting.mp4" controls muted preload/>
