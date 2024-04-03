# Integrate card payments in Android apps

Accept PayPal, credit, and debit card payments in a web or native experience using the PayPal Mobile Android SDK. Use customizable PayPal buttons with your custom checkout UI to align with your business branding. For more implementation details, see the <a href="https://github.com/paypal/paypal-android/" target="_blank">PayPal GitHub repository</a>.

## Know before you code

You need a <a href="https://developer.paypal.com/tools/sandbox/accounts/" target="_blank">developer account</a> to get sandbox credentials:

* PayPal uses REST API credentials which you can get from the <a href="https://developer.paypal.com/dashboard/" target="_blank">developer dashboard</a>.
* Client ID: Authenticates your account with PayPal and identifies an app in your sandbox.
* Client secret: Authorizes an app in your sandbox. Keep this secret safe and don’t share it.

Read <a href="https://developer.paypal.com/api/rest/" target="_blank">Get started with PayPal APIs</a> for more information.

You need a combination of PayPal and third-party tools:

* <a href="https://github.com/paypal/paypal-android" target="_blank">Android SDK</a>: Adds PayPal-supported payment methods for Android.
* <a href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">Orders REST API</a>: Create, update, retrieve, authorize, and capture orders.

## 1. Before you begin your integration

### Check your account setup for advanced card payments

This integration requires a sandbox business account with the Advanced Credit and Debit Card Payments capability. Your account should automatically have this capability.

To confirm that Advanced Credit and Debit Card Payments are enabled for you, check your sandbox business account as follows:

1. Log into the <a href="https://developer.paypal.com/dashboard/" target="_blank"><strong>PayPal Developer Dashboard<strong></a>, toggle **Sandbox**, and go to **Apps & Credentials**.
2. In **REST API apps**, select the name of your app.
3. Go to **Features** > **Accept payments**.
4. Select the **Advanced Credit and Debit Card Payments** checkbox and select **Save Changes**.

> **Note:** If you created a sandbox business account through <a href="https://www.sandbox.paypal.com/?_ga=1.158343865.248280996.1670866755" target="_blank">sandbox.paypal.com</a>, and the advanced credit and debit card payments status for the account is disabled, <a href="https://www.sandbox.paypal.com/bizsignup/#/checkAccount" target="_blank">complete the sandbox onboarding steps</a>.

### Check 3D Secure requirements

Add 3D Secure to reduce the chance of fraud and improve the payment experience by authenticating a cardholder through their card issuer.

Visit our <a href="https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/" target="_blank">3D Secure</a> page to see if 3D Secure is required in your region and learn more about implementing 3DS in your app.

## 2. Integrate the SDK into your app

The PayPal Mobile SDK is available through Maven Central. Add the `mavenCentral` repository to the `build.gradle` file of your project root:

```javascript
allprojects {
  repositories {
    mavenCentral()
  }
}
```

### Snapshot builds

You can also use snapshot builds to test upcoming features before release. To include a snapshot build:

### 1. Add snapshots repository

Add the snapshots repository to the `build.gradle` file of your project root.

```javascript
allprojects {
  repositories {
    mavenCentral()
    maven {
      url 'https://oss.sonatype.org/content/repositories/snapshots/'
    }
  }
}
```
<br />

### 2. Add snapshot to dependencies

Then, add a snapshot build by adding `-SNAPSHOT` to the current dependency version. For example, if you want to add a snapshot build for `CardPayments`, add the following:

```javascript
dependencies {
  implementation 'com.paypal.android:card-payments:CURRENT-VERSION-SNAPSHOT'
}
```

## 3. Payment integrations

Integrate 3 different types of payments using the PayPal Mobile SDK:

* **Card payments:** Add card fields that align with your branding.
* **PayPal native payments:** Launch a checkout page within your app, instead of a popup.
* **PayPal web payments:** A lighter integration that launches a checkout page in a browser within your app.

### Integrate with card payments

Build and customize the card fields to align with your branding.

### 1. Add card payments module to your app

Add the `card-payments` package dependency in your app's `build.gradle` file:

```javascript
dependencies {
  implementation "com.paypal.android:card-payments:CURRENT-VERSION"
}
```

### 2. Create CardClient

