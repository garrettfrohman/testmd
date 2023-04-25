---
id: "fraud-provider"
---

# Fraud Provider Rules

The PaymentIQ back office will give you access to 3rd party Risk Management Solutions. Currently, we can offer the services of WorldPay RiskGuardian. Merchants will need an agreement with WorldPay HCG (High Capacity Gateway) in order to be able to set risk scores. To be able to edit the risk score settings, the merchant must login to [WorldPay's RiskGuardian](https://sso1.wpstn.com/login.aspx?ReturnUrl=%2f%3fwa%3dwsignin1.0%26wtrealm%3dhttps%253a%252f%252fadmin1.wpstn.com%252fRGMAT%252f%26wctx%3drm%253d0%2526id%253dpassive%2526ru%253d%25252fRGMAT%25252fHome.aspx%26wct%3d2016-01-04T16%253a14%253a35Z&wa=wsignin1.0&wtrealm=https%3a%2f%2fadmin1.wpstn.com%2fRGMAT%2f&wctx=rm%3d0%26id%3dpassive%26ru%3d%252fRGMAT%252fHome.aspx&wct=2016-01-04T16%3a14%3a35Z) back office with the credentials that have been provided for you to log in.

![](/img/rulesettings/RulesFraudProvider/1.png)

RiskGuardian will provide you with guidelines on to how to set up specific risk scores. When you have the value of the risk score you will be required to set it up in the PaymentIQ back office.  Go to Rules > Routing  > Fraud Provider and select “New”

![](/img/rulesettings/RulesFraudProvider/2.png)

1. Under Conditions, Tx type – select CreditcardDeposit 
2. Under Actions, Fraud provider – select RiskGuardian 
3. Under Fraud Account, select RG. 
4. Under Threshold, you fill in the risk score you have decided to use in the WorldPay BackOffice. For example, if you set 70, players with score over 70 will be declined. You will then see in ‘Status description’ in the PaymentIQ BackOffice - ERR_DECLINED_FRAUD. 
