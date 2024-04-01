# Integrate card payments in iOS apps

Accept PayPal, credit, and debit card payments in a web or native experience using the PayPal Mobile iOS SDK. Use customizable PayPal buttons with your custom checkout UI to align with your business branding. For more implementation details, see the [PayPal GitHub repository](https://github.com/paypal/paypal-ios/).

## Know before you code

You need a [developer account](/tools/sandbox/accounts/) to get sandbox credentials:

* PayPal uses REST API credentials which you can get from the [developer dashboard](/dashboard/).
* Client ID: Authenticates your account with PayPal and identifies an app in your sandbox.
* Client secret: Authorizes an app in your sandbox. Keep this secret safe and don’t share it.

Read [Get started with PayPal APIs](/api/rest/) for more information.

You need a combination of PayPal and third-party tools:

* [iOS SDK](https://github.com/paypal/paypal-ios/): Adds PayPal-supported payment methods for iOS.
* [Orders REST API](/docs/api/orders/v2/): Create, update, retrieve, authorize, and capture orders.

<RunInPostman text="Use Postman to explore and test PayPal APIs." />

## 1. Before you begin your integration

### Check your account setup for advanced card payments

This integration requires a sandbox business account with the Advanced Credit and Debit Card Payments capability. Your account should automatically have this capability.

To confirm that Advanced Credit and Debit Card Payments are enabled for you, check your sandbox business account as follows:

1. Log into the [**PayPal Developer Dashboard**](/dashboard/), toggle **Sandbox**, and go to **Apps & Credentials**.
2. In **REST API apps**, select the name of your app.
3. Go to **Features** > **Accept payments**.
4. Select the **Advanced Credit and Debit Card Payments** checkbox and select **Save Changes**.

> **Note:** If you created a sandbox business account through [sandbox.paypal.com](https://www.sandbox.paypal.com/?_ga=1.158343865.248280996.1670866755), and the advanced credit and debit card payments status for the account is disabled, [complete the sandbox onboarding steps](https://www.sandbox.paypal.com/bizsignup/#/checkAccount).

### Check 3D Secure requirements

Add 3D Secure to reduce the chance of fraud and improve the payment experience by authenticating a cardholder through their card issuer.

Visit our [3D Secure](/docs/checkout/advanced/customize/3d-secure/) page to see if 3D Secure is required in your region and learn more about implementing 3D Secure in your app.

## 2. Integrate the SDK into your app

Integrate 3 different types of payments using the PayPal Mobile SDK:

* **Card payments:** Add card fields that align with your branding.
* **PayPal native payments:** Launch a checkout page within your app, instead of a popup.
* **PayPal web payments:** A lighter integration that launches a checkout page in a browser within your app.

<ContentTabs>
<ContentTab label="Card">

### Integrate with card payments

Build and customize the card fields to align with your branding.

### 1. Add card payments module to your app

Add the `CardPayments` package dependency for your app using **Swift Package Manager** or **CocoaPods**:

<Pills>
<Pill label="Swift Package Manager">

1. Open Xcode.
2. <a href="https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app">Follow the guide</a> to add package dependencies to your app.
3. Enter <a href="https://github.com/paypal/paypal-ios/"><code>https://github.com/paypal/paypal-ios/</code></a> as the repository URL.
4. Select the checkbox for the `CardPayments` framework.

</Pill>
<Pill label="CocoaPods">

Include `PayPal/CardPayments` in your Podfile:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
# Podfile
pod 'PayPal/CardPayments'
`}
></CodeBlock>
</CodeBlockWrapper>

</Pill>
</Pills>

### 2. Create CardClient

A `CardClient` helps you attach a card to a payment.

In your iOS app:
1. Use the `CLIENT_ID` to construct a `CoreConfig`.
2. Construct a `CardClient` using your `CoreConfig` object.

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let coreConfig = CoreConfig(clientID: "CLIENT_ID", environment: .sandbox)
let cardClient = CardClient(config: coreConfig)
`}
></CodeBlock>
</CodeBlockWrapper>

### 3. Get Order ID

On your server:

1. Create an `ORDER_ID` by using the <a href="/docs/api/orders/v2">Orders v2 API</a>.
2. Pass your `ACCESS_TOKEN` in the `Authorization` header. To get an `ACCESS_TOKEN`, use the [Authentication API](/api/rest/authentication/).
   > **Note:** This access token is only for the sandbox environment. When you're ready to go live, request a live access token by changing the request sandbox endpoint to https://api-m.paypal.com/v1/oauth2/token.
3. Pass the `intent`. You'll need to pass either `AUTHORIZE` or `CAPTURE` as the `intent` type. This type must match the `/authorize` or `/capture` endpoint you use to process your order.

<Tabs>
<Tab label="Sample request">
<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
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
`}
></CodeBlock>
</CodeBlockWrapper>
</Tab>
<Tab label="Sample response">
<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
{
  "id":"ORDER_ID",
  "status":"CREATED"
}
`}
></CodeBlock>
</CodeBlockWrapper>
</Tab>
</Tabs>

When a buyer starts a payment, send the `ORDER_ID` from your server to your client app.

### 4. Create card request

A `CardRequest` object:
* Attaches a card to an `ORDER_ID`.
* Launches 3D Secure when a payment requires additional authentication.

#### 1. Collect card payment details

Build a `card` object with the buyer's card details:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let card = Card(
  number: "4005519200000004",
  expirationMonth: "01",
  expirationYear: "2025",
  securityCode: "123",
  cardholderName: "Jane Smith",
  billingAddress: Address(
    addressLine1: "123 Main St.",
    addressLine2: "Apt. 1A",
    locality: "City",
    region: "IL",
    postalCode: "12345",
    countryCode: "US"
  )
)
`}
></CodeBlock>
</CodeBlockWrapper>

Collecting a billing address can reduce the number of  authentication challenges to customers.

#### 2. Build CardRequest

Build a `CardRequest` with the `card` object and your `ORDER_ID`:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let cardRequest = CardRequest(
  orderID: "ORDER_ID",
  card: card,
  sca: .scaAlways // default value is .scaWhenRequired
)
`}
></CodeBlock>
</CodeBlockWrapper>

