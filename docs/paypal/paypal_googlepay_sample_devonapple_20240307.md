# Integrate Google Pay with JavaScript SDK for direct merchants

<div className="purpleHeader">
  <div className="outerouter">
    <BellIcon />
    <div className="myStuff">
      <h4 className="stuffH2 ">
        We've made changes to this page and its layout to improve the developer experience
      </h4>
      <span className="stuffSpan">
        Let us know what you think of the updated documentation by selecting the feedback tab below.
      </span>
    </div>
  </div>
</div>

<NavigationTabs pageName="googlePayDM" buttonSizes="large" />

<SectionInView id="#link-googlepayintegration">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-googlepayintegration">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
          Google Pay integration
        </h2>
        <p>
          Google Pay is a mobile payment and digital wallet service provided by Alphabet Inc.
        </p>
        <p>
          Buyers can use Google Pay on PayPal to make payments on the web using a web browser.
        </p>
        <p>
          Sellers can use PayPal with Google Pay to sell physical goods,{" "}
          such as clothes and electronics, and intangible professional  services,{" "}
          such as concerts or gym memberships.
        </p>
      </Col>
      <Col className="imageCol">
        <ImageContainer
          src="https://paypalobjects.com/devdoc/sdk_mobile_googlepay.png"
          fileName="googlepay-xxl.png"
          className="productHero"
          caption="Google Pay mobile web illustration"
        />
      </Col>
    </Row>
    <Row>
      <Col>
        <h3 className="newH2 " style={{ marginTop: "2rem" }}>
          Supported countries and currencies
        </h3>
        <MobilePaymentEligibility paymentmethod="Google Pay"/>
        <AlertMessage type="tip">
          If you want to integrate additional methods of accepting payment beyond Google Pay, visit our <a href="/docs/checkout/advanced/integrate/" className="linkFormat">Advanced Checkout guide</a> for additional integration choices.
        </AlertMessage>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-howitworks">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-howitworks">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
          How it works
        </h2>
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
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-knowbeforeyoucode">
  <div className="outerBeforeRow" id="link-knowbeforeyoucode">
    <div className="innerBeforeRow">
      <div className="archetypeHeader">
        <KnowBeforeYouCodeWrapper>
          <KnowBeforeYouCodeCard
            badge="Required"
            title=""
            primaryType="button"
            primaryLabel="Check Compatibility"
            primaryLink="https://developers.google.com/pay/api/web/guides/test-and-deploy/integration-checklist#test-using-browser-developer-console"
          >
              <p className="boldArchText">
                Google Pay works on most web browsers, including:
              </p>
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
          </KnowBeforeYouCodeCard>
          <KnowBeforeYouCodeCard
            badge="Required"
            title=""
            primaryType="button"
            primaryLabel="Google Terms of Service"
            primaryLink="https://payments.developers.google.com/terms/sellertos"
            tertiaryLabel="Acceptable use policy"
            tertiaryLink="https://payments.developers.google.com/terms/aup"
          >
              <p className="boldArchText">
                Currently supports Google Pay one-time payments with the buyer present.
              </p>
              <p>
                Review Google's Google Pay API Terms of Service and Acceptable Use Policy
                for more information.
              </p>
          </KnowBeforeYouCodeCard>
        </KnowBeforeYouCodeWrapper>
      </div>
    </div>
  </div>
</SectionInView>

<div className="archetypeHeader">
  <Row style={{ marginTop: "3rem" }}>
    <Col>
      <div className="openInCodeSpaces-div">
        <OpenInGitHubCodeSpaces
          styleclass="medium-open-in-codespaces"
          headerText="Get up and running in GitHub Codespaces"
          text="GitHub Codespaces are cloud-based development environments where you can code and test your PayPal integrations. <a href='/api/rest/sandbox/codespaces/' target='_blank'>Learn more</a>"
          href="https://codespaces.new/paypal-examples/googlepay"
        />
      </div>
    </Col>
  </Row>
</div>

