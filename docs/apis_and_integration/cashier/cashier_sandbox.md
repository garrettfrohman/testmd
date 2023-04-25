---
id: "cashier_sandbox"
---

# Cashier Sandbox

The cashier can be configured by using the cashier sandbox application - a page that lets you play around with the
available settings and get a preview of how it will affect the cashier.

[Configuration App](https://pay.paymentiq.io/cashier-config)

Initially, the page will load with the default configurations along with the cashier next to it.

Play around how much you want with the cashier configs, the theme configs, and also the 'Custom CSS' section.

You can practically change all type of styling with custom CSS. Use the 'Theme' configs as much as possible and leave the rest (advanced work)
to custom CSS. You need to use the devtools to find the correct CSS classes to overwrite those with your own styling.

When you make any type of changes the cashier preview will automatically update.

## Updating The Cashier With JS API

You can also update/change the configurations via the **'JS API'** section who utilizes the api.set() method.
There you will also recieve all types of callbacks loggings that are included in the cashier. (See **'Javascript API'** section.)

Note: Some configs may need manual reload of the cashier to be properly updated in cashier preview when using the 'JS API' section.
Use the purple reload button in the top right corner.

## Saving Your Changes

When you are satisfied with the configurations and want to save them, you can save them as a custom preset.
The preset will be stored locally on your computer but can be shared by exporting it through the 'URL' or the 'Codesnippets' section.

If you want someone else to import your locally saved presets, go to the section "URL", copy that URL and send it to the new user, the user can then go to
the "Import" section and just paste that URL there and the cashier will be updated according to that URL.

You can also import a cashier configuration by using JSON, it's all under the "Import" section.

Note: Custom CSS changes will not be available via the URL. Those are meant to be imported through the bootstrapper via the api.css('...somecss') callback method. As seen in the **'Codesnippets'** section.

**Click the save changes button that will be enabled whenever you make changes in the top right corner**

![](/img/cashier/cashier-config-save.png)

**Write a name and click save preset**

![](/img/cashier/cashier-config-save-preset.png)

**Your preset is now available in the list of presets**

![](/img/cashier/config-was-saved.png)

## Apply The Settings

When you are satisfied with the settings you can head over to the **Codesnippets** section and export it the way you want.

## Use The Preset

See the documentation on cashier initialization on how to use the export in your implementation.