# Integrate Apple Pay with JavaScript SDK for direct merchants

## Apple Pay integration

<table>
  <tr>
    <td>
      <p>
        Apple Pay is a mobile payment and digital wallet service provided by Apple Inc.
      </p>
      <p>
        Buyers can use Apple Pay to make payments on the web using the Safari web browser or an iOS device.
      </p>
      <p>
        Sellers can use Apple Pay to sell:
      </p>
      <ul>
        <li>Physical goods, such as clothes and electronics.</li>
        <li>Digital goods, such as software.</li>
        <li>Intangible professional services, such as concerts or gym memberships.</li>
      </ul>
      <a target="_blank" href="https://developer.apple.com/documentation/passkit/apple_pay">Visit this site</a> for more information about Apple Pay.
    </td>
    <td>
      <img src="https://www.paypalobjects.com/ppdevdocs/img/applepay-sheet-xxl-m.png" alt="Completed Apple Pay checkout integration" width="800"/>
    </td>
  <tr>
</table>

### Supported countries and currencies

Apple Pay supports payments in 32 countries and 22 currencies:

* **Countries:** Australia, Austria, Belgium, Bulgaria, Canada, Cyprus, Czech Republic, Denmark, Estonia, Finland, France, Germany, Greece, Hungary, Ireland, Italy, Latvia, Liechtenstein, Lithuania, Luxembourg, Malta, Netherlands, Norway, Poland, Portugal, Romania, Slovakia, Slovenia, Spain, Sweden, United States, United Kingdom
* **Currencies:** `AUD`, `BRL`, `CAD`, `CHF`, `CZK`, `DKK`, `EUR`, `GBP`, `HKD`, `HUF`, `ILS`, `JPY`, `MXN`, `NOK`, `NZD`, `PHP`, `PLN`, `SEK`, `SGD`, `THB`, `TWD`, `USD`

> **Tip:** If you want to integrate additional methods of accepting payment beyond Apple Pay, visit our <a href="https://developer.paypal.com/docs/checkout/advanced/integrate/" target="_blank">Advanced Checkout guide</a> for additional integration choices.

## How it works

<table>
  <tr>
    <td>
    <p>
      The Apple Pay button shows up on your website when a customer uses the Safari web browser on an eligible device.
    </p>
    <p>
      When your buyer selects the Apple Pay button:
    </p>
    <ol>
      <li>
        Your website shows the buyer a payment sheet.
      </li>
      <li>
        The buyer confirms the purchase details, such as the shipping address and payment method.
      </li>
      <li>
        The buyer authorizes the purchase on the payment sheet.
      </li>
    </ol>
    <p>
      The payment sheet helps streamline the checkout process by showing the customer the information needed to make the payment.
    </p><p>
      Payment sheets can show the user's name, address, shipping information, and email address. You can customize this payment sheet to include the user details and payment information you need for your Apple Pay integration.
    </p>
    <p>
    <a href="https://support.apple.com/en-us/HT208531" target="_blank">Visit this site</a> for more details about Apple Pay's compatibility.
    </p>
    </td>
    <td>
      <img src="https://www.paypalobjects.com/ppdevdocs/img/applepay_mobile.png" alt="Screenshot of an Apple Pay payment sheet on a mobile device" width="400"/>
    </td>
  </tr>
</table>

## Know before you code

Apple Pay works on Safari browsers and the following versions of iOS devices:

<ul>
  <li>
    macOS 10.14.1 and later.
  </li>
  <li>
    iOS 12.1 and later.
  </li>
</ul>

<a href="https://support.apple.com/en-us/HT208531" target="_blank">
<button type="button">Check Compatibility</button>
</a>

<br />
Currently supports Apple Pay one-time payments with the buyer present.

<ul>
  <li>
    <a href="https://www.apple.com/legal/applepayments/" target="_blank">Review Apple's terms and conditions for the Apple Pay platform.</a>
  </li>
  <li>
    <a href="https://developer.apple.com/app-store/review/guidelines/" target="_blank">See Apple's developer terms for more information.</a>
  </li>
</ul>

## 1. Set up your sandbox account to accept Apple Pay

Before you can accept Apple Pay on your website, verify that your sandbox business account supports Apple Pay. Use the PayPal Developer Dashboard to set up your sandbox account to accept Apple Pay.