A `CardClient` helps you attach a card to a payment.

In your Android app:
1. Use the `CLIENT_ID` to construct a `CoreConfig`.
2. Construct a `CardClient` using your `CoreConfig` object.

```javascript
val config = CoreConfig("CLIENT_ID", environment = Environment.SANDBOX)

val cardClient = CardClient(config)
```

### 3. Get Order ID

On your server:

1. Create an `ORDER_ID` by using the <a href="https://developer.paypal.com/docs/api/orders/v2" target="_blank">Orders v2 API</a>.
2. Pass your `ACCESS_TOKEN` in the `Authorization` header. To get an `ACCESS_TOKEN`, use the <a href="https://developer.paypal.com/api/rest/authentication/" target="_blank">Authentication API</a>.
   > **Note:** This access token is only for the sandbox environment. When you're ready to go live, request a live access token by changing the request sandbox endpoint to https://api-m.paypal.com/v1/oauth2/token.
3. Pass the `intent`. You'll need to pass either `AUTHORIZE` or `CAPTURE` as the `intent` type. This type must match the `/authorize` or `/capture` endpoint you use to process your order.

#### Sample request

```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw '{
    "intent": "CAPTURE|AUTHORIZE",
    "purchase_units": [
      {
        "amount": {
          "currency_code": "USD",
          "value": "5.00"
        }
      }
    ]
  }'
```

#### Sample response

```javascript
{
  "id":"ORDER_ID",
  "status":"CREATED"
}
```

When a buyer starts a payment, send the `ORDER_ID` from your server to your client app.

### 4. Create card request

A `CardRequest` object:
* Attaches a card to an `ORDER_ID`.
* Launches 3D Secure when a payment requires additional authentication.

#### 1. Collect card payment details

Build a `card` object with the buyer's card details:

```javascript
val card = Card(
  number = "4005519200000004",
  expirationMonth = "01",
  expirationYear = "2025",
  securityCode = "123",
  billingAddress = Address(
    streetAddress = "123 Main St.",
    extendedAddress = "Apt. 1A",
    locality = "Anytown",
    region = "CA",
    postalCode = "12345",
    countryCode = "US"
  )
)
```

Collecting a billing address can reduce the number of  authentication challenges to customers.

#### 2. Build CardRequest

Build a `CardRequest` with the `card` object and your `ORDER_ID`:

```javascript
val cardRequest  = CardRequest(
  orderID = "ORDER_ID",
  card = card,
  returnUrl = "myapp://return_url", // custom URL scheme needs to be configured in AndroidManifest.xml
  sca = SCA.SCA_ALWAYS // default value is SCA.SCA_WHEN_REQUIRED
)
```

<a href="https://developer.paypal.com/api/nvp-soap/payflow/3d-secure-overview/" target="_blank">3D Secure</a>
is supported for all card payments to comply with the <a href="https://www.paypal.com/uk/webapps/mpp/PSD2?_ga=1.18434873.1625369690.1652045188" target="_blank">Second Payment Services Directive (PSD2)</a>.
PSD2 is a European Union regulation that introduces <a href="https://www.ukfinance.org.uk/our-expertise/payments-and-innovation/strong-customer-authentication" target="_blank">Strong Customer Authentication (SCA)</a> and other security requirements.

Select your SCA launch option type using the `sca` parameter in the `CardRequest` initializer:
* `SCA.SCA_WHEN_REQUIRED` launches an SCA challenge when applicable. This is enabled by default.
* `SCA.SCA_ALWAYS` requires an SCA challenge for all card transactions.

#### 3. Set up your app for browser switching

The `sca` challenge launches in a browser within your application. Your app needs to handle the browser switch between the `sca` challenge and the checkout page. Set up a return URL that returns to your app from the browser.

#### 4. Create a return URL

Provide a `returnUrl` so the browser returns to your application after the `sca` challenge finishes.

The `returnUrl` should have the following format:

```url
myapp://return_url
```

The `myapp://` portion of the `returnUrl` is a custom URL scheme that you need to register in your app's `AndroidManifest.xml`.

#### 5. Add card payment activity to the Android manifest

Update your app's `AndroidManifest.xml` with details about the card payment activity that will return the user to your app after completing the SCA check. Include the following elements:

