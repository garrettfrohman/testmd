---
id: "configuration"
---

# Configuration

The configuration tab is where merchant specific technical details are stored in PaymentIQ.

Warning: This area is very technical in nature and under normal circumstances should only be edited by members of PaymentIQ staff. A mistake in this area can lead to unforeseen consequences that may include the cessation of transaction processing.

As a brief explanation the menu items on the left include the XML setting details for the PaymentIQ merchant configurations, from specific PSP settings, to merchant setup details, and settings for how your merchants version of PaymentIQ is structured.

It is recommended that only the most confident of merchant users make any changes to this area whatsoever.

![](/img/settingsandadmin/AdminConfiguration/1.png)

## Masked config

Merchants sensitive config data in PaymentIQ backoffice has been masked. Like password or secretKey. Here is a example how a masked secretKey looks like this in the configuration view:

```XML
<secretKey id="f872f22e-c8c6-432c-91c0-228342054550">*****</secretKey>
```
To replace for example the value of the secret key just replace the `*****` with the value you want to replace it with. You don't need to remove the `id="f872f22e-c8c6-432c-91c0-228342054550"`. 

## Link id’s to to your own back-office

It is now possible to make user id’s a clickable link to your own back-office.
What is needed is a small configuration in your merchant-config and it could look something like this:

```XML
<externalUrls>
   <externalUrl>
      <column>User</column>
      <url>https://payment.myownbackoffice.com/api/customer/{User}</url>
      <title>Your tooltip message</title>
      <target>external</target>
   </externalUrl>
</externalUrls>
```

Where {User} is a mapping to the user-id column in PaymentIQ.
So copy a link to a user from your own back-office and replace the id with {User}

The result in PaymentIQ will look something like this:

![](/img/settingsandadmin/AdminConfiguration/2.png)

Another option is to link from the PSP ref-id column.

```XML
<externalUrls>
   <externalUrl>
      <column>PSP ref-id</column>
      <url>https://payment.myownbackoffice.com/api/customer/{PSP ref-id}</url>
      <title>Your tooltip message</title>
      <target>external</target>
   </externalUrl>
</externalUrls>
```

## Whitelist ip-addresses

It is possible to whitelist certain IP-addresses in your merchant-config. Do not remove the default whitelistIpAddress config if it exist, since this is needed for default behaviour to allow all IP-address to login. The syntax for whitelisting IP-addresses is configured by writing regex.

To whitelist all IP-addresses by default:
```XML
<whitelistIpAddresses></whitelistIpAddresses>
```

Can also be written as:
```XML
<whitelistIpAddresses>.*</whitelistIpAddresses>
```

To whitelist a certain IP-address:
```XML
<whitelistIpAddresses>150.123.31.13</whitelistIpAddresses>
```

To whitelist multiple IP-address:
```XML
<whitelistIpAddresses>150.123.31.13|20.33.11.143</whitelistIpAddresses>
```

To whitelist IP-address range, e.g 150.123.31.0/24:
```XML
<whitelistIpAddresses>150.123.31.([0-9]|[1-9][0-9]|1([0-9][0-9])|2([0-4][0-9]|5[0-5]))$</whitelistIpAddresses>
```

Can also be written as:
```XML
<whitelistIpAddresses>150.123.31.*</whitelistIpAddresses>
```

To whitelist IP-address range, e.g 150.123.31.32/24:
```XML
<whitelistIpAddresses>150.123.31.(3[2-9]|[4-5][0-9]|6[0-3])$</whitelistIpAddresses>
```

Can also be written as:
```XML
<whitelistIpAddresses>150.123.31.*</whitelistIpAddresses>
```