<ol>
  <li>Log into the <a target="_blank" href="https://developer.paypal.com/dashboard/applications/sandbox">PayPal Developer Dashboard</a> and go to your sandbox account.</li>
  <li>Go to <strong>Apps & Credentials</strong>.</li>
  <li>Make sure you are in the PayPal sandbox environment by selecting <strong>Sandbox</strong> at the top.</li>
  <li>Select or create an app.</li>
  <li>Scroll down to <strong>Features</strong> and check if Apple Pay is enabled. If Apple Pay isn't enabled, select the <strong> Apple Pay</strong> checkbox and select the <strong>Save</strong> link to enable Apple Pay.</li>
</ol>

If you created a sandbox business account through <a target="_blank" href="https://sandbox.paypal.com/">sandbox.paypal.com</a>, and the Apple Pay status for the account shows as disabled, <a target="_blank" href="https://www.sandbox.paypal.com/bizsignup/add-product?product=payment_methods&capabilities=APPLE_PAY&_ga=1.255056589.491931369.1702610895">complete the sandbox onboarding steps</a> to enable Apple Pay.

> **Tip:** When your integration is ready to go live, read the <strong>Go live</strong> section for details about the additional steps needed for Apple Pay onboarding.

## 2. Getting started in your testing environment

Before you develop your Apple Pay on the Web integration, you need to
complete <a href="https://developer.paypal.com/api/rest/" target="_blank">Get started</a> to set up your PayPal account, client ID, and sandbox emails for testing.

<ol>
  <li>
    <strong>Download and host</strong> the domain association file for your sandbox
    environment.
  </li>
  <li>
    <strong>Register your sandbox domain.</strong>
  </li>
  <li>
    <strong>Create an Apple Pay sandbox account</strong> for testing. You don't need
    an Apple developer account to go live.
  </li>
</ol>

> **Important:** You need to verify any domain names that you want to show an Apple Pay button. Apple rejects payments from unverified domains. The Apple Pay payment method won't work if the domain isn't registered.

### Download and host sandbox domain association file

<ol>
  <li>
    Download the domain association file for your sandbox environment.
  </li>
  <li>
    Host the file on your test environment at <code>/.well-known/apple-developer-merchantid-domain-association.</code>
  </li>
</ol>


<a href="https://paypalobjects.com/devdoc/apple-pay/sandbox/apple-developer-merchantid-domain-association" target="_blank">
<button type="button">Download</button>
</a>

### Register your sandbox domains

<ol>
  <li>Go to your PayPal Developer Dashboard.</li>
  <li>
    Register all high-level domains and subdomains that show the Apple
    Pay button, such as businessexample.com and
    checkout.businessexample.com.
  </li>
  <li>
    After the domains and subdomains are registered, you can test the
    Apple Pay buttons after you register the domains and subdomains.
  </li>
</ol>

## Create Apple Pay sandbox account

Create an Apple Pay sandbox account on the Apple Developer website to get
a test wallet and test cards to test your Apple Pay integration.

If you already have an Apple sandbox account, you can use that account and
move on to the next step.

<ol>
  <li>
    Create an <a href="https://developer.apple.com/" target="_blank">Apple developer account</a>.
  </li>
  <li>
    Create an <a href="https://developer.apple.com/apple-pay/sandbox-testing/" target="_blank">Apple sandbox account</a>.
  </li>
  <li>Get test cards from your Apple sandbox account.</li>
</ol>

## 3. Integrate Apple Pay checkout

Follow this integration process to add Apple Pay as a checkout option,
customize the payment experience, and process payments.

> **Important:** You can find a complete example in the <a target="_blank" href="https://github.com/paypal-examples/applepay">GitHub repo</a>.

### Call the Orders API

To accept Apple Pay directly on your website, create API endpoints on your
server that communicate with the <a href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">PayPal Orders V2 API</a>. These endpoints can create an order, authorize payment, and capture payment
for an order.

### Server-side example (Node.js)

The following example uses the <a href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">PayPal Orders V2 API</a> to add routes to an Express server for creating orders and capturing payments.

#### server.js

```javascript
import * as PayPal from "./paypal-api.js";\n
/* Create Order route Handler */
app.post("/api/orders", async (req, res) => {
  const order = await PayPal.createOrder();
  res.json(order);
});\n
/* Capture Order route Handler */
app.post("/api/orders/:orderID/capture", async (req, res) => {
  const {
    orderID
  } = req.params;
  const captureData = await PayPal.capturePayment(orderID);
  res.json(captureData);
});
```

