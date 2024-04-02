# Integrate card payments with JS SDK for direct merchants

<NavigationTabs pageName="integrateAdvancedCheckoutSDKv1" />

<div className="archetypeTip" style={{ marginBottom: "36px", backgroundColor: "#fff" }}>
  <svg
    width="48"
    height="48"
    viewBox="0 0 48 48"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      fillRule="evenodd"
      clipRule="evenodd"
      d="M42.6667 23.9999C42.6667 34.3092 34.3093 42.6666 24 42.6666C13.6907 42.6666 5.33334 34.3092 5.33334 23.9999C5.33334 13.6906 13.6907 5.33325 24 5.33325C34.3093 5.33325 42.6667 13.6906 42.6667 23.9999ZM22.5668 34.5833H25.4268C25.8168 34.5833 26.0248 34.3753 26.0248 33.9853V21.8479C26.0248 21.4579 25.8168 21.2499 25.4268 21.2499H22.5668C22.1768 21.2499 21.9688 21.4579 21.9688 21.8479V33.9853C21.9688 34.3753 22.1768 34.5833 22.5668 34.5833ZM24 17.3333C25.4728 17.3333 26.6667 16.1393 26.6667 14.6666C26.6667 13.1938 25.4728 11.9999 24 11.9999C22.5273 11.9999 21.3333 13.1938 21.3333 14.6666C21.3333 16.1393 22.5273 17.3333 24 17.3333Z"
      fill="#003087"
    />
  </svg>
  <p className="tipText" data-testid="dcai-step5-gl-imp">
    <span className="boldText">Important:</span> This version of the JavaScript SDK integration guide for direct merchants is a legacy integration. Use <a href="/docs/checkout/advanced/integrate/" className="linkFormat">version 2</a> for new integrations.
  </p>
</div>

<SectionInView id="#link-howitworks">
<div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-howitworks">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-howitworks-header">
          How it works
        </h2>
        <p data-testid="dcai-howitworks-p0">
          Advanced Checkout lets you offer the PayPal payment button and custom credit and debit card fields. This guide covers integrating the PayPal button, credit, and debit card payments. You can find more ways to extend your integration in our <a target="_blank" href="/docs/checkout/advanced/customize/" className="linkFormat dx-external-href">customization doc</a>.
        </p>
        <p data-testid="dcai-howitworks-p1">
          Once you integrate advanced Checkout, you can also offer options like Pay Later, Venmo, and alternative payment methods with some additional configuration.
        </p>
        <p data-testid="dcai-howitworks-p2">
          This integration guide follows the code in this <a target="_blank" href="https://github.com/paypal-examples/docs-examples/tree/main/advanced-integration/v1/" className="linkFormat dx-external-href">GitHub sample</a>.
        </p>
      </Col>
      <Col className="imageCol">
        <ImageContainer src="https://www.paypalobjects.com/ppdevdocs/img/advanced-checkout-integration-example.png" fileName="advanced-checkout-integration-example.png" className="productHero aci-example" caption="Advanced Checkout integration example" data-testid="dcai-howitworks-img" />
      </Col>
    </Row>
      <Row style={{ marginTop: "2rem" }}>
        <Col>
          <h2 className="newH2 " style={{ marginTop: "0" }} data-testid="dcai-howitworks-header">
            Which integration to use
          </h2>
          <p data-testid="dcai-howitworks-p0">
            There are 2 versions of card payment integrations for direct merchants using the JavaScript SDK:
          </p>
          <ul>
            <li>
              <span className="boldText">Recommended:</span> Version 2 uses the PayPal-hosted <a href="/sdk/js/reference/#link-cardfields" className="linkFormat"><code>CardFields</code></a> component to accept and save cards without handling card information. PayPal handles all security and compliance issues associated with processing cards. The <code>CardFields</code> component is the recommended integration method and receives ongoing enhancements and improvements.
            </li>
            <li>
              Version 1 is a legacy integration that uses the <a href="/sdk/js/v1/reference/#link-hostedfields" className="linkFormat"><code>HostedFields</code></a> component. This integration is no longer under active development and won’t receive further updates.
            </li>
          </ul>
          <p data-testid="dcai-howitworks-p0">
            Other elements of the JavaScript SDK integration for direct merchants remain the same.
          </p>
        </Col>
    </Row>
<div>
<ExperimentHoc experimentName="codespaces">
<div style={{marginTop: '60px'}}>
<OpenInGitHubCodeSpaces heading="Get up and running in GitHub Codespaces" styleclass="medium-open-in-codespaces" text="GitHub Codespaces are cloud-based developer containers that are ready right away. Use GitHub Codespaces to code and test your PayPal integration." href="https://github.com/codespaces/new/paypal-examples/docs-examples?devcontainer_path=.devcontainer%2Fadvanced-integration-v1%2Fdevcontainer.json"/>
</div>
</ExperimentHoc>
<ExperimentHoc experimentName="codespaces" control>
  <></>
</ExperimentHoc>
</div>
</div>
</SectionInView>

<SectionInView id="#link-integrationvideo">
<div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-integrationvideo">
      <Col>
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-intgvideo-header">
          Integration video
        </h2>
        <p>
          Watch our video tutorial for this integration:
        </p>
      </Col>
    </Row>
    <Row style={{ marginTop: "2rem", paddingBottom: "6rem" }} className="video-container">
      <Col>
        <YoutubeVideo embedUrl="https://www.youtube-nocookie.com/embed/pHbeILqVjOk" title="How to add card fields to your checkout integration with hosted fields" data-testid="dcai-intgvideo-ytvideo" />
      </Col>
    </Row>
</div>
</SectionInView>

<SectionInView id="#link-knowbeforeyoucode">
<div className="outerBeforeRow" id="link-knowbeforeyoucode">
  <div className="innerBeforeRow">
    <div className="archetypeHeader">
        <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-intgvideo-header">
          Know before you code
        </h2>
        <Row className="kbyc-white-section-wrapper">
          <Col md={6} sm={12}>
            <div className="kbyc-white-section">
              <div className="flexRow">
                <div className="flexCol">
                  <DocumentCheckIcon />
                </div>
                <div className="flexCol">
                  <Badge type="warning">Required</Badge>
                </div>
              </div>
              <p className="boldArchText" data-testid="dcai-kbyc-col0-p0">
                You need a developer account to get sandbox credentials
              </p>
              <p>
                <ul>
                  <li>
                    PayPal uses REST API credentials which you can get from the developer dashboard.
                  </li>
                  <li>
                    Client ID: Authenticates your account with PayPal and identifies an app in your sandbox.
                  </li>
                  <li>
                    Client secret: Authorizes an app in your sandbox. Keep this secret safe and don't share it.
                  </li>
                </ul>
              </p>
              <Col md={12} style={{ padding: "0" }}>
                <div style={{ display: "flex", alignItems: "center" }}>
                  <Button as="a" href="/dashboard/" role="button" data-testid="dcai-kbyc-col0-btn">Dashboard</Button>
                  <a href="/api/rest/" className="linkFormat" style={{ marginLeft: "24px" }}>Read the guide</a>
                </div>
              </Col>
            </div>
          </Col>
          <Col md={6} sm={12}>
            <div className="kbyc-white-section">
              <div className="flexRow">
                <div className="flexCol">
                  <DocumentCheckIcon />
                </div>
                <div className="flexCol">
                  <Badge type="warning">Required</Badge>
                </div>
              </div>
              <p className="boldArchText" data-testid="dcai-kbyc-col1-p0">
                You need a combo of PayPal and third-party tools
              </p>
              <p>
                <ul>
                  <li>
                    <a href="/sdk/js/" target="_blank" className="linkFormat dx-external-href">JavaScript SDK:</a> Adds PayPal-supported payment methods.
                  </li>
                  <li>
                    <a href="/docs/api/orders/v2/" target="_blank" className="linkFormat dx-external-href">Orders REST API:</a> Create, update, retrieve, authorize, and capture orders.
                  </li>
                  <li>
                    <a href="https://www.npmjs.com/" target="_blank" className="linkFormat dx-external-href">npm:</a> Registry used to install the necessary third-party libraries.
                  </li>
                </ul>
              </p>
              <RunInPostman text="You can use Postman to explore and test PayPal APIs." zIndex="50000"/>
            </div>
          </Col>
        </Row>
    </div>
  </div>
