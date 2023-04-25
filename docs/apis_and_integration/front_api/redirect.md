---
id: "redirect"
---

# Generic Redirect

Some providers require that the user is redirected to a page hosted by the provider in order to complete the transaction. When a response object contains the property ```redirectOutput``` the user must be redirected as specified otherwise the transaction will be pending and not completed. The redirect object contains following properties:
​

| JSON params | Type    | M/O | Description              |
|-------------|---------|-----|--------------------------|
| container   | String  | M   | The type of container that should handle the redirect. Valid values are `window`,`iframe` or `redirect`, but other values can be added in the future. Most redirects are handled by iframes, but some providers require windows. |
| method      | String  | O1  | Method to use when redirecting to the URL. Valid values are `POST` or `GET`.                                                             |
| parameters  | Object  | O1  | If parameter method is of type `POST` this parameter contains a map with form data that must be included when posting to the URL.        |
| url         | String  | O1  | Redirect URL to be opened when method is `GET`, or submitting form data if method is `POST` using values in `parameters`.                      |
| html        | String  | O2  | HTML page to display if the parameter `url` is null. HTML is very rarely used, and if it's used PaymentIQ can replace it with an URL if wanted, contact support to have it enabled. |
| width       | Integer | O1  | Width of the iframe or window which can be specified in the provider configuration in the PaymentIQ back office. 600 is default          |
| height      | Integer | O1  | Height of the iframe or window which can be specified in the provider configuration in the PaymentIQ back office. 600 is default.        |

**Note: The redirect object either contains properties ```method```, ```parameters```, and ```url```, or property ```html```.**

Example of a POST (iframe) redirect:

```json
{
  "txState": "WAITING_INPUT",
  "redirectOutput": {
    "html": null,
    "url": "https://secure.metacharge.com/mcpe/acs",
    "method": "POST",
    "container": "iframe",
    "parameters": {
      "PaReq": "VGVzdE1vZGVUcmF5+fn4=",
      "TermUrl": "http://dev2.devcode.se/success.html",
      "MD": "MTA4MTI3ODk1MTA4MTI3ODk1MTA4MTI3ODk1MTA4MTI3ODk1MTA4MTI3ODk1:1:2120"
    },
    "width": 600,
    "height": 600,
  },
  "messages": [],
  "txRefId": "1000A27023484",
  "success": true
}
```
Example of a HTML redirect:

```json
{
  "txState": "WAITING_INPUT",
  "redirectOutput": {
    "html": "<html><body><h1>TEST</h1></body></html>",
    "url": null,
    "method": "GET",
    "container": "iframe",
    "parameters": {},
    "height": 600,
    "width": 600
  },
  "messages": [],
  "txRefId": "1000A1002932",
  "success": true
}
```

Example of a POST redirect:

```json
{
  "txState": "WAITING_INPUT",
  "redirectOutput": {
    "html": null,
    "url": "https://secure.metacharge.com/mcpe/acs",
    "method": "POST",
    "container": "redirect",
    "parameters": {
      "PaReq": "VGVzdE1vZGVUcmF5+fn4=",
      "TermUrl": "http://dev2.devcode.se/success.html",
      "MD": "MTA4MTI3ODk1MTA4MTI3ODk1MTA4MTI3ODk1MTA4MTI3ODk1MTA4MTI3ODk1:1:2120"
    },
    "width": 600,
    "height": 600,
  },
  "messages": [],
  "txRefId": "1000A27023484",
  "success": true
}
```

## Post redirect handling
When redirect output has the method `POST`, many providers require the request to be a `form post`. Meaning the post-request must contain the request-header `Content-Type: application/x-www-form-urlencoded'` and the payload must be passed as `form-data`.

This can either be done using for example [axios](https://github.com/axios/axios) to make the reqeust

```
axios({
  method: 'post',
  url: redirectOutput.url,
  data: bodyFormData,
  config: { headers: {'Content-Type': 'multipart/form-data' }}
})
.then(function (response) {
  //handle success
  console.log(response);
})
.catch(function (response) {
  //handle error
  console.log(response);
});
```

Or by generating a `<form />` in your application, creating a hidden input field for every parameter in `redirectOutput`.
Then post the form and put the response into an iframe or a new window/tab.

Or by generating a `<form />` in your application, creating a hidden input field for every parameter in `redirectOutput`.

#### For opening in new window

```
let fields = ''
Object.keys(parameters).forEach(param => {
  fields += `<input type='hidden' name='${param}' value='${parameters[param]}' />`
})

const html = `
  <html><head><title>PaymentIQ Redirect</title></head>
    <body><div>
      <form id='providerRedirectForm' action=${redirectOutput.url} method='post' name='provider-redirect-form-window'>
        ${fields}
      </form>
    </div></body>
  </html>`

this.providerWindow.document.write(html)
this.providerWindow.document.getElementsByName('provider-redirect-form-window')[0].submit()
```

#### For opening in iframe
Specify a target of your form, and set it the the `name` of your iframe. This will put the request-response into the set iframe.

```
let fields = ''
Object.keys(parameters).forEach(param => {
  fields += `<input type='hidden' name='${param}' value='${parameters[param]}' />`
})

<form id={`providerRedirectForm_${this.type}`} action={redirectOutput.url} method='post' target='PROVIDER_IFRAME'>
  {fields}
</form>

<iframe name={`PROVIDER_IFRAME`} class={`provider-iframe ${!this.isLoading && 'visible'}`} onLoad={this.handleIntegrationLoaded} />
```

#### For redirect

##### GET

```
var fields = parameters.map(param => {
  var name = decodeURIComponent(param);
  var value = decodeURIComponent(parameters[param]);
  return `${name}=${value}`
})
window.location = `url?${fields.join('&')}`
```

##### POST

```
var fields = parameters.map(param => {
  return `<input type='hidden' name='${param}' value='${parameters[param]}' />`
}).join('')

const html = `
  <div>
      <form id='providerRedirectForm' action=${redirectOutput.url} method='post' name='provider-redirect-form-window'>
        ${fields}
      </form>
  </div>
  `

document.append(html)
document.getElementById('#providerRedirectForm').submit()
```