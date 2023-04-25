---
id: "configsteps"
---

# Configuring A PaymentIQ System

The versatility of PaymentIQ inevitably means there are a lot of different types of settings available. This document will give an overview of how settings are made in PaymentIQ and provide a general understanding of how these settings influences the system.


## What is a MID?

When you log into PaymentIQ Backoffice you are given access to one or more MerchantIDs (MIDs). These are the operational unit of PaymentIQ and it is here you will add the settings that are needed. You can see in the top right corner of PaymentIQ there is a drop down menu listing the MIDs you have access to.

Often Merchants will have several brands and PaymentIQ was designed with this in mind. Therefore the default structure is hierarchical with a "Master" MID which under it will have one or more "Sub" or "Brand" MIDs.

![](/img/settingsandadmin/midtree.svg)

The advantages of this is that you can manage backoffice user login access and control which MIDs/brands a user has access too, but also give the option of setting inheritance. For example if a merchant has several brands with their own PaymentIQ MIDs but want to connect them to the same Payment Provider accounts it could be easier to manage this by doing all those setting on the Master MID.

Inheritance and the hierarchical organization of PaymentIQ will be clearer when we cover what specific settings there are.

## What types of settings are there?

In addition to the standard administrator settings, PaymentIQ has two distinct types of settings that control a lot of the system behaviour:

- **Rules:** Comprise of a pairing of "conditions" and "actions", meaning that if a condition is met PaymentIQ will take some action. For example there could be rules to only show certain payment methods to a subset of customers, or rules to send email notifications on alerts. 
- **Configuration Files:** Are XML based settings defining credentials and options. For example you can set email account credentials or provider account settings.

## Merchant checklist for PaymentIQ configuration

Having now gone over some of the peculiar concepts of PaymentIQ we can outline a reasonable checklist for settings that all merchants.

### Decide where to place your rules and configuration settings

Decide if you should add rules and configurations on the Master MID or on the Brand (sub) MID. Most merchants will want to add the configurations on the sub MIDs.

### Add provider configuration files

For each payment provider you intend to use with your brand you will need to add a configuration file specific to that provider. You can add more providers later on or remove ones you no longer intend to use, but since the core feature of PaymentIQ is to provide an interface to payment providers this should be the starting point as other settings will require that there are at least one payment provider available.

The how to [Activate A Provider](../../getting_started/activateprovider) document explains the steps needed.

### Add payment method rules

Now that you have at least one provider configuration with at least one account with that payment provider set up you should add the two core rule types needed for PaymentIQ starting with a payment method rule which controls what is available to chose for the end customer. You can learn about payment method rules and see examples [here](payment-methods).

### Add routing rules

Where the payment method rule specifies what is available to chose, the payment method rule specifies which provider account to use in the transaction. You can learn about routing rules and see examples [here](routing).

### Test, repeat

With at least one provider configured, one payment method rule set to make sure that provider is available to the end user and at least one routing rule set to specify which account should be used with that provider you now have a complete minimal configuration of PaymentIQ ready and can test to make sure you can get a transaction through without errors.

If you can get a transaction through you can repeat these steps:

- Adding a payment provider account, specifying what provider credentials to use
- Adding a payment method rule, controlling what user can use a specific method
- Adding a routing rule, mapping what account to use when a user makes a transaction
- Test, to make sure you can get a successful transaction

With all the payment providers you intend to use.

### Add additional rules

With the core functionality configured and verified to be working it is now a good time to check what other types of rules may be of use for your setup. Have a look in the Rules dropdown in the left sidebar for this page and go over the rules available. Just as with Routing rules you add conditions and actions to define the behaviour. You may want to add Limit rules to certain customers or alerts that go to your mailboxes.