[3D Secure](/api/nvp-soap/payflow/3d-secure-overview/) is supported for all card payments to comply with the [Second Payment Services Directive (PSD2)](https://www.paypal.com/uk/webapps/mpp/PSD2?_ga=1.18434873.1625369690.1652045188). PSD2 is a European Union regulation that introduces [Strong Customer Authentication (SCA)](https://www.ukfinance.org.uk/our-expertise/payments-and-innovation/strong-customer-authentication) and other security requirements.

Select your SCA launch option type using the `sca` parameter in the `CardRequest` initializer:
* `SCA.scaWhenRequired` launches an SCA challenge when applicable. This is enabled by default.
* `SCA.scaAlways` requires an SCA challenge for all card transactions.

### 5. Approve order

After your `CardRequest` has the card details, call `cardClient.approveOrder()` to process the payment.

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
class MyViewController: UIViewController {
  func cardCheckoutTapped(cardRequest: CardRequest) {
    cardClient.approveOrder(request: cardRequest)
  }
}
`}
></CodeBlock>
</CodeBlockWrapper>

### 6. Handle payment result scenarios

Set up your `CardDelegate` to handle successful payments, errors, cancellations, and 3D Secure transaction flows.

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
extension MyViewController: CardDelegate {
  func setupCardClient() {
    cardClient.delegate = self
  }
  // MARK: - CardDelegate
  func card(_ cardClient: CardClient, didFinishWithResult result: CardResult) {
    // order was approved and is ready to be captured/authorized (see step 8)
  }
  func card(_ cardClient: CardClient, didFinishWithError error: CoreSDKError) {
    // handle the error by accessing \`error.localizedDescription\`
  }
  func cardDidCancel(_ cardClient: CardClient) {
    // 3D Secure auth was canceled by the user
  }
  func cardThreeDSecureWillLaunch(_ cardClient: CardClient) {
    // 3D Secure auth will launch
  }
  func cardThreeDSecureDidFinish(_ cardClient: CardClient) {
    // 3D Secure auth did finish successfully
  }
}
`}
></CodeBlock>
</CodeBlockWrapper>

