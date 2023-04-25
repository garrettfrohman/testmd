---
id: "cashier_theming"
---

# Theming And Styling

The PaymentIQ Cashier can be styled and themed to almost anything you want. It does however require some web & coding knowledge to customize the look&feel beyond what the built in theme properties can cater to.

If you wish a more in depth rework of the look-and-feel, we can do this as a service but it is not included in the onboarding.
Reach out to your account manager to get a price estimate.

Play around with theming over at the [configuration application](https://pay.paymentiq.io/cashier-config).

Toggle open **Theme color settings**, pick the colors you want and then head over to [Usage --> Api](https://pay.paymentiq.io/cashier-config/usage/api) to get the code.

## Custom colors and properties

During setup, the cashier accepts a theme object containing elements and properties for those, mostly colors (hex, rgb(a) or hsla) for certain element types.

The Button color theme-property must be set using HEX since we use the provided value to calculate corresponding :hover and :active color.

### input
Sets the text color of all input & dropdown fields.

Default:

```css
input: {
  color: '#222324',
  fontSize: '14px',
  height: '52px',
  borderRadius: '0px'
}
```

### inputbackground
Sets the background color of all input & dropdown fields

Default:

```css
inputbackground: {
  color: '#ffffff'
}
```

### labels
color of all labels

Default:

```css
labels: {
  color: '#424242',
  fontSize: '12px'
}
```

### headings
color of all headers

Default:

```css
headings: {
  color: '#333',
  fontSize: '14px'
}
```

### loader
color of spinners

Default:

```css
loader: {
  color: '#9c72b6'
}
```

### error
color of error boxes

Default:

```css
error: {
  color: '#ff2e56'
}
```

### buttons
color of all buttons

Default:

```css
buttons: {
  color: '#ffffff'
}
```


### headerbackground
If a a logoUrl is defined, a logo will be displayed in a header above the cashier.
That header will get the background color set for headerbackground.

Default:

```css
headerbackground: {
  color: '#ffffff'
}
```

### background
If a logoUrl is defined, and the cashier is displayed in full view, the container around the cashier will get the background-color
set for background.

Default:

```css
background: {
  color: '#ffffff'
}
```

### cashierbackground
The main background-color of the contents of the cashier. If no payment method is toggle open, this will be the background-color shown.

Default:

```css
cashierbackground: {
  color: '#ffffff'
}
```

### border radius
Global value for border-radius for buttons, dropdowns and other elements.

Default:

```css
border: {
  radius: '4px'
}
```

### margins
Global value for margin between elements, mainly used for space between items vertically.

Default:

```css
margin: {
  size: '14px'
}
```

### cardbackground
The background-color for each payment method when toggled open.
If **cashierbackground** is set, it's advised to pick a slightly lighter/darker color for cardbackground.

Default:

```css
cardbackground: {
  color: 'transparent'
}
```

### creditcardicons
Set custom icons for credit card fields.

Value must match filename and filetype of an uploaded file on PaymentIQ's CDN (ask your support/onboarding agent for help)


**Default**

```css
creditcardicons: {
  creditcardUrl: 'default',
  cvvUrl: 'default',
  expirydateUrl: 'default'
}
```
**Example**

```css
creditcardicons: {
  creditcardUrl: 'someIcon.png',
  cvvUrl: 'anotherIcon.svg',
  expirydateUrl: 'foobar.jpg'
}
```

This was updated on cashier version 1.1.11, earlier versions supported passing in any arbitrary URL to any logo.

## Theme examples

```js
var CashierInstance = new _PaymentIQCashier('#cashier',
  {
    "environment": "test",
    "theme": {
      "input": {
        "color": "#17191B"
      },
      "inputbackground": {
        "color": "#D1F0F9"
      },
      "buttons": {
        "color": "#07000B"
      },
      border: {
        "radius": "6px"
      },
      margin: {
       "size": "12px"
      }
    }
  },
  (api) => {}
)
```

Or a more complex example:

```js
var CashierInstance = new _PaymentIQCashier('#cashier',
  {
    "environment": "test",
     "theme": {
       "input": {
         "color": "#222",
         "height": "48px",
         "borderRadius": "4px"
       },
       "inputbackground": {
         "color": "#FFFFFF"
       },
       "labels": {
         "color": "hsla(0,0%,100%,.7)",
         "fontSize": "11px"
       },
       "headings": {
         "color": "hsla(0,0%,100%,.7)",
         "fontSize": "13px"
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
       },
       border: {
         "radius": "5px"
       },
       margin: {
         "size": "12px"
       }
     }
  },
  (api) => {}
)
```

## Custom CSS
You can also pass in  your custom CSS using the cashier's Javascript API.

```js
var CashierInstance = new _PaymentIQCashier('#cashier',
  {
    "environment": "test",
    "theme": {
      "input": {
        "color": "#17191B"
      },
      "inputbackground": {
        "color": "#D1F0F9"
      },
      "buttons": {
        "color": "#07000B"
      }
    }
  },
  (api) => {
    api.css(`
      * {
          font-family: monospace;
      }

      body {
        font-size: 1.2em;
      }
    `)
  }
)
```

## Re-assign CSS variables

You can manually re-assign a value of a defined CSS-variables by using the javascript API: `api.css()`

```css
api.css(`
  :root {
    --border-color: transparent !important;
  }
`)
```

Some css-variables we calculate based on the theme-values. These can also be re-assigned. See the defined css-variables by inspecting the cashiers DOM-tree in your browsers dev tools.

### Define variables for credit card fields

**Available from Cashier version 1.1.9**

The input fields shown for credit card payments are read from a secure PCI-environment. This means they are displayed from another domain as iframes.
Because of this, they can't be customized with the passed in custom CSS.

We allow you to re-assign a few CSS-variables for these fields:

```css
--hosted-fields-border-color: #fff; // defaults to the value of --border-color
--hosted-fields-border-focus-color: #fff; // not defined by default, fallback to calculated shade of --border-color
--hosted-fields-border-error-color: #fff; // not defined by default, fallback to calculated shade of --error-color
```
