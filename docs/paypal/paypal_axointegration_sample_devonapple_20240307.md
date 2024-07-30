# Integrate card payments with JavaScript SDK for direct merchants

## How it works

Advanced Checkout lets you offer the PayPal payment button and custom credit and debit card fields. This guide covers integrating the PayPal button, credit, and debit card payments. You can find more ways to extend your integration in our <a target="_blank" href="https://developer.paypal.com/docs/checkout/advanced/customize/">customization doc</a>.

Once you integrate advanced Checkout, you can also offer options like Pay Later, Venmo, and alternative payment methods with some additional configuration.

This integration guide follows the code in this <a target="_blank" href="https://github.com/paypal-examples/docs-examples/tree/main/advanced-integration/v1/">GitHub sample</a>.


## Know before you code

You need a developer account to get sandbox credentials. PayPal uses REST API credentials which you can get from the developer dashboard.

* Client ID: Authenticates your account with PayPal and identifies an app in your sandbox.
* Client secret: Authorizes an app in your sandbox. Keep this secret safe and don't share it.

<a href="https://developer.paypal.com/dashboard/" target="_blank"><button type="button">Dashboard</button></a>
<a href="https://developer.paypal.com/api/rest/" target="_blank"><button type="button">Read the guide</button></a>

You need a combo of PayPal and third-party tools.

* <a href="https://developer.paypal.com/sdk/js/" target="_blank">JavaScript SDK</a>: Adds PayPal-supported payment methods.
* <a href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">Orders REST API</a>: Create, update, retrieve, authorize, and capture orders.
* <a href="https://www.npmjs.com/" target="_blank">npm</a>: Registry used to install the necessary third-party libraries.

## 1. Before you begin your integration

### Check your account setup for advanced card payments

This integration requires a sandbox business account with the Advanced Credit and Debit Card Payments capability. Your account should automatically have this capability.

To confirm that Advanced Credit and Debit Card Payments are enabled for you, check your sandbox business account as follows:
1. Log into the <a href="https://developer.paypal.com/dashboard/" target="_blank">PayPal Developer Dashboard</a>, toggle **Sandbox**, and go to **Apps & Credentials**.
1. In **REST API apps**, select the name of your app.
1. Go to **Features** > **Accept payments**.
1. Select the **Advanced Credit and Debit Card Payments** checkbox and select Save Changes.

> **Note:** If you created a sandbox business account through <a href="https://www.sandbox.paypal.com/?_ga=1.158343865.248280996.1670866755" target="_blank">sandbox.paypal.com</a>, and the **Advanced Credit and Debit Card Payments** status for the account is disabled, <a href="https://www.sandbox.paypal.com/bizsignup/#/checkAccount" target="_blank">complete the sandbox onboarding steps</a>.

### Check 3D Secure requirements

Add 3D Secure to reduce the chance of fraud and improve the payment experience by authenticating a card holder through their card issuer.

Visit our <a href="https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/" target="_blank">3D Secure</a> page to see if 3D Secure is required in your region and learn more about implementing 3D Secure in your app.

### Set up npm

One of the requirements to run this sample application is to have npm installed. For more info, <a href="https://www.npmjs.com/package/npm" target="_blank">visit npm’s documentation</a>.

#### 1. Install third-party libraries

Install the following third-party libraries to set up your integration. Here is a sample command to install them all at the same time:

```bash
npm install dotenv ejs express node-fetch
```

Select any of the links below to see more detailed installation instructions for each library:
| Third-party libraries | Description |
| :--- | :--- |
| <a href="https://www.npmjs.com/package/dotenv" target="_blank">Dotenv</a> | This zero-dependency module separates your configuration and code by loading environment variables from a `.env` file into `process.env`. |
| <a href="https://www.npmjs.com/package/ejs" target="_blank">ejs</a> | These templates help you deliver HTML markup using plain JavaScript. |
| <a href="https://www.npmjs.com/package/express" target="_blank">express</a> | This lean Node.js web application framework supports web and mobile applications. |
| <a href="https://www.npmjs.com/package/node-fetch" target="_blank">node-fetch</a> | This function helps you make API requests, similar to `window.fetch`. |

#### 2. Verify package.json

A `package.json` file has a list of the packages and version numbers needed for your app. You can share your `package.json` file with other developers so they can use the same settings as you.

The following snippet is an example of a `package.json` file for a PayPal integration. Compare this sample to the `package.json` in your project:

```json
{
  "name": "@paypalcorp/advanced-integration",
  "version": "1.0.0",
  "description": "",
  "main": "YOUR-SERVER-NAME.js",
  "type": "module",
  "scripts": {
    "test": "echo "Error: no test specified" && exit 1",
    "start": "node YOUR-SERVER-NAME.js"
  },
  "author": "",
  "license": "Apache-2.0",
  "dependencies": {
    "dotenv": "^16.0.0",
    "ejs": "^3.1.6",
    "express": "^4.17.3",
    "node-fetch": "^3.2.1"
  }
}
```

* Pass the name of your server file using `main` by replacing the default `YOUR-SERVER-NAME.js` on lines 5 and 9.
* Use `scripts.test` and `scripts.start` to customize how your app starts up.

If you're having trouble with your app, try reinstalling your local library and package files using `npm install`.

If you're getting the node error below, you need to include `"type": "module"` in your `package.json` file. This line isn't automatically added when `package.json` is created:

```
Warning: To load an ES module, set "type": "module" in the `package.json` or use the .mjs extension (Use `node --trace-warnings ...` to show where the warning was created)
```

See line 6 of the sample `package.json` file for an example.

#### 3. Set up .env

A `.env` file is a line-delimited text file that sets your local working environment variables. Use this `.env` file to securely pass the client ID and app secret for your app.

This code shows an example `.env` file. Rename `.env.example` to `.env` and replace the `PAYPAL_CLIENT_ID` and `PAYPAL_CLIENT_SECRET` with values from your app:

> **Note:** View your `PAYPAL_CLIENT_ID` and `PAYPAL_CLIENT_SECRET` in your <a href="https://developer.paypal.com/dashboard/" target="_blank">PayPal Developer Dashboard</a> under **Apps & Credentials**.

```
PAYPAL_CLIENT_ID="YOUR_CLIENT_ID_GOES_HERE"
PAYPAL_CLIENT_SECRET="YOUR_SECRET_GOES_HERE"
```

## 2. Integrate back end

This section explains how to set up your back end to integrate advanced Checkout payments.

### Back-end process

<ol>
  <li>
    Your app creates an order on the back-end by making a call to the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_create" target="_blank">Create order</a> endpoint of the Orders v2 API.
  </li>
  <li>
    Your app makes a call to the <a target="_blank" href="https://developer.paypal.com/docs/api/orders/v2/#orders_capture">Capture payment</a> endpoint of the Orders v2 API to move the money when the buyer confirms the order.
  </li>
</ol>

#### Back-end code

The following example uses 2 files, <code>/server/server.js</code> and <code>/server/views/checkout.ejs</code>, to show how to set up the back end to integrate with advanced payments.

##### /server/server.js

The <code>/server/server.js</code> file provides methods and functions for making the API calls and handling errors, and creates the endpoints that your app uses to:

<ul>
  <li>
    Generate an access token to use PayPal APIs.
  </li>
  <li>
    Create an order.
  </li>
  <li>
    Capture payment for the order.
  </li>
  <li>
    Simulate errors for negative testing.
  </li>
</ul>


You'll need to save the <code>server.js</code> file in a folder named <code>/server</code>.

##### /server/views/checkout.ejs

The <code>/server/views/checkout.ejs</code> file is an Embedded JavaScript (EJS) file that:

<ul>
  <li>
    Generate an access token to use PayPal APIs.
  </li>
  <li>
    Create an order.
  </li>
  <li>
    Capture payment for the order.
  </li>
  <li>
    Simulate errors for negative testing.
  </li>
</ul>

You'll need to save the <code>checkout.ejs</code> file in a folder named <code>/server/views</code>.

##### /server/server.js

```javascript
import express from "express";
import fetch from "node-fetch";
import "dotenv/config";

const { PAYPAL_CLIENT_ID, PAYPAL_CLIENT_SECRET, PORT = 8888 } = process.env;
const base = "https://api-m.sandbox.paypal.com";
const app = express();
app.set("view engine", "ejs");
app.set("views", "./server/views");
app.use(express.static("client"));

// parse post params sent in body in json format
app.use(express.json());

/**
 * Generate an OAuth 2.0 access token for authenticating with PayPal REST APIs.
 * See https://developer.paypal.com/api/rest/authentication/
 */
const generateAccessToken = async () => {
  try {
    if (!PAYPAL_CLIENT_ID || !PAYPAL_CLIENT_SECRET) {
      throw new Error("MISSING_API_CREDENTIALS");
    }
    const auth = Buffer.from(
      PAYPAL_CLIENT_ID + ":" + PAYPAL_CLIENT_SECRET,
    ).toString("base64");
    const response = await fetch(`${base}/v1/oauth2/token`, {
      method: "POST",
      body: "grant_type=client_credentials",
      headers: {
        Authorization: `Basic ${auth}`,
      },
    });

    const data = await response.json();
    return data.access_token;
  } catch (error) {
    console.error("Failed to generate Access Token:", error);
  }
};

/**
 * Generate a client token for rendering the hosted card fields.
 * See https://developer.paypal.com/docs/checkout/advanced/sdk/v1/#link-integratebackend
 */
const generateClientToken = async () => {
  const accessToken = await generateAccessToken();
  const url = `${base}/v1/identity/generate-token`;
  const response = await fetch(url, {
    method: "POST",
    headers: {
      Authorization: `Bearer ${accessToken}`,
      "Accept-Language": "en_US",
      "Content-Type": "application/json",
    },
  });

  return handleResponse(response);
};

/**
 * Create an order to start the transaction.
 * See https://developer.paypal.com/docs/api/orders/v2/#orders_create
 */
const createOrder = async (cart) => {
  // use the cart information passed from the front-end to calculate the purchase unit details
  console.log(
    "shopping cart information passed from the frontend createOrder() callback:",
    cart,
  );

  const accessToken = await generateAccessToken();
  const url = `${base}/v2/checkout/orders`;
  const payload = {
    intent: "CAPTURE",
    purchase_units: [
      {
        amount: {
          currency_code: "USD",
          value: "100.00",
        },
      },
    ],
  };

  const response = await fetch(url, {
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${accessToken}`,
      // Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
      // https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
      // "PayPal-Mock-Response": '{"mock_application_codes": "MISSING_REQUIRED_PARAMETER"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "PERMISSION_DENIED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
    },
    method: "POST",
    body: JSON.stringify(payload),
  });

  return handleResponse(response);
};

/**
 * Capture payment for the created order to complete the transaction.
 * See https://developer.paypal.com/docs/api/orders/v2/#orders_capture
 */
