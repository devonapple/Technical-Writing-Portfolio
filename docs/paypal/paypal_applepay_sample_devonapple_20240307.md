# Integrate Apple Pay with JavaScript SDK for direct merchants

<div className="purpleHeader">
  <div className="outerouter">
    <BellIcon />
    <div className="myStuff">
      <h4 className="stuffH2 ">
        We've made changes to this page and its layout to improve the developer experience.
      </h4>
      <span className="stuffSpan">
        Let us know what you think of the updated documentation by selecting the feedback tab below.
      </span>
    </div>
  </div>
</div>

<NavigationTabs pageName="applePayDM" buttonSizes="large" />

<SectionInView id="#link-applepayintegration">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-applepayintegration">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
          Apple Pay integration
        </h2>
        <p>
          Apple Pay is a mobile payment and digital wallet service provided by Apple Inc.
        </p>
        <p>
          Buyers can use Apple Pay to make payments on the web using the Safari web browser or an iOS device.
        </p>
        <p>Sellers can use Apple Pay to sell:</p>
        <ul>
          <li>Physical goods, such as clothes and electronics.</li>
          <li>Digital goods, such as software.</li>
          <li>Intangible professional services, such as concerts or gym memberships.</li>
        </ul>
        <p>
          <a target="_blank" className="linkFormat dx-external-href" href="https://developer.apple.com/documentation/passkit/apple_pay">Visit this site</a> for more information about Apple Pay.
        </p>
      </Col>
      <Col className="imageCol">
        <ImageContainer
          src="https://www.paypalobjects.com/ppdevdocs/img/applepay-sheet-xxl-m.png"
          fileName="applepay-xxl.png"
          className="productHero"
          caption="Completed Apple Pay checkout integration"
        />
      </Col>
    </Row>
    <Row style={{ paddingBottom: "54px" }}>
      <Col>
          <h3 className="newH2 " style={{ marginTop: "0px", marginBottom: "36px" }}>
            Supported countries and currencies
          </h3>
          <MobilePaymentEligibility paymentmethod="Apple Pay"/>
          <AlertMessage type="tip">
            If you want to integrate additional methods of accepting payment beyond Apple Pay, visit our <a href="/docs/checkout/advanced/integrate/" className="linkFormat">Advanced Checkout guide</a> for additional integration choices.
          </AlertMessage>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-howitworks">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-howitworks">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>How it works</h2>
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
        </p>
        <p>
          Payment sheets can show the user's name, address, shipping information, and email address. You can customize this payment sheet to include the user details and payment information you need for your Apple Pay integration.
        </p>
        <p>
          <a
            href="https://support.apple.com/en-us/HT208531"
            className="linkFormat dx-external-href"
            target="_blank"
          >
            Visit this site
          </a>{" "}
          for more details about Apple Pay's compatibility.
        </p>
      </Col>
      <Col className="imageCol">
        <ImageContainer
          src="https://www.paypalobjects.com/ppdevdocs/img/applepay_mobile.png"
          fileName="applepaymobile.png"
          className="productHero"
          caption="Screenshot of a payment sheet on a mobile device"
        />
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-integrationvideo">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "5rem" }} id="link-integrationvideo">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-intgapplepayvideo-header">Integration video</h2>
        <p>
          Watch our video tutorial for this integration:
        </p>
      </Col>
    </Row>
    <Row style={{ marginTop: "2rem" }} className="video-container">
      <Col>
        <YoutubeVideo embedUrl="https://www.youtube-nocookie.com/embed/E3gUASHQMrU?si=OIaQryAIniy4i6F6" title="How to integrate Apple Pay" data-testid="dcai-intgapplepayvideo-ytvideo" />
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
          primaryLink="https://support.apple.com/en-us/HT208531"
        >
          <p className="boldArchText">Apple Pay works on Safari browsers and the following versions of iOS devices:</p>
          <ul>
            <li>
              macOS 10.14.1 and later.
            </li>
            <li>
              iOS 12.1 and later.
            </li>
          </ul>
        </KnowBeforeYouCodeCard>
        <KnowBeforeYouCodeCard
          badge="Required"
          title=""
          primaryType="button"
          primaryLabel="Apple Terms and Conditions"
          primaryLink="https://www.apple.com/legal/applepayments/"
          tertiaryLabel="Apple Developer Terms"
          tertiaryLink="https://developer.apple.com/app-store/review/guidelines/"
        >
          <p className="boldArchText">
            Currently supports Apple Pay one-time payments with the buyer present.
          </p>
          <ul>
            <li>
              Review Apple's terms and conditions for the Apple Pay platform.
            </li>
            <li>
              See Apple's developer terms for more information.
            </li>
          </ul>
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
          href="https://codespaces.new/paypal-examples/applepay"
        />
      </div>
    </Col>
  </Row>