#### paypal-api.js

```javascript
// create an order
export async function createOrder() {
  const purchaseAmount = "100.00";
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v2/checkout/orders\`\;
  const response = await fetch(url, {
    method: "post",
    headers: {
      "Content=Type": "application/json",
      Authorization: \`Bearer \${accessToken}\`\,
    },
    body: JSON.stringify({
      intent: "CAPTURE",
      purchase_units: [
        {
          amount: {
            currency_code: "USD",
            value: purchaseAmount,
          },
        },
      ],
    }),
  });
  const data = await response.json();
  return data;
}\n
// capture payment for an order
export async function capturePayment(orderId) {
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v2/checkout/orders/\${orderId}/capture\`\;
  const response = await fetch(url, {
    method: "post",
    headers: {
      "Content-Type": "application/json",
      Authorization: \`Bearer \${accessToken}\`\,
    },
  });
  const data = await response.json();
  return data;
}
```

## 4. Set up your Apple Pay button

You need to Integrate with the Apple Pay JavaScript SDK and PayPal
JavaScript SDK to add Apple Pay to your site.

### Integrate PayPal JavaScript SDK

Use this script to integrate with the PayPal JavaScript SDK:

```html
<script src="https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID&currency=USD&buyer-country=US&merchant-id=SUB_MERCHANT_ID&components=applepay"></script>
```

Include <code>applepay</code> in the <code>components</code> list.

### Integrate Apple JavaScript SDK

Use this script to integrate with the Apple JavaScript SDK:

```html
<script src="https://applepay.cdn-apple.com/jsapi/v1/apple-pay-sdk.js"></script>
```

PayPal's Apple Pay component interacts with your JavaScript code in 4
areas:

<ol>
  <li>
    Checking merchant eligibility for Apple Pay: <code>paypal.Applepay().config()</code>.
  </li>
  <li>Creating an Apple Pay session.</li>
  <li>
    Handling the <code>onvalidatemerchant</code> callback: <code>paypal.Applepay().validateMerchant()</code>.
  </li>
  <li>
    Handling the <code>onpaymentauthorized</code> callback: <code>paypal.Applepay().confirmOrder()</code>.
  </li>
</ol>

Before you show the Apple Pay button, make sure that you can create an
Apple Pay instance and that the device can make an Apple Pay payment.

Use <code>ApplePaySession.canMakePayments</code> to check if the device
can make Apple Pay payments.

> **Tip:** When testing, you need to be logged into the iCloud account for your testing environment. Testing in the sandbox requires you to log into an <a target="_blank" href="https://developer.apple.com/apple-pay/sandbox-testing/">iTunes Connect sandbox tester account</a>, which you can create with an <a target="_blank" href="https://developer.apple.com/help/account/">Apple Developer account</a>. When you test in a live environment, log into a live iCloud account.

Check for device and merchant eligibility before setting up the Apple Pay
button.

To check eligibility, use the PayPal JavaScript SDK API <code>paypal.Applepay().config()</code>.

```html
<div id="applepay-container"></div>
```

```javascript
if (!window.ApplePaySession) {
  console.error('This device does not support Apple Pay');
}
if (!ApplePaySession.canMakePayments()) {
  console.error('This device is not capable of making Apple Pay payments');
}
const applepay = paypal.Applepay();
applepay.config()
.then(applepayConfig => {
  if (applepayConfig.isEligible) {
    document.getElementById("applepay-container").innerHTML = '<apple-pay-button id="btn-appl" buttonstyle="black" type="buy" locale="en">';
  }
})
.catch(applepayConfigError => {
  console.error('Error while fetching Apple Pay configuration.');
});
```

> **Tip:** You can find more details on how to set up the Apple Pay button in <a href="https://developer.apple.com/documentation/applepayjs/displaying_apple_pay_buttons" target="_blank">Apple's developer documentation</a>.

## 5. Create Apple Pay session

The <code>ApplePaySession</code> object manages the Apple Pay payment
process on the web. Create a new <code>ApplePaySession</code> each time a
buyer explicitly requests a payment, such as inside an
<code>onclick</code> event. If you don't create an
<code>ApplePaySession</code> each time, you get a "Must create a new
<code>ApplePaySession</code> from a user gesture handler" JavaScript exception.
For more information about this error, visit Apple's Creating an Apple Pay
Session page.

