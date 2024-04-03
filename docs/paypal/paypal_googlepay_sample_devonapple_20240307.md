# Integrate Google Pay with JavaScript SDK for direct merchants

## Google Pay integration

<table>
  <tr>
    <td>
      <p>
        Google Pay is a mobile payment and digital wallet service provided by Alphabet Inc.
      </p>
      <p>
        Buyers can use Google Pay on PayPal to make payments on the web using a web browser.
      </p>
      <p>
        Sellers can use PayPal with Google Pay to sell physical goods, such as clothes and electronics, and intangible professional services, such as concerts or gym memberships.
      </p>
    </td>
    <td>
      <img src="https://paypalobjects.com/devdoc/sdk_mobile_googlepay.png" alt="Google Pay mobile web illustration" width="800"/>
    </td>
  <tr>
</table>

### Supported countries and currencies

Google Pay supports payments in 32 countries and 22 currencies:

* **Countries:** Australia, Austria, Belgium, Bulgaria, Canada, Cyprus, Czech Republic, Denmark, Estonia, Finland, France, Germany, Greece, Hungary, Ireland, Italy, Latvia, Liechtenstein, Lithuania, Luxembourg, Malta, Netherlands, Norway, Poland, Portugal, Romania, Slovakia, Slovenia, Spain, Sweden, United States, United Kingdom
* **Currencies:** `AUD`, `BRL`, `CAD`, `CHF`, `CZK`, `DKK`, `EUR`, `GBP`, `HKD`, `HUF`, `ILS`, `JPY`, `MXN`, `NOK`, `NZD`, `PHP`, `PLN`, `SEK`, `SGD`, `THB`, `TWD`, `USD`

> **Tip:** If you want to integrate additional methods of accepting payment beyond Google Pay, visit our <a href="https://developer.paypal.com/docs/checkout/advanced/integrate/" target="_blank">Advanced Checkout guide</a> for additional integration choices.

## How it works

<ol>
  <li>
    The Google Pay button shows up on your website when a customer uses a web browser.
  </li>
  <li>
    The buyer selects the Google Pay button on your website.
  </li>
  <li>
    Your website shows the buyer a payment sheet.
  </li>
  <li>
    The buyer can choose a different shipping address and payment method.
  </li>
  <li>
    The buyer authorizes the payment.
  </li>
</ol>

## Know before you code

Google Pay works on most web browsers, including:
<ul>
  <li>
    Google Chrome.
  </li>
  <li>
    Mozilla Firefox.
  </li>
  <li>
    Apple Safari.
  </li>
  <li>
    Microsoft Edge.
  </li>
</ul>

<a href="https://developers.google.com/pay/api/web/guides/test-and-deploy/integration-checklist#test-using-browser-developer-console" target="_blank"><button type="button">Check Compatibility</button></a>

Currently supports Google Pay one-time payments with the buyer present. Review Google's Google Pay API Terms of Service and Acceptable Use Policy
  for more information.

<a href="https://payments.developers.google.com/terms/sellertos" target="_blank"><button type="button">Google Terms of Service</button></a> <a href="https://payments.developers.google.com/terms/aup" target="_blank"><button type="button">Acceptable use policy</button></a>

## 1. Set up your sandbox account to accept Google Pay

Before you can accept Google Pay on your website, verify that your sandbox business account supports Google Pay.

Direct merchants can use the PayPal Developer Dashboard to set up their sandbox accounts to accept Google Pay.

<ol>
  <li>
    Log into the PayPal <a href="https://developer.paypal.com/dashboard/" target="_blank">Developer Dashboard</a> and go to your sandbox account.
  </li>
  <li>
    Go to <strong>Apps & Credentials</strong>.
  </li>
  <li>
    Make sure you are in the PayPal sandbox environment by selecting <strong>Sandbox</strong> at the top.
  </li>
  <li>Select or create an app.</li>
  <li>
    Scroll down to <strong>Features</strong> and check if Google Pay is enabled.  If Google Pay isn't enabled, select the <strong>Google Pay</strong> checkbox and select the "Save" link to enable Google Pay.
  </li>
</ol>

If you created a sandbox business account through <a href="https://sandbox.paypal.com" target="_blank" >
    sandbox.paypal.com</a>, and the Google Pay status for the account shows as disabled, <a href="https://www.sandbox.paypal.com/bizsignup/add-product?product=payment_methods&capabilities=GOOGLE_PAY" target="_blank">complete the sandbox onboarding steps</a> to enable Google Pay.

