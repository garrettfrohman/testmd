---
id: "cashier_use_merchantcashierconfig"
---

# Configure The Cashier In PaymentIQ Backoffice

**Available from**: `version 1.1.0`

**Required settings**: `fetchConfig: true`

You can configure the cashier in PaymentIQ backoffice, allowing you to update your configuration on the fly.

The Cashier requires to be setup using the [Boostrapper script](cashier_init_bootstrapper) with with a few key settings defined:

* [environment](cashier_parameter_details#environment)
* [merchantId](cashier_parameter_details#merchantid)
* [userId](cashier_parameter_details#userid)
* [sessionId](cashier_parameter_details#sessionid)
* [method](cashier_parameter_details#method)
* [fetchConfig: true](cashier_parameter_details#fetchconfig)

If you require a specific size of the cashier, you must also specify this during setup

* [containerWidth](cashier_parameter_details#containerwidth) (optional, defaults to 100% of its parent element)
* [containerHeight](cashier_parameter_details#containerheight) (optional, defaults to 100% of its parent element)

If you use a custom [font](cashier_parameter_details#font) that must also be configured during setup and not in PaymentIQ Backoffice.

From **version 1.1.1** you can also add a **css** tag to the **MerchantCashierConfig** file with custom CSS that would otherwise be
handled via the [cashiers API](cashier_javascript_api).

## Setup MerchantCashierConfig in PaymentIQ Backoffice
In PaymentIQ backoffice, navigate to **Admin** -> **Configuration**. Add a new file called **MerchantCashierConfig** with:

```xml
<com.devcode.paymentiq.service.cashier.MerchantCashierConfig>
  <enabled>true</enabled>
  <checkIfFirstDeposit>false</checkIfFirstDeposit>
  <css>
    .tabs {
      background: #333333;
      color: #ffffff;
    }
  </css>
  <config>
    {
      "amount": 10,
      "tabs": true,
      "theme": {
        "input": {
          "color": "#222"
        },
        "labels": {
          "color": "#ffffffcc"
        },
        "headings": {
          "color": "#ffffffcc"
        },
        "loader": {
          "color": "#f0cc11"
        },
        "buttons": {
          "color": "#f0cc11"
        },
        "headerbackground": {
          "color": "#2f3333"
        },
        "background": {
          "color": "#2e3436"
        },
        "cashierbackground": {
          "color": "#2e3436"
        }
      }
    }
  </config>
</com.devcode.paymentiq.service.cashier.MerchantCashierConfig>
```

Any configuration added here will be applied to the cashier that targets the same merchantId as specified during setup, except for **environment**, **merchantId**, **userId**, **sessionId** and **method (deposit/withdrawal)**

Any configuration included during setup will take precedence over config in PaymentIQ Backoffice.

You can also copy a complete **MerchantCashierConfig** file from [cashier sandbox page](https://pay.paymentiq.io/cashier-config/configs)
in the **Codesnippets** section and then select **MerchantCashierConfig XML** as output format.

## Multiple configuration sections in PaymentIQ Backoffice

You can also define multiple different configurations and dynamically apply these in the Payment method rules.
For example - use different configurations for deposit / withdrawal, for different countries or any other properties available in the Payment method rules tool.

**Example containing 3 different configs called** `Deposit`, `Withdrawal` and `BlankExample`. The name is set in the <string>{CONFIG_NAME}</string>
```xml
<com.devcode.paymentiq.service.cashier.MerchantCashierConfig>
    <enabled>true</enabled>
    <checkIfFirstDeposit>true</checkIfFirstDeposit>
    <configs>
    <!-- Add different cashiers as 'entry' -->
      <entry>
        <string>Deposit</string> <!-- Set the name of the cashier. This will be what you use in Payments Methods rules to call the version -->
        <cashierConfigEntry>
          <config>
            <!--Config for deposits-->
            {
              "listType": "grid"
            }
          </config>

          <css>
          </css>
        </cashierConfigEntry>
      </entry>
 <!-- This is the end of the first entry -->      
 
      <entry>
        <string>Withdrawal</string>
        <cashierConfigEntry>
          <config>
            <!-- Config for Withdrawal  -->
              {
              	"singlePageFlow": "true"
              }
          </config>
        </cashierConfigEntry>
      </entry>
   
      <!-- This is what you would copy for adding a new config -->
            <entry>
              <string>BlankExample</string>
              <cashierConfigEntry>
                <config>
                  {}
                </config>
                <css>
                  
                </css>
              </cashierConfigEntry>
            </entry> 
      <!-- End of BlankExample -->

      </configs>
</com.devcode.paymentiq.service.cashier.MerchantCashierConfig>
```

These can then be targeted in PaymentIQ Backoffice -> Payment Methods. For example, apply `Deposit` for when Payment method is Deposit

![](/img/cashier/cashier-piq-config-payment-rules.png)

