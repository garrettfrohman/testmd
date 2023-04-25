---
id: "usersettings"
---

# Configure User Settings

## About

The user settings is a `XML` configuration that is located under `Admin` > `Configuration` > `LocaleConfig`. This configuration is used for specifying user specific configurations for example the export csv separator or the format of the exported date.

## Example config

```xml
<com.devcode.service.config.LocaleConfig>
  <enabled>true</enabled>
  <userSettings>
    <entry>
      <string>default</string>
      <userLocaleSetting>
        <decimalSeparator>.</decimalSeparator>
        <groupingSeparator>,</groupingSeparator>
        <datePattern>yyyy-MM-dd HH:mm:ss</datePattern>
        <csvSeparator>,</csvSeparator>
      </userLocaleSetting>
    </entry>
  </userSettings>
</com.devcode.service.config.LocaleConfig>
```

## Default

If the configuration contains a user settings called `default` then this will be used for all users that does not have its own user settings.

## Adding a user specific user settings

To add a user specific user settings add a `<entry>` inside of the `userSettings` tag. Then add a `<string>` tag and that should contain the username of the user that should have this user settings. Then add a `<userLocaleSetting>` with the the following attributes `<csvSeparator>;</csvSeparator><decimalSeparator>,</decimalSeparator><groupingSeparator> </groupingSeparator>`. Check [here](#attributes) for more info about the specific attributes.

### Example 

```xml
<com.devcode.service.config.LocaleConfig>
  <enabled>true</enabled>
  <userSettings>
    ...
    <entry>
      <string>my-user-name</string>
      <userLocaleSetting>
        <csvSeparator>;</csvSeparator>
        <decimalSeparator>,</decimalSeparator>
        <groupingSeparator> </groupingSeparator>
      </userLocaleSetting>
    </entry>
	...
  </userSettings>
</com.devcode.service.config.LocaleConfig>
```

## Attributes

|Name             |Description                                            |Example            |
|-----------------|-------------------------------------------------------|-------------------|
|csvSeparator     |Csv separator for export of transactions, messages etc.|;                  |
|decimalSeparator |Decimal separator of numbers                           |,                  |
|groupingSeparator|Grouping separator of numbers                          |                   |
|datePattern      |Format of exported dates. The format is a java simple date format. For more info see [here](#datePattern)             |yyyy-MM-dd HH:mm:ss|

### datePattern

|Name             |Description                                            |Example            |
|-----------------|-------------------------------------------------------|-------------------|
|yyyy             |Year in 4 digit format                                 |2020               |
|yy               |Year in 2 digit format                                 |20                 |
|MM               |Month in year                                          |11                 |
|dd               |Day in month                                           |11                 |
|HH               |Hours (0-23)                                           |22                 |
|mm               |Minutes (0-60)                                         |22                 |
|ss               |Seconds (0-60)                                         |22                 |

More examples can be found [here](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html)