> **Tip:** When your integration is ready to go live, read the <strong>Go live</strong> section for details about the additional steps needed for Google Pay onboarding.

This screenshot shows the Google Pay sandbox settings in the mobile and digital payments section of the PayPal Developer Dashboard. This only applies to direct merchant integrations:

<img src="https://paypalobjects.com/devdoc/sdk_acdc_acceptpayments.png" alt="Google Pay sandbox settings in the PayPal Developer Dashboard" width="400"/>

## 2. Getting started in your testing environment

Before you develop your Google Pay on the Web integration, you need to complete <a href="https://developer.paypal.com/api/rest/" target="_blank">Get started </a> to set up your PayPal account, client ID, and sandbox emails for testing.

## 3. Integrate Google Pay checkout

Follow this integration process to add Google Pay as a checkout option, customize the payment experience, and process payments.

### Call the Orders API

To accept Google Pay directly on your website, create API endpoints on your
  server that communicate with the <a href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">PayPal Orders V2 API</a>. These endpoints can create an order, authorize payment, and capture payment for an order.

### Server-side example (Node.js)

This code demonstrates using the <a href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">PayPal Orders V2 API</a> to add routes to an Express server for creating orders and capturing payments.

Find the complete sample code in the <a href="https://github.com/paypal-examples/googlepay" target="_blank">GitHub repo</a>.

#### server.js

```javascript
import * as PayPal from "./paypal-api.js";

/* Create Order route Handler */
app.post("/api/orders", async (req, res) => {
  const order = await PayPal.createOrder();
  res.json(order);
});

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
  const url = \`\${base}/v2/checkout/orders\`;
  const response = await fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: \`Bearer \${accessToken}\`,
    },
    body: JSON.stringify({
      intent: "CAPTURE",
      purchase_units: [
        {
          amount: {
            currency_code: "USD",
            value: purchaseAmount
          },
        },
      ],
    }),
  });
  const data = await response.json();
  return data;
}

// capture payment for an order
export async function capturePayment(orderId) {
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v2/checkout/orders/\${orderId}/capture\`;
  const response = await fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: \`Bearer \${accessToken}\`,
    },
  });
  const data = await response.json();
  return data;
}
```

## 4. Set up your Google Pay button

You need to integrate with the Google Pay JavaScript SDK and PayPal JavaScript SDK to add Google Pay to your site.

### Integrate PayPal JavaScript SDK

Use this script to integrate with the PayPal JavaScript SDK:

```javascript
<script src="https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID&currency=USD&buyer-country=US&merchant-id=SUB_MERCHANT_ID&components=googlepay"></script>
```

Include <code>googlepay</code> in the <code>components</code> list.

### Integrate Google JavaScript SDK

Use this script to integrate with the Google Pay JavaScript SDK:

```javascript
<script async src="https://pay.google.com/gp/p/js/pay.js" onload="onGooglePayLoaded()"></script>
```

PayPal's Google Pay component interacts with your JavaScript code in 2 areas:

<ol>
  <li>
    Checking merchant eligibility and providing <a target="_blank" href="https://developers.google.com/pay/api/web/reference/request-objects#PaymentDataRequest"><code>PaymentDataRequest</code></a> parameters for Google Pay: <code>paypal.Googlepay().config()</code>.
  </li>
  <li>
    Handling the <code>onPaymentAuthorized()</code> callback: <code>paypal.Googlepay().confirmOrder()</code>.
  </li>
</ol>

Check for device and merchant eligibility before setting up the GooglePay Button.

The PayPal JavaScript SDK API <code>paypal.Googlepay().config()</code> response object provides the <code>allowedPaymentMethods</code> parameter, which is part of the" "}
  Google API's <a target="_blank" href="https://developers.google.com/pay/api/web/reference/request-objects#IsReadyToPayRequest"><code>isReadyToPayRequest</code></a> object.

Check whether the Google Pay API supports a device, browser, and payment method:

<ul>
  <li>Add <code>allowedPaymentMethods</code> to the <code>isReadyToPayRequest</code>.</li>
  <li>Call the <code>isReadyToPay()</code> method to check compatibility and render the Google Pay Button.</li>
</ul>