1. Set the activity `launchMode` to `singleTop`.
2. Set the `android:scheme` on the Activity that will be responsible for handling the deep link back into the app.
2. Add an `intent-filter`.
3. Register the `myapp://` custom URL scheme in the `intent-filter`.

> Note: `android:exported` is required if your app compile SDK version is API 31 (Android 12) or later.

```javascript
<activity
  android:name=".MyCardPaymentActivity"
  android:launchMode="singleTop"
  android:exported="true"
  >
  <intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <data android:scheme="myapp" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
  </intent-filter>
</activity>
```
<br />

#### 6. Connect the card payment activity

Add `onNewIntent` to your activity:

```javascript
override fun onNewIntent(newIntent: Intent?) {
  super.onNewIntent(intent)
  intent = newIntent
}
```

### 5. Approve order

After your `CardRequest` has the card details, call `cardClient.approveOrder()` to process the payment.

```javascript
class MyCardPaymentActivity: FragmentActivity {
  fun cardCheckoutTapped(cardRequest: CardRequest) {
    cardClient.approveOrder(this, cardRequest)
  }
}
```

### 6. Handle payment result scenarios

Set up your `ApproveOrderListener` to handle successful payments, errors, cancellations, and 3D Secure transaction flows.

```javascript
class MyCardPaymentActivity: FragmentActivity, ApproveOrderListener {
  fun cardCheckoutTapped(cardRequest: CardRequest) {
    val result = cardClient.approveOrder(this, cardRequest)
  }
  fun setupCardClient() {
    cardClient.listener = this
  }
  fun onApproveOrderSuccess(result: CardResult) {
    // order was approved and is ready to be captured/authorized (see step 6)
  }
  fun onApproveOrderFailure(error: PayPalSDKError) {
    // inspect 'error' for more information
  }
  fun onApproveOrderCanceled() {
    // 3D Secure flow was canceled
  }
  fun onApproveOrderThreeDSecureWillLaunch() {
    // 3D Secure flow will launch
  }
  fun onApproveOrderThreeDSecureDidFinish() {
    // 3D Secure auth did finish successfully
  }
}
```

### 7. Authorize and capture order

Submit your `ORDER_ID` for authorization or capture when the PayPal Android SDK calls the `onApproveOrderSuccess` method.

Call the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_authorize" target="_blank"><code>authorize</code></a> endpoint of the Orders V2 API to place the money on hold:

#### Sample request: Authorize order

```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/authorize' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
```
<br />

Call the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_capture" target="_blank"><code>capture</code></a> endpoint of the Orders V2 API to capture the money immediately:

#### Sample request: Capture order

```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/capture' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
```

### 8. Test integration

Before going live, test your integration in the <a href="https://developer.paypal.com/tools/sandbox/" target="_blank">sandbox environment</a>.

Learn more about the following resources on the <a href="https://developer.paypal.com/tools/sandbox/card-testing/" target="_blank">Card Testing</a> page:

* Use <a href="tools/sandbox/card-testing/#link-testcardnumbers" target="_blank">test card numbers</a> to simulate successful payments for advanced checkout integrations.
* Use <a href="https://developer.paypal.com/tools/sandbox/card-testing/#link-rejectiontriggers" target="_blank">rejection triggers</a> to simulate card error scenarios.
* Test <a href="https://developer.paypal.com/tools/sandbox/card-testing/#link-simulate3dsecurecardpayments" target="_blank">3D Secure authentication</a> scenarios.
* Test your integration by following <a href="https://developer.paypal.com/tools/sandbox/card-testing/#link-testintegration" target="_blank">these recommended use cases</a>. See the <a href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">Orders v2 API</a> for details about billing address fields and other parameters. For example, use the <a href="https://developer.paypal.com/api/rest/reference/country-codes/" target="_blank">2-character country code</a> to test the billing address.

> **Note:** Use the <a href="https://developer.paypal.com/tools/sandbox/card-testing/#link-creditcardgenerator" target="_blank">credit card generator</a> to generate additional test credit cards for sandbox testing.

When prompted for required data for the sandbox business request, such as a phone number, enter any number that fits the required format. Because this is a sandbox request, the data doesn't have to be factual.