</div>

<SectionInView id="#link-setupyoursandboxaccounttoacceptapplepay">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-setupyoursandboxaccounttoacceptapplepay">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
          1. Set up your sandbox account to accept Apple Pay
        </h2>
        <p>
          Before you can accept Apple Pay on your website, verify that your sandbox business account supports Apple Pay. Use the PayPal Developer Dashboard to set up your sandbox account to accept Apple Pay.
        </p>
        <ol>
          <li>Log into the <a target="_blank" className="dx-external-href linkFormat" href="/dashboard/applications/sandbox">PayPal Developer Dashboard</a> and go to your sandbox account.</li>
          <li>Go to <b>Apps & Credentials</b>.</li>
          <li>Make sure you are in the PayPal sandbox environment by selecting <b>Sandbox</b> at the top.</li>
          <li>Select or create an app.</li>
          <li>Scroll down to <b>Features</b> and check if Apple Pay is enabled. If Apple Pay isn't enabled, select the <b> Apple Pay</b> checkbox and select the "Save" link to enable Apple Pay.</li>
        </ol>
        <p>
          If you created a sandbox business account through <a target="_blank" className="linkFormat" href="https://sandbox.paypal.com/">sandbox.paypal.com</a>, and the Apple Pay status for the account shows as disabled, <a target="_blank" className="linkFormat" href="https://www.sandbox.paypal.com/bizsignup/add-product?product=payment_methods&capabilities=APPLE_PAY&_ga=1.255056589.491931369.1702610895">complete the sandbox onboarding steps</a> to enable Apple Pay.
        </p>
        <AlertMessage type="tip">
          When your integration is ready to go live, read the <span className="boldArchText">Go live</span> section for details about the additional steps needed for Apple Pay onboarding.
        </AlertMessage>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-setupyourtestingenvironments">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-setupyourtestingenvironments">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      2. Getting started in your testing environment
    </h2>
    <p>
      Before you develop your Apple Pay on the Web integration, you need to
      complete{" "}
      <a href="/api/rest/" target="_blank" className="linkFormat dx-external-href">
        Get started
      </a>{" "}
      to set up your PayPal account, client ID, and sandbox emails for testing.
    </p>
    <ol>
      <li>
        <b>Download and host</b> the domain association file for your sandbox
        environment.
      </li>
      <li>
        <b>Register your sandbox domain.</b>
      </li>
      <li>
        <b>Create an Apple Pay sandbox account</b> for testing. You don't need
        an Apple developer account to go live.
      </li>
    </ol>
    <AlertMessage type="important">
      You need to verify any domain names that you want to show an Apple Pay button. Apple rejects payments from unverified domains. The Apple Pay payment method won't work if the domain isn't registered.
    </AlertMessage>
    <h2 className="newH2 " style={{ marginTop: "10px" }}>
      Download and host sandbox domain association file
    </h2>
    <ol>
      <li>
        Download the domain association file for your sandbox environment.
      </li>
      <li>
        Host the file on your test environment at <code>/.well-known/apple-developer-merchantid-domain-association.</code>
      </li>
    </ol>
    <Button as="a" href="https://paypalobjects.com/devdoc/apple-pay/sandbox/apple-developer-merchantid-domain-association" role="button">
      Download
    </Button>
        <h2 className="newH2 " style={{ marginTop: "10px" }}>Register your sandbox domains</h2>
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
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-createapplepaysandboxaccount">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-createapplepaysandboxaccount">
      <Col>
    <h2 className="newH2 ">
      Create Apple Pay sandbox account
    </h2>
    <p>
      Create an Apple Pay sandbox account on the Apple Developer website to get
      a test wallet and test cards to test your Apple Pay integration.
    </p>
    <p>
      If you already have an Apple sandbox account, you can use that account and
      move on to the next step.
    </p>
    <ol>
      <li>
        Create an{" "}
        <a
          href="https://developer.apple.com/"
          className="linkFormat dx-external-href"
          target="_blank"
        >
          Apple developer account
        </a>
        .
      </li>{" "}
      <li>
        Create an{" "}
        <a
          href="https://developer.apple.com/apple-pay/sandbox-testing/"
          target="_blank"
          className="linkFormat dx-external-href"
        >
          Apple sandbox account
        </a>
        .
      </li>
      <li>Get test cards from your Apple sandbox account.</li>
    </ol>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-integratepplepaycheckout">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-integratepplepaycheckout">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      3. Integrate Apple Pay checkout
    </h2>
    <p>
      Follow this integration process to add Apple Pay as a checkout option,
      customize the payment experience, and process payments.
    </p>
    <AlertMessage type="important">
      You can find a complete example in the <a target="_blank" className="dx-external-href linkFormat" href="https://github.com/paypal-examples/applepay">GitHub repo</a>.
    </AlertMessage>
    <h3 className="newH2 " style={{ marginTop: "60px" }}>
      Call the Orders API
    </h3>
    <p>
      To accept Apple Pay directly on your website, create API endpoints on your
      server that communicate with the{" "}
      <a href="/docs/api/orders/v2/" className="linkFormat" target="_blank">
        PayPal Orders V2 API
      </a>
      . These endpoints can create an order, authorize payment, and capture payment
      for an order.
    </p>
    <h3 className="newH2 " style={{ marginTop: "60px" }}>
      Server-side example (Node.js)
    </h3>
    <p>
      The following example uses the{" "}
      <a href="/docs/api/orders/v2/" className="linkFormat" target="_blank">
        PayPal Orders V2 API
      </a>{" "}
      to add routes to an Express server for creating orders and capturing
      payments.
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
});`}
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
`} />
      </NewCodeTab>
    </NewCodeTabs>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-setupyourapplepaybutton">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-setupyourapplepaybutton">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      4. Set up your Apple Pay button
    </h2>
    <p>
      You need to Integrate with the Apple Pay JavaScript SDK and PayPal
      JavaScript SDK to add Apple Pay to your site.
    </p>
    <h3 className="newH2 " style={{ marginTop: "60px" }}>
      Integrate PayPal JavaScript SDK
    </h3>
    <p>Use this script to integrate with the PayPal JavaScript SDK:</p>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-html"
        children={`<script src="https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID&currency=USD&buyer-country=US&merchant-id=SUB_MERCHANT_ID&components=applepay"></script> `}
      />
    </NewCodeBlockWrapper>
    <p>
      Include <code>applepay</code> in the <code>components</code> list.
    </p>
    <h3 className="newH2 " style={{ marginTop: "60px" }}>
      Integrate Apple JavaScript SDK
    </h3>
    <p>Use this script to integrate with the Apple JavaScript SDK:</p>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-html"
        children={`<script src="https://applepay.cdn-apple.com/jsapi/v1/apple-pay-sdk.js"></script>`}
      />
    </NewCodeBlockWrapper>
    <p>
      PayPal's Apple Pay component interacts with your JavaScript code in 4
      areas:
    </p>
    <ol>
      <li>
        Checking merchant eligibility for Apple Pay:{" "}
        <code>paypal.Applepay().config()</code>.
      </li>
      <li>Creating an Apple Pay session.</li>
      <li>
        Handling the <code>onvalidatemerchant</code> callback:{" "}
        <code>paypal.Applepay().validateMerchant()</code>.
      </li>
      <li>
        Handling the <code>onpaymentauthorized</code> callback:{" "}
        <code>paypal.Applepay().confirmOrder()</code>.
      </li>
    </ol>
    <p>
      Before you show the Apple Pay button, make sure that you can create an
      Apple Pay instance and that the device can make an Apple Pay payment.
    </p>
    <p>
      Use <code>ApplePaySession.canMakePayments</code> to check if the device
      can make Apple Pay payments.
    </p>
    <AlertMessage type="tip">
      When testing, you need to be logged into the iCloud account for your testing environment. Testing in the sandbox requires you to log into an <a target="_blank" className="dx-external-href linkFormat" href="https://developer.apple.com/apple-pay/sandbox-testing/">iTunes Connect sandbox tester account</a>, which you can create with an <a target="_blank" className="dx-external-href linkFormat" href="https://developer.apple.com/help/account/">Apple Developer account</a>. When you test in a live environment, log into a live iCloud account.
    </AlertMessage>
    <p style={{marginTop: '18px'}}>
      Check for device and merchant eligibility before setting up the Apple Pay
      button.
    </p>
    <p>
      To check eligibility, use the PayPal JavaScript SDK API{" "}
      <code>paypal.Applepay().config()</code>.
    </p>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-html"
        children={`<div id="applepay-container"></div>`}
      />
    </NewCodeBlockWrapper>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-javascript"
        children={`if (!window.ApplePaySession) {
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
      `}
      />
    </NewCodeBlockWrapper>
    <AlertMessage type="tip">
      You can find more details on how to set up the Apple Pay button in{" "}
      <a
        href="https://developer.apple.com/documentation/applepayjs/displaying_apple_pay_buttons"
        target="_blank"
        className="linkFormat dx-external-href"
      >
        Apple's developer documentation
      </a>
      .
    </AlertMessage>
  </Col>