const captureOrder = async (orderID) => {
  const accessToken = await generateAccessToken();
  const url = `${base}/v2/checkout/orders/${orderID}/capture`;

  const response = await fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${accessToken}`,
      // Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
      // https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
      // "PayPal-Mock-Response": '{"mock_application_codes": "INSTRUMENT_DECLINED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "TRANSACTION_REFUSED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
    },
  });

  return handleResponse(response);
};

async function handleResponse(response) {
  try {
    const jsonResponse = await response.json();
    return {
      jsonResponse,
      httpStatusCode: response.status,
    };
  } catch (err) {
    const errorMessage = await response.text();
    throw new Error(errorMessage);
  }
}

// render checkout page with client id & unique client token
app.get("/", async (req, res) => {
  try {
    const { jsonResponse } = await generateClientToken();
    res.render("checkout", {
      clientId: PAYPAL_CLIENT_ID,
      clientToken: jsonResponse.client_token,
    });
  } catch (err) {
    res.status(500).send(err.message);
  }
});

app.post("/api/orders", async (req, res) => {
  try {
    // use the cart information passed from the front-end to calculate the order amount detals
    const { cart } = req.body;
    const { jsonResponse, httpStatusCode } = await createOrder(cart);
    res.status(httpStatusCode).json(jsonResponse);
  } catch (error) {
    console.error("Failed to create order:", error);
    res.status(500).json({ error: "Failed to create order." });
  }
});

app.post("/api/orders/:orderID/capture", async (req, res) => {
  try {
    const { orderID } = req.params;
    const { jsonResponse, httpStatusCode } = await captureOrder(orderID);
    res.status(httpStatusCode).json(jsonResponse);
  } catch (error) {
    console.error("Failed to create order:", error);
    res.status(500).json({ error: "Failed to capture order." });
  }
});

app.listen(PORT, () => {
  console.log(`Node server listening at http://localhost:${PORT}/`);
});
```

<details><summary>This is a breakdown of the <code>/server/server.js</code> code sample.</summary>

###### Declare imports

 This section of code imports the dependencies for your Node.js application:

```javascript
import express from "express";
import fetch from "node-fetch";
import "dotenv/config";
```

<ul>
  <li>
    Line 1 imports the Express.js framework to get started with creating a web server.
  </li>
  <li>
    Line 2 imports a <code>node-fetch</code> dependency needed to make <code>http</code> requests to PayPal REST APIs.
  </li>
  <li>
    Line 3 imports the dotenv library needed for loading sensitive data from environment variables, such as a PayPal client secret.
  </li>
</ul>

###### Set up port and server

This section of code collects the environment variables, sets up the port to run your server, and sets the base sandbox URL:

```javascript"
const { PAYPAL_CLIENT_ID, PAYPAL_CLIENT_SECRET, PORT = 8888 } = process.env;
const base = "https://api-m.sandbox.paypal.com";
```

Lines 7-10 start the express Node.js web application framework:

```javascript
const app = express();
app.set("view engine", "ejs");
app.set("views", "./server/views");
app.use(express.static("client"));
```

Line 8 declares that the rendering engine uses Embedded JavaScript templates.

###### Generate client token

A client token uniquely identifies your payer. You need a client token for the payer so your app can use the hosted card fields. The following code sample creates a client token for you by making a <code>POST</code> call to the <code>/v1/identity/generate-token</code> endpoint:

```javascript
/**
 * Generate a client token for rendering the hosted card fields.
 * See https://developer.paypal.com/docs/checkout/advanced/sdk/v1/#link-integratebackend
 */
const generateClientToken = async () => {
  const accessToken = await generateAccessToken();
  const url = `${base}/v1/identity/generate-token`;
  const response = await fetch(url, {
    method: "POST",
    headers: {
      Authorization: `Bearer ${accessToken}`,
      "Accept-Language": "en_US",
      "Content-Type": "application/json",
    },
  });

  return handleResponse(response);
};
```

This code runs your app on <code>localhost</code>, using the port <code>8888</code> that you set up in line 5 of the API call:

```javascript
app.listen(PORT, () => {
  console.log(`Node server listening at http://localhost:${PORT}/`);
});
```

###### Render checkout page

Set up your app's checkout page to load this section of code when it's rendered by your server:

```javascript
// render checkout page with client id & unique client token
app.get("/", async (req, res) => {
  try {
    const { jsonResponse } = await generateClientToken();
    res.render("checkout", {
      clientId: PAYPAL_CLIENT_ID,
      clientToken: jsonResponse.client_token,
    });
  } catch (err) {
    res.status(500).send(err.message);
  }
});

app.post("/api/orders", async (req, res) => {
  try {
    // use the cart information passed from the front-end to calculate the order amount details
    const { cart } = req.body;
    const { jsonResponse, httpStatusCode } = await createOrder(cart);
    res.status(httpStatusCode).json(jsonResponse);
  } catch (error) {
    console.error("Failed to create order:", error);
    res.status(500).json({ error: "Failed to create order." });
  }
});

app.post("/api/orders/:orderID/capture", async (req, res) => {
  try {
    const { orderID } = req.params;
    const { jsonResponse, httpStatusCode } = await captureOrder(orderID);
    res.status(httpStatusCode).json(jsonResponse);
  } catch (error) {
    console.error("Failed to create order:", error);
    res.status(500).json({ error: "Failed to capture order." });
  }
});
```

<ul>
  <li>
    Line 143 generates a client token by calling the <code>generateClientToken()</code> function.
  </li>
  <li>
    Lines 144-147 render the checkout page, pass the <code>clientId</code> and <code>clientToken</code> to the page, and inject the value into the script tag.
  </li>
</ul>

###### Run createOrder()

This section of code defines a <code>createOrder()</code> callback function for the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_create" target="_blank">Create orders</a> endpoint of the Orders v2 API. Call the function when the payment is submitted, for example, when the payer selects the PayPal button, or submits a card payment. See the <code>/client/app.js</code> section for more information.

This <code>createOrder()</code> callback returns a promise that contains the <code>orderID</code>. You can customize this callback for many use cases, such as a  physical inventory for a cart, or a digital good with a fixed amount.

> **Important:** To keep your integration secure, don't pass dollar amounts in your finished integration. Define your <code>purchase_units</code> payload on the server side and pass the <code>cart</code> array from the front-end to the server.

```javascript
/**
 * Create an order to start the transaction.
 * See https://developer.paypal.com/docs/api/orders/v2/#orders_create
 */