Before you go live, you'll need to complete <a href="https://www.paypal.com/bizsignup/entry/product/ppcp" target="_blank">live onboarding</a> to be eligible to process cards with your live PayPal account.

### Use PayPal native payments

Use `PayPalNativePayments` to add a PayPal paysheet to your app. The paysheet is a checkout page that the client launches within your app, instead of showing up as a pop-up. The paysheet shows all the PayPal payment methods available and helps the payer complete their payment.

#### Native checkout for a first-time customer

<img src="https://www.paypalobjects.com/devdoc/iOS_SDK_native-checkout-first-time-flow_01.png" alt="Mobile phone screenshots of a native checkout flow for a first-time customer, with screens that show selecting PayPal as a payment method, the login flow prompts, entering an email, the one-time passcode flow, and the one-time passcode received." style="background-color:white;padding:15px;" />

<img src="https://www.paypalobjects.com/devdoc/iOS_SDK_native-checkout-first-time-flow_02.png" alt="Mobile phone screenshots of a native checkout flow for a first-time customer, with screens that show the one-time payment code entry, logging the buyer into their wallet, the in-content paysheet with a carousel of payment options, and returning the buyer to the merchant's confirmation page." style="background-color:white;padding:15px;" />

#### Native checkout for a returning customer

<img src="https://www.paypalobjects.com/devdoc/iOS_SDK_native-checkout-repeat-time-flow.png" alt="Mobile phone screenshots of a native checkout flow for a returning customer, with screens that show selecting PayPal as a payment method, the seamless logins through LLS, the in-content paysheet with a carousel of payment options, and returning the customer to the merchant's confirmation page." style="background-color:white;padding:15px;" />

### 1. Add PayPalNativePayments module to your app

Add the `paypal-native-payments` package dependency in your app's `build.gradle` file:

```javascript
dependencies {
  implementation "com.paypal.android:paypal-native-payments:CURRENT-VERSION"
}
```

Add the following Cardinal SDK Maven repository to your project’s top-level `build.gradle` file to pass credentials to Gradle:

```javascript
allprojects {
  repositories {
    maven {
      url  "https://cardinalcommerceprod.jfrog.io/artifactory/android"
      credentials {
        username "firstname_lastname"
        password "PASSWORD"
      }
    }
  }
}
```

### 2. Enable Native Checkout SDK

You'll need to set up authorization to use the Native Checkout SDK. To create a client ID and secret, follow the steps in <a href="https://developer.paypal.com/api/rest/#link-getstarted" target="_blank">Get Started</a>. You need these values to generate an `ACCESS_TOKEN`.

#### Sandbox business account

Set up your sandbox business account to use native checkout as follows:

1. Log into the <a href="https://developer.paypal.com/dashboard/" target="_blank"><strong>PayPal Developer Dashboard</strong></a>, toggle **Sandbox**, and go to **Apps & Credentials**.
2. In **REST API apps**, select the name of your app.
3. Go to **Features** > **Accept payments** and select ***Native Checkout SDK**.
4. Select **Save Changes**.

#### Add return URL

A return URL redirects users to the app after authenticating. Use the following steps to create a return URL:

1. Select your app from the **My Apps & Credentials** page on the Developer Dashboard.
2. Go to **Features** > **Other features**. Select the **Log in with PayPal** checkbox. Click on **Advanced Settings**. A pop-up window will open, and you'll see the **Return URL** field in the new window.

- You can use an <a href="https://developer.android.com/training/app-links" target="_blank">Android App Link</a> registered within the Developer Console to handle SDK redirects.
* Alternatively, you can use your application ID (typically referenced via `BuildConfig.APPLICATION_ID`) and register your return URL with `://paypalpay` as the suffix. For example, if your application ID is `com.paypal.app`, input `com.paypal.app://paypalpay` as the return URL.
* The return URL in the Developer Dashboard and the SDK must match exactly.
* The application ID and return URL must use lower case letters. The return URL is passed to the SDK via an intent filter and <a href="https://developer.android.com/guide/topics/manifest/data-element#:~:text=Host%20name%20matching%20in%20the%20Android%20framework%20is%20case%2Dsensitive%2C%20unlike%20the%20formal%20RFC.%20As%20a%20result%2C%20always%20specify%20host%20names%20using%20lowercase%20letters" target="_blank">host name matching in the Android framework is case-sensitive</a>

