---
id: "cashier_add_multiple_configuration_sections"
---

# Add Multiple Configuration Sections in MerchantCashierConfig

You can define multiple different configurations and dynamically apply these in the Payment method rules.
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