const createOrder = async (cart) => {
  // use the cart information passed from the front-end to calculate the purchase unit details
  console.log(
    "shopping cart information passed from the frontend createOrder() callback:",
    cart,
  );

  const accessToken = await generateAccessToken();
  const url = `${base}/v2/checkout/orders`;
  const payload = {
    intent: "CAPTURE",
    purchase_units: [
      {
        amount: {
          currency_code: "USD",
          value: "100.00",
        },
      },
    ],
  };

  const response = await fetch(url, {
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${accessToken}`,
      // Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
      // https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
      // "PayPal-Mock-Response": '{"mock_application_codes": "MISSING_REQUIRED_PARAMETER"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "PERMISSION_DENIED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
    },
    method: "POST",
    body: JSON.stringify(payload),
  });

  return handleResponse(response);
};
```

<ul>
  <li>
    Line 65 passes information from the <code>cart</code> into the <code>createOrder</code> function.
  </li>
  <li>
    Line 72 checks that you have the correct access token.
  </li>
  <li>
    Line 73 sets up the <code>url</code> for the API call.
  </li>
  <li>
    Lines 74-84 pass the <code>intent</code> and <code>purchase_units</code> to an object called <code>payload</code>. This gets passed to the API call.
  </li>
  <li>
    Lines 86-98 create an order by sending a <code>POST</code> request to the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_create" target="_blank">Create orders</a> endpoint of the Orders v2 API, using <code>accessToken</code>, <code>url</code>, and the <code>payload</code> from lines 74-84.
  </li>
  <li>
    Line 97 converts the <code>payload</code> information into JSON format and passes it into the <code>body</code> section of the request.
  </li>
</ul>

###### Negative testing for createOrder()

This section of the <code>createOrder()</code> function provides 3 negative testing opportunities behind content tags:

<ul>
  <li>
    <code>MISSING_REQUIRED_PARAMETER</code>
  </li>
  <li>
    <code>PERMISSION_DENIED</code>
  </li>
  <li>
    <code>INTERNAL_SERVER_ERROR</code>
  </li>
</ul>

Remove the <code>//</code> from the beginning of a line to simulate that error. the <code>createOrder()</code> call will pass that line as a <a href="https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/" target="_blank"><code>PayPal-Mock-Response</code></a> header in the <code>POST</code> request to the Orders v2 API:

```javascript
// Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
// https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
// "PayPal-Mock-Response": '{"mock_application_codes": "MISSING_REQUIRED_PARAMETER"}'
// "PayPal-Mock-Response": '{"mock_application_codes": "PERMISSION_DENIED"}'
// "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
```

###### Run captureOrder()

This section of code defines the <code>captureOrder()</code> function. Call the function to capture the order and move money from the payer's payment method to the seller:

```javascript
/**
 * Capture payment for the created order to complete the transaction.
 * See https://developer.paypal.com/docs/api/orders/v2/#orders_capture
 */
const captureOrder = async (orderID) => {
  const accessToken = await generateAccessToken();
  const url = `${base}/v2/checkout/orders/${orderID}/capture`;

  const response = await fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${accessToken}`,
      // Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
      // https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
      // "PayPal-Mock-Response": '{"mock_application_codes": "INSTRUMENT_DECLINED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "TRANSACTION_REFUSED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
    },
  });

  return handleResponse(response);
};
```
<ul>
  <li>
    Line 107 passes the <code>orderID</code> from the request parameters into the <code>createOrder</code> function.
  </li>
  <li>
    Line 108 checks that you have the correct access token.
  </li>
  <li>
    Line 109 sets up the <code>url</code> for the API call, which includes the <code>orderID</code>.
  </li>
  <li>
    Lines 111-122 capture an order by sending a <code>POST</code> request to the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_capture" target="_blank">Capture payment</a> endpoint of the Orders v2 API, using <code>accessToken</code> and <code>url</code>.
  </li>
</ul>

See <code>/client/app.js</code> in the next section for more details on capturing payments from the front-end.

###### Negative testing for captureOrder()

This section of the <code>captureOrder()</code> function provides 3 negative testing opportunities behind content tags:

<ul>
  <li>
    <code>INSTRUMENT_DECLINED</code>
  </li>
  <li>
    <code>TRANSACTION_REFUSED</code>
  </li>
  <li>
    <code>INTERNAL_SERVER_ERROR</code>
  </li>
</ul>

Remove the <code>//</code> from the beginning of a line to simulate that error. The <code>captureOrder()</code> call will pass that line as a <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_capture" target="_blank"><code>PayPal-Mock-Response</code></a> header in the <code>POST</code> request to the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_capture" target="_blank">Capture payment</a> endpoint of the Orders v2 API:

```javascript
// Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
// https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
// "PayPal-Mock-Response": '{"mock_application_codes": "INSTRUMENT_DECLINED"}'
// "PayPal-Mock-Response": '{"mock_application_codes": "TRANSACTION_REFUSED"}'
// "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
```

</details>

###### Test server

Run <code>npm start</code> to confirm your setup is correct.

This command starts the server on <code>localhost:8888</code>. You can specify a port number by modifying line 4 in the sample <code>/server/server.js</code> file.

##### server/views/checkout.ejs

```html
<!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>PayPal JS SDK Advanced Integration</title>
      <link
        rel="stylesheet"
        type="text/css"
        href="https://www.paypalobjects.com/webstatic/en_US/developer/docs/css/cardfields.css"
      >
      <script
        src="https://www.paypal.com/sdk/js?components=buttons,hosted-fields&client-id=<%= clientId %>"
        data-client-token="<%= clientToken %>"
      ></script>
    </head>
    <body>
      <div id="paypal-button-container" class="paypal-button-container"></div>
      <div class="card_container">
        <form id="card-form">
          <label for="card-number">Card Number</label>
          <div id="card-number" class="card_field"></div>
          <div style="display: flex; flex-direction: row">
            <div>
              <label for="expiration-date">Expiration Date</label>
              <div id="expiration-date" class="card_field"></div>
            </div>
            <div style="margin-left: 10px">
              <label for="cvv">CVV</label>
              <div id="cvv" class="card_field"></div>
            </div>
          </div>
          <label for="card-holder-name">Name on Card</label>
          <input
            type="text"
            id="card-holder-name"
            name="card-holder-name"
            autocomplete="off"
            placeholder="card holder name"
          >
          <div>
            <label for="card-billing-address-street">Billing Address</label>
            <input
              type="text"
              id="card-billing-address-street"
              name="card-billing-address-street"
              autocomplete="off"
              placeholder="street address"
            >
          </div>
          <div>
            <label for="card-billing-address-unit">&nbsp;</label>
            <input
              type="text"
              id="card-billing-address-unit"
              name="card-billing-address-unit"
              autocomplete="off"
              placeholder="unit"
            >
          </div>
          <div>
            <input
              type="text"
              id="card-billing-address-city"
              name="card-billing-address-city"
              autocomplete="off"
              placeholder="city"
            >
          </div>
          <div>
            <input
              type="text"
              id="card-billing-address-state"
              name="card-billing-address-state"
              autocomplete="off"
              placeholder="state"
            >
          </div>
          <div>
            <input
              type="text"
              id="card-billing-address-zip"
              name="card-billing-address-zip"
              autocomplete="off"
              placeholder="zip / postal code"
            >
          </div>
          <div>
            <input
              type="text"
              id="card-billing-address-country"
              name="card-billing-address-country"
              autocomplete="off"
              placeholder="country code"
            >
          </div>
          <br><br>
          <button value="submit" id="submit" class="btn">Pay</button>
        </form>
        <p id="result-message"></p>
      </div>
      <script src="app.js"></script>
    </body>
  </html>