> **Note:** If you change the return URL in the Developer Dashboard, PayPal must review your app again. The review period automatically begins any time the return URL changes.

3. Select the **Full Name** and **Email** checkboxes found within the **Advanced Settings**. These are scopes of the <a href="https://developer.paypal.com/api/identity/v1/" target="_blank">Identity API</a>.

### 3. Create PayPalNativeCheckoutClient

Use the following steps to set up the PayPal Native Checkout client for your app:

#### 1. Construct CoreConfig

In your Android app, use the `CLIENT_ID` to construct a `CoreConfig`.

```javascript
val coreConfig = CoreConfig("CLIENT_ID", environment = Environment.SANDBOX)
```
<br />

#### 2. Create native checkout request

Create a `PayPalNativeCheckoutClient` request to approve an order with a PayPal payment method and include the `RETURN_URL`:

```javascript
val payPalNativeClient = PayPalNativeCheckoutClient(
  application = requireActvitiy().application,
  coreConfig = coreConfig,
  returnUrl = "RETURN_URL"
)
```
<br />

#### 3. Set up payment listener

Implement the `PayPalNativeCheckoutListener` on the `PayPalNativeCheckoutClient` to listen for result notifications from the SDK.

```javascript
payPalNativeClient.listener = object : PayPalNativeCheckoutListener {
  override fun onPayPalCheckoutStart() {
    // the PayPal paysheet is about to show up
  }
  override fun onPayPalCheckoutSuccess(result: PayPalNativeCheckoutResult) {
    // order was approved and is ready to be captured/authorized
  }
  override fun onPayPalCheckoutFailure(error: PayPalSDKError) {
    // handle the error
  }
  override fun onPayPalCheckoutCanceled() {
    // the user canceled the flow
  }
}
```
<br />

#### 4. Listen for shipping details

When a payer chooses to use shipping details from their PayPal profile, use `PayPalNativeShippingListener` to listen for changes to their shipping address or shipping method.

You can only implement `PayPalNativeShippingListener` if the <a href="https://developer.paypal.com/docs/api/orders/v2/#definition-experience_context_base" target="_blank"><code>shipping_preference</code></a> in the order ID is set to `GET_FROM_FILE.`

> **Note:** Skip this step if you created your order ID with the `shipping_preference` set to `NO_SHIPPING` or `SET_PROVIDED_ADDRESS`.

Set a `shippingListener` on the `PayPalNativeCheckoutClient` to send notifications to your app when the user updates their shipping address or shipping method.

This code sample uses a `try…catch` function to handle the response:

```javascript
payPalNativeClient.shippingListener = object : PayPalNativeShippingListener {
  override fun onPayPalNativeShippingAddressChange(
    actions: PayPalNativePaysheetActions,
    shippingAddress: PayPalNativeShippingAddress
  ) {
    // called when the user updates their chosen shipping address
    // you must call actions.approve() or actions.reject() in this callback
    actions.approve()
    // OPTIONAL: you can optionally patch your order. Once complete, call actions.approve() if successful or actions.reject() if not.
  }
  override fun onPayPalNativeShippingMethodChange(
    actions: PayPalNativePaysheetActions,
    shippingMethod: PayPalNativeShippingMethod
  ) {
    // called when the user updates their chosen shipping method
    // patch your order server-side with the updated shipping amount.
    // Once complete, call \`actions.approve()\` or \`actions.reject()\`
    try {
      // TODO: patch order on server side, notify SDK of success by calling actions.approve()
      actions.approve()
    } catch (e: Exception) {
      // catch any errors from patching the order e.g. network unavailable
      // and notify SDK that the update was unsuccessful
      actions.reject()
    }
  }
}
```

#### 5. Modify shipping details

When the shipping method changes, update the order details on your server by sending a `PATCH` request to the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_patch" target="_blank">Update order</a> endpoint of the Orders API.

Approve or reject changes to the shipping information to see changes appear in the paysheet UI by calling either `PayPalNativePaysheetActions.approve()` or `PayPalNativePaysheetActions.reject()`.