</div>
</SectionInView>

<SectionInView id="#link-beforeyoubeginyourintegration">
  <div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-beforeyoubeginyourintegration">
    <Col>
    <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-step1-byi">
      1. Before you begin your integration
    </h2>
    <div>
      <div style={{ margin: "2rem 0", fontSize: "28px" }} data-testid="dcai-step1-byi-sub1">
        <span className="sub-step-number">1</span>Check your account setup for advanced card payments
      </div>
      <p data-testid="dcai-step1-byi-sub1-p0">
        This integration requires a sandbox business account with the Advanced Credit and Debit Card Payments capability. Your account should automatically have this capability.
      </p>
      <p data-testid="dcai-step1-byi-sub1-p1">
        To confirm that Advanced Credit and Debit Card Payments are enabled for you, check your sandbox business account as follows:
      </p>
      <p>
        <ol>
          <li>
            Log into the <a target="_blank" className="dx-external-href linkFormat" href="/dashboard/">PayPal Developer Dashboard</a>, toggle <span className="boldText">Sandbox</span>, and go to <span className="boldText">Apps & Credentials</span>.
          </li>
          <li>
            In <span className="boldText">REST API apps</span>, select the name of your app.
          </li>
          <li>
            Go to <span className="boldText">Features</span> > <span className="boldText">Accept payments</span>.
          </li>
          <li>
            Select the <span className="boldText">Advanced Credit and Debit Card Payments</span> checkbox and select <span className="boldText">Save Changes</span>.
          </li>
        </ol>
      </p>
      <div className="archetypeTip" style={{ marginBottom: "36px", backgroundColor: "#fff" }}>
        <svg
          width="48"
          height="48"
          viewBox="0 0 48 48"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fillRule="evenodd"
            clipRule="evenodd"
            d="M42.6667 23.9999C42.6667 34.3092 34.3093 42.6666 24 42.6666C13.6907 42.6666 5.33334 34.3092 5.33334 23.9999C5.33334 13.6906 13.6907 5.33325 24 5.33325C34.3093 5.33325 42.6667 13.6906 42.6667 23.9999ZM22.5668 34.5833H25.4268C25.8168 34.5833 26.0248 34.3753 26.0248 33.9853V21.8479C26.0248 21.4579 25.8168 21.2499 25.4268 21.2499H22.5668C22.1768 21.2499 21.9688 21.4579 21.9688 21.8479V33.9853C21.9688 34.3753 22.1768 34.5833 22.5668 34.5833ZM24 17.3333C25.4728 17.3333 26.6667 16.1393 26.6667 14.6666C26.6667 13.1938 25.4728 11.9999 24 11.9999C22.5273 11.9999 21.3333 13.1938 21.3333 14.6666C21.3333 16.1393 22.5273 17.3333 24 17.3333Z"
            fill="#003087"
          />
        </svg>
        <p className="tipText" data-testid="dcai-step1-byi-sub1-note">
          <span className="boldText">Note:</span> If you created a sandbox business account through <a href="https://www.sandbox.paypal.com/?_ga=1.158343865.248280996.1670866755" target="_blank" className="linkFormat dx-external-href">sandbox.paypal.com</a>, and the Advanced Credit and Debit Card Payments status for the account is disabled, <a target="_blank" href="https://www.sandbox.paypal.com/bizsignup/#/checkAccount" className="linkFormat dx-external-href">complete the sandbox onboarding steps</a>.
        </p>
      </div>
    </div>
    <div>
      <div style={{ margin: "2rem 0", fontSize: "28px" }} data-testid="dcai-step1-sub2-byi">
        <span className="sub-step-number">2</span> Check 3D Secure requirements
      </div>
      <p data-testid="dcai-step1-sub2-byi-p0">
        Add 3D Secure to reduce the chance of fraud and improve the payment experience by authenticating a card holder through their card issuer.
      </p>
      <p data-testid="dcai-step1-sub2-byi-p0">
        Visit our <a href="/docs/checkout/advanced/customize/3d-secure/" className="nextStep-link linkFormat">3D Secure</a> page to see if 3D Secure is required in your region and learn more about implementing 3D Secure in your app.
      </p>
    </div>
    <div>
      <div style={{ margin: "2rem 0", fontSize: "28px" }} data-testid="dcai-step1-sub2-byi">
        <span className="sub-step-number">3</span> Set up npm
      </div>
      <p data-testid="dcai-step1-sub2-byi-p0">
        One of the requirements to run this sample application is to have npm installed. For more info, <a target="_blank" href="https://www.npmjs.com/package/npm" className="linkFormat dx-external-href">visit npm’s documentation</a>.
      </p>
      <div>
        <HeadingText size="title" className="u-margin-bottom--s" data-testid="dcai-step1-sub2-byi-sub2-1">1. Install third-party libraries</HeadingText>
        <p data-testid="dcai-step1-sub2-byi-sub2-1-p0">
          Install the following third-party libraries to set up your integration. Here is a sample command to install them all at the same time:
        </p>
        <NewCodeBlockWrapper>
          <NewCodeBlock
            className="language-javascript"
            children={`
npm install dotenv ejs express node-fetch
            `}
          />
        </NewCodeBlockWrapper>
        <p data-testid="dcai-step1-sub2-byi-sub2-1-p1">
          Select any of the links below to see more detailed installation instructions for each library:
        </p>
        <table>
          <thead>
            <tr>
              <th>Third-party libraries</th>
              <th>Description</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                <a href="https://www.npmjs.com/package/dotenv" target="_blank" className="linkFormat dx-external-href">Dotenv</a>
              </td>
              <td>
                This zero-dependency module separates your configuration and code by loading environment variables from a .env file into process.env.
              </td>
            </tr>
            <tr>
              <td>
                <a href="https://www.npmjs.com/package/ejs" target="_blank" className="linkFormat dx-external-href">ejs</a>
              </td>
              <td>
                These templates help you deliver HTML markup using plain JavaScript.
              </td>
            </tr>
            <tr>
              <td>
                <a href="https://www.npmjs.com/package/express" target="_blank" className="linkFormat dx-external-href">express</a>
              </td>
              <td>
                This lean Node.js web application framework supports web and mobile applications.
              </td>
            </tr>
            <tr>
              <td>
                <a href="https://www.npmjs.com/package/node-fetch" target="_blank" className="linkFormat dx-external-href">node-fetch</a>
              </td>
              <td>
                This function helps you make API requests, similar to window.fetch.
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div>
        <HeadingText size="title" className="u-margin-bottom--s" data-testid="dcai-step1-sub2-byi-sub2-2">2. Verify package.json</HeadingText>
        <p data-testid="dcai-step1-sub2-byi-sub2-2-p0">
          A <code>package.json</code> file has a list of the packages and version numbers needed for your app. You can share your <code>package.json</code> file with other developers so they can use the same settings as you.
        </p>
        <p data-testid="dcai-step1-sub2-byi-sub2-2-p1">
          The following snippet is an example of a <code>package.json</code> file for a PayPal integration. Compare this sample to the <code>package.json</code> in your project:
        </p>
        <NewCodeBlockWrapper>
          <NewCodeBlock
            className="language-json"
            children={`
{
  "name": "@paypalcorp/advanced-integration",
  "version": "1.0.0",
  "description": "",
  "main": "YOUR-SERVER-NAME.js",
  "type": "module",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
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
            `}
          />
        </NewCodeBlockWrapper>
        <p>
          <ul>
            <li>
              Pass the name of your server file using <code>main</code> by replacing the default <code>YOUR-SERVER-NAME.js</code> on lines 5 and 9.
            </li>
            <li>
              Use <code>scripts.test</code> and <code>scripts.start</code> to customize how your app starts up.
            </li>
          </ul>
        </p>
        <p data-testid="dcai-step1-sub2-byi-sub2-2-p2">
          If you're having trouble with your app, try reinstalling your local library and package files using <code>npm install</code>.
        </p>
        <p data-testid="dcai-step1-sub2-byi-sub2-2-p3">
          If you're getting the node error below, you need to include <code>"type": "module"</code> in your <code>package.json</code> file. This line isn't automatically added when <code>package.json</code> is created:
        </p>
        <p data-testid="dcai-step1-sub2-byi-sub2-2-p4">
          <code>Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension (Use `node --trace-warnings ...` to show where the warning was created)</code>
        </p>
        <p data-testid="dcai-step1-sub2-byi-sub2-2-p5">
          See line 6 of the sample <code>package.json</code> file for an example.
        </p>
      </div>
      <div>
        <HeadingText size="title" className="u-margin-bottom--s" data-testid="dcai-step1-sub2-byi-sub2-3">3. Set up .env</HeadingText>
        <p data-testid="dcai-step1-sub2-byi-sub2-3-p0">
          A <code>.env</code> file is a line-delimited text file that sets your local working environment variables. Use this <code>.env</code> file to securely pass the client ID and app secret for your app.
        </p>
        <p data-testid="dcai-step1-sub2-byi-sub2-3-p1">
          This code shows an example <a target="_blank" href="https://github.com/paypal-examples/docs-examples/blob/main/advanced-integration/v1/env.example" className="linkFormat dx-external-href"><code>.env</code></a> file. Rename <code>.env.example</code> to <code>.env</code> and replace the <code>PAYPAL_CLIENT_ID</code> and <code>PAYPAL_CLIENT_SECRET</code> with values from your app:
        </p>
        <div className="archetypeTip" style={{ backgroundColor: "#fff", marginTop: "1rem" }}>
            <svg
              width="48"
              height="48"
              viewBox="0 0 48 48"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fillRule="evenodd"
                clipRule="evenodd"
                d="M42.6667 23.9999C42.6667 34.3092 34.3093 42.6666 24 42.6666C13.6907 42.6666 5.33334 34.3092 5.33334 23.9999C5.33334 13.6906 13.6907 5.33325 24 5.33325C34.3093 5.33325 42.6667 13.6906 42.6667 23.9999ZM22.5668 34.5833H25.4268C25.8168 34.5833 26.0248 34.3753 26.0248 33.9853V21.8479C26.0248 21.4579 25.8168 21.2499 25.4268 21.2499H22.5668C22.1768 21.2499 21.9688 21.4579 21.9688 21.8479V33.9853C21.9688 34.3753 22.1768 34.5833 22.5668 34.5833ZM24 17.3333C25.4728 17.3333 26.6667 16.1393 26.6667 14.6666C26.6667 13.1938 25.4728 11.9999 24 11.9999C22.5273 11.9999 21.3333 13.1938 21.3333 14.6666C21.3333 16.1393 22.5273 17.3333 24 17.3333Z"
                fill="#003087"
              />
            </svg>
            <p className="tipText" style={{ marginLeft: "6px" }} data-testid="dcai-step1-sub2-byi-sub2-3-note">
              <span className="boldText">Note:</span> View your <code>PAYPAL_CLIENT_ID</code> and <code>PAYPAL_CLIENT_SECRET</code> in your <a target="_blank" href="/dashboard/" className="linkFormat dx-external-href">PayPal Developer Dashboard</a> under "Apps & Credentials".
            </p>
          </div>
        <NewCodeBlockWrapper>
          <NewCodeBlock
            className="language-json"
            children={`
PAYPAL_CLIENT_ID="YOUR_CLIENT_ID_GOES_HERE"
PAYPAL_CLIENT_SECRET="YOUR_SECRET_GOES_HERE"
            `}
          />
        </NewCodeBlockWrapper>
      </div>
    </div>
    </Col>
    </Row>