```javascript
/**
 * Initialize Google PaymentsClient after Google-hosted JavaScript has loaded
 *
 * Display a Google Pay payment button after confirmation of the viewer's
 * ability to pay.
 */
function onGooglePayLoaded() {
  const paymentsClient = getGooglePaymentsClient();
  paymentsClient.isReadyToPay(isReadyToPayRequest)
      .then(function(response) {
        if (response.result) {
          addGooglePayButton();
        }
      })
      .catch(function(err) {
        console.error(err);
      });
}
/**
 * Add a Google Pay purchase button
 */
function addGooglePayButton() {
  const paymentsClient = getGooglePaymentsClient();
  const button =
      paymentsClient.createButton({
        onClick: onGooglePaymentButtonClicked /* To be defined later */,
        allowedPaymentMethods: [baseCardPaymentMethod]
      });
  document.getElementById('container').appendChild(button);
}
```

> **Tip:** For more information refer to steps 6 and 7 in <a href="https://developers.google.com/pay/api/web/guides/tutorial#isreadytopay" target="_blank">Google's developer documentation</a>.

## 5. Create PaymentDataRequest

The <code>PaymentDataRequest</code> object manages the Google Pay payment process on the web. Create a new <code>PaymentDataRequest</code> each time a buyer explicitly requests a payment, such as inside the <code>onclick</code> handler for the Google Pay Button.

For each checkout session, create a `PaymentDataRequest` object, which includes information about payment processing capabilities, the payment amount, and shipping information.

The response object of the PayPal JavaScript SDK API <code>paypal.Googlepay().config()</code> provides the following parameters
  in the <code>PaymentDataRequest</code> object:

<ul>
  <li><code>allowedPaymentMethods</code></li>
  <li><code>merchantInfo</code></li>
</ul>

```javascript
/* Note: the \`googlePayConfig\` object in this request is the response from \`paypal.Googlepay().config()\` */
async function getGooglePaymentDataRequest() {
  const googlePayConfig = await paypal.Googlepay().config();
  const paymentDataRequest = Object.assign({}, baseRequest);
  paymentDataRequest.allowedPaymentMethods = googlePayConfig.allowedPaymentMethods;
  paymentDataRequest.transactionInfo = getGoogleTransactionInfo();
  paymentDataRequest.merchantInfo = googlePayConfig.merchantInfo;
  paymentDataRequest.callbackIntents = ["PAYMENT_AUTHORIZATION"];
  return paymentDataRequest;
}
function getGoogleTransactionInfo(){
    return {
        currencyCode: 'USD',
        totalPriceStatus: 'FINAL',
        totalPrice: '100.00' // Your amount
      }
}
```

For more details about the response parameters, see the <strong><code>ConfigResponse</code></strong> section.

For more details about how Google Pay handles <code>paymentDataRequest</code>, refer to steps 8, 9, and 10 in <a target="_blank" href="https://developers.google.com/pay/api/web/guides/tutorial#paymentdatarequest">Google's developer documentation</a>.

> **Tip:** See the <a target="_blank" href="https://developers.google.com/pay/api/web/reference/request-objects#PaymentDataRequest">Google Pay PaymentDataRequest Object API reference</a> for the complete list of properties available for the <code>PaymentDataRequest</code> object.

### Register click handler

Register a click event handler for the Google Pay purchase button. Call <code>loadPaymentData()</code> in the event handler when the user interacts with the purchase button and pass the <code>PaymentDataRequest</code> object.

```javascript
/* Show Google Pay payment sheet when Google Pay payment button is clicked */
async function onGooglePaymentButtonClicked() {
  const paymentDataRequest = await getGooglePaymentDataRequest();
  const paymentsClient = getGooglePaymentsClient();
  paymentsClient.loadPaymentData(paymentDataRequest);
}
```

Add the click handler <code>onGooglePaymentButtonClicked</code> to the Button defined in <strong>Set up your Google Pay button</strong>.

For more details about <code>paymentDataRequest</code> refer to step 9 in <a target="_blank" href="https://developers.google.com/pay/api/web/guides/tutorial#paymentdatarequest">Google's developer documentation</a>.

### onpaymentauthorized callback

Google calls the <code>onPaymentAuthorized()</code> callback with a <a target="_blank" href="https://developers.google.com/pay/api/web/reference/response-objects#PaymentData"><code>PaymentData</code></a> object when a customer consents to your site collecting their payment information and optional contact details.

Register the <code>onPaymentAuthorized()</code> callback as part of the <code>PaymentClient</code> initialization as shown in Google Pay's <a target="_blank" href="https://developers.google.com/pay/api/web/reference/client#PaymentsClient">Client Reference page</a>.

