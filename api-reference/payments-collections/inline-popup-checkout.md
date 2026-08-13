# Inline/Popup Checkout



Inline Checkout lets you accept payment without leaving your page — no redirect, just a JS-powered popup.

### Integration Steps

{% stepper %}
{% step %}
#### Load Inline Script

Include the checkout inline script in your front-end HTML.

```html
<script src="https://api.oneappgo.com/v1/inline-checkout.js"></script>
```
{% endstep %}

{% step %}
#### Initialize Checkout

Trigger the popup by calling the `BolddCheckout()` helper with payment payload.

```javascript
BolddCheckout({
    public_key: 'YOUR_PUBLIC_KEY',
    amount: 5000,
    email: 'customer@example.com',
    // ...
});
```
{% endstep %}

{% step %}
#### Verify Payment on Backend

Upon callback, verify the transaction status programmatically on your backend. Verify Payment
{% endstep %}
{% endstepper %}

### 1. Add the checkout script

```html
<script src="https://js.oneappgo.com/v1/checkout.js"></script>
```

### 2. Add a payment button

```html
<button type="button" onclick="makePayment()">Make Payment</button>
```

### 3. Call BolddCheckout with your transaction details

```javascript
function makePayment() {
  const initpay = BolddCheckout({
    publickey: PUBLIC_KEY,
    amount: 20000,
    fname: "John",
    lname: "Doe",
    customer_email: "johndoe@example.com",
    phone: "09012345678",
    reference: "SH9992IOQP820",
    currency: "NGN",

    onComplete: async (response) => {
      if (response.status && response.responsecode === '01') {
        // Always verify server-side before granting access to goods/services
        await verifyOnServer(response.reference);
      } else {
        alert(response.message);
      }
    }
  });

  initpay.makePayment();
}
```

### Parameters

| Field             | Description                                        |
| ----------------- | -------------------------------------------------- |
| `publickey`       | Your account's public key — see **Authentication** |
| `amount`          | The amount the customer is to pay                  |
| `fname` / `lname` | Customer's first and last name                     |
| `customer_email`  | Customer's email                                   |
| `phone`           | Customer's phone number                            |
| `reference`       | A unique reference you generate per transaction    |
| `currency`        | `NGN` or `USD`                                     |

`onComplete` fires with a JavaScript object once the popup flow finishes.

{% hint style="info" %}
**Always verify server-side.** Even with a successful `onComplete` callback, confirm the transaction on your backend using **Verify Payment** before releasing goods or services — client-side callbacks can be spoofed.
{% endhint %}

{% hint style="danger" %}
**Review:** the legacy docs reference a global `OneAppCheckout()` function name. Renamed to `BolddCheckout()` here to match the rebrand — confirm with the API/frontend team whether the actual shipped JS library has been renamed yet, since publishing the wrong function name would break every integration copying this sample.
{% endhint %}