For each <code>ApplePaySession</code>, create an
<a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest" target="_blank"><code>ApplePayPaymentRequest</code>
</a> object, which includes information about payment processing capabilities,
the payment amount, and shipping information.

The response object of the PayPal JavaScript SDK API{" "}
<code>paypal.Applepay().config()</code> provides the following parameters
in the <code>ApplePayPaymentRequest</code> object:

<ul>
  <li><code>countryCode</code></li>
  <li><code>merchantCapabilities</code></li>
  <li><code>supportedNetworks</code></li>
</ul>

```javascript
const paymentRequest = {
  countryCode: applepayConfig.countryCode,
  merchantCapabilities: applepayConfig.merchantCapabilities,
  supportedNetworks: applepayConfig.supportedNetworks,
  currencyCode: "USD",
  requiredShippingContactFields: ["name", "phone", "email", "postalAddress"],
  requiredBillingContactFields: ["postalAddress"],
  total: {
    label: "Demo",
    type: "final",
    amount: "100.00",
  }
};
const session = new ApplePaySession(4, paymentRequest);
```

Include the new <code>ApplePaySession</code> inside a gesture handler,
such as an <code>onclick</code> event or an <code>addEventListener</code>{" "}
click handler.

Creating an <code>ApplePaySession</code> object throws a JavaScript
exception if any of the following occurs:

<ul>
  <li>
    Any Apple Pay JavaScript API is called from an insecure page that
    doesn't use <code>https</code>.
  </li>
  <li>An incorrect payment request is passed. Payment requests are incorrect if they contain missing, unknown or invalid properties, or if the total amount is negative.</li>
</ul>

### onvalidatemerchant callback

Use <code>paypal.Applepay().validateMerchant()</code> in the <code>onvalidatemerchant</code> callback to create a validated Apple Pay
session object:

```javascript
      children={`session.onvalidatemerchant = (event) => {
  applepay.validateMerchant({
    validationUrl: event.validationURL,
    displayName: "My Store"
  })
  .then(validateResult => {
    session.completeMerchantValidation(validateResult.merchantSession);
  })
  .catch(validateError => {
    console.error(validateError);
    session.abort();
  });
};
```

### onpaymentauthorized callback

Safari calls the <code>onpaymentauthorized</code> callback with an 
<code>event</code> object. The <code>event</code> object passes a 
<code>token</code> which you need to send to PayPal to confirm the order.


Capture the order using the <a href="https://developer.paypal.com/api/orders/v2" target="_blank">PayPal Orders V2 API</a>. Use <code>paypal.Applepay().confirmOrder()</code> to send the <code>orderID</code>, the Apple Pay token, billing contact details, and confirm the order.

```javascript
session.onpaymentauthorized = (event) => {
    console.log('Your billing address is:', event.payment.billingContact);
    console.log('Your shipping address is:', event.payment.shippingContact);
    fetch("/api/orders", {
      method: 'post' ,
      body : {}
    })
    .then(res => res.json())
    .then((createOrderData) => {
      var orderId = createOrderData.id;
      applepay.confirmOrder({
        orderId: orderId,
        token: event.payment.token,
        billingContact: event.payment.billingContact
      })
      .then(confirmResult => {
        session.completePayment(ApplePaySession.STATUS_SUCCESS);
        fetch(\`/api/orders/\${orderId}/capture\`\, {
          method: "post",
        })
        .then(res => res.json())
        .then(captureResult => {
          console.log(captureResult);
        })
        .catch(captureError => console.error(captureError));
      })
      .catch(confirmError => {
        if (confirmError) {
          console.error('Error confirming order with applepay token');
          console.error(confirmError);
          session.completePayment(ApplePaySession.STATUS_FAILURE);
        }
      });
    });
  };
```

## 6. Show the payment sheet

After you have created the Apple Pay session and added the callbacks, call the <code>session.begin</code> method to show the payment sheet. You can only call the <code>begin</code> method when a buyer explicitly requests a payment, such as inside an <code>onclick</code> event. The <code>begin</code> method throws a JavaScript exception if the buyer does not explicitly request the action:


```javascript
session.begin();
```

After the buyer starts a payment in the browser, they use their Apple
device to authorize the payment.

### Customize payment

Customize the payment experience using the <a href="https://developer.apple.com/documentation/apple_pay_on_the_web" target="_blank">Apple Pay JavaScript SDK</a>.

Per Apple's development guidelines, your Apple Pay integration needs to follow these rules:

<ol>
  <li>
    The last step of an Apple Pay transaction should be when the buyer uses the payment sheet to confirm the payment.
  </li>
  <li>
    Don't ask the buyer to complete additional confirmation after they use the Apple Pay payment sheet to confirm the payment.
  </li>
  <li>
    Don't allow changes to the order after the buyer confirms the payment on the Apple Pay payment sheet.
  </li>
</ol>

The commonly used customizations for Apple Pay are:

| Customization	| Apple Pay SDK Details |
| :--- | :--- |
| A set of line items that explain the subtotal, tax, discount, and additional charges for the payment. | <a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/1916120-lineitems"><code>lineItems</code></a> |
| The billing information fields that the buyer must provide to fulfill the order. | <a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/2216120-requiredbillingcontactfields"><code>requiredBillingContactFields</code></a> |
| The shipping information fields that the buyer must provide to fulfill the order. | <a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/2216121-requiredshippingcontactfields"><code>requiredShippingContactFields</code></a> |
| The buyer's billing contact information. | <a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/1916125-billingcontact"><code>billingContact</code></a> |
| The buyer's shipping contact information. | <a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/2216121-requiredshippingcontactfields"><code>requiredShippingContactFields</code></a><br />Call the <a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaysession/1778009-onshippingcontactselected"><code>onshippingcontactselected</code></a> event handler when the user selects a shipping contact in the payment sheet. |
| The shipping method for a payment request. | <a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepayshippingmethod"><code>ApplePayShippingMethod</code></a><br />Call the <a href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaysession/1778028-onshippingmethodselected"><code>onshippingmethodselected</code></a> event handler when the user selects a shipping method in the payment sheet. |

## 7. Test your integration

Test your Apple Pay integration in the PayPal sandbox and production environments to ensure that your app works correctly.

Use your personal sandbox login information during checkout to complete a payment using Apple Pay. Then, log into the sandbox site <a href="https://sandbox.paypal.com" target="_blank">sandbox.paypal.com</a> to see that the money has moved into your account.

<ol>
  <li>
    Open your test page with the Safari web browser on an iOS device or computer.
  </li>
  <li>Get a test card from your Apple sandbox account.</li>
  <li>
    Add the test card to your Apple Wallet on your iOS device or by using the Safari browser on the web.
  </li>
  <li>
    Tap the <strong>Apple Pay</strong> button to open a pop-up with the Apple Pay payment sheet.
  </li>
  <li>Make a payment using the Apple Pay payment sheet.</li>
  <li>
    If you have an additional confirmation page on your merchant website, continue to confirm the payment.
  </li>
  <li>
    Log in to your merchant account and continue to your confirmation page to confirm that the money you used for payment showed up in the account.
  </li>
</ol>

## 8. Go live

Make Apple Pay available to buyers using your website or app.

> **Important:** Before going live, complete <a target="_blank" href="https://www.paypal.com/bizsignup/add-product?product=payment_methods&capabilities=APPLE_PAY">production onboarding</a> to process Apple Pay payments with your live PayPal account.

### Live environment

If you're a new merchant, sign up for a <a href="https://www.paypal.com/us/business" target="_blank">PayPal business account</a>.

Use your personal production login information during checkout to complete an Apple Pay transaction. Then log into <strong>paypal.com</strong> to see the money move out of your account.

### Getting started in your live environment

Verify any domain names in your live environment that will show an Apple Pay button. Apple Pay transactions only work on a domain and site registered to you.

<ul>
  <li>
    <a href="#download-host">
      Download and host</a> the domain association file for your live environment.
  </li>
  <li>
    <a href="#register-your-live-domain">
      Register your live domain</a> on your PayPal Developer Dashboard.
  </li>
</ul>

> **Important:** The Apple Pay payment method won't work if the domain and site aren't registered. The merchant that owns the domain is responsible for registering that domain.


#### Prerequisites

Enable Apple Pay for your live account:

<ol>
  <li>
    Log into the PayPal Developer Dashboard with your live PayPal account.
  </li>
  <li>
    Select the <strong>Sandbox/Live</strong> toggle so it shows <strong>Live</strong>.
  </li>
  <li>
    Go to <strong>Apps & Credentials</strong>.
  </li>
  <li>
    Scroll down to <strong>Features</strong>.
  </li>
  <li>
    Select the <strong>Apple Pay</strong> checkbox and select the <strong>Save</strong> link.
  </li>
</ol>

Create an app:

<ol>
  <li>
    Log into the PayPal Developer Dashboard with your live PayPal account.
  </li>
  <li>
    Select the <strong>Sandbox/Live</strong> toggle so it shows <strong>Live</strong>.
  </li>
  <li>
    Go to <strong>Apps & Credentials</strong>.
  </li>
  <li>
    Create an app similar to what you created in the sandbox. You don't need to log into a separate test account.
  </li>
</ol>

<a name="download-host"></a>

#### Download and host live domain association file

Host a domain association file for each high-level domain and subdomain that show the Apple Pay button.

<ol>
  <li>Download the domain association file for your live environment.
  </li>
  <li>
    Host the file on your live site for each domain and subdomain you want to register, at <code>/.well-known/apple-developer-merchantid-domain-association</code>. For example:
      <ul>
        <li>
          <code>https://example.com/.well-known/apple-developer-merchantid-domain-association</code>
        </li>
        <li>
          <code>https://subdomain.example.com/.well-known/apple-developer-merchantid-domain-association</code>
        </li>
      </ul>
  </li>
</ol>

<a href="https://paypalobjects.com/devdoc/apple-pay/well-known/apple-developer-merchantid-domain-association" target="_blank"><button>Download</button></a>


> **Note:** Remove the file extension from the domain association file when you host it on your server.


<a name="register-your-live-domain"></a>

#### Register your live domain on PayPal


Add all high-level domains that show the Apple Pay button.

<ol>
  <li>
    Log into the PayPal Developer Dashboard with your live PayPal account.
  </li>
  <li>
    Select the <strong>Sandbox/Live</strong> toggle so it shows <strong>Live</strong>.
  </li>
  <li>
    Go to <strong>Apps & Credentials</strong>.
  </li>
  <li>
    Select your app.
  </li>
  <li>
    Scroll down to <strong>Features</strong> > <strong>Accept payments</strong> > <strong>Advanced Credit and Debit Card Payments</strong>.
  </li>
  <li>
    Check if Apple Pay is enabled. If Apple Pay isn't enabled, select the <strong>Apple Pay</strong> checkbox and select the <strong>Save</strong> link to enable Apple Pay.
  </li>
  <li>
    Select the <strong>Manage</strong> link in the <strong>Apple Pay</strong> section.
  </li>
  <li>
    Select <strong>Add Domain</strong> and enter your domain name.
  </li>
  <li>
    Select <strong>Register Domain</strong>. If registration fails, check that the domain association file is live and saved to the right place on your live site.
  </li>
</ol>

After your domain is registered:

<ul>
  <li>
    The domain appears under <strong>Domains registered with Apple Pay</strong>.
  </li>
  <li>
    Buyers can make payments using the <strong>Apple Pay</strong> button on the registered website.
  </li>
</ul>

### Testing in your live environment

When testing a purchase in production, consider:

<ul>
  <li>
    The business account receiving money can't also make the purchase.
  </li>
  <li>
    If you create a personal account with the same information as the
    business account, those accounts might experience restrictions.
  </li>
</ul>

How to test Apple Pay payments in a live environment:

<ol>
  <li>Open your test page with Safari on iOS or desktop.</li>
  <li>
    Select the Apple Pay button to open a pop-up with the Apple Pay payment
    sheet.
  </li>
  <li>Proceed with the Apple Pay checkout transaction.</li>
  <li>
    If you have an additional confirmation page on your merchant website,
    confirm the payment.
  </li>
  <li>
    Log in to your merchant account and confirm that the money has moved
    into that account.
  </li>
</ol>

### Troubleshoot your integration

Make sure that there are no browser console warnings or errors. The
JavaScript SDK configuration attributes have distinct validation checks
for input formatting and values.

If the validation fails, the web browser's developer console shows warning
messages that say which property is incorrect and what you need to do to
address the issue. The library generally attempts to revert to the safe
default values if missing or incorrect inputs exist.