</div>
</SectionInView>

<SectionInView id="#link-integratebackend">
<div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-integratebackend">
    <Col>
      <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-step2-ibe">
        2. Integrate back end
      </h2>
      <div>
      <p>
        This section explains how to set up your back end to integrate advanced Checkout payments.
      </p>
      <p style={{ fontSize: "20px", marginBottom: "10px" }}  data-testid="dcai-step2-ibe-sub1">
        Back-end process
      </p>
      <p>
        <ol style={{ marginTop: "0", lineHeight: "24px" }}>
          <li>
            Your app creates an order on the back-end by making a call to the <a href="/docs/api/orders/v2/#orders_create" className="linkFormat dx-external-href">Create order</a> endpoint of the Orders v2 API.
          </li>
          <li>
            Your app makes a call to the <a target="_blank" href="/docs/api/orders/v2/#orders_capture" className="linkFormat dx-external-href">Capture payment</a> endpoint of the Orders v2 API to move the money when the buyer confirms the order.
          </li>
        </ol>
      </p>
      <p style={{ fontSize: "20px", marginBottom: "10px" }} data-testid="dcai-step2-ibe-sub2">
        Back-end code
      </p>
      <p>
        The following example uses 2 files, <code>/server/server.js</code> and <code>/server/views/checkout.ejs</code>, to show how to set up the back end to integrate with advanced payments.
      </p>
      <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2-a">
        /server/server.js
      </p>
      <p>
        The <code>/server/server.js</code> file provides methods and functions for making the API calls and handling errors, and creates the endpoints that your app uses to:
      </p>
      <p>
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
      </p>
      <p>
        You'll need to save the <code>server.js</code> file in a folder named <code>/server</code>.
      </p>
      <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2-b">
        /server/views/checkout.ejs
      </p>
      <p>
        The <code>/server/views/checkout.ejs</code> file is an Embedded JavaScript (EJS) file that:
      </p>
      <p>
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
      </p>
      <p>
        You'll need to save the <code>checkout.ejs</code> file in a folder named <code>/server/views</code>.
      </p>
      <NewCodeTabs>
        <NewCodeTab label="/server/server.js">
          <NewCodeBlock
            className="language-javascript"
            children={`
import express from "express";
import fetch from "node-fetch";
import "dotenv/config";\n
const { PAYPAL_CLIENT_ID, PAYPAL_CLIENT_SECRET, PORT = 8888 } = process.env;
const base = "https://api-m.sandbox.paypal.com";
const app = express();
app.set("view engine", "ejs");
app.set("views", "./server/views");
app.use(express.static("client"));\n
// parse post params sent in body in json format
app.use(express.json());\n
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
    const response = await fetch(\`\${base}/v1/oauth2/token\`, {
      method: "POST",
      body: "grant_type=client_credentials",
      headers: {
        Authorization: \`Basic \${auth}\`,
      },
    });\n
    const data = await response.json();
    return data.access_token;
  } catch (error) {
    console.error("Failed to generate Access Token:", error);
  }
};\n
/**
 * Generate a client token for rendering the hosted card fields.
 * See https://developer.paypal.com/docs/checkout/advanced/sdk/v1/#link-integratebackend
 */
const generateClientToken = async () => {
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v1/identity/generate-token\`;
  const response = await fetch(url, {
    method: "POST",
    headers: {
      Authorization: \`Bearer \${accessToken}\`,
      "Accept-Language": "en_US",
      "Content-Type": "application/json",
    },
  });\n
  return handleResponse(response);
};\n
/**
 * Create an order to start the transaction.
 * See https://developer.paypal.com/docs/api/orders/v2/#orders_create
 */
const createOrder = async (cart) => {
  // use the cart information passed from the front-end to calculate the purchase unit details
  console.log(
    "shopping cart information passed from the frontend createOrder() callback:",
    cart,
  );\n
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v2/checkout/orders\`;
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
  };\n
  const response = await fetch(url, {
    headers: {
      "Content-Type": "application/json",
      Authorization: \`Bearer \${accessToken}\`,
      // Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
      // https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
      // "PayPal-Mock-Response": '{"mock_application_codes": "MISSING_REQUIRED_PARAMETER"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "PERMISSION_DENIED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
    },
    method: "POST",
    body: JSON.stringify(payload),
  });\n
  return handleResponse(response);
};\n
/**
 * Capture payment for the created order to complete the transaction.
 * See https://developer.paypal.com/docs/api/orders/v2/#orders_capture
 */
const captureOrder = async (orderID) => {
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v2/checkout/orders/\${orderID}/capture\`;\n
  const response = await fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: \`Bearer \${accessToken}\`,
      // Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
      // https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
      // "PayPal-Mock-Response": '{"mock_application_codes": "INSTRUMENT_DECLINED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "TRANSACTION_REFUSED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
    },
  });\n
  return handleResponse(response);
};\n
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
}\n
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
});\n
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
});\n
app.post("/api/orders/:orderID/capture", async (req, res) => {
  try {
    const { orderID } = req.params;
    const { jsonResponse, httpStatusCode } = await captureOrder(orderID);
    res.status(httpStatusCode).json(jsonResponse);
  } catch (error) {
    console.error("Failed to create order:", error);
    res.status(500).json({ error: "Failed to capture order." });
  }
});\n
app.listen(PORT, () => {
  console.log(\`Node server listening at http://localhost:\${PORT}/\`);
});
            `}
          />
        </NewCodeTab>
        <NewCodeTab label="/server/views/checkout.ejs">
          <NewCodeBlock
            className="language-html"
            children={`
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
              `}
            />
        </NewCodeTab>
      </NewCodeTabs>
      <ContentAccordion>
        <AccordionRow heading="/server/server.js">
          <p style={{ marginTop: "1rem" }} data-testid="dcai-step2-ibe-acc1-p0">
            This is a breakdown of the <code>/server/server.js</code> code sample.
          </p>
          <p className="boldText" style={{ marginTop: "1rem" }} data-testid="dcai-step2-ibe-acc1-sub1">
            Declare imports
          </p>
          <br/>
          <p data-testid="dcai-step2-ibe-acc1-sub1-p0">
            This section of code imports the dependencies for your Node.js application:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              className="language-javascript"
              children={`
import express from "express";
import fetch from "node-fetch";
import "dotenv/config";
              `}
            />
          </NewCodeBlockWrapper>
          <p>
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
          </p>
          <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2">
            Set up port and server
          </p>
          <br/>
          <p data-testid="dcai-step2-ibe-acc1-sub2-p0">
            This section of code collects the environment variables, sets up the port to run your server, and sets the base sandbox URL:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="5"
              className="language-javascript"
              children={`
const { PAYPAL_CLIENT_ID, PAYPAL_CLIENT_SECRET, PORT = 8888 } = process.env;
const base = "https://api-m.sandbox.paypal.com";
              `}
            />
          </NewCodeBlockWrapper>
        <p>
          Lines 7-10 start the express Node.js web application framework:
        </p>
        <NewCodeBlockWrapper>
          <NewCodeBlock
            startFrom="7"
            className="language-javascript"
            children={`
const app = express();
app.set("view engine", "ejs");
app.set("views", "./server/views");
app.use(express.static("client"));
              `}
            />
        </NewCodeBlockWrapper>
        <p>
          Line 8 declares that the rendering engine uses Embedded JavaScript templates.
        </p>
        <br/>
        <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2">
          Generate client token
        </p>
        <br/>
        <p data-testid="dcai-step2-ibe-acc1-sub2-p0">
          A client token uniquely identifies your payer. You need a client token for the payer so your app can use the hosted card fields. The following code sample creates a client token for you by making a <code>POST</code> call to the <code>/v1/identity/generate-token</code> endpoint:
        </p>
        <NewCodeBlockWrapper>
          <NewCodeBlock
            startFrom="42"
            className="language-javascript"
            children={`
/**
 * Generate a client token for rendering the hosted card fields.
 * See https://developer.paypal.com/docs/checkout/advanced/sdk/v1/#link-integratebackend
 */
const generateClientToken = async () => {
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v1/identity/generate-token\`;
  const response = await fetch(url, {
    method: "POST",
    headers: {
      Authorization: \`Bearer \${accessToken}\`,
      "Accept-Language": "en_US",
      "Content-Type": "application/json",
    },
  });\n
  return handleResponse(response);
};
            `}
          />
        </NewCodeBlockWrapper>
        <p>
          This code runs your app on <code>localhost</code>, using the port <code>8888</code> that you set up in line 5 of the API call:
        </p>
        <NewCodeBlockWrapper>
          <NewCodeBlock
            startFrom="176"
            className="language-javascript"
            children={`
app.listen(PORT, () => {
  console.log(\`Node server listening at http://localhost:\${PORT}/\`);
});
            `}
          />
        </NewCodeBlockWrapper>
        <br/>
        <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2">
          Render checkout page
        </p>
        <br/>
        <p data-testid="dcai-step2-ibe-acc1-sub2-p0">
          Set up your app's checkout page to load this section of code when it's rendered by your server:
        </p>
        <NewCodeBlockWrapper>
          <NewCodeBlock
            startFrom="140"
            className="language-javascript"
            children={`
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
});\n
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
});\n
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
            `}
          />
        </NewCodeBlockWrapper>
        <p>
          <ul>
            <li>
              Line 143 generates a client token by calling the <code>generateClientToken()</code> function.
            </li>
            <li>
              Lines 144-147 render the checkout page, pass the <code>clientId</code> and <code>clientToken</code> to the page, and inject the value into the script tag.
            </li>
          </ul>
        </p>
        <br/>
        <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2">
          Run createOrder()
        </p>
        <br/>
        <p>
          This section of code defines a <code>createOrder()</code> callback function for the <a href="/docs/api/orders/v2/#orders_create">Create orders</a> endpoint of the Orders v2 API. Call the function when the payment is submitted, for example, when the payer selects the PayPal button, or submits a card payment. See the <code>/client/app.js</code> section for more information.
        </p>
        <p>
          This <code>createOrder()</code> callback returns a promise that contains the <code>orderID</code>. You can customize this callback for many use cases, such as a  physical inventory for a cart, or a digital good with a fixed amount.
        </p>
        <br/>
        <div className="archetypeTip" style={{ marginBottom: "36px", backgroundColor: "#fff" }}>
          <svg
            width="48"
            height="48"
            viewBox="0 0 48 48"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fillRule="evenodd"
              clipRule="evenodd"
              d="M42.6667 23.9999C42.6667 34.3092 34.3093 42.6666 24 42.6666C13.6907 42.6666 5.33334 34.3092 5.33334 23.9999C5.33334 13.6906 13.6907 5.33325 24 5.33325C34.3093 5.33325 42.6667 13.6906 42.6667 23.9999ZM22.5668 34.5833H25.4268C25.8168 34.5833 26.0248 34.3753 26.0248 33.9853V21.8479C26.0248 21.4579 25.8168 21.2499 25.4268 21.2499H22.5668C22.1768 21.2499 21.9688 21.4579 21.9688 21.8479V33.9853C21.9688 34.3753 22.1768 34.5833 22.5668 34.5833ZM24 17.3333C25.4728 17.3333 26.6667 16.1393 26.6667 14.6666C26.6667 13.1938 25.4728 11.9999 24 11.9999C22.5273 11.9999 21.3333 13.1938 21.3333 14.6666C21.3333 16.1393 22.5273 17.3333 24 17.3333Z"
              fill="#003087"
            />
          </svg>
          <p className="tipText" data-testid="dcai-step5-gl-imp">
            <span className="boldText">Important:</span> To keep your integration secure, don't pass dollar amounts in your finished integration. Define your <code>purchase_units</code> payload on the server side and pass the <code>cart</code> array from the front-end to the server.
          </p>
        </div>
        <NewCodeBlockWrapper>
          <NewCodeBlock
            startFrom="61"
            className="language-javascript"
            children={`
/**
 * Create an order to start the transaction.
 * See https://developer.paypal.com/docs/api/orders/v2/#orders_create
 */
const createOrder = async (cart) => {
  // use the cart information passed from the front-end to calculate the purchase unit details
  console.log(
    "shopping cart information passed from the frontend createOrder() callback:",
    cart,
  );\n
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v2/checkout/orders\`;
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
  };\n
  const response = await fetch(url, {
    headers: {
      "Content-Type": "application/json",
      Authorization: \`Bearer \${accessToken}\`,
      // Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
      // https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
      // "PayPal-Mock-Response": '{"mock_application_codes": "MISSING_REQUIRED_PARAMETER"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "PERMISSION_DENIED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
    },
    method: "POST",
    body: JSON.stringify(payload),
  });\n
  return handleResponse(response);
};
              `}
            />
          </NewCodeBlockWrapper>
          <p>
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
                Lines 86-98 create an order by sending a <code>POST</code> request to the <a href="/docs/api/orders/v2/#orders_create">Create orders</a> endpoint of the Orders v2 API, using <code>accessToken</code>, <code>url</code>, and the <code>payload</code> from lines 74-84.
              </li>
              <li>
                Line 97 converts the <code>payload</code> information into JSON format and passes it into the <code>body</code> section of the request.
              </li>
            </ul>
          </p>
          <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2">
            Negative testing for createOrder()
          </p>
          <br/>
          <p>
            This section of the <code>createOrder()</code> function provides 3 negative testing opportunities behind content tags:
          </p>
          <p>
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
          </p>
          <p>
            Remove the <code>//</code> from the beginning of a line to simulate that error. the <code>createOrder()</code> call will pass that line as a <a href="/tools/sandbox/negative-testing/request-headers/"><code>PayPal-Mock-Response</code></a> header in the <code>POST</code> request to the Orders v2 API:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="90"
              className="language-javascript"
              children={`
// Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
// https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
// "PayPal-Mock-Response": '{"mock_application_codes": "MISSING_REQUIRED_PARAMETER"}'
// "PayPal-Mock-Response": '{"mock_application_codes": "PERMISSION_DENIED"}'
// "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
              `}
            />
          </NewCodeBlockWrapper>
          <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2">
            Run captureOrder()
          </p>
          <br/>
          <p>
            This section of code defines the <code>captureOrder()</code> function. Call the function to capture the order and move money from the payer's payment method to the seller:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="103"
              className="language-javascript"
              children={`
/**
 * Capture payment for the created order to complete the transaction.
 * See https://developer.paypal.com/docs/api/orders/v2/#orders_capture
 */
const captureOrder = async (orderID) => {
  const accessToken = await generateAccessToken();
  const url = \`\${base}/v2/checkout/orders/\${orderID}/capture\`;\n
  const response = await fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: \`Bearer \${accessToken}\`,
      // Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
      // https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
      // "PayPal-Mock-Response": '{"mock_application_codes": "INSTRUMENT_DECLINED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "TRANSACTION_REFUSED"}'
      // "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
    },
  });\n
  return handleResponse(response);
};
              `}
            />
          </NewCodeBlockWrapper>
          <p>
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
                Lines 111-122 capture an order by sending a <code>POST</code> request to the <a href="/docs/api/orders/v2/#orders_capture">Capture payment</a> endpoint of the Orders v2 API, using <code>accessToken</code> and <code>url</code>.
              </li>
            </ul>
          </p>
          <p>
            See <code>/client/app.js</code> in the next section for more details on capturing payments from the front-end.
          </p>
          <br/>
          <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2">
            Negative testing for captureOrder()
          </p>
          <br/>
          <p>
            This section of the <code>captureOrder()</code> function provides 3 negative testing opportunities behind content tags:
          </p>
          <p>
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
          </p>
          <p>
            Remove the <code>//</code> from the beginning of a line to simulate that error. The <code>captureOrder()</code> call will pass that line as a <a href="/docs/api/orders/v2/#orders_capture"><code>PayPal-Mock-Response</code></a> header in the <code>POST</code> request to the <a href="/docs/api/orders/v2/#orders_capture">Capture payment</a> endpoint of the Orders v2 API:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="116"
              className="language-javascript"
              children={`
// Uncomment one of these to force an error for negative testing (in sandbox mode only). Documentation:
// https://developer.paypal.com/tools/sandbox/negative-testing/request-headers/
// "PayPal-Mock-Response": '{"mock_application_codes": "INSTRUMENT_DECLINED"}'
// "PayPal-Mock-Response": '{"mock_application_codes": "TRANSACTION_REFUSED"}'
// "PayPal-Mock-Response": '{"mock_application_codes": "INTERNAL_SERVER_ERROR"}'
              `}
            />
          </NewCodeBlockWrapper>
          <br/>
          <p style={{ fontSize: "20px", marginBottom: "10px" }}  data-testid="dcai-step2-ibe-sub1">
            Test server
          </p>
          <p>
            Run <code>npm start</code> to confirm your setup is correct.
          </p>
          <p>
            This command starts the server on <code>localhost:8888</code>. You can specify a port number by modifying line 4 in the sample <code>/server/server.js</code> file.
          </p>
        </AccordionRow>
      </ContentAccordion>
      <br/>
      <ContentAccordion>
        <AccordionRow heading="/server/views/checkout.ejs">
          <p>
            This breakdown focuses on key lines from the <code>/server/views/checkout.ejs</code> code sample.
          </p>
          <br/>
          <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2-a">
            Import style sheet
          </p>
          <br/>
          <p>
            This section calls the JavaScript SDK that defines the PayPal buttons:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="7"
              className="language-javascript"
              children={`
<link
  rel="stylesheet"
  type="text/css"
  href="https://www.paypalobjects.com/webstatic/en_US/developer/docs/css/cardfields.css"
>
              `}
            />
          </NewCodeBlockWrapper>
          <p>
            <ul>
              <li>
                Lines 7-11 declare a sample CSS file for demonstration purposes. Replace these with styles that align with your brand using the <a href="/docs/checkout/advanced/customize/card-field-style/">CSS properties supported by this integration</a>.
              </li>
              <li>
                Optional: The <a href="/sdk/js/configuration/">JavaScript SDK</a> has configurations that you can override, such as <code>currency</code> and <code>intent</code>.
              </li>
            </ul>
          </p>
          <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2-a">
            Add PayPal button
          </p>
          <br/>
          <p>
            Include the PayPal Checkout button before you request the credit card fields, or on the same page that you request this information. For more information, see Section 8, <strong>Required Use of PayPal Checkout, PayPal Credit</strong>, in the <a href="https://www.paypal.com/us/legalhub/pocpsa-full?_ga=1.169690530.248280996.1670866755#pocpsa-full-8">PayPal Online Card Payments Services Agreement</a>.
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="18"
              className="language-javascript"
              children={`
<div id="paypal-button-container" class="paypal-button-container"></div>
              `}
            />
          </NewCodeBlockWrapper>
          <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2-a">
            Create your card form
          </p>
          <br/>
          <p>
            This section of code shows how to create the form fields and <strong>Submit</strong> button you need to take card payments:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="19"
              className="language-javascript"
              children={`
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
              `}
            />
          </NewCodeBlockWrapper>
          <p>
            <ul>
              <li>
                Lines 19-99 declare a <code>card-form</code> object with fields for <code>card-number</code>, <code>expiration-date</code>, <code>cvv</code>, <code>card-holder-name</code>, and billing address information. See the <a href="/docs/api/orders/v2/">Orders v2 API</a> for details about billing address fields and other parameters. For example, use the <a href="/api/rest/reference/country-codes/">2-character country code</a> to test the billing address.
              </li>
              <li>
                Line 100 declares a <code>result-message</code> object that displays the output of the <code>resultMessage</code> function from lines 107-110 of the <code>/client/app.js</code> file.
              </li>
              <li>
                The fields in this example match up with fields from lines 145-169 of the <strong>Capture eligible payment</strong> code sample.
              </li>
            </ul>
          </p>
          <p className="boldText" data-testid="dcai-step2-ibe-acc1-sub2-a">
            Import app.js
          </p>
          <br/>
          <p>
            This code sample renders the hosted card fields for an eligible payment by importing the <code>/client/app.js</code> file that you created:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="102"
              className="language-javascript"
              children={`
<script src="app.js"></script>
              `}
            />
          </NewCodeBlockWrapper>
        </AccordionRow>
      </ContentAccordion>
      </div>
      </Col>
    </Row>
