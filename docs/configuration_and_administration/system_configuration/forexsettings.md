---
id: "forex_rates"
---

# Forex Rates

## About

As explained in the [Forex Rules](forex), PaymentIQ allows the merchant to perform foreign currency exchanges during transactions if desired.  

The area within PaymentIQ where the merchant can define which currencies have exchange rates downloaded, and edit the exchange rates applied if desired is `Admin > Forex Rates`.

PaymentIQ will provide x number of default exchange rates that will be inherited for each merchant. In the Forex section you can define new exchange rate that PaymentIQ don't provide or manually change a exchange rate to override the PaymentIQ defaults.

![](/img/settingsandadmin/AdminForex/1.png)

## Columns

Here is a explanation of some specific columns.

| Name    | Description                                                                               | Example value               |
|---------|-------------------------------------------------------------------------------------------|-----------------------------|
| Source  | If the exchange rate was imported from a external service or was added from PaymentIQ BO. | `Manual or Imported`        |
| Service | What service that imported the exchange rate or blank if it was PaymentIQ BO.             | `ECB, Riksbanken, NYX etc.` |

## Filter Forex Rates

You can filter the exchange rates based on the rate date. By default it will show the active exchange rates. Pick a other date to show exchange rates for that date.

## Add custom Forex Rates

A new currency can be added using the `Action > Add new`, if required.

![](/img/settingsandadmin/AdminForex/3.png)

The following dialog will be shown. The from currency is your configured default currency (Only one can be defined) in the `ForexConfig > defaultCurrency`. The selectable `To currencies` are configured in your `MerchantConfig > currencies`. The exchange rate will be active when saved.

## Edit Forex Rates

To edit a exchange rate. Double-click the `Buy rate` or `Sell rate` and a input field will be shown where you can enter the new value. When you are done leave the input field. The row should now be marked with green to mark this row as changed. When you are done editing the rows goto `Action > Save changes`. The edited exchange rates will be active when saved.

## Delete Forex Rates

Select the exchange rates you want to delete then goto `Action > Delete`. The exchange rates will be marked as deleted . This can be reverted if this was made by mistake. Please contact the technicalsupport@bambora.com to do that.

## Configuration

The Forex configuration, that determines from where and at what frequency the exchange rates are sourced is defined in the `Admin > Configuration` section of PaymentIQ. You will be able to activate any of the following forex providers and even to identify a fallback:
* Open Exchange Rates (openExchangeRatesForexIntegrationService)
* ECB (ecbForexIntegrationService)
* NYX (nyxForexIntegrationService)
* Riksbanken (riksbankenExchangeRatesForexIntegrationService)

This is generally set by PaymentIQ staff but for reference an example setup is provided below.  Please contact technicalsupport@bambora.com if you have additional specific requirements.

![](/img/settingsandadmin/AdminForex/2.png)