</Row>
</div>
</SectionInView>

<SectionInView id="#link-createapplepaysession">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-createapplepaysession">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      5. Create Apple Pay session
    </h2>
    <p>
      The <code>ApplePaySession</code> object manages the Apple Pay payment
      process on the web. Create a new <code>ApplePaySession</code> each time a
      buyer explicitly requests a payment, such as inside an
      <code>onclick</code> event. If you don't create an
      <code>ApplePaySession</code> each time, you get a "Must create a new
      <code>ApplePaySession</code> from a user gesture handler" JavaScript exception.
      For more information about this error, visit Apple's Creating an Apple Pay
      Session page.
    </p>
    <p>
      For each <code>ApplePaySession</code>, create an
      <a
        href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest"
        target="_blank"
        className="linkFormat dx-external-href"
      >
        <code>ApplePayPaymentRequest</code>
      </a> object, which includes information about payment processing capabilities,
      the payment amount, and shipping information.
    </p>
    <p>
      The response object of the PayPal JavaScript SDK API{" "}
      <code>paypal.Applepay().config()</code> provides the following parameters
      in the <code>ApplePayPaymentRequest</code> object:
    </p>
    <ul>
      <li><code>countryCode</code></li>
      <li><code>merchantCapabilities</code></li>
      <li><code>supportedNetworks</code></li>
    </ul>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-javascript"
        children={`const paymentRequest = {
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
const session = new ApplePaySession(4, paymentRequest);`}
      />
    </NewCodeBlockWrapper>
    <p>
      Include the new <code>ApplePaySession</code> inside a gesture handler,
      such as an <code>onclick</code> event or an <code>addEventListener</code>{" "}
      click handler.
    </p>
    <p>
      Creating an <code>ApplePaySession</code> object throws a JavaScript
      exception if any of the following occurs:
    </p>
    <ul>
      <li>
        Any Apple Pay JavaScript API is called from an insecure page that
        doesn't use <code>https</code>.
      </li>
      <li>An incorrect payment request is passed. Payment requests are incorrect if they contain missing, unknown or invalid properties, or if the total amount is negative.</li>
    </ul>
  <h3 className="newH2 " style={{ marginTop: "60px" }}>onvalidatemerchant callback</h3>
  <p>
    Use <code>paypal.Applepay().validateMerchant()</code> in the{" "}
    <code>onvalidatemerchant</code> callback to create a validated Apple Pay
    session object:
  </p>
  <NewCodeBlockWrapper>
    <NewCodeBlock
      className="language-javascript"
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
};`}
    />
  </NewCodeBlockWrapper>
  <h3 className="newH2 " style={{ marginTop: "60px" }}>onpaymentauthorized callback</h3>
  <p>
    Safari calls the <code>onpaymentauthorized</code> callback with an 
    <code>event</code> object. The <code>event</code> object passes a 
    <code>token</code> which you need to send to PayPal to confirm the order.
  </p>
  <p>
    Capture the order using the{" "}
    <a href="/api/orders/v2" className="linkFormat dx-external-href" target="_blank">
      PayPal Orders V2 API
    </a>
    . Use <code>paypal.Applepay().confirmOrder()</code> to send the <code>
      orderID
    </code>, the Apple Pay token, billing contact details, and confirm the order.
  </p>
  <NewCodeBlockWrapper>
    <NewCodeBlock
      className="language-javascript"
      children={`session.onpaymentauthorized = (event) => {
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
  };`}
    />
  </NewCodeBlockWrapper>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-showthepaymentsheet">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-showthepaymentsheet">
      <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }}>
      6. Show the payment sheet
    </h2>
    <p>
      After you have created the Apple Pay session and added the callbacks, call
      the <code>session.begin</code> method to show the payment sheet. You can only call
      the 
      <code>begin</code> method when a buyer explicitly requests a payment, such
      as inside an <code>onclick</code> event. The <code>begin</code> method throws
      a JavaScript exception if the buyer does not explicitly request the action:
    </p>
    <NewCodeBlockWrapper>
      <NewCodeBlock
        className="language-javascript"
        children={`session.begin();`}
      />
    </NewCodeBlockWrapper>
    <p>
      After the buyer starts a payment in the browser, they use their Apple
      device to authorize the payment.
    </p>
    <h3 className="newH2 " style={{ marginTop: "60px" }}>Customize payment</h3>
    <p>
      Customize the payment experience using the{" "}
      <a
        href="https://developer.apple.com/documentation/apple_pay_on_the_web"
        target="_blank"
        className="linkFormat dx-external-href"
      >
        Apple Pay JavaScript SDK
      </a>
      .
    </p>
    <p>
      Per Apple's development guidelines, your Apple Pay integration needs to follow these rules:
    </p>
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
    <p>The commonly used customizations for Apple Pay are:</p>
    <PayPalTable
      isFullWidth
      style={{ border: "1px solid #929496" }}
      className="payPalTable"
    >
      <thead>
        <tr className="noBackground" style={{ backgroundColor: "transparent" }}>
          <th style={{ background: "transparent" }}>Customization</th>
          <th style={{ background: "transparent" }}>Apple Pay SDK Details</th>
        </tr>
      </thead>
      <tbody className="archTable">
        <tr
          style={{
            borderTop: "1px solid #929496",
            borderTopLeftRadius: "12px",
            borderTopRightRadius: "12px",
            background: "none",
          }}
        >
          <td className="">
            A set of line items that explain the subtotal, tax, discount, and
            additional charges for the payment.
          </td>
          <td>
            <a
              href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/1916120-lineitems"
              target="_blank"
              className="linkFormat dx-external-href"
            >
              <code>lineItems</code>
            </a>
          </td>
        </tr>
        <tr>
          <td className="">
            The billing information fields that the buyer must provide to
            fulfill the order.
          </td>
          <td>
            <a
              href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/2216120-requiredbillingcontactfields"
              target="_blank"
              className="linkFormat dx-external-href"
            >
              <code>requiredBillingContactFields</code>
            </a>
          </td>
        </tr>
        <tr>
          <td className="">
            The shipping information fields that the buyer must provide to
            fulfill the order.
          </td>
          <td>
            <a
              href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/2216121-requiredshippingcontactfields"
              target="_blank"
              className="linkFormat dx-external-href"
            >
              <code>requiredShippingContactFields</code>
            </a>
          </td>
        </tr>
        <tr>
          <td className="">The buyer's billing contact information.</td>
          <td>
            <a
              href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/1916125-billingcontact"
              target="_blank"
              className="linkFormat dx-external-href"
            >
              <code>billingContact</code>
            </a>
          </td>
        </tr>
        <tr>
          <td className="">The buyer's shipping contact information.</td>
          <td>
            <a
              href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentrequest/2216121-requiredshippingcontactfields"
              target="_blank"
              className="linkFormat dx-external-href"
            >
              <code>requiredShippingContactFields</code>
            </a>
            <br/>
            Call the <a
              href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaysession/1778009-onshippingcontactselected"
              className="linkFormat dx-external-href"
              target="_blank"
            >
              <code>onshippingcontactselected</code>{" "}
            </a>
            event handler when the user selects a shipping contact in the
            payment sheet.
          </td>
        </tr>
        <tr>
          <td className="">The shipping method for a payment request.</td>
          <td>
            <a
              href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepayshippingmethod"
              target="_blank"
              className="linkFormat dx-external-href"
            >
              <code>ApplePayShippingMethod</code>
            </a>
            <br/>
            Call the <a
              href="https://developer.apple.com/documentation/apple_pay_on_the_web/applepaysession/1778028-onshippingmethodselected"
              className="linkFormat dx-external-href"
              target="_blank"
            >
              <code>onshippingmethodselected</code>{" "}
            </a> event handler when the user selects a shipping method in the payment
            sheet.
          </td>
        </tr>
      </tbody>
    </PayPalTable>
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
      Test your Apple Pay integration in the PayPal sandbox and production environments to ensure that your app works correctly.
    </p>
    <p>
      Use your personal sandbox login information during checkout to complete a payment using Apple Pay. Then, log into the sandbox site <a href="https://sandbox.paypal.com" target="_blank" className="linkFormat">sandbox.paypal.com</a> to see that the money has moved into your account.
    </p>
    <ol>
      <li>
        Open your test page with the Safari web browser on an iOS device or computer.
      </li>
      <li>Get a test card from your Apple sandbox account.</li>
      <li>
        Add the test card to your Apple Wallet on your iOS device or by using the Safari browser on the web.
      </li>
      <li>
        Tap the <span className="boldText">Apple Pay</span> button to open a pop-up with the Apple Pay payment sheet.
      </li>
      <li>Make a payment using the Apple Pay payment sheet.</li>
      <li>
        If you have an additional confirmation page on your merchant website, continue to confirm the payment.
      </li>
      <li>
        Log in to your merchant account and continue to your confirmation page to confirm that the money you used for payment showed up in the account.
      </li>
    </ol>
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
    <p>Make Apple Pay available to buyers using your website or app.</p>
    <AlertMessage type="important">
      Before going live, complete <a target="_blank" className="dx-external-href linkFormat" href="https://www.paypal.com/bizsignup/add-product?product=payment_methods&capabilities=APPLE_PAY">production onboarding</a> to process Apple Pay payments with your live PayPal account.
    </AlertMessage>
    <h3 className="newH2 " style={{ marginTop: "60px" }}>
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
      Use your personal production login information during checkout to complete
      an Apple Pay transaction. Then log into <b>paypal.com</b> to see the money
      move out of your account.
    </p>
    <h3 className="newH2 " style={{ marginTop: "60px" }}>
      Getting started in your live environment
    </h3>
    <p>
      Verify any domain names in your live environment that will show an Apple Pay button. Apple Pay transactions only work on a domain and site registered to you.
    </p>
    <ul>
      <li>
        <a href="#download-host" className="linkFormat">
          Download and host
        </a>{" "}
        the domain association file for your live environment.
      </li>
      <li>
        <a href="#register-your-live-domain" className="linkFormat">
          Register your live domain
        </a>{" "}
        on your PayPal Developer Dashboard.
      </li>
    </ul>
    <AlertMessage type="important">
      The Apple Pay payment method won't work if the domain and site aren't registered. The merchant that owns the domain is responsible for registering that domain.
    </AlertMessage>
    <p style={{marginTop: '16px'}} id="download-host">
      <b>Prerequisites</b>
    </p>
    <p>
      Enable Apple Pay for your live account:
    </p>
    <ol>
      <li>
        Log into the PayPal Developer Dashboard with your live PayPal account.
      </li>
      <li>
        Select the <span className="boldText">Sandbox/Live</span> toggle so it shows <span className="boldText">Live</span>.
      </li>
      <li>
        Go to <span className="boldText">Apps & Credentials</span>.
      </li>
      <li>
        Scroll down to <span className="boldText">Features</span>.
      </li>
      <li>
        Select the <span className="boldText">Apple Pay</span> checkbox and select the <span className="boldText">Save</span> link.
      </li>
    </ol>
    <p>
      Create an app:
    </p>
    <ol>
      <li>
        Log into the PayPal Developer Dashboard with your live PayPal account.
      </li>
      <li>
        Select the <span className="boldText">Sandbox/Live</span> toggle so it shows <span className="boldText">Live</span>.
      </li>
      <li>
        Go to <span className="boldText">Apps & Credentials</span>.
      </li>
      <li>
        Create an app similar to what you created in the sandbox. You don't need to log into a separate test account.
      </li>
    </ol>
    <p style={{marginTop: '16px'}} id="download-host">
      <b>Download and host live domain association file</b>
    </p>
    <p>
      Host a domain association file for each high-level domain and subdomain that show the Apple Pay button.
    </p>
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
    <Button
    as="a"
    href="https://paypalobjects.com/devdoc/apple-pay/well-known/apple-developer-merchantid-domain-association"
    role="button"
  >
    Download
  </Button>
  </Col>
  </Row>
  <Row style={{ marginTop: "2rem" }}>
  <Col>
  <AlertMessage type="note">
    Remove the file extension from the domain association file when you host it on your server.
  </AlertMessage>
    <p style={{marginTop: '24px'}} id="register-your-live-domain">
      <b>Register your live domain on PayPal</b>
    </p>
    <p>
      Add all high-level domains that show the Apple Pay button.
    </p>
    <ol>
      <li>
        Log into the PayPal Developer Dashboard with your live PayPal account.
      </li>
      <li>
        Select the <span className="boldText">Sandbox/Live</span> toggle so it shows <span className="boldText">Live</span>.
      </li>
      <li>
        Go to <span className="boldText">Apps & Credentials</span>.
      </li>
      <li>
        Select your app.
      </li>
      <li>
        Scroll down to <span className="boldText">Features</span> > <span className="boldText">Accept payments</span> > <span className="boldText">Advanced Credit and Debit Card Payments</span>.
      </li>
      <li>
        Check if Apple Pay is enabled. If Apple Pay isn't enabled, select the <span className="boldText">Apple Pay</span> checkbox and select the <span className="boldText">Save</span> link to enable Apple Pay.
      </li>
      <li>
        Select the <span className="boldText">Manage</span> link in the <span className="boldText">Apple Pay</span> section.
      </li>
      <li>
        Select <span className="boldText">Add Domain</span> and enter your domain name.
      </li>
      <li>
        Select <span className="boldText">Register Domain</span>. If registration fails, check that the domain association file is live and saved to the right place on your live site.
      </li>
    </ol>
    <p>
      After your domain is registered:
    </p>
    <ul>
      <li>
        The domain appears under <span className="boldText">Domains registered with Apple Pay</span>.
      </li>
      <li>
        Buyers can make payments using the <span className="boldText">Apple Pay</span> button on the registered website.
      </li>
    </ul>
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
    <p>How to test Apple Pay payments in a live environment:</p>
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
    <h2 className="newH2">Troubleshoot your integration</h2>
    <p>
      Make sure that there are no browser console warnings or errors. The
      JavaScript SDK configuration attributes have distinct validation checks
      for input formatting and values.
    </p>
    <p>
      If the validation fails, the web browser's developer console shows warning
      messages that say which property is incorrect and what you need to do to
      address the issue. The library generally attempts to revert to the safe
      default values if missing or incorrect inputs exist.
    </p>
      </Col>
    </Row>
  </div>
</SectionInView>

<SectionInView id="#link-nextsteps">
  <div className="outerBeforeRow" id="link-nextsteps">
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