```

<details><summary>This is a breakdown of the <code>/server/views/checkout.ejs</code> code sample.</summary>

###### Import style sheet

This section calls the JavaScript SDK that defines the PayPal buttons:

```javascript
<link
  rel="stylesheet"
  type="text/css"
  href="https://www.paypalobjects.com/webstatic/en_US/developer/docs/css/cardfields.css"
>
```

<ul>
  <li>
    Lines 7-11 declare a sample CSS file for demonstration purposes. Replace these with styles that align with your brand using the <a href="https://developer.paypal.com/docs/checkout/advanced/customize/card-field-style/" target="_blank">CSS properties supported by this integration</a>.
  </li>
  <li>
    Optional: The <a href="https://developer.paypal.com/sdk/js/configuration/" target="_blank">JavaScript SDK</a> has configurations that you can override, such as <code>currency</code> and <code>intent</code>.
  </li>
</ul>

###### Add PayPal button

Include the PayPal Checkout button before you request the credit card fields, or on the same page that you request this information. For more information, see Section 8, <strong>Required Use of PayPal Checkout, PayPal Credit</strong>, in the <a href="https://www.paypal.com/us/legalhub/pocpsa-full?_ga=1.169690530.248280996.1670866755#pocpsa-full-8" target="_blank">PayPal Online Card Payments Services Agreement</a>.

```javascript
<div id="paypal-button-container" class="paypal-button-container"></div>
```

###### Create your card form

This section of code shows how to create the form fields and <strong>Submit</strong> button you need to take card payments:

```javascript
<div class="card_container">
  <form id="card-form">
    <label for="card-number">Card Number</label>
    <div id="card-number" class="card_field"></div>
    <div style="display: flex; flex-direction: row">
      <div>
        <label for="expiration-date">Expiration Date</label>
        <div id="expiration-date" class="card_field"></div>
      </div>
      <div style="margin-left: 10px">
        <label for="cvv">CVV</label>
        <div id="cvv" class="card_field"></div>
      </div>
    </div>
    <label for="card-holder-name">Name on Card</label>
    <input
      type="text"
      id="card-holder-name"
      name="card-holder-name"
      autocomplete="off"
      placeholder="card holder name"
    >
    <div>
      <label for="card-billing-address-street">Billing Address</label>
      <input
        type="text"
        id="card-billing-address-street"
        name="card-billing-address-street"
        autocomplete="off"
        placeholder="street address"
      >
    </div>
    <div>
      <label for="card-billing-address-unit">&nbsp;</label>
      <input
        type="text"
        id="card-billing-address-unit"
        name="card-billing-address-unit"
        autocomplete="off"
        placeholder="unit"
      >
    </div>
    <div>
      <input
        type="text"
        id="card-billing-address-city"
        name="card-billing-address-city"
        autocomplete="off"
        placeholder="city"
      >
    </div>
    <div>
      <input
        type="text"
        id="card-billing-address-state"
        name="card-billing-address-state"
        autocomplete="off"
        placeholder="state"
      >
    </div>
    <div>
      <input
        type="text"
        id="card-billing-address-zip"
        name="card-billing-address-zip"
        autocomplete="off"
        placeholder="zip / postal code"
      >
    </div>
    <div>
      <input
        type="text"
        id="card-billing-address-country"
        name="card-billing-address-country"
        autocomplete="off"
        placeholder="country code"
      >
    </div>
    <br><br>
    <button value="submit" id="submit" class="btn">Pay</button>
  </form>
  <p id="result-message"></p>