To update the paysheet with a new shipping method, or when `onPayPalNativeShippingMethodChange` is called:

1. Patch the order on your server using the `replace` operation with all shipping methods.
    * Mark the new shipping method as selected.
    * Optional: Update the amount to reflect the new shipping cost.
2. Call `approve()` or `reject()` to accept or reject the changes and continue the payment flow.

For more information, visit the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_patch" target="_blank">Update order</a> endpoint of the Orders v2 API.

### 4. Get Order ID

On your server:

1. Create an `ORDER_ID` by using the <a href="https://developer.paypal.com/docs/api/orders/v2" target="_blank">Orders v2 API</a>.
2. Pass your `ACCESS_TOKEN` in the `Authorization` header. To get an `ACCESS_TOKEN`, use the <a href="https://developer.paypal.com/api/rest/authentication/" target="_blank">Authentication API</a>.
   > **Note:** This access token is only for the sandbox environment. When you're ready to go live, request a live access token by changing the request sandbox endpoint to https://api-m.paypal.com/v1/oauth2/token.
3. Pass the `intent`. You'll need to pass either `AUTHORIZE` or `CAPTURE` as the `intent` type. This type must match the `/authorize` or `/capture` endpoint you use to process your order.

#### Sample request

```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw '{
    "intent": "CAPTURE|AUTHORIZE",
    "purchase_units": [
      {
        "amount": {
          "currency_code": "USD",
          "value": "5.00"
        }
      }
    ]
  }'
```

#### Sample response

```javascript
{
  "id":"ORDER_ID",
  "status":"CREATED"
}
```

When a buyer starts a payment, send the `ORDER_ID` from your server to your client app.

### 5. Start PayPal Native Payments flow

To start the PayPal Native Payments flow, call the `startCheckout` function in `PayPalNativeCheckoutClient`, with a `PayPalNativeCheckoutRequest`:

```javascript
val request = PayPalNativeCheckoutRequest("ORDER_ID")
paypalNativeClient.startCheckout(request)
```

### 6. Authorize and capture order

Submit your `ORDER_ID` for authorization or capture when the PayPal Android SDK calls the `onPayPalSuccess` method.

Call the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_authorize" target="_blank"><code>authorize</code></a> endpoint of the Orders V2 API to place the money on hold:

#### Sample request: Authorize order

```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/authorize' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
```
<br />

Call the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_capture" target="_blank"><code>capture</code></a> endpoint of the Orders V2 API to capture the money immediately:

#### Sample request: Capture order

```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/capture' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
```

### PayPal Web Payments

Integrate `PayPalWebPayments` to add a lighter checkout integration to your app. The checkout experience is launched in a browser within your application, reducing the size of the SDK.

Follow these steps to integrate `PayPalWebPayments`:

### 1. Add PayPalWebPayments to your app

Add the `paypal-web-payments` package dependency in your app's `build.gradle` file:

```javascript
dependencies {
  implementation "com.paypal.android:paypal-web-payments:CURRENT-VERSION"
}
```

### 2. Set up your app for browser switching

`PayPalWebPayments` launches a checkout page in a browser within your application. Your app needs to handle the browser switch between the checkout page and your app. Set up a return URL that returns to your app from the browser.

Update your app's `AndroidManifest.xml` with details about the card payment activity that will return the user to your app after completing the payment. Include the following elements:

1. Set the activity `launchMode` to `singleTop`.
2. Set the `android:scheme` on the Activity that will be responsible for handling the deep link back into the app.
2. Add an `intent-filter`.
3. Register the `myapp://` custom URL scheme in the `intent-filter`.

> Note: `android:exported` is required if your app compile SDK version is API 31 (Android 12) or later.

```javascript
<activity android:name="com.company.app.MyPaymentsActivity"
          android:exported="true"
          android:launchMode="singleTop">
          ...
  <intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <data android:scheme="custom-url-scheme" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
  </intent-filter>
</activity>
```

Also, add `onNewIntent` to the host activity in your app:

```javascript
override fun onNewIntent(newIntent: Intent?) {
  super.onNewIntent(intent)
  intent = newIntent
}
```