Create an order by using the <a href="https://developer.paypal.com/api/orders/v2" target="_blank">PayPal Orders V2 API</a>. Use <code>paypal.Googlepay().confirmOrder()</code> to send the <code>orderID</code>, the Google Pay Payment Data, and optional contact details, and confirm the order.

Confirm the order using the <code>paypal.Googlepay().confirmOrder()</code> method.

If the order confirmation status is <code>APPROVED</code>, capture the order using the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_capture" target="_blank">Capture payment for order endpoint</a> of the PayPal Orders V2 API.

For more details, see step 11 of <a target="_blank" href="https://developers.google.com/pay/api/web/guides/tutorial#authorize-payments">Google's developer documentation</a>.

> **Tip:** You can see an <a target="_blank" href="https://developers.google.com/pay/api/web/guides/tutorial#authorize-payments_1">example of an Authorize Payments call</a> in the <strong>Put it all together</strong> section of Google's developer documentation.

```javascript
async function processPayment(paymentData) {
  return new Promise(async function (resolve, reject) {
    try {
        // Create the order on your server
        const {id} = await fetch(\`/orders\`, {
        method: "POST",
        body:
        // You can use the "body" parameter to pass optional, additional order information, such as:
        // amount, and amount breakdown elements like tax, shipping, and handling
        // item data, such as sku, name, unit_amount, and quantity
        // shipping information, like name, address, and address type
      });
      const confirmOrderResponse = await paypal.Googlepay().confirmOrder({
          orderId: id,
          paymentMethodData: paymentData.paymentMethodData
        });
      /** Capture the Order on your Server  */
      if(confirmOrderResponse.status === "APPROVED"){
           const response =  await fetch(\`/capture/\${id}\`, {
              method: 'POST',
            }).then(res => res.json());
          if(response.capture.status === "COMPLETED")
              resolve({transactionState: 'SUCCESS'});
          else
              resolve({
                transactionState: 'ERROR',
                error: {
                  intent: 'PAYMENT_AUTHORIZATION',
                  message: 'TRANSACTION FAILED',
                }
      })
      } else {
           resolve({
            transactionState: 'ERROR',
            error: {
              intent: 'PAYMENT_AUTHORIZATION',
              message: 'TRANSACTION FAILED',
            }
          })
      }
    } catch(err) {
      resolve({
        transactionState: 'ERROR',
        error: {
          intent: 'PAYMENT_AUTHORIZATION',
          message: err.message,
        }
      })
    }
  });
}
```

### Customize payment experience

Customize the payment experience using the <a target="_blank" href="https://developers.google.com/pay/api/web/reference/client">Google Pay JavaScript SDK</a>. The following table shows the 2 most popular Google Pay customizations:

<table>
  <thead>
    <tr>
      <th>Customization</th>
      <th>Details</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a target="_blank" href="https://developers.google.com/pay/api/web/reference/client#onPaymentDataChanged"><code>PaymentDataChange</code></a>
      </td>
      <td>
        This method is used to handle payment data changes in the payment sheet such as shipping address and shipping options.
      </td>
    </tr>
    <tr>
      <td>
        <a target="_blank" href="https://developers.google.com/pay/api/web/reference/request-objects#PaymentDataRequest"><code>PaymentDataRequest</code></a>
      </td>
      <td>
        Provides optional properties to collect details, such as shipping address and email.
      </td>
    </tr>
  </tbody>
</table>

## 6. Put it all together

The following code samples show a Google Pay integration:

### HTML

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Googlepay Example</title>
    <script src="./script.js"></script>
    <script src="https://www.paypal.com/sdk/js?client-id=<client_id>&components=googlepay"></script>
    <link rel="stylesheet" type="text/css" href="styles.css" />
  </head>
  <body>
    <main>
      <section>
        <div id="button-container"></div>
      </section>
    </main>
    <script src="https://pay.google.com/gp/p/js/pay.js"></script>
    <script>
      document.addEventListener("DOMContentLoaded", (event) => {
        if (google && paypal.Googlepay) {
          onGooglePayLoaded().catch(console.log);
        }
      });
    </script>
  </body>
</html>
```

### JavaScript

```javascript
/*
* Define the version of the Google Pay API referenced when creating your
* configuration
*/
const baseRequest = {
  apiVersion: 2,
  apiVersionMinor: 0,
};
let paymentsClient = null,
  allowedPaymentMethods = null,
  merchantInfo = null;