</div>
```

<ul>
  <li>
    Lines 19-99 declare a <code>card-form</code> object with fields for <code>card-number</code>, <code>expiration-date</code>, <code>cvv</code>, <code>card-holder-name</code>, and billing address information. See the <a target="_blank" href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">Orders v2 API</a> for details about billing address fields and other parameters. For example, use the <a target="_blank" href="https://developer.paypal.com/api/rest/reference/country-codes/">2-character country code</a> to test the billing address.
  </li>
  <li>
    Line 100 declares a <code>result-message</code> object that displays the output of the <code>resultMessage</code> function from lines 107-110 of the <code>/client/app.js</code> file.
  </li>
  <li>
    The fields in this example match up with fields from lines 145-169 of the <strong>Capture eligible payment</strong> code sample.
  </li>
</ul>

###### Import app.js

This code sample renders the hosted card fields for an eligible payment by importing the <code>/client/app.js</code> file that you created:

```javascript
<script src="app.js"></script>
```

</details>

## 3. Integrate front end

This section explains how to set up your front end to integrate advanced Checkout payments.

### Front-end process

<ol>
  <li>
    Your app displays the PayPal Checkout button and the card checkout form.
  </li>
  <li>
    Your app calls server endpoints to create the order and capture payment. The specific method depends on whether the buyer uses the PayPal button or checkout form.
  </li>
</ol>

### Front-end code

The <code>/client/app.js</code> file handles the client-side logic and defines how the PayPal front-end components connect with the back-end. Use this file to set up the PayPal checkout using the PayPal JavaScript SDK, and handle the payer's interactions with the PayPal checkout button.

You'll need to save the <code>app.js</code> file in a folder named <code>/client</code>:

##### /client/app.js

```javascript
async function createOrderCallback() {
  try {
    const response = await fetch("/api/orders", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      // use the "body" param to optionally pass additional order information
      // like product ids and quantities
      body: JSON.stringify({
        cart: [
          {
            id: "YOUR_PRODUCT_ID",
            quantity: "YOUR_PRODUCT_QUANTITY",
          },
        ],
      }),
    });

    const orderData = await response.json();

    if (orderData.id) {
      return orderData.id;
    } else {
      const errorDetail = orderData?.details?.[0];
      const errorMessage = errorDetail
        ? `${errorDetail.issue} ${errorDetail.description} (${orderData.debug_id})`
        : JSON.stringify(orderData);

      throw new Error(errorMessage);
    }
  } catch (error) {
    console.error(error);
    resultMessage(`Could not initiate PayPal Checkout...<br><br>${error}`);
  }
}

async function onApproveCallback(data, actions) {
  try {
    const response = await fetch(`/api/orders/${data.orderID}/capture`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
    });

    const orderData = await response.json();
    // Three cases to handle:
    //   (1) Recoverable INSTRUMENT_DECLINED -> call actions.restart()
    //   (2) Other non-recoverable errors -> Show a failure message
    //   (3) Successful transaction -> Show confirmation or thank you message

    const transaction =
      orderData?.purchase_units?.[0]?.payments?.captures?.[0] ||
      orderData?.purchase_units?.[0]?.payments?.authorizations?.[0];
    const errorDetail = orderData?.details?.[0];

    // this actions.restart() behavior only applies to the Buttons component
    if (errorDetail?.issue === "INSTRUMENT_DECLINED" && !data.card && actions) {
      // (1) Recoverable INSTRUMENT_DECLINED -> call actions.restart()
      // recoverable state, per https://developer.paypal.com/docs/checkout/standard/customize/handle-funding-failures/
      return actions.restart();
    } else if (
      errorDetail ||
      !transaction ||
      transaction.status === "DECLINED"
    ) {
      // (2) Other non-recoverable errors -> Show a failure message
      let errorMessage;
      if (transaction) {
        errorMessage = `Transaction ${transaction.status}: ${transaction.id}`;
      } else if (errorDetail) {
        errorMessage = `${errorDetail.description} (${orderData.debug_id})`;
      } else {
        errorMessage = JSON.stringify(orderData);
      }

      throw new Error(errorMessage);
    } else {
      // (3) Successful transaction -> Show confirmation or thank you message
      // Or go to another URL:  actions.redirect('thank_you.html');
      resultMessage(
        `Transaction ${transaction.status}: ${transaction.id}<br><br>See console for all available details`,
      );
      console.log(
        "Capture result",
        orderData,
        JSON.stringify(orderData, null, 2),
      );
    }
  } catch (error) {
    console.error(error);
    resultMessage(
      `Sorry, your transaction could not be processed...<br><br>${error}`,
    );
  }
}

window.paypal
  .Buttons({
    createOrder: createOrderCallback,
    onApprove: onApproveCallback,
  })
  .render("#paypal-button-container");

// Example function to show a result to the user. Your site's UI library can be used instead.
function resultMessage(message) {
  const container = document.querySelector("#result-message");
  container.innerHTML = message;
}