### 3. Create PayPalWebCheckoutClient

Use the following steps to set up the PayPal Native Checkout client for your app:

#### 1. Construct CoreConfig

In your Android app, use the `CLIENT_ID` to construct a `CoreConfig`.

```javascript
val config = CoreConfig("CLIENT_ID", environment = Environment.SANDBOX)
```
<br />

#### 2. Create return URL

Set a return URL using the custom scheme you configured in the `ActivityManifest.xml`:

```javascript
val returnUrl = "custom-url-scheme"
```
<br />

#### 3. Create web checkout request

Create a `PayPalWebCheckoutClient` to approve an order with a PayPal payment method:

```javascript
    val payPalWebCheckoutClient = PayPalWebCheckoutClient(requireActivity(), config, returnUrl)
```
<br />

#### 4. Set up payment listener

Set a `PayPalWebCheckoutListener` on the client to receive payment flow callbacks:

```javascript
payPalWebCheckoutClient.listener = object : PayPalWebCheckoutListener {
  override fun onPayPalWebSuccess(result: PayPalWebCheckoutResult) {
    // order was approved and is ready to be captured/authorized (see step 7)
  }
  override fun onPayPalWebFailure(error: PayPalSDKError) {
    // handle the error
  }
  override fun onPayPalWebCanceled() {
    // the user canceled the flow
  }
}
```

> **Note:** Collecting a billing address can reduce the number of  authentication challenges to customers.

### 4. Get Order ID

On your server:

1. Create an `ORDER_ID` by using the <a href="https://developer.paypal.com/docs/api/orders/v2" target="_blank">Orders v2 API</a>.
2. Pass your `ACCESS_TOKEN` in the `Authorization` header. To get an `ACCESS_TOKEN`, use the <a href="https://developer.paypal.com/api/rest/authentication/" target="_blank">Authentication API</a>.
   > **Note:** This access token is only for the sandbox environment. When you're ready to go live, request a live access token by changing the request sandbox endpoint to https://api-m.paypal.com/v1/oauth2/token.
3. Pass the `intent`. You'll need to pass either `AUTHORIZE` or `CAPTURE` as the `intent` type. This type must match the `/authorize` or `/capture` endpoint you use to process your order.

<Tabs>
<Tab label="Sample request">
```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw '{
    "intent": "CAPTURE|AUTHORIZE",
    "purchase_units": [
      {
        "amount": {
          "currency_code": "USD",
          "value": "5.00"
        }
      }
    ]
  }'
```
</Tab>
<Tab label="Sample response">
```javascript
{
 "id":"ORDER_ID",
 "status":"CREATED"
}
```
</Tab>
</Tabs>

When a buyer starts a payment, send the `ORDER_ID` from your server to your client app.

### 5. Create web checkout request

Configure your `PayPalWebCheckoutRequest` with the `ORDER_ID`. You can also specify one of the following funding sources for your order: `PayPal` (default), `PayLater`, or `PayPalCredit`.

```javascript
val payPalWebCheckoutRequest = PayPalWebCheckoutRequest("ORDER_ID", fundingSource = PayPalWebCheckoutFundingSource.PAYPAL)
```

### 6. Approve order

Call `payPalWebCheckoutClient.start()` to process the payment.

```javascript
class MyCardPaymentActivity: FragmentActivity {
  fun payPalWebCheckoutTapped(payPalWebCheckoutRequest: PayPalWebCheckoutRequest) {
    payPalWebCheckoutClient.start(payPalWebCheckoutRequest)
  }
}
```

### 7. Authorize and capture order

Submit your `ORDER_ID` for authorization or capture when the PayPal Android SDK calls the `onPayPalWebSuccess` method on `PayPalWebCheckoutListener`.

Call the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_authorize" target="_blank"><code>authorize</code></a> endpoint of the Orders V2 API to place the money on hold:

#### Sample request: Authorize order

```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/authorize' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
```
<br />

Call the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_capture" target="_blank"><code>capture</code></a> endpoint of the Orders V2 API to capture the money immediately:

#### Sample request: Capture order

```curl
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/capture' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
```

## Payment buttons and fraud protection