</div>
</SectionInView>

<SectionInView id="#link-integratefrontend">
<div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-integratefrontend">
    <Col>
      <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-step3-ife">
        3. Integrate front end
      </h2>
      <div>
      <p data-testid="dcai-step3-ife-p0">
        This section explains how to set up your front end to integrate advanced Checkout payments.
      </p>
      <p style={{ fontSize: "20px", marginBottom: "10px" }} data-testid="dcai-step3-ife-sub1">
        Front-end process
      </p>
      <p>
        <ol style={{ marginTop: "0", lineHeight: "24px" }}>
          <li>
            Your app displays the PayPal Checkout button and the card checkout form.
          </li>
          <li>
            Your app calls server endpoints to create the order and capture payment. The specific method depends on whether the buyer uses the PayPal button or checkout form.
          </li>
        </ol>
      </p>
      <p style={{ fontSize: "20px", marginBottom: "10px" }} data-testid="dcai-step3-ife-sub2">
        Front-end code
      </p>
      <p data-testid="dcai-step3-ife-sub2-p0">
        The <code>/client/app.js</code> file handles the client-side logic and defines how the PayPal front-end components connect with the back-end. Use this file to set up the PayPal checkout using the PayPal JavaScript SDK, and handle the payer's interactions with the PayPal checkout button.
      </p>
      <p>
        You'll need to save the <code>app.js</code> file in a folder named <code>/client</code>:
      </p>
      <NewCodeTabs>
        <NewCodeTab label="/client/app.js">
          <NewCodeBlock
            className="language-javascript"
            children={`
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
    });\n
    const orderData = await response.json();\n
    if (orderData.id) {
      return orderData.id;
    } else {
      const errorDetail = orderData?.details?.[0];
      const errorMessage = errorDetail
        ? \`\${errorDetail.issue} \${errorDetail.description} (\${orderData.debug_id})\`
        : JSON.stringify(orderData);\n
      throw new Error(errorMessage);
    }
  } catch (error) {
    console.error(error);
    resultMessage(\`Could not initiate PayPal Checkout...<br><br>\${error}\`);
  }
}\n
async function onApproveCallback(data, actions) {
  try {
    const response = await fetch(\`/api/orders/\${data.orderID}/capture\`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
    });\n
    const orderData = await response.json();
    // Three cases to handle:
    //   (1) Recoverable INSTRUMENT_DECLINED -> call actions.restart()
    //   (2) Other non-recoverable errors -> Show a failure message
    //   (3) Successful transaction -> Show confirmation or thank you message\n
    const transaction =
      orderData?.purchase_units?.[0]?.payments?.captures?.[0] ||
      orderData?.purchase_units?.[0]?.payments?.authorizations?.[0];
    const errorDetail = orderData?.details?.[0];\n
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
        errorMessage = \`Transaction \${transaction.status}: \${transaction.id}\`;
      } else if (errorDetail) {
        errorMessage = \`\${errorDetail.description} (\${orderData.debug_id})\`;
      } else {
        errorMessage = JSON.stringify(orderData);
      }\n
      throw new Error(errorMessage);
    } else {
      // (3) Successful transaction -> Show confirmation or thank you message
      // Or go to another URL:  actions.redirect('thank_you.html');
      resultMessage(
        \`Transaction \${transaction.status}: \${transaction.id}<br><br>See console for all available details\`,
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
      \`Sorry, your transaction could not be processed...<br><br>\${error}\`,
    );
  }
}\n
window.paypal
  .Buttons({
    createOrder: createOrderCallback,
    onApprove: onApproveCallback,
  })
  .render("#paypal-button-container");\n
// Example function to show a result to the user. Your site's UI library can be used instead.
function resultMessage(message) {
  const container = document.querySelector("#result-message");
  container.innerHTML = message;
}\n
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
            \`Sorry, your transaction could not be processed...<br><br>\${JSON.stringify(
              orderData,
            )}\`,
          );
        });
    });
  });
} else {
  // Hides card fields if the merchant isn't eligible
  document.querySelector("#card-form").style = "display: none";
}
            `}
          />
        </NewCodeTab>
      </NewCodeTabs>
      <p style={{ fontSize: "20px", marginBottom: "10px" }} data-testid="dcai-step3-ife-sub3">
        Understand the front-end code
      </p>
      <p>
        This section explains critical parts of the front-end code sample.
      </p>
      <ContentAccordion>
        <AccordionRow heading="/client/app.js">
          <p>
            This breakdown focuses on key lines from the <code>/client/app.js</code> code sample.
          </p>
          <p className="boldText" style={{ marginTop: "1rem" }} data-testid="dcai-step2-ibe-acc1-sub1">
            Create order
          </p>
          <br/>
          <p>
            This code sample defines the <code>createOrder()</code> function:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              className="language-javascript"
              children={`
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
    });\n
    const orderData = await response.json();\n
    if (orderData.id) {
      return orderData.id;
    } else {
      const errorDetail = orderData?.details?.[0];
      const errorMessage = errorDetail
        ? \`\${errorDetail.issue} \${errorDetail.description} (\${orderData.debug_id})\`
        : JSON.stringify(orderData);\n
      throw new Error(errorMessage);
    }
  } catch (error) {
    console.error(error);
    resultMessage(\`Could not initiate PayPal Checkout...<br><br>\${error}\`);
  }
}
              `}
            />
          </NewCodeBlockWrapper>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="38"
              className="language-javascript"
              children={`
async function onApproveCallback(data, actions) {
  try {
    const response = await fetch(\`/api/orders/\${data.orderID}/capture\`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
    });\n
    const orderData = await response.json();
    // Three cases to handle:
    //   (1) Recoverable INSTRUMENT_DECLINED -> call actions.restart()
    //   (2) Other non-recoverable errors -> Show a failure message
    //   (3) Successful transaction -> Show confirmation or thank you message\n
    const transaction =
      orderData?.purchase_units?.[0]?.payments?.captures?.[0] ||
      orderData?.purchase_units?.[0]?.payments?.authorizations?.[0];
    const errorDetail = orderData?.details?.[0];\n
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
        errorMessage = \`Transaction \${transaction.status}: \${transaction.id}\`;
      } else if (errorDetail) {
        errorMessage = \`\${errorDetail.description} (\${orderData.debug_id})\`;
      } else {
        errorMessage = JSON.stringify(orderData);
      }\n
      throw new Error(errorMessage);
    } else {
      // (3) Successful transaction -> Show confirmation or thank you message
      // Or go to another URL:  actions.redirect('thank_you.html');
      resultMessage(
        \`Transaction \${transaction.status}: \${transaction.id}<br><br>See console for all available details\`,
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
      \`Sorry, your transaction could not be processed...<br><br>\${error}\`,
    );
  }
}
              `}
            />
          </NewCodeBlockWrapper>
          <p>
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
          </p>
          <p className="boldText" style={{ marginTop: "1rem" }} data-testid="dcai-step2-ibe-acc1-sub1">
            PayPal Button JavaScript
          </p>
          <br/>
          <p>
            This section calls the JavaScript SDK that defines the PayPal buttons:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="99"
              className="language-javascript"
              children={`
window.paypal
  .Buttons({
    createOrder: createOrderCallback,
    onApprove: onApproveCallback,
  })
  .render("#paypal-button-container");
              `}
            />
          </NewCodeBlockWrapper>
          <p className="boldText" style={{ marginTop: "1rem" }} data-testid="dcai-step2-ibe-acc1-sub1">
            Send results to user
          </p>
          <br/>
          <p>
            This section declares a <code>resultMessage</code> function that shows a message to the user by passing data to the <code>result-message</code> HTML element container in line 100 of the <code>/server/views/checkout.ejs</code>:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="106"
              className="language-javascript"
              children={`
// Example function to show a result to the user. Your site's UI library can be used instead.
function resultMessage(message) {
  const container = document.querySelector("#result-message");
  container.innerHTML = message;
              `}
            />
          </NewCodeBlockWrapper>
          <p>
            Lines 108-109 direct the message to the HTML element container.
          </p>
          <p className="boldText" style={{ marginTop: "1rem" }} data-testid="dcai-step2-ibe-acc1-sub1">
            Check for HostedFields eligibility
          </p>
          <br/>
          <p>
            Hosted card fields use the JavaScript SDK to help non-PCI-compliant sellers save a payer's card data and create a token for future payments. During an eligible payment, the hosted fields show up in the payment experience and prompt the payer for consent to save their card data. For more information about hosted fields, see <a href="/sdk/js/reference/#hosted-fields">Hosted fields</a>.
          </p>
          <div className="archetypeTip" style={{ backgroundColor: "#fff", marginTop: "1rem" }}>
            <svg
              width="48"
              height="48"
              viewBox="0 0 48 48"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fillRule="evenodd"
                clipRule="evenodd"
                d="M42.6667 23.9999C42.6667 34.3092 34.3093 42.6666 24 42.6666C13.6907 42.6666 5.33334 34.3092 5.33334 23.9999C5.33334 13.6906 13.6907 5.33325 24 5.33325C34.3093 5.33325 42.6667 13.6906 42.6667 23.9999ZM22.5668 34.5833H25.4268C25.8168 34.5833 26.0248 34.3753 26.0248 33.9853V21.8479C26.0248 21.4579 25.8168 21.2499 25.4268 21.2499H22.5668C22.1768 21.2499 21.9688 21.4579 21.9688 21.8479V33.9853C21.9688 34.3753 22.1768 34.5833 22.5668 34.5833ZM24 17.3333C25.4728 17.3333 26.6667 16.1393 26.6667 14.6666C26.6667 13.1938 25.4728 11.9999 24 11.9999C22.5273 11.9999 21.3333 13.1938 21.3333 14.6666C21.3333 16.1393 22.5273 17.3333 24 17.3333Z"
                fill="#003087"
              />
            </svg>
            <p className="tipText" style={{ marginLeft: "6px" }} data-testid="dcai-step1-sub2-byi-sub2-3-note">
              <span className="boldText">Note:</span> You need to complete the account setup in sandbox to be eligible for testing hosted fields.
            </p>
          </div>
          <p>
          <br/>
            This code sample checks to see if a payment is eligible for hosted card fields. If not, the hosted card fields won’t show up during the payment flow:
          </p>
          <NewCodeBlockWrapper>
                  <NewCodeBlock
                    startFrom="112"
                    className="language-javascript"
                    children={`
// If this returns false or the card fields aren't visible, see Step #1.
if (window.paypal.HostedFields.isEligible()) {
  // Renders card fields
  window.paypal.HostedFields.render(
  {...}
  } else {
  // Hides card fields if the merchant isn't eligible
  document.querySelector("#card-form").style = "display: none";
  }
              `}
            />
          </NewCodeBlockWrapper>
          <p>
            You can modify this code to show a custom message for eligible or ineligible payments.
          </p>
          <p className="boldText" style={{ marginTop: "1rem" }} data-testid="dcai-step2-ibe-acc1-sub1">
            Render hosted card fields and create order
          </p>
          <br/>
          <p>
            This code sample renders the hosted card fields for an eligible payment:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="114"
              className="language-javascript"
              children={`
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
              `}
            />
          </NewCodeBlockWrapper>
          <p>
            <ul>
              <li>
                Line 117 creates the order by calling the <code>createOrderCallback</code> function.
              </li>
              <li>
                Lines 118-125 define styles for the hosted card fields. You can change these styles as needed for your implementation.
              </li>
              <li>
                Lines 126-139 define the <code>selector</code> and <code>placeholder</code> values for the input fields. You can edit this section as needed for your implementation, such as adding more fields. For more information about optional configurations, see <a href="/sdk/js/reference/#link-options">Options in the JavaScript SDK reference</a>.
              </li>
            </ul>
          </p>
          <p className="boldText" style={{ marginTop: "1rem" }} data-testid="dcai-step2-ibe-acc1-sub1">
            Capture eligible payment
          </p>
          <br/>
          <p>
            This code sample captures the payment when it is eligible for hosted card fields. Add this code to the PayPal button in <code>/client/app.js</code>, right after rendering the card fields:
          </p>
          <NewCodeBlockWrapper>
            <NewCodeBlock
              startFrom="140"
              className="language-javascript"
              children={`
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
            \`Sorry, your transaction could not be processed...<br><br>\${JSON.stringify(
              orderData,
            )}\`,
          );
        });
    });
  });
              `}
            />
          </NewCodeBlockWrapper>
          <p>
            <ul>
              <li>
                Line 140 sets up an event listener for when the payer submits an eligible card payment.
              </li>
              <li>
                Lines 143-170 pass the hosted card field values, such as the cardholder's name and address, to the <code>POST</code> call in lines 128-131. Anything you pass into the submit is sent to the iframe that communicates with the Orders API. The iframe retrieves the data and sends it along to the <code>POST</code> call. See the <a href="/docs/api/orders/v2/">Orders v2 API</a> for details about billing address fields and other parameters. For example, use the <a href="/api/rest/reference/country-codes/">2-character country code</a> to test the billing address.
              </li>
              <li>
                Lines 171-173 call the <code>onApproveCallback</code> function from lines 38-97, which sends a <code>POST</code> call to <code>/v2/checkout/orders/&#123;id&#125;/capture</code> that captures the order using the <code>orderId</code> in the <code>data</code> object in <code>/server/server.js</code>.
              </li>
              <li>
                Lines 174-178 pass an error message if the payment isn't successful.
              </li>
            </ul>
          </p>
        </AccordionRow>
      </ContentAccordion>
      <br/>
      <p style={{ fontSize: "20px", marginBottom: "10px" }} data-testid="dcai-step3-ife-sub3">
        Run front end integration
      </p>
      <p>
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
      </p>
      </div>
      </Col>
    </Row>