/* Configure your site's support for payment methods supported by the Google Pay */
function getGoogleIsReadyToPayRequest(allowedPaymentMethods) {
  return Object.assign({}, baseRequest, {
    allowedPaymentMethods: allowedPaymentMethods,
  });
}
/* Fetch Default Config from PayPal via PayPal SDK */
async function getGooglePayConfig() {
  if (allowedPaymentMethods == null || merchantInfo == null) {
    const googlePayConfig = await paypal.Googlepay().config();
    allowedPaymentMethods = googlePayConfig.allowedPaymentMethods;
    merchantInfo = googlePayConfig.merchantInfo;
  }
  return {
    allowedPaymentMethods,
    merchantInfo,
  };
}
/* Configure support for the Google Pay API */
async function getGooglePaymentDataRequest() {
  const paymentDataRequest = Object.assign({}, baseRequest);
  const { allowedPaymentMethods, merchantInfo } = await getGooglePayConfig();
  paymentDataRequest.allowedPaymentMethods = allowedPaymentMethods;
  paymentDataRequest.transactionInfo = getGoogleTransactionInfo();
  paymentDataRequest.merchantInfo = merchantInfo;
  paymentDataRequest.callbackIntents = ["PAYMENT_AUTHORIZATION"];
  return paymentDataRequest;
}
function onPaymentAuthorized(paymentData) {
  return new Promise(function (resolve, reject) {
    processPayment(paymentData)
      .then(function (data) {
        resolve({ transactionState: "SUCCESS" });
      })
      .catch(function (errDetails) {
        resolve({ transactionState: "ERROR" });
      });
  });
}
function getGooglePaymentsClient() {
  if (paymentsClient === null) {
    paymentsClient = new google.payments.api.PaymentsClient({
      environment: "TEST",
      paymentDataCallbacks: {
        onPaymentAuthorized: onPaymentAuthorized,
      },
    });
  }
  return paymentsClient;
}
async function onGooglePayLoaded() {
  const paymentsClient = getGooglePaymentsClient();
  const { allowedPaymentMethods } = await getGooglePayConfig();
  paymentsClient
    .isReadyToPay(getGoogleIsReadyToPayRequest(allowedPaymentMethods))
    .then(function (response) {
      if (response.result) {
        addGooglePayButton();
      }
    })
    .catch(function (err) {
      console.error(err);
    });
}
function addGooglePayButton() {
  const paymentsClient = getGooglePaymentsClient();
  const button = paymentsClient.createButton({
    onClick: onGooglePaymentButtonClicked,
  });
  document.getElementById("container").appendChild(button);
}
function getGoogleTransactionInfo() {
  return {
    displayItems: [
      {
        label: "Subtotal",
        type: "SUBTOTAL",
        price: "100.00",
      },
      {
        label: "Tax",
        type: "TAX",
        price: "10.00",
      },
    ],
    countryCode: "US",
    currencyCode: "USD",
    totalPriceStatus: "FINAL",
    totalPrice: "110.00",
    totalPriceLabel: "Total",
  };
}
async function onGooglePaymentButtonClicked() {
  const paymentDataRequest = await getGooglePaymentDataRequest();
  paymentDataRequest.transactionInfo = getGoogleTransactionInfo();
  const paymentsClient = getGooglePaymentsClient();
  paymentsClient.loadPaymentData(paymentDataRequest);
}
async function processPayment(paymentData) {
  try {
    const { currencyCode, totalPrice } = getGoogleTransactionInfo();
    const order = {
      intent: "CAPTURE",
      purchase_units: [
        {
          amount: {
            currency_code: currencyCode,
            value: totalPrice,
          },
        },
      ],
    };
    /* Create Order */
    const { id } = await fetch(\`/orders\`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(order),
    }).then((res) => res.json());
    const { status } = await paypal.Googlepay().confirmOrder({
      orderId: id,
      paymentMethodData: paymentData.paymentMethodData,
    });
    if (status === "APPROVED") {
      /* Capture the Order */
      const captureResponse = await fetch(\`/orders/\${id}/capture\`, {
        method: "POST",
      }).then((res) => res.json());
      return { transactionState: "SUCCESS" };
    } else {
      return { transactionState: "ERROR" };
    }
  } catch (err) {
    return {
      transactionState: "ERROR",
      error: {
        message: err.message,
      },
    };
  }
}
```

## Strong Customer Authentication (SCA)

When the <code>ConfirmOrder</code> <a href="https://developer.paypal.com/docs/api/orders/v2/#definition-order_status" target="_blank">status</a> is <code>PAYER_ACTION_REQUIRED</code>, the order requires additional authentication from the payer, such as 3D Secure.

The PayPal JavaScript SDK Client provides an API to handle 3DS Secure authentication. Pass the <code>orderId</code> to <code>initiatePayerAction</code>.

> **Tip:** Refer to <code>initiatePayerAction</code></a> for more details.

When the payer completes authentication, confirm that the <code>liability_shift</code> status has shifted:

<ul>
  <li>
    Make a call to the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_get" target="_blank">Show order details endpoint</a> of the Orders v2 API, using the <code>id</code> of the order.
  </li>
  <li>
    Check the <code>liability_shift</code> status in the <a href="https://developer.paypal.com/docs/api/orders/v2/#definition-authentication_response" target="_blank"><code>authentication_response</code></a>.
  </li>
</ul>

```javascript
...
const { status } = await paypal.Googlepay().confirmOrder({
  orderId: id,
  paymentMethodData: paymentData.paymentMethodData,
});
if (status === "PAYER_ACTION_REQUIRED") {
  console.log("==== Confirm Payment Completed Payer Action Required =====");
  paypal
    .Googlepay()
    .initiatePayerAction({ orderId: id })
    .then(async () => {
      console.log("===== Payer Action Completed =====");
      /** GET Order */
      const orderResponse = await fetch(\`/orders/\${id}\`, {
        method: "GET",
      }).then((res) => res.json());
      console.log("===== 3DS Contingency Result Fetched =====");
      console.log(
        orderResponse?.payment_source?.google_pay?.card?.authentication_result
      );
      /* CAPTURE THE ORDER*/
      const captureResponse = await fetch(\`/orders/\${id}/capture\`, {
        method: "POST",
      }).then((res) => res.json());
      console.log(" ===== Order Capture Completed ===== ");
    });
}
...
```

## 7. Test your integration

Test your Google Pay integration in the PayPal sandbox and production environments to ensure that your app works correctly.

### Sandbox

Use your personal sandbox login information during checkout to complete a payment using Google Pay. Then, log into the sandbox site <a href="https://sandbox.paypal.com" target="_blank">sandbox.paypal.com</a> to see that the money has moved into your account.

<ol>
  <li>
    Open your test page with a supported web browser on any supported device.
  </li>
  <li>
    Add a test card to your Google Wallet on your device. Google provides test cards through their <a target="_blank" href="https://developers.google.com/pay/api/web/guides/resources/test-card-suite">Test card suite</a>.
  </li>
  <li>
    Tap the <strong>Google Pay</strong> button to open a pop-up with the Google Pay payment sheet.
  </li>
  <li>
    Make a payment using the Google Pay payment sheet.
  </li>
  <li>
    If you have an additional confirmation page on your merchant website, continue to confirm the payment.
  </li>
  <li>
    Log in to your merchant account and continue to your confirmation page to confirm that the money you used for payment showed up in the account.
  </li>
</ol>

### Google Pay test card suite

Use Google Pay <a href="https://developer.paypal.com/docs/checkout/apm/test-cards/google-pay/">test card numbers</a> to test your Google Pay integration.

## 8. Go live

Make Google Pay available to buyers using your website or app.

> **Tip:** Before going live, complete <a target="_blank" href="https://www.paypal.com/bizsignup/add-product?product=payment_methods&capabilities=GOOGLE_PAY">production onboarding</a> to process Google Pay payments with your live PayPal account.

### Live environment

If you're a new merchant, sign up for a <a href="https://www.paypal.com/us/business" target="_blank">PayPal business account</a>.

Use your personal production login information during checkout to complete a Google Pay transaction. Then log into <strong>paypal.com</strong> to see the money move out of your account.

## Testing in your live environment

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
<p>How to test Google Pay payments in a live environment:
<ol>
  <li>Open your test page with a supported browser.</li>
  <li>
    Select the Google Pay button to open a pop-up with the Google Pay payment sheet.
  </li>
  <li>
    Proceed with the Google Pay checkout transaction.
  </li>
  <li>
    If you have an additional confirmation page on your merchant website, continue to confirm the payment.
  </li>
  <li>
    Log in to your merchant account and confirm that the money has moved into that account.
  </li>
</ol>

## Troubleshoot your integration

Make sure that there are no browser console warnings or errors. The JavaScript SDK configuration attributes have distinct validation checks for input formatting and values.

If the validation fails, the web browser's developer console shows warning messages that say which property is incorrect and what you need to do to address the issue. The library generally attempts to revert to the safe default values if missing or incorrect inputs exist.