// If this returns false or the card fields aren't visible, see Step #1.
if (window.paypal.HostedFields.isEligible()) {
  // Renders card fields
  window.paypal.HostedFields.render({
    // Call your server to set up the transaction
    createOrder: createOrderCallback,
    styles: {
      ".valid": {
        color: "green",
      },
      ".invalid": {
        color: "red",
      },
    },
    fields: {
      number: {
        selector: "#card-number",
        placeholder: "4111 1111 1111 1111",
      },
      cvv: {
        selector: "#cvv",
        placeholder: "123",
      },
      expirationDate: {
        selector: "#expiration-date",
        placeholder: "MM/YY",
      },
    },
  }).then((cardFields) => {
    document.querySelector("#card-form").addEventListener("submit", (event) => {
      event.preventDefault();
      cardFields
        .submit({
          // Cardholder's first and last name
          cardholderName: document.getElementById("card-holder-name").value,
          // Billing Address
          billingAddress: {
            // Street address, line 1
            streetAddress: document.getElementById(
              "card-billing-address-street",
            ).value,
            // Street address, line 2 (Ex: Unit, Apartment, etc.)
            extendedAddress: document.getElementById(
              "card-billing-address-unit",
            ).value,
            // State
            region: document.getElementById("card-billing-address-state").value,
            // City
            locality: document.getElementById("card-billing-address-city")
              .value,
            // Postal Code
            postalCode: document.getElementById("card-billing-address-zip")
              .value,
            // Country Code
            countryCodeAlpha2: document.getElementById(
              "card-billing-address-country",
            ).value,
          },
        })
        .then((data) => {
          return onApproveCallback(data);
        })
        .catch((orderData) => {
          resultMessage(
            `Sorry, your transaction could not be processed...<br><br>${JSON.stringify(
              orderData,
            )}`,
          );
        });
    });
  });
} else {
  // Hides card fields if the merchant isn't eligible
  document.querySelector("#card-form").style = "display: none";
}
```

<details><summary>This breakdown focuses on key lines from the <code>/client/app.js</code> code sample.</summary>

###### Create order

This code sample defines the <code>createOrder()</code> function:

```javascript
async function createOrderCallback() {
  try {
    const response = await fetch("/api/orders", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      // use the "body" param to optionally pass additional order information
      // like product ids and quantities
      body: JSON.stringify({
        cart: [
          {
            id: "YOUR_PRODUCT_ID",
            quantity: "YOUR_PRODUCT_QUANTITY",
          },
        ],
      }),
    });

    const orderData = await response.json();

    if (orderData.id) {
      return orderData.id;
    } else {
      const errorDetail = orderData?.details?.[0];
      const errorMessage = errorDetail
        ? `${errorDetail.issue} ${errorDetail.description} (${orderData.debug_id})`
        : JSON.stringify(orderData);

      throw new Error(errorMessage);
    }
  } catch (error) {
    console.error(error);
    resultMessage(`Could not initiate PayPal Checkout...<br><br>${error}`);
  }
}
```

This code sample defines the <code>onApprove()</code> function:

```javascript
async function onApproveCallback(data, actions) {
  try {
    const response = await fetch(`/api/orders/${data.orderID}/capture`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
    });

    const orderData = await response.json();
    // Three cases to handle:
    //   (1) Recoverable INSTRUMENT_DECLINED -> call actions.restart()
    //   (2) Other non-recoverable errors -> Show a failure message
    //   (3) Successful transaction -> Show confirmation or thank you message

    const transaction =
      orderData?.purchase_units?.[0]?.payments?.captures?.[0] ||
      orderData?.purchase_units?.[0]?.payments?.authorizations?.[0];
    const errorDetail = orderData?.details?.[0];

    // this actions.restart() behavior only applies to the Buttons component
    if (errorDetail?.issue === "INSTRUMENT_DECLINED" && !data.card && actions) {
      // (1) Recoverable INSTRUMENT_DECLINED -> call actions.restart()
      // recoverable state, per https://developer.paypal.com/docs/checkout/standard/customize/handle-funding-failures/
      return actions.restart();
    } else if (
      errorDetail ||
      !transaction ||
      transaction.status === "DECLINED"
    ) {
      // (2) Other non-recoverable errors -> Show a failure message
      let errorMessage;
      if (transaction) {
        errorMessage = `Transaction ${transaction.status}: ${transaction.id}`;
      } else if (errorDetail) {
        errorMessage = `${errorDetail.description} (${orderData.debug_id})`;
      } else {
        errorMessage = JSON.stringify(orderData);
      }

      throw new Error(errorMessage);
    } else {
      // (3) Successful transaction -> Show confirmation or thank you message
      // Or go to another URL:  actions.redirect('thank_you.html');
      resultMessage(
        `Transaction ${transaction.status}: ${transaction.id}<br><br>See console for all available details`,
      );
      console.log(
        "Capture result",
        orderData,
        JSON.stringify(orderData, null, 2),
      );
    }
  } catch (error) {
    console.error(error);
    resultMessage(
      `Sorry, your transaction could not be processed...<br><br>${error}`,
    );
  }
}
```

<ul>
  <li>
    Line 40 calls your server's capture endpoint to capture the order.
  </li>
  <li>
    Lines 58-97 declare how to handle the payment capture response.
  </li>
  <li>
    Lines 59-79 declare what happens when the payer's instrument is declined.
  </li>
  <li>
    Lines 79-90 declare what happens when the payment is successfully captured. When you're ready to go live, you can remove the alert and either show a success message or redirect the payer to another URL.
  </li>
  <li>
    Lines 91-96 pass an error message to the <code>console</code>.
  </li>
</ul>

###### PayPal Button JavaScript

This section calls the JavaScript SDK that defines the PayPal buttons:

```javascript
window.paypal
  .Buttons({
    createOrder: createOrderCallback,
    onApprove: onApproveCallback,
  })
  .render("#paypal-button-container");