</div>
</SectionInView>

<SectionInView id="#link-testintegration">
<div className="archetypeHeader">
    <Row style={{ marginTop: "2rem" }} id="link-testintegration">
    <Col>
    <h2 className="newH2 "  style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-step4-ti">
      4. Test integration
    </h2>
    <div>
    <p data-testid="dcai-step4-ti-p0">
      Before going live, test your integration in the <a target="_blank" href="/tools/sandbox/" className="linkFormat dx-external-href">sandbox environment</a>.
    </p>
    <p data-testid="dcai-step4-ti-p1">
      Learn more about the following resources on the <a target="_blank" href="/tools/sandbox/card-testing/" className="linkFormat dx-external-href">Card Testing</a> page:
    </p>
    <p>
      <ul>
        <li>
          Use <a target="_blank" href="/tools/sandbox/card-testing/#link-testcardnumbers" className="linkFormat dx-external-href">test card numbers</a> to simulate successful payments for advanced Checkout integrations.
        </li>
        <li>
          Use <a target="_blank" href="/tools/sandbox/card-testing/#link-rejectiontriggers" className="linkFormat dx-external-href">rejection triggers</a> to simulate card error scenarios.
        </li>
        <li>
          Test <a target="_blank" href="/tools/sandbox/card-testing/#link-simulate3dsecurecardpayments" className="linkFormat dx-external-href">3D Secure authentication</a> scenarios.
        </li>
        <li>
          Test your integration by following <a target="_blank" href="/tools/sandbox/card-testing/#link-testintegration" className="linkFormat dx-external-href">these recommended use cases</a>. See the <a href="/docs/api/orders/v2/" className="linkFormat dx-external-href">Orders v2 API</a> for details about billing address fields and other parameters. For example, use the <a href="/api/rest/reference/country-codes/" className="linkFormat dx-external-href">2-character country code</a> to test the billing address.
        </li>
      </ul>
    </p>
    <div className="archetypeTip">
      <svg
        width="48"
        height="48"
        viewBox="0 0 48 48"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          fillRule="evenodd"
          clipRule="evenodd"
          d="M42.6667 23.9999C42.6667 34.3092 34.3093 42.6666 24 42.6666C13.6907 42.6666 5.33334 34.3092 5.33334 23.9999C5.33334 13.6906 13.6907 5.33325 24 5.33325C34.3093 5.33325 42.6667 13.6906 42.6667 23.9999ZM22.5668 34.5833H25.4268C25.8168 34.5833 26.0248 34.3753 26.0248 33.9853V21.8479C26.0248 21.4579 25.8168 21.2499 25.4268 21.2499H22.5668C22.1768 21.2499 21.9688 21.4579 21.9688 21.8479V33.9853C21.9688 34.3753 22.1768 34.5833 22.5668 34.5833ZM24 17.3333C25.4728 17.3333 26.6667 16.1393 26.6667 14.6666C26.6667 13.1938 25.4728 11.9999 24 11.9999C22.5273 11.9999 21.3333 13.1938 21.3333 14.6666C21.3333 16.1393 22.5273 17.3333 24 17.3333Z"
          fill="#003087"
        />
      </svg>
      <p className="tipText">
        <span className="boldText">Note:</span> Use the <a target="_blank" href="/tools/sandbox/card-testing/#link-creditcardgenerator" className="linkFormat dx-external-href">credit card generator</a> to generate additional test credit cards for sandbox testing.
      </p>
    </div>
    </div>
    </Col>
    </Row>