<SectionInView id="#link-setupyoursandboxaccounttoacceptgooglepay">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-setupyoursandboxaccounttoacceptgooglepay">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
          1. Set up your sandbox account to accept Google Pay
        </h2>
    <p>
      Before you can accept Google Pay on your website, verify that your{" "}
      sandbox business account supports Google Pay.{" "}
    </p>
        <p>
          Direct merchants can use the PayPal Developer Dashboard to set up their sandbox accounts{" "}
          to accept Google Pay.
        </p>
        <ol>
          <li>
            Log into the PayPal{" "}
            <a href="/dashboard" target="_blank" className="linkFormat">
              Developer Dashboard
            </a>{" "}
            and go to your sandbox account.
          </li>
          <li>
            Go to <b>Apps & Credentials</b>.
          </li>
          <li>
            Make sure you are in the PayPal sandbox environment by selecting{" "}
            <b>Sandbox</b> at the top.
          </li>
          <li>Select or create an app.</li>
          <li>
            Scroll down to <b>Features</b> and check if Google Pay is enabled. {" "}
            If Google Pay isn't enabled, select the{" "}
            <b>Google Pay</b> checkbox and select the "Save" link to enable Google Pay.
          </li>
        </ol>
        <p>
          If you created a sandbox business account through{" "}
          <a
            href="https://sandbox.paypal.com"
            target="_blank"
            className="linkFormat"
          >
            sandbox.paypal.com
          </a>
          , and the Google Pay status for the account shows as disabled, <a
            href="https://www.sandbox.paypal.com/bizsignup/add-product?product=payment_methods&capabilities=GOOGLE_PAY"
            target="_blank"
            className="linkFormat"
          >
            complete the sandbox onboarding steps
          </a> to enable Google Pay.
        </p>
        <AlertMessage type="tip">
          When your integration is ready to go live, read the <span className="boldText">Go live</span> section for details about the additional steps needed for Google Pay onboarding.
        </AlertMessage>
      </Col>
    </Row>
    <Row style={{ marginTop: "2rem" }} >
      <Col>
        <p>
          This screenshot shows the Google Pay sandbox settings in the mobile and digital payments section{" "}
          of the PayPal Developer Dashboard. This only applies to direct merchant integrations:
        </p>
      </Col>
    </Row>
    <Row>
      <Col className="imageCol">
        <ImageContainer
          src="https://paypalobjects.com/devdoc/sdk_acdc_acceptpayments.png"
          fileName="googlepay-sandbox-xxl.png"
          className="productHero"
          caption="Google Pay sandbox settings in the PayPal Developer Dashboard"
        />
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-gettingstartedinyourtestingenvironment">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-gettingstartedinyourtestingenvironment">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
          2. Getting started in your testing environment
        </h2>
        <p>
          Before you develop your Google Pay on the Web integration, you need to complete{" "}
          <a href="/api/rest/" target="_blank" className="linkFormat">
            Get started
          </a>{" "}
          to set up your PayPal account, client ID, and sandbox emails for testing.
        </p>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-integrategooglepaycheckout">
  <div className="archetypeHeader">
    <Row id="link-integrategooglepaycheckout">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      3. Integrate Google Pay checkout
    </h2>
    <p>
      Follow this integration process to add Google Pay as a checkout option, customize the payment experience, and process payments.
    </p>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Call the Orders API
    </h3>
    <p>
      To accept Google Pay directly on your website, create API endpoints on your
      server that communicate with the{" "}
      <a href="/docs/api/orders/v2/" target="_blank" className="linkFormat">
        PayPal Orders V2 API
      </a>
      . These endpoints can create an order, authorize payment, and capture payment
      for an order.
    </p>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Server-side example (Node.js)
    </h3>
    <p>
      This code demonstrates using the{" "}
      <a href="/docs/api/orders/v2/" target="_blank" className="linkFormat">
        PayPal Orders V2 API
      </a>{" "}
      to add routes to an Express server for creating orders and capturing payments.
    </p>
    <p>
      Find the complete sample code in the{" "}
      <a href="https://github.com/paypal-examples/googlepay" target="_blank" className="linkFormat">
        GitHub repo
      </a>
      .
    </p>
    <NewCodeTabs>
      <NewCodeTab label="server.js">
        <NewCodeBlock
          className="language-javascript"
          children={`
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
              `}
            />
          </NewCodeTab>
          <NewCodeTab label="paypal-api.js">
            <NewCodeBlock
              className="language-javascript"
              children={`
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
}\n
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
            `} />
          </NewCodeTab>
        </NewCodeTabs>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-setupyourgooglepaybutton">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-setupyourgooglepaybutton">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      4. Set up your Google Pay button
    </h2>
    <p>
      You need to integrate with the Google Pay JavaScript SDK and PayPal JavaScript SDK to add Google Pay to your site.
    </p>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Integrate PayPal JavaScript SDK
    </h3>
    <p>Use this script to integrate with the PayPal JavaScript SDK:</p>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-javascript"
        children={`
<script src="https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID&currency=USD&buyer-country=US&merchant-id=SUB_MERCHANT_ID&components=googlepay"></script> `}
      />
    </NewCodeBlockWrapper>
    <p>
      Include <code>googlepay</code> in the <code>components</code> list.
    </p>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Integrate Google JavaScript SDK
    </h3>
    <p>Use this script to integrate with the Google Pay JavaScript SDK:</p>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-javascript"
        children={`
<script async src="https://pay.google.com/gp/p/js/pay.js" onload="onGooglePayLoaded()"></script> `}
      />
    </NewCodeBlockWrapper>
    <p>
      PayPal's Google Pay component interacts with your JavaScript code in 2 areas:
    </p>
    <ol>
      <li>
        Checking merchant eligibility and providing <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/request-objects#PaymentDataRequest"><code>PaymentDataRequest</code></a> parameters for Google Pay: <code>paypal.Googlepay().config()</code>.
      </li>
      <li>
        Handling the <code>onPaymentAuthorized()</code> callback:{" "}
        <code>paypal.Googlepay().confirmOrder()</code>.
      </li>
    </ol>
    <p>
      Check for device and merchant eligibility before setting up the GooglePay Button.
    </p>
    <p>
      The PayPal JavaScript SDK API <code>paypal.Googlepay().config()</code> response object{" "}
      provides the <code>allowedPaymentMethods</code> parameter, which is part of the" "}
      Google API's <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/request-objects#IsReadyToPayRequest"><code>isReadyToPayRequest</code></a> object.
    </p>
    <p>
      Check whether the Google Pay API supports a device, browser, and payment method:
    </p>
    <ul>
      <li>Add <code>allowedPaymentMethods</code> to the <code>isReadyToPayRequest</code>.</li>
      <li>Call the <code>isReadyToPay()</code> method to check compatibility and render the Google Pay Button.</li>
    </ul>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-javascript"
        children={`
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
      `}
      />
    </NewCodeBlockWrapper>
    <AlertMessage type="tip">
      For more information refer to steps 6 and 7 in{" "}
      <a
        href="https://developers.google.com/pay/api/web/guides/tutorial#isreadytopay"
        className="linkFormat dx-external-href"
        target="_blank"
      >
        Google's developer documentation
      </a>
      .
    </AlertMessage>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-createpaymentdatarequest">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-createpaymentdatarequest">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      5. Create PaymentDataRequest
    </h2>
    <p>
      The <code>PaymentDataRequest</code> object manages the Google Pay payment{" "}
      process on the web. Create a new <code>PaymentDataRequest</code> each time a{" "}
      buyer explicitly requests a payment, such as inside the{" "}
      <code>onclick</code> handler for the Google Pay Button.
    </p>
    <p>
      For each checkout session, create a `PaymentDataRequest` object,{" "}
      which includes information about payment processing capabilities,{" "}
      the payment amount, and shipping information.
    </p>
    <p>
      The response object of the PayPal JavaScript SDK API{" "}
      <code>paypal.Googlepay().config()</code> provides the following parameters
      in the <code>PaymentDataRequest</code> object:
    </p>
    <ul>
      <li><code>allowedPaymentMethods</code></li>
      <li><code>merchantInfo</code></li>
    </ul>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-javascript"
        children={`
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
        `}
      />
    </NewCodeBlockWrapper>
    <p>
      For more details about the response parameters, see the <span className="boldText"><code>ConfigResponse</code></span> section.
    </p>
    <p>
      For more details about how Google Pay handles <code>paymentDataRequest</code>, refer to steps 8, 9, and 10 in <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/guides/tutorial#paymentdatarequest">Google's developer documentation</a>.
    </p>
    <AlertMessage type="tip">
      See the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/request-objects#PaymentDataRequest">Google Pay PaymentDataRequest Object API reference</a> for the complete list of properties available for the <code>PaymentDataRequest</code> object.
    </AlertMessage>
  <h3 className="newH2 " style={{ marginTop: "2rem" }}>
    Register click handler
  </h3>
  <p>
  </p>
  <p>
    Register a click event handler for the Google Pay purchase button.{" "}
    Call <code>loadPaymentData()</code> in the event handler when the user interacts{" "}
    with the purchase button and pass the <code>PaymentDataRequest</code> object.
  </p>
  <NewCodeBlockWrapper>
    <NewCodeBlock
      className="language-javascript"
      children={`
/* Show Google Pay payment sheet when Google Pay payment button is clicked */
async function onGooglePaymentButtonClicked() {
  const paymentDataRequest = await getGooglePaymentDataRequest();
  const paymentsClient = getGooglePaymentsClient();
  paymentsClient.loadPaymentData(paymentDataRequest);
}
      `}
    />
  </NewCodeBlockWrapper>
  <p>
    Add the click handler <code>onGooglePaymentButtonClicked</code> to the Button{" "}
    defined in <a href="#link-setupyourgooglepaybutton" className="linkFormat">Set up your Google Pay button</a>.
  </p>
  <p>
    For more details about <code>paymentDataRequest</code> refer to step 9 in{" "}
    <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/guides/tutorial#paymentdatarequest">Google's developer documentation</a>.
  </p>
  <h3 className="newH2 " style={{ marginTop: "2rem" }}>
    onpaymentauthorized callback
  </h3>
  <p>
    Google calls the <code>onPaymentAuthorized()</code> callback with a <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/response-objects#PaymentData"><code>PaymentData</code></a> object when a customer consents to your site collecting their payment information and optional contact details.
  </p>
  <p>
    Register the <code>onPaymentAuthorized()</code> callback as part of the <code>PaymentClient</code> initialization as shown in Google Pay's <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/client#PaymentsClient">Client Reference page</a>.
  </p>
  <p>
    Create an order by using the <a href="/api/orders/v2" target="_blank" className="linkFormat">PayPal Orders V2 API</a>. Use <code>paypal.Googlepay().confirmOrder()</code> to send the <code>orderID</code>, the Google Pay Payment Data, and optional contact details, and confirm the order.
  </p>
  <p>
    Confirm the order using the <a href="#link-confirmorderconfirmorderparams" className="linkFormat"><code>paypal.Googlepay().confirmOrder()</code></a> method in the API SDK Reference.
  </p>
  <p>
    If the order confirmation status is <code>APPROVED</code>, capture the order using the <a href="/docs/api/orders/v2/#orders_capture" target="_blank" className="linkFormat">Capture payment for order endpoint</a> of the PayPal Orders V2 API.
  </p>
  <p>
    For more details, see step 11 of <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/guides/tutorial#authorize-payments">Google's developer documentation</a>.
  </p>
  <AlertMessage type="tip">
    You can see an <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/guides/tutorial#authorize-payments_1">example of an Authorize Payments call</a> in the <span className="boldText">Put it all together</span> section of Google's developer documentation.
  </AlertMessage>
  <NewCodeBlockWrapper>
    <NewCodeBlock
      className="language-javascript"
      children={`
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
      `}
    />
  </NewCodeBlockWrapper>