### 7. Authorize and capture order

Submit your `ORDER_ID` for authorization or capture when the PayPal iOS SDK calls the `didFinishWithResult` method.

Call the [`authorize`](/docs/api/orders/v2/#orders_authorize) endpoint of the Orders V2 API to place the money on hold:

#### Sample request: Authorize order

<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/authorize' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
`}
></CodeBlock>
</CodeBlockWrapper>
<br />

Call the [`capture`](/docs/api/orders/v2/#orders_capture) endpoint of the Orders V2 API to capture the money immediately:

#### Sample request: Capture order

<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/capture' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
`}
></CodeBlock>
</CodeBlockWrapper>

### 8. Test integration

Before going live, test your integration in the [sandbox environment](/tools/sandbox/).

Learn more about the following resources on the [Card Testing](/tools/sandbox/card-testing/) page:

* Use [test card numbers](tools/sandbox/card-testing/#link-testcardnumbers) to simulate successful payments for advanced checkout integrations.
* Use [rejection triggers](/tools/sandbox/card-testing/#link-rejectiontriggers) to simulate card error scenarios.
* Test [3D Secure authentication](/tools/sandbox/card-testing/#link-simulate3dsecurecardpayments) scenarios.
* Test your integration by following [these recommended use cases](/tools/sandbox/card-testing/#link-testintegration). See the [Orders v2 API](/docs/api/orders/v2/) for details about billing address fields and other parameters. For example, use the [2-character country code](/api/rest/reference/country-codes/) to test the billing address.

> **Note:** Use the [credit card generator](/tools/sandbox/card-testing/#link-creditcardgenerator) to generate additional test credit cards for sandbox testing.

When prompted for required data for the sandbox business request, such as a phone number, enter any number that fits the required format. Because this is a sandbox request, the data doesn't have to be factual.

Before you go live, you'll need to complete [live onboarding](https://www.paypal.com/bizsignup/entry/product/ppcp) to be eligible to process cards with your live PayPal account.

</ContentTab>
<ContentTab label="Native payments">

### Use PayPal native payments

Use `PayPalNativePayments` to add a PayPal paysheet to your app. The paysheet is a checkout page that the client launches within your app, instead of showing up as a pop-up. The paysheet shows all the PayPal payment methods available and helps the payer complete their payment.

#### Native checkout for a first-time customer

![img](https://www.paypalobjects.com/devdoc/iOS_SDK_native-checkout-first-time-flow_01.png)
![img](https://www.paypalobjects.com/devdoc/iOS_SDK_native-checkout-first-time-flow_02.png)

#### Native checkout for a returning customer

![img](https://www.paypalobjects.com/devdoc/iOS_SDK_native-checkout-repeat-time-flow.png)

Follow these steps to add `PayPalNativePayments`:

### 1. Add PayPalNativePayments module to your app

Add the `PayPal/PayPalNativePayments` package dependency for your app using **Swift Package Manager** or **CocoaPods**:

<Pills>
<Pill label="Swift Package Manager">

1. Open Xcode.
2. <a href="https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app">Follow the guide</a> to add package dependencies to your app.
3. Enter <a href="https://github.com/paypal/paypal-ios/"><code>https://github.com/paypal/paypal-ios/</code></a> as the repository URL.
4. Select the checkbox for the `PayPalNativePayments` framework.

</Pill>
<Pill label="CocoaPods">

Include `PayPal/PayPalNativePayments` in your Podfile:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
# Podfile
pod 'PayPal/PayPalNativePayments'
`}
></CodeBlock>
</CodeBlockWrapper>

</Pill>
</Pills>

### 2. Enable Native Checkout SDK

You'll need to set up authorization to use the Native Checkout SDK. To create a client ID and secret, follow the steps in [Get Started](/api/rest/#link-getstarted). You need these values to generate an `ACCESS_TOKEN`.

Set up your sandbox business account to use native checkout as follows:

1. Log into the [**PayPal Developer Dashboard**](/dashboard/), toggle **Sandbox**, and go to **Apps & Credentials**.
2. In **REST API apps**, select the name of your app.
3. Go to **Features** > **Accept payments** and select ***Native Checkout SDK**.
4. Select **Save Changes**.

> **Note:** This access token is only for the sandbox environment. When you're ready to go live, request a live access token by changing the request sandbox endpoint to https://api-m.paypal.com/v1/oauth2/token.

### 3. Create PayPalNativeCheckoutClient

Use the following steps to set up the PayPal Native Checkout client for your app:

#### 1. Construct CoreConfig

In your iOS app, use the `CLIENT_ID` to construct a `CoreConfig`.

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let config = CoreConfig(clientID: "CLIENT_ID", environment: .sandbox)
`}
></CodeBlock>
</CodeBlockWrapper>
<br />

#### 2. Create native checkout request

Create a `PayPalNativeCheckoutClient` request to approve an order with a PayPal payment method:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let payPalNativeClient = PayPalNativeCheckoutClient(config: config)
`}
></CodeBlock>
</CodeBlockWrapper>
<br />

#### 3. Set up payment delegate

Set a `PayPalNativeCheckoutDelegate` to listen for result notifications from the SDK:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
extension MyViewController: PayPalNativeCheckoutDelegate {
  func paypal(_ payPalClient: PayPalNativeCheckoutClient, didFinishWithResult approvalResult: Approval) {
    // order was approved and is ready to be captured/authorized (see step 5)
  }
  func paypal(_ payPalClient: PayPalNativeCheckoutClient, didFinishWithError error: CoreSDKError) {
    // handle the error by accessing \`error.localizedDescription\`
  }
  func paypalDidCancel(_ payPalClient: PayPalNativeCheckoutClient) {
    // the user canceled
  }
  func paypalWillStart(_ payPalClient: PayPalNativeCheckoutClient) {
    // the PayPal paysheet is about to show up. Handle loading views, spinners, etc.
  }
}
`}
></CodeBlock>
</CodeBlockWrapper>
<br />

#### 4. Listen for shipping details

When a payer chooses to use shipping details from their PayPal profile, use `PayPalNativeShippingDelegate` to listen for changes to their shipping address or shipping method.

You can only implement `PayPalNativeShippingDelegate` if the [`shipping_preference`](/docs/api/orders/v2/#definition-experience_context_base) in the order ID is set to `GET_FROM_FILE.`

> **Note:** Skip this step if you created your order ID with `shipping_preference` set to `NO_SHIPPING` or `SET_PROVIDED_ADDRESS`.

Set a `shippingDelegate` on the `PayPalNativeCheckoutClient` to send notifications to your app when the user updates their shipping address or shipping method.

<CodeBlockWrapper>
<CodeBlock
className="language-swift"
children={`
extension MyViewModel: PayPalNativeShippingDelegate {
  func setup() {
    paypalNativeClient.delegate = self         // always required
    paypalNativeClient.shippingDelegate = self // required for \`GET_FROM_FILE\` orders
  }
  func paypal(
    _ payPalClient: PayPalNativeCheckoutClient,
    didShippingAddressChange shippingAddress: PayPalNativeShippingAddress,
    withAction shippingActions: PayPalNativePaysheetActions
  ) {
    // called when the user updates their chosen shipping address
    // you must call shippingActions.approve() or shippingActions.reject() in this callback
    shippingActions.approve()
    // OPTIONAL: you can optionally patch your order. Once complete, call shippingActions.approve() if successful or shippingActions.reject() if not.
  }
  func paypal(
    _ payPalClient: PayPalNativeCheckoutClient,
    didShippingMethodChange shippingMethod: PayPalNativeShippingMethod,
    withAction shippingActions: PayPalNativePaysheetActions
  ) {
    // called when the user updates their chosen shipping method
    // patch your order server-side with the updated shipping amount.
    // Once complete, call \`shippingActions.approve()\` or \`shippingActions.reject()\`
    if patchOrder() == .success {
      shippingActions.approve()
    } else {
      shippingActions.reject()
    }
  }
}
`}
></CodeBlock>
</CodeBlockWrapper>
<br />

#### 5. Modify shipping details

When the shipping method changes, update the order details on your server by sending a `PATCH` request to the [Update order](/docs/api/orders/v2/#orders_patch) endpoint of the Orders API.

Approve or reject changes to the shipping information to see changes appear in the paysheet UI by calling either `PayPalNativePaysheetActions.approve()` or `PayPalNativePaysheetActions.reject()`.

To update the paysheet with a new shipping method, or when `didShippingMethodChange` is called:

1. Patch the order on your server using the `replace` operation with all shipping methods.
    * Mark the new shipping method as selected.
    * Optional: Update the amount to reflect the new shipping cost.
2. Call `approve()` or `reject()` to accept or reject the changes and continue the payment flow.

For more information, visit the <a href="/docs/api/orders/v2/#orders_patch">Update order</a> endpoint of the Orders v2 API.

### 4. Get Order ID

On your server:

1. Create an `ORDER_ID` by using the <a href="/docs/api/orders/v2">Orders v2 API</a>.
2. Pass your `ACCESS_TOKEN` in the `Authorization` header. To get an `ACCESS_TOKEN`, use the [Authentication API](/api/rest/authentication/).
   > **Note:** This access token is only for the sandbox environment. When you're ready to go live, request a live access token by changing the request sandbox endpoint to https://api-m.paypal.com/v1/oauth2/token.
3. Pass the `intent`. You'll need to pass either `AUTHORIZE` or `CAPTURE` as the `intent` type. This type must match the `/authorize` or `/capture` endpoint you use to process your order.

<Tabs>
<Tab label="Sample request">
<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
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
`}
></CodeBlock>
</CodeBlockWrapper>
</Tab>
<Tab label="Sample response">
<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
{
  "id":"ORDER_ID",
  "status":"CREATED"
}
`}
></CodeBlock>
</CodeBlockWrapper>
</Tab>
</Tabs>

When a buyer starts a payment, send the `ORDER_ID` from your server to your client app.

### 5. Start PayPal Native Payments flow

To start the PayPal Native Payments flow, call the `startCheckout` function in `PayPalNativeCheckoutClient`, with a `PayPalNativeCheckoutRequest`:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let request = PayPalNativeCheckoutRequest(orderID: "ORDER_ID")
paypalNativeClient.start(request: request)
`}
></CodeBlock>
</CodeBlockWrapper>

### 6. Authorize and capture order

Submit your `ORDER_ID` for authorization or capture when the PayPal iOS SDK calls the `onPayPalSuccess` method.

Call the [`authorize`](/docs/api/orders/v2/#orders_authorize) endpoint of the Orders V2 API to place the money on hold:

#### Sample request: Authorize order

<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/authorize' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
`}
></CodeBlock>
</CodeBlockWrapper>
<br />

Call the [`capture`](/docs/api/orders/v2/#orders_capture) endpoint of the Orders V2 API to capture the money immediately:

#### Sample request: Capture order

<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/capture' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
`}
></CodeBlock>
</CodeBlockWrapper>

</ContentTab>
<ContentTab label="Web payments">

### PayPal Web Payments

Integrate `PayPalWebPayments` to add a lighter checkout integration to your app. The checkout experience is launched in a browser within your application, reducing the size of the SDK.

Follow these steps to integrate `PayPalWebPayments`:

### 1. Add PayPalWebPayments to your app

Add the `PayPalWebPayments` package dependency for your app using **Swift Package Manager** or **CocoaPods**:

<Pills>
<Pill label="Swift Package Manager">

1. Open Xcode.
2. <a href="https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app">Follow the guide</a> to add package dependencies to your app.
3. Enter <a href="https://github.com/paypal/paypal-ios/"><code>https://github.com/paypal/paypal-ios/</code></a> as the repository URL.
4. Select the checkbox for the `PayPalWebPayments` framework.

</Pill>
<Pill label="CocoaPods">

Include `PayPal/PayPalWebPayments` in your Podfile:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
# Podfile
pod 'PayPal/PayPalWebPayments'
`}
></CodeBlock>
</CodeBlockWrapper>

</Pill>
</Pills>

### 2. Create PayPalWebCheckoutClient

Use the following steps to set up the PayPal Native Checkout client for your app:

#### 1. Construct CoreConfig

In your iOS app, use the `CLIENT_ID` to construct a `CoreConfig`.

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let config = CoreConfig(clientID: "CLIENT_ID", environment: .sandbox)
`}
></CodeBlock>
</CodeBlockWrapper>
<br />

#### 2. Create web checkout request

Create a `PayPalWebCheckoutClient` to approve an order with a PayPal payment method:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let payPalClient = PayPalWebCheckoutClient(config: config)
`}
></CodeBlock>
</CodeBlockWrapper>

### 3. Get Order ID

On your server:

1. Create an `ORDER_ID` by using the <a href="/docs/api/orders/v2">Orders v2 API</a>.
2. Pass your `ACCESS_TOKEN` in the `Authorization` header. To get an `ACCESS_TOKEN`, use the [Authentication API](/api/rest/authentication/).
   > **Note:** This access token is only for the sandbox environment. When you're ready to go live, request a live access token by changing the request sandbox endpoint to https://api-m.paypal.com/v1/oauth2/token.
3. Pass the `intent`. You'll need to pass either `AUTHORIZE` or `CAPTURE` as the `intent` type. This type must match the `/authorize` or `/capture` endpoint you use to process your order.

<Tabs>
<Tab label="Sample request">
<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
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
`}
></CodeBlock>
</CodeBlockWrapper>
</Tab>
<Tab label="Sample response">
<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
{
 "id":"ORDER_ID",
 "status":"CREATED"
}
`}
></CodeBlock>
</CodeBlockWrapper>
</Tab>
</Tabs>

When a buyer starts a payment, send the `ORDER_ID` from your server to your client app.

> **Note:** Collecting a billing address can reduce the number of  authentication challenges to customers.

### 4. Create web checkout request

Configure your `PayPalWebCheckoutRequest` with the `ORDER_ID`. You can also specify one of the following funding sources for your order: `PayPal` (default), `PayLater`, or `PayPalCredit`.

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let payPalWebRequest = PayPalWebCheckoutRequest(orderID: "ORDER_ID", fundingSource: .paypal)
`}
></CodeBlock>
</CodeBlockWrapper>

### 5. Approve order

Call `PayPalWebCheckoutClient.start()` to process the payment. Implement `PayPalWebCheckoutDelegate` in your `ViewController` to listen for result notifications from the SDK:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
extension MyViewController: PayPalWebCheckoutDelegate {
  func checkoutWithPayPal(payPalWebRequest: PayPalWebCheckoutRequest) {
    payPalWebCheckoutClient.delegate = self
    payPalWebCheckoutClient.start(request: payPalWebRequest)
  }
  // MARK: - PayPalWebCheckoutDelegate
  func payPal(_ payPalClient: PayPalWebCheckoutClient, didFinishWithResult result: PayPalWebCheckoutResult) {
    // order was approved and is ready to be captured/authorized (see step 7)
  }
  func payPal(_ payPalClient: PayPalWebCheckoutClient, didFinishWithError error: CoreSDKError) {
    // handle the error by accessing \`error.localizedDescription\`
  }
  func payPalDidCancel(_ payPalClient: PayPalWebCheckoutClient) {
    // the user canceled
  }
}
`}
></CodeBlock>
</CodeBlockWrapper>

### 6. Authorize and capture order

Submit your `ORDER_ID` for authorization or capture when the PayPal iOS SDK calls the `onPayPalWebSuccess` method on `PayPalWebCheckoutListener`.

Call the [`authorize`](/docs/api/orders/v2/#orders_authorize) endpoint of the Orders V2 API to place the money on hold:

#### Sample request: Authorize order

<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/authorize' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
`}
></CodeBlock>
</CodeBlockWrapper>
<br />

Call the [`capture`](/docs/api/orders/v2/#orders_capture) endpoint of the Orders V2 API to capture the money immediately:

#### Sample request: Capture order

<CodeBlockWrapper>
<CodeBlock
className="language-curl"
children={`
curl --location --request POST 'https://api-m.sandbox.paypal.com/v2/checkout/orders/ORDER_ID/capture' \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer ACCESS_TOKEN' \\
  --data-raw ''
`}
></CodeBlock>
</CodeBlockWrapper>

</ContentTab>
</ContentTabs>

## Payment buttons and fraud protection

After you integrate a payment method, add a payment button to your page to start the payment process. You can also add fraud protection to your app.

<ContentTabs>
<ContentTab label="Payment buttons">

### Use PayPal buttons in your UI

The `PaymentButtons` module provides a set of PayPal-branded buttons to seamlessly integrate with PayPal `web` and `native` payments.

Follow these steps to add PayPal buttons to your integration:

### 1. Add PaymentButtons to your app

Add the `PaymentButtons` package dependency for your app using **Swift Package Manager** or **CocoaPods**:

<Pills>
<Pill label="Swift Package Manager">

1. Open Xcode.
2. <a href="https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app">Follow the guide</a> to add package dependencies to your app.
3. Enter <a href="https://github.com/paypal/paypal-ios/"><code>https://github.com/paypal/paypal-ios/</code></a> as the repository URL.
4. Select the checkbox for the `PaymentButtons` framework.

</Pill>
<Pill label="CocoaPods">

Include `PayPal/PaymentButtons` in your Podfile:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
# Podfile
pod 'PayPal/PaymentButtons'
`}
></CodeBlock>
</CodeBlockWrapper>

</Pill>
</Pills>

### 2. Create PayPal button

The `PaymentButtons` module provides 3 buttons that you can use in your application:

<ul>
  <li><code>PayPalButton</code>: A generic PayPal button.</li>
  <li><code>PayPalPayLater</code>: A PayPal button with a PayLater label.</li>
  <li><code>PayPalCredit</code>: A PayPal button with the PayPalCredit logo.</li>
</ul>

These buttons include customization options such as color, shape, size, and labels. Here's how to style the button corner radius:

| Value  | Description | Button |
|--------|-------------|--------|
| `rectangle` | Button shape with sharp corners. | |
| `rounded` | **Recommended**<br />Button shape with rounded corner radius. The default button shape. | <iframe src="https://www.paypal.com/webapps/hermes/button?version=4&env=production&style.color=gold&style.shape=rect&style.size=medium&sessionID=46171950e0&locale.x=en_US&logLevel=warn&uid=f6713002fd&xcomponent=1&style.label=paypal" width="250" height="70" frameBorder="0"></iframe> |
| `pill` | Button in pill shape. | <iframe src="https://www.paypal.com/webapps/hermes/button?version=4&env=production&style.color=gold&style.shape=pill&style.size=medium&sessionID=46171950e0&locale.x=en_US&logLevel=warn&uid=f6713002fd&xcomponent=1&style.label=paypal" width="250" height="70" frameBorder="0"></iframe> |
| `custom(CGFloat)` | Customize the button's corner radius. The minimum value is 10 px and is applied to all 4 corners. | |

Add buttons using either `UKit` or `SwiftUI` as follows:

<Pills>
<Pill label="UKit">

<CodeBlockWrapper>
<CodeBlock
className="language-swift"
children={`
class MyViewController: UIViewController {
  lazy var payPalButton: PayPalButton = {
    let payPalButton = PayPalButton()
    payPalButton.addTarget(self, action: #selector(payPalButtonTapped), for: .touchUpInside)
    return payPalButton
  }()
  @objc func payPalButtonTapped() {
    // Insert your code here
  }
  override func viewDidLoad() {
    super.viewDidLoad()
    view.addSubview(payPalButton)
  }
}
`}
></CodeBlock>
</CodeBlockWrapper>

</Pill>
<Pill label="SwiftUI">

<CodeBlockWrapper>
<CodeBlock
className="language-swiftui"
children={`
struct MyApp: View {
  @ViewBuilder
  var body: some View {
    VStack {
      PayPalButton.Representable() {
        // Insert your code here
      }
    }
  }
}
`}
></CodeBlock>
</CodeBlockWrapper>

</Pill>
</Pills>

</ContentTab>
<ContentTab label="Fraud protection">

### Protect from fraud

The `FraudProtection` module helps you collect data about a customer's device and match it with a session identifier on your server. For more information, see [Fraud protection](/docs/checkout/advanced/customize/fraud-protection/).

### 1. Add FraudProtection to your app

Add the `FraudProtection` package dependency for your app using **Swift Package Manager** or **CocoaPods**:

<Pills>
<Pill label="Swift Package Manager">

1. Open Xcode.
2. <a href="https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app">Follow the guide</a> to add package dependencies to your app.
3. Enter <a href="https://github.com/paypal/paypal-ios/"><code>https://github.com/paypal/paypal-ios/</code></a> as the repository URL.
4. Select the checkbox for the `FraudProtection` framework.

</Pill>
<Pill label="CocoaPods">

Include `PayPal/FraudProtection` in your Podfile:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
# Podfile
pod 'PayPal/FraudProtection'
`}
></CodeBlock>
</CodeBlockWrapper>

</Pill>
</Pills>

### 2. Create PayPalDataCollector

In your iOS app:
1. Use the `CLIENT_ID` to construct a `CoreConfig`.
2. Construct a `PayPalDataCollector` using your `CoreConfig` object.

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
let coreConfig = CoreConfig(clientID: "CLIENT_ID", environment: .sandbox)
let dataCollector = PayPalDataCollector(config: coreConfig)
`}
></CodeBlock>
</CodeBlockWrapper>

### 3. Collect client metadata

Collect the client metadata ID before starting a payment from a mobile device:

<CodeBlockWrapper>
<CodeBlock
className="language-javascript"
children={`
val clientMetadataId = dataCollector.collectDeviceData()
`}
></CodeBlock>
</CodeBlockWrapper>

Pass the result to your server, and include the client metadata ID in the payment request you send to PayPal. Don't cache or store this value.

</ContentTab>
</ContentTabs>

## Go live

If you have fulfilled the requirements for accepting Advanced Credit and Debit Card Payments for your [business account](https://www.paypal.com/myaccount/bundle/business/upgrade), review the **[Move your app to production](/api/rest/production/)** page to learn how to test and go live.

If this is your first time testing in a live environment, follow these steps:

1. Log into the [PayPal Developer Dashboard](/dashboard/) with your PayPal business account.
2. Complete [production onboarding](https://www.paypal.com/bizsignup/entry?_ga=1.171321763.248280996.1670866755) so you can process card payments with your live PayPal business account.
3. Request [Advanced Credit and Debit Card Payments](https://www.paypal.com/signin/client?flow=provisionUser&country.x=US&locale.x=en_US&_ga=1.95899167.248280996.1670866755) for your business account.

> **Important:** The code for the integration checks eligibility requirements, so the payment card fields only display when the production request is successful.