</div>
</SectionInView>

<SectionInView id="#link-golive">
<div className="archetypeHeader">
  <Row style={{ marginTop: "2rem" }} id="link-golive">
  <Col>
    <h2 className="newH2 "  style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-step5-gl">5. Go Live</h2>
    <p>
      If you have fulfilled the requirements for accepting Advanced Credit and Debit Card Payments for your <a target="_blank" className="dx-external-href linkFormat" href="https://www.paypal.com/myaccount/bundle/business/upgrade">business account</a>, review the <a href="/api/rest/production/" className="linkFormat"><span className="boldText">Move your app to production</span></a> page to learn how to test and go live.
    </p>
    <p>
      If this is your first time testing in a live environment, follow these steps:
    </p>
    <p>
      <ol>
        <li>
          Log into the <a target="_blank" href="/dashboard/" className="dx-external-href linkFormat">PayPal Developer Dashboard</a> with your PayPal business account.
        </li>
        <li>
          Complete <a target="_blank" href="https://www.paypal.com/bizsignup/entry?_ga=1.171321763.248280996.1670866755" className="dx-external-href linkFormat">production oboarding</a> so you can process card payments with your live PayPal business account.
        </li>
        <li>
          Request <a target="_blank" href="https://www.paypal.com/signin/client?flow=provisionUser&country.x=US&locale.x=en_US&_ga=1.95899167.248280996.1670866755" className="dx-external-href linkFormat">Advanced Credit and Debit Card Payments</a> for your business account.
        </li>
      </ol>
    </p>
    <div className="archetypeTip" style={{ marginBottom: "36px", backgroundColor: "#fff" }}>
      <svg
        width="48"
        height="48"
        viewBox="0 0 48 48"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          fillRule="evenodd"
          clipRule="evenodd"
          d="M42.6667 23.9999C42.6667 34.3092 34.3093 42.6666 24 42.6666C13.6907 42.6666 5.33334 34.3092 5.33334 23.9999C5.33334 13.6906 13.6907 5.33325 24 5.33325C34.3093 5.33325 42.6667 13.6906 42.6667 23.9999ZM22.5668 34.5833H25.4268C25.8168 34.5833 26.0248 34.3753 26.0248 33.9853V21.8479C26.0248 21.4579 25.8168 21.2499 25.4268 21.2499H22.5668C22.1768 21.2499 21.9688 21.4579 21.9688 21.8479V33.9853C21.9688 34.3753 22.1768 34.5833 22.5668 34.5833ZM24 17.3333C25.4728 17.3333 26.6667 16.1393 26.6667 14.6666C26.6667 13.1938 25.4728 11.9999 24 11.9999C22.5273 11.9999 21.3333 13.1938 21.3333 14.6666C21.3333 16.1393 22.5273 17.3333 24 17.3333Z"
          fill="#003087"
        />
      </svg>
      <p className="tipText" data-testid="dcai-step5-gl-imp">
        <span className="boldText">Important:</span> The code for the integration checks eligibility requirements, so the payment card fields only display when the production request is successful.
      </p>
    </div>
    </Col>
  </Row>