<h3 className="newH2 " style={{ marginTop: "2rem" }}>
  Customize payment experience
</h3>
<p>
Customize the payment experience using the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/client">Google Pay JavaScript SDK</a>. The following table shows the 2 most popular Google Pay customizations:
</p>
<table>
  <thead>
    <tr>
      <th>Customization</th>
      <th>Details</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/client#onPaymentDataChanged"><code>PaymentDataChange</code></a>
      </td>
      <td>
        This method is used to handle payment data changes in the payment sheet such as shipping address and shipping options.
      </td>
    </tr>
    <tr>
      <td>
        <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/request-objects#PaymentDataRequest"><code>PaymentDataRequest</code></a>
      </td>
      <td>
        Provides optional properties to collect details, such as shipping address and email.
      </td>
    </tr>
  </tbody>
</table>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-putitalltogether">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-putitalltogether">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      6. Put it all together
    </h2>
    <p>
      The following code samples show a Google Pay integration:
    </p>
    <NewCodeTabs>
      <NewCodeTab label="HTML">
        <NewCodeBlock
          className="language-html"
          children={`
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
        `} />
      </NewCodeTab>
      <NewCodeTab label="JavaScript">
          <NewCodeBlock
            className="language-javascript"
            children={`
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
              `} />
            </NewCodeTab>
        </NewCodeTabs>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-strongcustomerauthenticationsca">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-strongcustomerauthenticationsca">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      Strong Customer Authentication (SCA)
    </h2>
    <p>
      When the <code>ConfirmOrder</code> <a href="/docs/api/orders/v2/#definition-order_status" target="_blank" className="linkFormat">status</a> is <code>PAYER_ACTION_REQUIRED</code>, the order requires additional authentication from the payer, such as 3D Secure.
    </p>
    <p>
      The PayPal JavaScript SDK Client provides an API to handle 3DS Secure authentication. Pass the <code>orderId</code> to <code>initiatePayerAction</code>.
    </p>
    <AlertMessage type="tip">
      Refer to <a href="#link-initiatepayeractionparams" className="linkFormat"><code>initiatePayerAction</code></a> for more details.
    </AlertMessage>
    <br />
      <p>
        When the payer completes authentication, confirm that the <code>liability_shift</code> status has shifted:
      </p>
      <ul>
        <li>
          Make a call to the <a href="/docs/api/orders/v2/#orders_get" target="_blank" className="linkFormat">Show order details endpoint</a> of the Orders v2 API, using the <code>id</code> of the order.
        </li>
        <li>
          Check the <code>liability_shift</code> status in the <a href="/docs/api/orders/v2/#definition-authentication_response" target="_blank" className="linkFormat"><code>authentication_response</code></a>.
        </li>
      </ul>
      <NewCodeBlockWrapper>
        <NewCodeBlock
          className="language-javascript"
          children={`
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
          `}
        />
      </NewCodeBlockWrapper>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-testyourintegration">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-testyourintegration">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      7. Test your integration
    </h2>
    <p>
      Test your Google Pay integration in the PayPal sandbox and production environments to ensure that{" "}
      your app works correctly.
    </p>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Sandbox
    </h3>
    <p>
      Use your personal sandbox login information during checkout to complete a payment using Google Pay. Then, log into the sandbox site <a href="https://sandbox.paypal.com" target="_blank" className="linkFormat">sandbox.paypal.com</a> to see that the money has moved into your account.
    </p>
    <ol>
      <li>
        Open your test page with a supported web browser on any supported device.
      </li>
      <li>
        Add a test card to your Google Wallet on your device.{" "}
        Google provides test cards through their{" "}
        <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/guides/resources/test-card-suite">Test card suite</a>.
      </li>
      <li>
        Tap the <span className="boldText">Google Pay</span> button to open a pop-up with the Google Pay payment sheet.
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
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Google Pay test card suite
    </h3>
    <p>
      Use Google Pay <a href="/docs/checkout/apm/test-cards/google-pay/" className="linkFormat">test card numbers</a> to test your Google Pay integration.
    </p>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-golive">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-golive">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      8. Go live
    </h2>
    <p>Make Google Pay available to buyers using your website or app.</p>
    <AlertMessage type="tip">
      Before going live, complete <a target="_blank" className="dx-external-href linkFormat" href="https://www.paypal.com/bizsignup/add-product?product=payment_methods&capabilities=GOOGLE_PAY">production onboarding</a> to process Google Pay payments with your live PayPal account.
    </AlertMessage>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Live environment
    </h3>
    <p>
      If you're a new merchant, sign up for a{" "}
      <a
        href="https://www.paypal.com/us/business"
        className="linkFormat dx-external-href"
        target="_blank"
      >
        PayPal business account
      </a>
      .
    </p>
    <p>
      Use your personal production login information during checkout to complete{" "}
      a Google Pay transaction. Then log into <b>paypal.com</b> to see the money{" "}
      move out of your account.
    </p>
    </Col>
  </Row>
  <Row>
    <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      Testing in your live environment
    </h2>
    <p>When testing a purchase in production, consider:</p>
    <ul>
      <li>
        The business account receiving money can't also make the purchase.
      </li>
      <li>
        If you create a personal account with the same information as the
        business account, those accounts might experience restrictions.
      </li>
    </ul>
    <p>How to test Google Pay payments in a live environment:</p>
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
    <h2 className="newH2">Troubleshoot your integration</h2>
    <p>
      Make sure that there are no browser console warnings or errors. The JavaScript SDK configuration attributes have distinct validation checks for input formatting and values.
    </p>
    <p>
      If the validation fails, the web browser's developer console shows warning messages that say which property is incorrect and what you need to do to address the issue. The library generally attempts to revert to the safe default values if missing or incorrect inputs exist.
    </p>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-nextstepscustomizations">
  <div className="outerBeforeRow" id="link-nextstepscustomizations">
    <div className="archetypeHeader">
      <div style={{ paddingTop: "60px", paddingBottom: "60px" }}>
        <Row>
          <Col>
            <h2 className="newH2 ">Next steps & customizations</h2>
            <p>
              Get started testing, add security to your checkout experience or
              create customizations for your audience.
            </p>
          </Col>
        </Row>
        <Row>
          <Col md={6} sm={12}>
            <div className="whiteBox">
              <div className="flexRow">
                <div className="flexCol">
                  <DocumentIcon />
                </div>
                <div className="flexCol">
                  <Badge type="neutral">Optional</Badge>
                </div>
              </div>
              <div className="box-internal">
                <a
                  href="/docs/checkout/advanced/"
                  className="nextStep-link linkFormat"
                >
                  Advanced credit and debit card payments
                </a>
                <p>Add PayPal payment buttons and customized card fields.</p>
              </div>
            </div>
          </Col>
        </Row>
      </div>
    </div>
  </div>