```

###### Send results to user

This section declares a <code>resultMessage</code> function that shows a message to the user by passing data to the <code>result-message</code> HTML element container in line 100 of the <code>/server/views/checkout.ejs</code>:

```javascript
// Example function to show a result to the user. Your site's UI library can be used instead.
function resultMessage(message) {
  const container = document.querySelector("#result-message");
  container.innerHTML = message;
```

Lines 108-109 direct the message to the HTML element container.

###### Check for HostedFields eligibility

Hosted card fields use the JavaScript SDK to help non-PCI-compliant sellers save a payer's card data and create a token for future payments. During an eligible payment, the hosted fields show up in the payment experience and prompt the payer for consent to save their card data. For more information about hosted fields, see <a target="_blank" href="https://developer.paypal.com/sdk/js/reference/#hosted-fields">Hosted fields</a>.

> **Note:** You need to complete the account setup in sandbox to be eligible for testing hosted fields.

This code sample checks to see if a payment is eligible for hosted card fields. If not, the hosted card fields won’t show up during the payment flow:

```javascript
// If this returns false or the card fields aren't visible, see Step #1.
if (window.paypal.HostedFields.isEligible()) {
  // Renders card fields
  window.paypal.HostedFields.render(
  {...}
  } else {
  // Hides card fields if the merchant isn't eligible
  document.querySelector("#card-form").style = "display: none";
  }
```

You can modify this code to show a custom message for eligible or ineligible payments.

###### Render hosted card fields and create order

This code sample renders the hosted card fields for an eligible payment:

```javascript
// Renders card fields
  window.paypal.HostedFields.render({
    // Call your server to set up the transaction
    createOrder: createOrderCallback,
    styles: {
      ".valid": {
        color: "green",
      },
      ".invalid": {
        color: "red",
      },
    },
    fields: {
      number: {
        selector: "#card-number",
        placeholder: "4111 1111 1111 1111",
      },
      cvv: {
        selector: "#cvv",
        placeholder: "123",
      },
      expirationDate: {
        selector: "#expiration-date",
        placeholder: "MM/YY",
      },
    },
  })
```

<ul>
  <li>
    Line 117 creates the order by calling the <code>createOrderCallback</code> function.
  </li>
  <li>
    Lines 118-125 define styles for the hosted card fields. You can change these styles as needed for your implementation.
  </li>
  <li>
    Lines 126-139 define the <code>selector</code> and <code>placeholder</code> values for the input fields. You can edit this section as needed for your implementation, such as adding more fields. For more information about optional configurations, see <a target="_blank" href="https://developer.paypal.com/sdk/js/reference/#link-options">Options in the JavaScript SDK reference</a>.
  </li>
</ul>

###### Capture eligible payment

This code sample captures the payment when it is eligible for hosted card fields. Add this code to the PayPal button in <code>/client/app.js</code>, right after rendering the card fields:

```javascript
.then((cardFields) => {
    document.querySelector("#card-form").addEventListener("submit", (event) => {
      event.preventDefault();
      cardFields
        .submit({
          // Cardholder's first and last name
          cardholderName: document.getElementById("card-holder-name").value,
          // Billing Address
          billingAddress: {
            // Street address, line 1
            streetAddress: document.getElementById(
              "card-billing-address-street",
            ).value,
            // Street address, line 2 (Ex: Unit, Apartment, etc.)
            extendedAddress: document.getElementById(
              "card-billing-address-unit",
            ).value,
            // State
            region: document.getElementById("card-billing-address-state").value,
            // City
            locality: document.getElementById("card-billing-address-city")
              .value,
            // Postal Code
            postalCode: document.getElementById("card-billing-address-zip")
              .value,
            // Country Code
            countryCodeAlpha2: document.getElementById(
              "card-billing-address-country",
            ).value,
          },
        })
        .then((data) => {
          return onApproveCallback(data);
        })
        .catch((orderData) => {
          resultMessage(
            `Sorry, your transaction could not be processed...<br><br>${JSON.stringify(
              orderData,
            )}`,
          );
        });
    });
  });
```

<ul>
  <li>
    Line 140 sets up an event listener for when the payer submits an eligible card payment.
  </li>
  <li>
    Lines 143-170 pass the hosted card field values, such as the cardholder's name and address, to the <code>POST</code> call in lines 128-131. Anything you pass into the submit is sent to the iframe that communicates with the Orders API. The iframe retrieves the data and sends it along to the <code>POST</code> call. See the <a target="_blank" href="https://developer.paypal.com/docs/api/orders/v2/">Orders v2 API</a> for details about billing address fields and other parameters. For example, use the <a target="_blank" href="https://developer.paypal.com/api/rest/reference/country-codes/">2-character country code</a> to test the billing address.
  </li>
  <li>
    Lines 171-173 call the <code>onApproveCallback</code> function from lines 38-97, which sends a <code>POST</code> call to <code>/v2/checkout/orders/&#123;id&#125;/capture</code> that captures the order using the <code>orderId</code> in the <code>data</code> object in <code>/server/server.js</code>.
  </li>
  <li>
    Lines 174-178 pass an error message if the payment isn't successful.
  </li>
</ul>

</details>

### Run front end integration

<ul>
  <li>
    Run <code>npm start</code> to run your server.
  </li>
  <li>
    Open your browser and navigate to <code>localhost:8888</code>.
  </li>
  <li>
    When your server is running, proceed to the next section to test your integration.
  </li>
</ul>

## 4. Test integration

Before going live, test your integration in the <a target="_blank" href="https://developer.paypal.com/tools/sandbox/">sandbox environment</a>.

Learn more about the following resources on the <a target="_blank" href="https://developer.paypal.com/tools/sandbox/card-testing/">Card Testing</a> page:

<ul>
  <li>
    Use <a target="_blank" href="https://developer.paypal.com/tools/sandbox/card-testing/#link-testcardnumbers">test card numbers</a> to simulate successful payments for advanced Checkout integrations.
  </li>
  <li>
    Use <a target="_blank" href="https://developer.paypal.com/tools/sandbox/card-testing/#link-rejectiontriggers">rejection triggers</a> to simulate card error scenarios.
  </li>
  <li>
    Test <a target="_blank" href="https://developer.paypal.com/tools/sandbox/card-testing/#link-simulate3dsecurecardpayments">3D Secure authentication</a> scenarios.
  </li>
  <li>
    Test your integration by following <a target="_blank" href="https://developer.paypal.com/tools/sandbox/card-testing/#link-testintegration">these recommended use cases</a>. See the <a target="_blank" href="https://developer.paypal.com/docs/api/orders/v2/">Orders v2 API</a> for details about billing address fields and other parameters. For example, use the <a target="_blank" href="https://developer.paypal.com/api/rest/reference/country-codes/">2-character country code</a> to test the billing address.
  </li>
</ul>

> **Note:** Use the <a target="_blank" href="https://developer.paypal.com/tools/sandbox/card-testing/#link-creditcardgenerator">credit card generator</a> to generate additional test credit cards for sandbox testing.

## 5. Go Live

If you have fulfilled the requirements for accepting Advanced Credit and Debit Card Payments for your <a target="_blank"  href="https://www.paypal.com/myaccount/bundle/business/upgrade">business account</a>, review the <a target="_blank" href="https://developer.paypal.com/api/rest/production/" ><strong>Move your app to production</strong></a> page to learn how to test and go live.

If this is your first time testing in a live environment, follow these steps:

<ol>
  <li>
    Log into the <a target="_blank" href="https://developer.paypal.com/dashboard/">PayPal Developer Dashboard</a> with your PayPal business account.
  </li>
  <li>
    Complete <a target="_blank" href="https://www.paypal.com/bizsignup/entry?_ga=1.171321763.248280996.1670866755">production oboarding</a> so you can process card payments with your live PayPal business account.
  </li>
  <li>
    Request <a target="_blank" href="https://www.paypal.com/signin/client?flow=provisionUser&country.x=US&locale.x=en_US&_ga=1.95899167.248280996.1670866755">Advanced Credit and Debit Card Payments</a> for your business account.
  </li>
</ol>

> **Important:** The code for the integration checks eligibility requirements, so the payment card fields only display when the production request is successful.