</div>
</SectionInView>

<SectionInView id="#link-nextsteps">
<div className="outerBeforeRow" style={{ marginTop: "80px" }}>
  <div className="archetypeHeader" style={{ padding: "60px 0" }}>
    <Row>
      <Col>
      <h2 className="newH2 " style={{ marginTop: "60px", display: "flex" }} data-testid="dcai-nsc">
        Next steps & customizations
      </h2>
      <p data-testid="dcai-nsc-p0">
        Add security to your checkout integration, or create customizations for your audience.
      </p>
      </Col>
    </Row>
    <p style={{ fontSize: "20px", marginBottom: "10px" }} data-testid="dcai-nsc-sub1">
      Add more payment methods
    </p>
    <Row>
      <Col class="dcai-nextsteps">
        <div className="whiteBox">
          <div className="flexRow">
            <div className="flexCol"><DocumentIcon /></div>
            <div className="flexCol"><Badge type="neutral">Optional</Badge></div>
          </div>
          <div>
            <a href="/docs/checkout/pay-later/us/" className="nextStep-link linkFormat" data-testid="dcai-nsc-sub1-card1-link">Pay Later</a>
            <p data-testid="dcai-nsc-sub1-card1-p1">
              Payers buy now and pay in installments.
            </p>
          </div>
        </div>
        <div className="whiteBox">
          <div className="flexRow">
            <div className="flexCol"><DocumentIcon /></div>
            <div className="flexCol"><Badge type="neutral">Optional</Badge></div>
          </div>
          <div>
            <a href="/docs/checkout/pay-with-venmo/integrate/" className="nextStep-link linkFormat" data-testid="dcai-nsc-sub1-card2-link">Pay with Venmo</a>
            <p data-testid="dcai-nsc-sub1-card2-p1">
              Add the Venmo button to your checkout integration.
            </p>
          </div>
        </div>
        <div className="whiteBox">
          <div className="flexRow">
            <div className="flexCol"><DocumentIcon /></div>
            <div className="flexCol"><Badge type="neutral">Optional</Badge></div>
          </div>
          <div>
            <a href="/docs/checkout/apm/" className="nextStep-link linkFormat" data-testid="dcai-nsc-sub1-card3-link">Alternative payment methods</a>
            <p data-testid="dcai-nsc-sub1-card3-p1">
              Accept local payment methods across the globe.
            </p>
          </div>
        </div>
        <div className="whiteBox">
          <div className="flexRow">
            <div className="flexCol"><DocumentIcon /></div>
            <div className="flexCol"><Badge type="neutral">Optional</Badge></div>
          </div>
          <div>
            <a href="/docs/checkout/apm/apple-pay/" className="nextStep-link linkFormat" data-testid="dcai-nsc-sub1-card4-link">Apple Pay</a>
            <p data-testid="dcai-nsc-sub1-card4-p">
              Add Apple Pay as a payment button.
            </p>
          </div>
        </div>
      </Col>
    </Row>
    <br/>
    <p style={{ fontSize: "20px", marginBottom: "10px" }} data-testid="dcai-nsc-sub2">
      Security and customizations
    </p>
    <Row>
      <Col className="dcai-nextsteps">
        <div className="whiteBox">
          <div className="flexRow">
            <div className="flexCol"><DocumentIcon /></div>
            <div className="flexCol"><Badge type="warning">Required</Badge></div>
          </div>
          <div>
            <a target="_blank" href="/docs/checkout/advanced/customize/3d-secure/" className="nextStep-link linkFormat" data-testid="dcai-nsc-sub2-card1-link">Implement 3D Secure</a>
            <p data-testid="dcai-nsc-sub2-card1-p1">
              Authenticate card holders through card issuers.
            </p>
          </div>
        </div>
        <div className="whiteBox">
          <div className="flexRow">
            <div className="flexCol"><DocumentIcon /></div>
            <div className="flexCol"><Badge type="neutral">Optional</Badge></div>
          </div>
          <div>
            <a target="_blank" href="/docs/api/orders/v2/#orders_capture" className="nextStep-link linkFormat" data-testid="dcai-nsc-sub2-card2-link">Capture payment</a>
            <p data-testid="dcai-nsc-sub2-card2-p1">
              Captures payment for an order.
            </p>
          </div>
        </div>
        <div className="whiteBox">
          <div className="flexRow">
            <div className="flexCol"><DocumentIcon /></div>
            <div className="flexCol"><Badge type="neutral">Optional</Badge></div>
          </div>
          <div>
            <a href="/docs/api/payments/v2/#captures_refund" className="nextStep-link linkFormat" data-testid="dcai-nsc-sub2-card3-link">Refund a captured payment</a>
            <p data-testid="dcai-nsc-sub2-card3-p1">
              Refund all or part of a captured payment.
            </p>
          </div>
        </div>
        <div className="whiteBox">
          <div className="flexRow">
            <div className="flexCol"><DocumentIcon /></div>
            <div className="flexCol"><Badge type="neutral">Optional</Badge></div>
          </div>
          <div>
            <a target="_blank" href="/docs/checkout/advanced/customize/rtau/" className="nextStep-link linkFormat" data-testid="dcai-nsc-sub2-card4-link">Real-time account updater</a>
            <p data-testid="dcai-nsc-sub2-card4-p1">
              Reduce declines by getting card updates from the issuer.
            </p>
          </div>
        </div>
      </Col>
    </Row>
  </div>
</div>
</SectionInView>
