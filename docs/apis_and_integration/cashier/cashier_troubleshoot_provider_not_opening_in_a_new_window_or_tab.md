---
id: "cashier_troubleshoot_provider_not_opening_in_a_new_window_or_tab"
---

# Troubleshoot Provider Not Opening In A New Window Or Tab

Most providers can be configured to be opened in a new window in their providerConfig

```
<container>window</container>
```

This will make the provider be displayed in a new tab.

This is regarded by browsers as a popup which some browser blocks by default. The user can also configure their browser to automatically block popups.

In those cases, the provider window can't be automatically opened without the user manually triggers the popup to be shown, by clicking something. This is limitation we can't get around. When we have detected that the popup was blocked, the cashier will display an additional information text about this with the messagekey `failed_to_open_provider_window`.