After you integrate a payment method, add a payment button to your page to start the payment process. You can also add fraud protection to your app.

### Use PayPal buttons in your UI

The `PaymentButtons` module provides a set of PayPal-branded buttons to seamlessly integrate with PayPal `web` and `native` payments.

Follow these steps to add PayPal buttons to your integration:

### 1. Add PaymentButtons to your app

Add the `payment-buttons` package dependency in your app's `build.gradle` file:

```kotlin
dependencies {
  implementation "com.paypal.android:payment-buttons:CURRENT-VERSION"
}
```

### 2. Create PayPal button

The `PaymentButtons` module provides 3 buttons that you can use in your application:

<ul>
  <li><code>PayPalButton</code>: A generic PayPal button.</li>
  <li><code>PayPalPayLater</code>: A PayPal button with a PayLater label.</li>
  <li><code>PayPalCredit</code>: A PayPal button with the PayPalCredit logo.</li>
</ul>

These buttons include customization options such as color, edges, size, and labels. Here's how to style the button corner radius:

| Value  | Description |
|--------|-------------|
| `rectangle` | Button shape with sharp corners. |
| `rounded` | **Recommended**<br />Button shape with rounded corner radius. The default button shape. |
| `pill` | Button in pill shape. |
| `customCornerRadius` | Customize the button's corner radius. The minimum value is 10 px and is applied to all 4 corners. |

Add <code>PayPalButton</code> to your layout XML:

```kotlin
<com.paypal.android.paymentbuttons.PayPalButton
  android:id="@+id/paypal_button"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"/>
```

### 3. Reference PayPal button

Add the PayPal button to your code:

```kotlin
val payPalButton = findViewById<PayPalButton>(R.id.paypal_button)
payPalButton.setOnClickListener {
  // start the PayPal web or native
}
```

### Protect from fraud

The `FraudProtection` module helps you collect data about a customer's device and match it with a session identifier on your server. For more information, see <a href="https://developer.paypal.com/docs/checkout/advanced/customize/fraud-protection/" target="_blank">Fraud protection</a>.

> **Note:** If you integrated 3D Secure before June 2020, the `liabilityShifted`, `authenticationStatus`, and `AuthenticationReason` parameters are no longer supported, but continue to work on the server.

### 1. Add FraudProtection to your app

Add the `fraud-protection` package dependency in your app's `build.gradle` file:

```javascript
dependencies {
  implementation "com.paypal.android:fraud-protection:CURRENT-VERSION"
}
```

### 2. Create PayPalDataCollector

In your Android app:
1. Use the `CLIENT_ID` to construct a `CoreConfig`.
2. Construct a `PayPalDataCollector` using your `CoreConfig` object.

```kotlin
val config = CoreConfig("CLIENT_ID", environment = Environment.SANDBOX)

val dataCollector = PayPalDataCollector(coreConfig = coreConfig)
```

### 3. Collect client metadata

Collect the client metadata ID before starting a payment from a mobile device:

```javascript
val clientMetadataId = dataCollector.getClientMetadataId(context)
```

Pass the result to your server, and include the client metadata ID in the payment request you send to PayPal. Don't cache or store this value.

## Go live

If you have fulfilled the requirements for accepting Advanced Credit and Debit Card Payments for your <a href="https://www.paypal.com/myaccount/bundle/business/upgrade" target="_blank">business account</a>,
review the <strong><a href="https://developer.paypal.com/api/rest/production/" target="_blank">Move your app to production</a></strong>>
If this is your first time testing in a live environment, follow these steps:

1. Log into the <a href="https://developer.paypal.com/dashboard/" target="_blank">PayPal Developer Dashboard</a> with your PayPal business account.
2. Complete <a href="https://www.paypal.com/bizsignup/entry?_ga=1.171321763.248280996.1670866755" target="_blank">production onboarding</a> so you can process card payments with your live PayPal business account.
3. Request <a href="https://www.paypal.com/signin/client?flow=provisionUser&country.x=US&locale.x=en_US&_ga=1.95899167.248280996.1670866755" target="_blank">Advanced Credit and Debit Card Payments</a> for your business account.

> **Important:** The code for the integration checks eligibility requirements, so the payment card fields only display when the production request is successful.
