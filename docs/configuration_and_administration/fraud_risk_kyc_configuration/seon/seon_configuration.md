---
id: "seon_configuration"

---

# Seon Configuration


There are some setup steps that needs to be done on the merchant's site to activate Seon. 

## Configuration in PaymentIQ

Please contact our technical support team for assistance with this configuration.

### Example Configuration file

```xml
  <com.devcode.paymentiq.integration.seon.DiDSeonConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
      <accounts>
        <entry>
            <string>default</string>
          <account>
            <serviceEndpoint>https://demo-api.gii.cloud/api/data-sources/userinfo</serviceEndpoint>
            <username>???</username>
            <password>???</password>
          </account>
        </entry>
   </accounts>
  </com.devcode.paymentiq.integration.seon.DiDSeonConfig>
```

### Attributes

| Attribute       | Description                                 |
|-----------------|---------------------------------------------|
| serviceEndpoint | Provider URL                                |
| username        | User name provided by DevCode Identity      |
| password        | Password provided by DevCode Identity       |

### Seon's extra parameters

Merchants can submit extra data to Seon by implementing Seons' JavaScript Agent v4 API. The API details can be found at: https://developers.seon.io/#javascript-agent-v4 . In order to activate sending such data, the merchant should send the session_id and session value to PaymentIQ.

`session_id`: Session ID is a custom, unique ID that links a user’s device data with transactions. It should be based on the user’s current browsing session, by tracking cookies for example. If you are using JavaScript Agent v4, send the encrypted payload returned by the SDK (supported by JS Agent v4, iOS SDK 3.0.0, Android SDK 3.0.0) in the session field instead of the session_id.

`session`: This field should contain the base64 encoded session data returned by the SDKs. This is only compatible with Fraud API v2.0 and can be retrieved by calling seon.getBase64Session().


## From Seon's documentation:

To activate Seon's JavaScript Agent v4 API, you need to include agent.js script in your project:

```html
<html>
  <head>
    ...
    <script src="https://cdn.seon.io/js/v4/agent.js"></script>
  </head>
  <body>
    ...
  </body>
</html>
```

Don’t forget to replace [session_id] with your unique session identifier. We recommend to use UUID, but you can use your own implementation as well.

Seon session setup:

```
seon.config({
  session_id: "[session_id]",
  audio_fingerprint: true,
  canvas_fingerprint: true,
  webgl_fingerprint: true,
  onSuccess: function(message) {
    console.log("success", message);
  },
  onError: function(message) {
    console.log("error", message);
  }
});
```


Retrieving Seon's session value:

```
seon.getBase64Session(function(data) {
  if (data) {
    console.log("Session payload", data);
  } else {
    console.log("Failed to retrieve session data.");
  }
});
```

## PaymentIQ attributes:

Seon's `session_id` and `session` fields should be sent to PaymentIQ as attributes with the following corresponding names: `SeonSessionId` and `SeonSession`.

`SeonSessionId` represents merchants own generated session_id that is submitted through JavaScript agent API.

`SeonSession` represents the value retrieved from Seon's JavaScript agent API, which is retrieved by triggering seon.getBase64Session().