</SectionInView>

<SectionInView id="#link-sdkapireference">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-sdkapireference">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      SDK API reference
    </h2>
    <p>
      This section provides details about functions, objects, and parameters in the SDK API.
    </p>
    </Col>
  </Row>
  <Row>
    <Col>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Initialize payment with paypal.Googlepay()
    </h3>
      <p>
        Creates an instance of a PayPal Google Pay SDK Client.
      </p>
      <p>
        <span className="boldText">Arguments</span>
      </p>
      <p>
        None
      </p>
      <p>
        <span className="boldText">Returns</span>
      </p>
      <p>
        <a href="#link-jssdkclientobject" className="linkFormat">JavaScript SDK Client</a>
      </p>
      </Col>
    </Row>
    <Row>
      <Col>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      JavaScript SDK client methods
    </h3>
      <p>
        Use the JavaScript SDK client methods to start a Google Pay payment and confirm an order.
      </p>
      <ContentAccordion>
        <AccordionRow id="link-config" heading="config()">
          <p>
            Use <code>config()</code> to fetch the <code>PaymentMethod</code> data needed to start the payment.
          </p>
          <br />
          <p>
            <span className="boldText">Arguments</span>
          </p>
          <br />
          <p>
            None
          </p>
          <br />
          <p>
            <span className="boldText">Returns</span>
          </p>
          <br />
          <table>
            <thead>
              <tr>
                <th>Type</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>
                  <a target="_blank" className="dx-external-href linkFormat" href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise"><code>Promise</code></a>
               </td>
                <td>
                  <p><span className="boldText">Resolved:</span> An object that contains the payment data needed to create a <code>PaymentDataRequest</code> to the Google SDK. For more details, see <a href="#link-configresponse" className="linkFormat"><code>ConfigResponse</code></a>.</p>
                  <p><span className="boldText">Rejected:</span> An error object that passes information about why the call wasn't successful.</p>
               </td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      <ContentAccordion>
        <AccordionRow id="link-confirmorderconfirmorderparams" heading="confirmOrder(confirmOrderParams)">
          <br />
          <p>
            Use <code>confirmOrder()</code> to confirm that the buyer intends to pay for the order using the payment source.
          </p>
          <br />
          <p>
            <span className="boldText">Arguments</span>
          </p>
          <br />
          <table>
            <thead>
              <tr>
                <th>Name</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>
                  <code>confirmOrderParams</code>
               </td>
                <td>
                  For details on the different properties you can configure, see <a href="#link-confirmorderparams" className="linkFormat"><code>ConfirmOrderParams</code></a>.
               </td>
              </tr>
            </tbody>
          </table>
          <p>
            <span className="boldText">Returns</span>
          </p>
          <table>
            <thead>
              <tr>
                <th>Name</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>
                  <a target="_blank" className="dx-external-href linkFormat" href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise"><code>Promise</code></a>
               </td>
                <td>
                  <p><span className="boldText">Resolved:</span> An object that returns the response of a successful <code>confirmOrder</code>. For more details, see <a href="#link-confirmorderresponse" className="linkFormat"><code>ConfirmOrderResponse</code></a>.</p>
                  <p><span className="boldText">Rejected:</span> An error object that passes information about why the call wasn't successful.</p>
               </td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      <ContentAccordion>
        <AccordionRow id="link-initiatepayeractioninitiatepayeractionparams" heading="initiatePayerAction(initiatePayerActionParams)">
          <p>
            <span className="boldText">Arguments</span>
          </p>
          <table>
            <thead>
              <tr>
                <th>Name</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>initiatePayerActionParams</code></td>
                <td>
                  <p>For details on the different properties you can configure, see <a href="#link-initiatepayeractionparams" className="linkFormat"><code>InitiatePayerActionParams</code></a>.</p>
               </td>
              </tr>
            </tbody>
          </table>
          <br />
          <p>
            <span className="boldText">Returns</span>
          </p>
          <table>
            <thead>
              <tr>
                <th>Type</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><a target="_blank" className="dx-external-href linkFormat" href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise"><code>Promise</code></a></td>
                <td>
                  <p><span className="boldText">Resolved:</span> An object that passes information about 3D Secure liability shift. See <a href="#link-initiatepayeractionresponse" className="linkFormat"><code>InitiatePayerActionResponse</code></a> for more information.</p>
                  <p><span className="boldText">Rejected:</span> An error object that passes information about why the call wasn't successful.</p>
               </td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      </Col>
    </Row>
    <Row>
      <Col>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Request objects
    </h3>
      <p>
        Use the following JavaScript SDK request objects in a Google Pay payment:
      </p>
      <ContentAccordion>
        <AccordionRow id="link-confirmorderparams" heading="ConfirmOrderParams">
          <table>
            <thead>
              <tr>
                <th>Property</th>
                <th>Type</th>
                <th>Required</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>paymentMethodData</code></td>
                <td>object</td>
                <td>Yes</td>
                <td>
                  <p>Details about a selected payment method. When a buyer approves payment, the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/response-objects#PaymentData"><code>PaymentData</code></a> response object from Google passes the <code>paymentMethodData</code>.</p>
                  <p>For more details about this object, see the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/response-objects#PaymentMethodData">Google Pay documentation</a>.</p>
               </td>
              </tr>
              <tr>
                <td><code>orderId</code></td>
                <td>string</td>
                <td>Yes</td>
                <td>The PayPal order ID.</td>
              </tr>
              <tr>
                <td><code>shippingAddress</code></td>
                <td>object</td>
                <td>No</td>
                <td>
                  <p>Passes the shipping address when <code>shippingAddressRequired</code> in the <code>PaymentDataRequest</code> is set to <code>true</code>.</p>
                  <p>For more details about this object, see the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/response-objects#Address">Google Pay documentation</a>.</p>
               </td>
              </tr>
              <tr>
                <td><code>billingAddress</code></td>
                <td>object</td>
                <td>No</td>
                <td>
                  <p>The default billing address is part of the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/response-objects#CardInfo"><code>CardInfo</code></a> object. Use this property to pass a new billing address and overwrite the default.</p>
                  <p>For more details about this object, see the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/response-objects#Address">Google Pay documentation</a>.</p>
               </td>
              </tr>
              <tr>
                <td><code>email</code></td>
                <td>string</td>
                <td>No</td>
                <td>Passes the email address when <code>emailRequired</code> in the <code>PaymentDataRequest</code> is set to <code>true</code>.</td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      <ContentAccordion>
        <AccordionRow id="link-initiatepayeractionparams" heading="InitiatePayerActionParams">
          <table>
            <thead>
              <tr>
                <th>Property</th>
                <th>Type</th>
                <th>Required</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>orderId</code></td>
                <td>string</td>
                <td>Yes</td>
                <td>PayPal OrderID</td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      </Col>
    </Row>
    <Row>
      <Col>
    <h3 className="newH2 " style={{ marginTop: "2rem" }}>
      Response objects
    </h3>
      <p>
        Google Pay responses include the following objects:
      </p>
      <ContentAccordion>
        <AccordionRow id="link-jssdkclientobject" heading="JSSDKClientObject">
          <table>
            <thead>
              <tr>
                <th>Property</th>
                <th>Type</th>
                <th>Always exists</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>config</code></td>
                <td><a href="#link-config" className="linkFormat">function</a></td>
                <td>Yes</td>
                <td>API for <code>PaymentData</code>.</td>
              </tr>
              <tr>
                <td><code>confirmOrder</code></td>
                <td><a href="#link-confirmorderconfirmorderparams" className="linkFormat">function</a></td>
                <td>Yes</td>
                <td>API for <code>confirmOrder</code>.</td>
              </tr>
              <tr>
                <td><code>initiatePayerAction</code></td>
                <td><a href="#link-initiatepayeractioninitiatepayeractionparams" className="linkFormat">function</a></td>
                <td>Yes</td>
                <td>API for 3D Secure handling.</td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      <ContentAccordion>
        <AccordionRow id="link-configresponse" heading="ConfigResponse">
          <table>
            <thead>
              <tr>
                <th>Property</th>
                <th>Type</th>
                <th>Always exists</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>allowedPaymentMethods</code></td>
                <td>object</td>
                <td>Yes</td>
                <td>
                  <p>Passes the payment methods supported by the Google Pay API.</p>
                  <p>For more details about this object, see the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/request-objects#PaymentMethod">Google Pay documentation</a>.</p>
               </td>
              </tr>
              <tr>
                <td><code>merchantInfo</code></td>
                <td>object</td>
                <td>Yes</td>
                <td>
                  <p>Passes information about the seller requesting payment data.</p>
                  <p>For more details about this object, see the <a target="_blank" className="dx-external-href linkFormat" href="https://developers.google.com/pay/api/web/reference/request-objects#MerchantInfo">Google Pay documentation</a>.</p>
               </td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      <ContentAccordion>
        <AccordionRow id="link-confirmorderresponse" heading="ConfirmOrderResponse">
          <table>
            <thead>
              <tr>
                <th>Property</th>
                <th>Type</th>
                <th>Always exists</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>id</code></td>
                <td>string</td>
                <td>Yes</td>
                <td>The ID of the order.</td>
              </tr>
              <tr>
                <td><code>status</code></td>
                <td>string</td>
                <td>Yes</td>
                <td>
                  <p>The order status.</p>
                  <p>For a list of supported values for this property, see the <a href="/docs/api/orders/v2/#definition-order_status" className="linkFormat">Orders API documentation</a>.</p>
               </td>
              </tr>
              <tr>
                <td><code>payment_source</code></td>
                <td>object</td>
                <td>Yes</td>
                <td>
                  <p>The payment source used to fund the payment.</p>
                  <p>For more details about this object, see the <a href="/docs/api/orders/v2/#definition-payment_source_response" className="linkFormat">Orders API documentation</a>.</p>
               </td>
              </tr>
              <tr>
                <td><code>links</code></td>
                <td>array of objects</td>
                <td>Yes</td>
                <td>
                  <p>The request-related <a href="/api/rest/responses/#hateoas-links" className="linkFormat">HATEOAS</a> link information.</p>
                  <p>For more details about this property, see the <a href="/docs/api/orders/v2/#definition-link_description" className="linkFormat">Orders API documentation</a>.</p>
               </td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      <ContentAccordion>
        <AccordionRow id="link-initiatepayeractionresponse" heading="InitiatePayerActionResponse">
          <table>
            <thead>
              <tr>
                <th>Property</th>
                <th>Type</th>
                <th>Always exists</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>liabilityShift</code></td>
                <td>string</td>
                <td>Yes</td>
                <td>
                  <p>The liability shift indicator shows the outcome of the issuer's authentication.</p>
                  <p>For a list of supported values for this property, see the <a href="/docs/api/orders/v2/#definition-liability_shift" className="linkFormat">Orders API documentation</a>.</p>
               </td>
              </tr>
            </tbody>
          </table>
        </AccordionRow>
      </ContentAccordion>
      </Col>
    </Row>
  </div>
</SectionInView>
