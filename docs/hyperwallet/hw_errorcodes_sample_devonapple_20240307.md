FORMAT: 1A
HOST: https://uat-api.paylution.com/rest/v4

# Hyperwallet API

# Group Overview

## Accessing the API [/overview/accessing-the-api]

### Accessing the API [POST]

The Hyperwallet REST API provides broad access to your program as well as granular role controls on each endpoint. As a general best practice, your REST API user will be created at the top level of your [program hierarchy][hierarchy] in order to allow full access to your program and all the resources within.

> All requests to the REST API must be made over <a href="https://en.wikipedia.org/wiki/HTTPS" target="_blank">HTTPS</a> using the <a href="https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.2" target="_blank">TLS</a> protocol. Requests will be rejected if they are made over HTTP or use an insecure protocol.

## IP Allowlisting

Hyperwallet provides 3 [distinct environments][hyperwallet-environments], each of which has distinct security policies in place affecting REST API access.


## Authentication & Headers

All requests to the REST API are authenticated individually using <a href="https://en.wikipedia.org/wiki/Basic_access_authentication" target="_blank">HTTP Basic Authentication</a>. You will have a set of credentials for each of the above environments. Please ensure that the following headers are provided with each API request:

### Authorization

```http
Authorization: Basic dGVzdHVzZXJAMTIzNDU2Nzg6bXlBY2NQYXNzdzByZA==
```

All requests to the API must include the `Authorization` header with your credentials passed as the value.

If you are a Hyperwallet client, your credentials will be generated and provided to you during the implementation of your program. If you have signed up for a Sandbox account, you can find your API credentials on the Credentials page.

### Content-Type

```http
Content-Type: application/json
```

Any `POST` or `PUT` request to the REST API must include the `Content-Type` header with `application/json` passed as the value. Not including this header, or passing a different value, will result in a `415 Unsupported Media Type` error.

A request that uses [Payload Encryption](/content/api/v4/overview/payload-encryption) needs to pass `application/jose+json` as the value for the `Content-Type` header.

### Accept

```http
Accept: application/json
```

All requests to the API should include the `Accept` header with `application/json` passed as the value.

A request that uses [Payload Encryption](/content/api/v4/overview/payload-encryption) needs to pass `application/jose+json` as the value for the `Accept` header.


## Environments [/overview/environments]

### Environments [POST]

Hyperwallet provides 3 environments, each environment has distinct security policies in place affecting REST API access. The 3 environments are as follows:

* 	<a href="https://portal.hyperwallet.com/login" target="_blank">Developer Sandbox</a>
* 	User Acceptance Testing (UAT)
*	Production

## Developer Sandbox
This environment is accessible by anyone through <a href="https://portal.hyperwallet.com/login" target="_blank">self registration</a>. The sandbox provides a standard configuration with which to develop your integration. New users will be provided with auto-generated REST API credentials in order to have unrestricted access to our API.

There is no inbound restriction on API requests so you are able to make requests from anywhere.


## User Acceptance Testing (UAT)
This environment is tailored to match your business requirements. As part of the implementation effort, a REST API user will be configured for you with the necessary roles to access your program.

Unlike the Developer Sandbox, there **is** an inbound restriction on API requests. Outbound notifications originating from the Hyperwallet platform, such as our [Webhook Notifications][webhooks] require allowlisting in our firewall. To configure these notifications, we require the URL of your application server that listens for the notifications.


## Production
Alongside your UAT, you will also have a Production environment that mirrors the configuration of your UAT program. Access to Production is tightly controlled. Your REST API user will be able to make requests from only a small range of IPs specified by you. Generally, Hyperwallet cannot permit an allowlist larger than 254 IPs. In practice, this means that Hyperwallet clients must ensure they use a static IP when accessing our REST API.

As with the UAT environment, outbound [webhoook notifications][webhooks] must be allowlisted in our firewall. To configure these notifications, we require the URL of your application server that listens for the notifications.


## Best Practices
It is recommended that requests to the UAT and Production environments originate from separate IP ranges. This allows for granular access control and prevents users from mistakenly making requests to the incorrect environment.

For information on API throttling in the environments, see the [Error Handling](/content/api/v4/overview/errors#api-throttling) section.


## Payload Encryption [/overview/payload-encryption]

### Payload Encryption [GET]

Use the Payload Encryption API as a second factor of authentication.

### How Hyperwallet protects sensitive data

The Payload Encryption endpoint is an alternative to IP allowlisting that you can use as a second factor of authentication. Payload Encryption uses Javascript Object Signing and Encryption (JOSE) and JSON Web Tokens (JWT) to guarantee the confidentiality, accuracy, integrity, and origin of your payment data.

#### Standards

Hyperwallet uses the following standards in our Payload Encryption process:

* We use the [Javascript Object Signing and Encryption (JOSE)](https://jose.readthedocs.io/en/latest/) framework.
* We follow the [JSON Web Tokens (JWT)](https://datatracker.ietf.org/doc/html/rfc7519) standard.
* We sign using [JSON Web Signature (JWS)](https://datatracker.ietf.org/doc/html/rfc7515) and encrypt using [JSON Web Encryption (JWE)](https://datatracker.ietf.org/doc/html/rfc7516)
* We use [JSON Web Keys (JWK)](https://datatracker.ietf.org/doc/html/rfc7517) to publish public keys for the JWTs.
* We use the RS256 algorithm by default. See [JWS Algorithms](#jws-algorithms) for the full list of algorithms we support.

### REST API Authentication

Hyperwallet offers 2 second factor options for authentication:

*   IP address allowlisting
*   Layer 7 encryption using Javascript Object Signing and Encryption (JOSE) and JSON Web Tokens (JWT)

#### Allowlisting

You need to provide source IP addresses if you choose allowlisting as the second factor for authentication. Hyperwallet will only accept API calls that originate from these IP addresses. We also support Classless Inter-Domain Routing (CIDR) notation.

#### Payload Encryption

Hyperwallet accepts requests from any IP address if you choose Payload Encryption as the second factor for authentication.

### How encryption works

![Payload Encryption diagram](https://www.paypalobjects.com/devdoc/payload_encryption_diagram.png "Payload Encryption diagram")

1. JSON is first signed using the client's private signing key.
2. It is then encrypted using one of Hyperwallet's public encryption keys:
    * Production: https://api.paylution.com/jwkset
    * User Acceptance Testing (UAT): https://uat-api.paylution.com/jwkset.
3. The request is sent to Hyperwallet with the content-type: `application/jose+json`.
4. The payload is decrypted using the corresponding Hyperwallet private encryption key.
5. The signed payload is then verified using the client's public signing key.
6. System performs the request and then generates a response that will be signed and encrypted.
7. The system looks for a match using the same algorithm used to sign in with the client's private signing key in step 1. For example:
    * The client signed the payload using a RS256 signing key.
    * The system looks in Hyperwallet's private keyset for an RS256 signing key to sign the response.
8. The system looks for a match in the hosted client public keyset using the same algorithm as the one used to encrypt Hyperwallet's public encryption key in step 2. For example:
    * The client encrypted the payload using an RSA_OAEP_256 encryption key.
    * System looks in client's hosted public keyset for an RSA_OAEP_256 encryption key to encrypt the response.

The Payload Encryption endpoint uses "Basic" HTTP authentication (BA) for all clients. You need to provide usernames and passwords for BA during onboarding.

Request payloads need to be signed and encrypted, in addition to BA and Transport Layer Security (TLS). You also need to decrypt and then validate the signatures of any responses that access the payload.

Host your public keys as a JSON Web Keys (JWK) set and provide the public JWK URL during onboarding. Use different keys for User Acceptance Testing (UAT) and production. Host these keys at different URLs, using TLS with a valid certificate.

Hyperwallet caches your public keys when possible. However, you need to ensure that your public keys are always accessible to avoid service interruption. Hyperwallet supports public/private keys and compact JWT serialization. Hyperwallet doesn't support shared secrets or password-based encryption.

Payload Encryption signs requests and responses using JSON Web Signatures (JWS), and encrypts them using JSON Web Encryption (JWE). A payload needs to be signed then encrypted. Payloads are formatted as `JWE(JWS(payload)))`. JOSE requests and responses are identical to their unencrypted representations. Use the `ContentType` header to pass the payload format.

An **encrypted request** needs to pass `application/jose+json` as the value for the `Content-Type` and `Accept` headers:

```http
Content-Type: application/jose+json
Accept: application/jose+json
```

A request that isn't encrypted needs to pass `application/json` as the value for the `Content-Type` and `Accept` headers.

If the encrypted request can't be decrypted, is incorrect, or uses an unsupported algorithm, the Payload Encryption endpoint rejects the request with a response that includes `Content-Type: application/jose+json`.

When the encrypted request uses an unsupported algorithm or an incorrect token, the Payload Encryption endpoint rejects the request with a `4xx HTTP` response.

Hyperwallet updates the list of supported algorithms based on the latest security best practices.

### How decryption works

This algorithm sample shows how to construct a request using the HS256 algorithm and a JSON Web Token (JWT).

#### Algorithm example

**Header: algorithm token type**

```json
{
  "alg": "HS256",
  typ": "JWT",
  "kid": "01-2822"
}
```

**Payload: data**

```json
{
  "token" : "usr-f9154e16-94e8-4686-a84e-a75688ace7b5",
  "status" : "PRE_ACTIVATED",
  "verificationstatus" : "NOT_REQUIRED",
  "createdOn" : "201910-30T22:15:45",
  "c1ientUserId" : "CSK7b8Ffch",
  "profi1eType" : "INDIVIDUAL",
  "firstName" : John",
  "lastName" : "Smith",
  dateOfBirth" : "1980-01-01",
  "email" : "john@company.com",
  "addressLine1" : "123 Maln Street",
  "city" : "New York",
  "stateProvince" : "NY",
  "country" : "US",
  "postalCode" : "10016",
  "language" : "en",
  "programToken": "prg-83836cdf-2ce2-4696-8bc5-f1b860777238c",
  "links" : [
    {
      "params" {
        "rel" : :self"
      },
      "href" : "https://uat-api.paylution.com/rest/v4/users/usr-
      f9154e16-94e8-4686-a84e-a75688ace7b5"
      }
    ]
}
```

**Verify signature**

```json
HMACSHA256(
  base64UrlEncode(header) +
  base64UrlEncode(payload) ,
  your-256-b1t-secret
) secret base64 encoded
```

### Signature

Use your private key to sign request payloads.

Hyperwallet uses your public JSON Web Key (JWK) set to validate the signature on payout requests. We look for this JWK at the URL that you provide during onboarding. The Basic HTTP authentication process passes the JWK set URL with the request user's details.

The Payload Encryption endpoint ignores any `jku` and `jwk` headers used with JWK public keys.

Hyperwallet signs response payloads with our private key.

The Payload Encryption response passes a `kid` header to identify the public key that you use to validate the signature. The `jti` header serves as a nonce with JWT and passes a UUID.

> **Note:** It isn't practical to validate a nonce for all solutions, so you and Hyperwallet can choose whether or not to validate this nonce.

### JWS Algorithms

Payload Encryption supports the following JWS algorithms:

* [RSASSA-PKCS1-v1_5](https://datatracker.ietf.org/doc/html/rfc7518#section-3.3): RS256, RS384, RS512
* [RSASSA-PSS](https://datatracker.ietf.org/doc/html/rfc7518#section-3.5): PS256, PS384, PS512
* [ECDSA](https://datatracker.ietf.org/doc/html/rfc7518#section-3.4): ES256, ES384, ES512

### Expiry

Payload Encryption uses the `exp` header with JWS to prevent token reuse. The `exp` header is defined as a part of the JSON Web Token (JWT), not part of the JWS. Use the `crit` header to show that Payload Encryption needs to process the `exp` header.

Signatures expire 5 minutes after generation.

### JSON Web Encryption

The content encryption keys (CEK) in a request need to be encrypted with Hyperwallet's public key.

Hyperwallet's public keys are available at https://api.paylution.com/jwkset (Production) and https://uat-api.paylution.com/jwkset (UAT). JWE headers need to pass a key identifier (`kid`) which can be used to locate the appropriate key from the JWK public key set.

> **Note:** UAT and Production environments use different keys.

Hyperwallet uses your public key to encrypt the Content Encryption Key (CEK) in a response. Decrypt the CEK using your private key, and then use that CEK to decrypt the response payload.

Hyperwallet uses the same algorithm as the request if an appropriate public key can be found at the JWK at the URL you provided.

### JWE Algorithms

Payload Encryption supports the following JWE algorithms. The `alg` parameter in the JWE header passes the algorithm:

* [RSA-OAEP-256](https://datatracker.ietf.org/doc/html/draft-ietf-jose-json-web-algorithms#section-4.3)
* [ECDH-ES](https://datatracker.ietf.org/doc/html/draft-ietf-jose-json-web-algorithms#section-4.6): ECDH-ES+A128KW, ECDH-ES+A192KW, ECDH-ES+A256KW

### JWE Encryption Algorithms

Payload Encryption supports the following JWE Encryption algorithms. The `enc` parameter in the CEK header passes the encryption algorithm:

* [AES_CBC_HMAC_SHA2](https://datatracker.ietf.org/doc/html/draft-ietf-jose-json-web-algorithms#section-5.2.6): A128CBC-HS256, A192CBC-HS384, A256CBC-HS512
* [AES GCM](https://datatracker.ietf.org/doc/html/draft-ietf-jose-json-web-algorithms#section-5.3): A128GCM, A192GCM, A256GCM

### Publishing Public Keys

Publish your public keys at the URL that you provided for the JWK when onboarding. You may publish these keys as a JWK keyset. Use DNS-compliant bucket names when publishing to an [Amazon S3 bucket](https://aws.amazon.com/s3/).

### Key Rotation

You can rotate your keys without coordinating with Hyperwallet because you control the publication of your public keys at your own URL:

1. Update your keyset to include your new and old keys.
2. Update your application to use the new key ID in all active requests.
3. Remove the old key from the keyset and republish with only the new key.

Publish your keys to the same URL that you provided to Hyperwallet during onboarding. You can change the JWK URL by coordinating with Hyperwallet's production support team.

When we refresh keys, we publish the key at least 1 hour before using the key. If a merchant fetches and caches a JWK at least once every hour, they are unlikely to use an uncached key.

Hyperwallet fetches and caches a merchant's JWK keys every hour. When a merchant refreshes their keys, they need to wait at least 1 hour before using that key in the payload.

Hyperwallet rotates their keys once per year, and encourages you and your merchants to do the same.

### Error Messages

Possible error messages a client might receive when integrating. These are wrapped in our standard error message JSON.

```json
{
  "errors" : [ {
    "message" : "JWS signature is expired. crit-exp header was in the past.",
    "code" : "JWT_ERROR"
  } ]
}
```

| Status code | Error message | Explanation |
| ----------- | ----------- | ----------- |
| `400` | User is configured to use only JWT JOSE encrypted messages.<br><br>Expected contentType or accept header value is `application/jose+json` | The client tried to send a plaintext json request. They must encrypt everything if they are configured for JOSE. |
| `400` | Signature could not be verified | The signature the client used was not valid. |
| `400` | Payload not a signed JWS Object | The client encrypted something other than a signed JWS object. |
| `400` | Only JWE Objects are permitted | The client sent a JOSE object that is not a JWE object. |
| `500` | No Hyperwallet JWK candidate was found to sign the response so the request not fulfilled | The client attempted to use a signing algorithm which we do not support. They should refer to the reference doc for our supported list. |
| `500` | No JWK found in the client key set which matches the requested encryption method and algorithm so the request was not fulfilled. | The client requested an algorithm which they themselves do not support. |
| `400` | JWE Encryption algorithm (`enc` header) " + `encryptionMethod` + "is not supported<br><br>Algorithm (`alg` header) " + `jweAlgorithm` + "is not supported for JWE<br><br>Algorithm (`alg` header) " + `jwsAlgorithm` + "is not supported for JWS | The client attempted to use an algorithm which we do not support. They should refer to the reference doc for our supported list. |
| `400` | JWS signature is expired. `crit-exp` header was in the past. | The client sent an expired signature. |
| `400` | Empty or invalid crit header `exp` | The client did not send the expiry header. |


## SDK [/overview/sdk]

### SDK [GET]

The Hyperwallet REST SDK libraries can be used to manage users, transfer methods and payments through the Hyperwallet API.
The SDK is available in:
+ [Java](#java)
+ [Node](#node)
+ [PHP](#php)

### Java

Hyperwallet's Java server SDK requires at minimum JDK (Java Development Kit) version 1.7 and above. The SDK can be downloaded from <a href="https://github.com/hyperwallet/java-sdk" target="_blank">GitHub</a>. See the [SDK changelog](https://github.com/hyperwallet/java-sdk/blob/master/CHANGELOG.md) for updates.

> Note: For API v4, use the latest SDK version 2.x.x. This version supports API v4 only and cannot be used in conjunction with API v3.

##### **Installation**
To install the SDK using <a href="https://maven.apache.org/" target="_blank">Maven</a>, insert the following into the POM:
```xml
<dependency>
    <groupId>com.hyperwallet</groupId>
    <artifactId>sdk</artifactId>
    <version>2.0.0</version>
</dependency>
```

To install the SDK using <a href="https://gradle.org/" target="_blank">Gradle</a>, insert the following into the dependency section of your build.gradle file:
```groovy
compile 'com.hyperwallet:sdk:2.0.0'
```

##### **Create Instance**
Create an instance of the Hyperwallet Client (with username, password, program token and server) to test with your Sandbox account. For UAT and Production environments, use the server and credentials provided by your Hyperwallet Technical Implementation Specialist during onboarding.

```java
Hyperwallet client = new Hyperwallet("restapiuser@4917301618", "mySecurePassword!", "prg-645fc30d-83ed-476c-a412-32c82738a20e", "https://uat-api.paylution.com/rest/v4");
```

### Node

Hyperwallet's Node server SDK requires at minimum NodeJS 6.15.1 and above. The SDK can be downloaded from <a href="https://github.com/hyperwallet/node-sdk" target="_blank">GitHub</a>. Further API documentation is available <a href="http://hyperwallet.github.io/node-sdk" target="_blank">here</a>. See the [SDK changelog](https://github.com/hyperwallet/node-sdk/blob/master/CHANGELOG.md) for updates.

> Note: For API v4, use the latest SDK version 2.x.x. This version supports API v4 only and cannot be used in conjunction with API v3.

##### **Installation**
To install the SDK using <a href="https://www.npmjs.com/" target="_blank">npm</a>, type the following into the terminal:
```bash
$ npm install hyperwallet-sdk
```

Add the SDK to your `package.json` file:
```json
hyperwallet-sdk
```

Add the SDK module to your project using the following code:
  ```javascript
  var Hyperwallet = require("hyperwallet-sdk");
  ```

##### **Create Instance**
Create an instance of the Hyperwallet Client (with username, password, program token and server) to test with your Sandbox account. For UAT and Production environments, use the server and credentials provided by your Hyperwallet Technical Implementation Specialist during onboarding.
  ```javascript
  var client = new Hyperwallet({
    username: "restapiuser@4917301618",
    password: "mySecurePassword!",
    programToken: "prg-645fc30d-83ed-476c-a412-32c82738a20e",
    server: "https://uat-api.paylution.com"
  });
  ```

### PHP

Hyperwallet's PHP server SDK requires at minimum PHP 5.6 and above. The SDK can be downloaded from <a href="https://github.com/hyperwallet/php-sdk" target="_blank">GitHub</a>. Further API documentation is available <a href="http://hyperwallet.github.io/php-sdk" target="_blank">here</a>. See the [SDK changelog](https://github.com/hyperwallet/php-sdk/blob/master/CHANGELOG.md) for updates.

> Note: For API v4, use the latest SDK version 2.x.x. This version supports API v4 only and cannot be used in conjunction with API v3.

##### **Installation**
To install the SDK using <a href="https://getcomposer.org/" target="_blank">Composer</a>, type the following command into the terminal:
```bash
$ composer require hyperwallet/sdk
```

Add the SDK as a dependency to your `composer.json`:
```json
hyperwallet/sdk
```

##### **Create Instance**
Create an instance of the Hyperwallet Client (with username, password, program token and server) to test with your Sandbox account. For UAT and Production environments, use the server and credentials provided by your Hyperwallet Technical Implementation Specialist during onboarding.
```php
$client = new \Hyperwallet\Hyperwallet("restapiuser@4917301618", "mySecurePassword!", "prg-645fc30d-83ed-476c-a412-32c82738a20e", "https://uat-api.paylution.com");
```

## Error Handling [/overview/errors]

### Error Handling [GET]

The Hyperwallet REST API uses standard <a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes" target="_blank">HTTP Status Codes</a> to indicate whether the request succeeded or failed. Additionally, the `errors` array is returned for most failed calls and contains error objects corresponding to specific exceptions encountered during processing.


## Idempotent Requests

The API supports idempotency for safely retrying requests without accidentally performing the same operation twice and duplicating the results. You can make idempotent calls any number of times without concern that the server creates or completes an action on a resource more than once. You can use idempotent calls for POST calls that fail with network timeouts or HTTP 5xx status codes. Idempotency enables you to correlate request payloads with response payloads, eliminate duplicate requests, and retry failed requests or requests with unclear responses.

> Note: If you change the unique identifier (`clientUserId`, `clientPaymentId`, `clientTransferId`, `clientRefundId`) in the subsequent request, instead of returning the saved result, the request will be duplicated.


## HTTP Status Codes

The following table lists which status codes are used by the Hyperwallet REST API. Generally, the status codes can be categorized as follows:

* `2xx` - the request was successful
* `4xx` - the request failed
* `5xx` - a server error occurred

Status Code | Description
----------- | -----------
`200 OK` | Standard success response for requests
`201 Created` | The request was fulfilled and the data was created as requested
`202 Accepted` | The request was accepted and the data is currently waiting to be processed
`204 No Content` | The request was successfully processed but no matching data was found
`304 Not Modified` | The request was accepted but the cached data is still valid (the response will be empty)
`400 Bad Request` | The request failed due to invalid data
`401 Unauthorized` | Your authentication credentials are not valid
`403 Forbidden` | You are not configured to access the requested resource
`404 Not Found` | The requested resource could not be found
`405 Method Not Allowed` | The HTTP method used in the call is not supported for the requested resource
`415 Unsupported Media Type` | The `Content-Type` header was not supplied or contained invalid content types
`429 Too Many Requests` | There were too many requests to access the API within an acceptable time frame
`5xx` | Something went wrong on our end

## The Error Object

An `error` object describes a specific error. It can be returned for any `4xx` and `5xx` HTTP response, but is usually used to describe `400` errors.

Attribute | Description
--------- | -----------
`fieldName` | The request field that was responsible for the error
`message` | A brief description of the error
`code` | The Hyperwallet error code for the error
`relatedResources` | The token of the identical resource already present in the program

## Handling Communication Errors

In the event of a network disruption or application failure, it may be necessary to ensure that your Hyperwallet program and your application are in sync. For instance, synchronization would be necessary if a user is created in your application but the request to create the user in your Hyperwallet program is disrupted.

### POST Requests

In the event that a POST request does not complete a full request and response, your Hyperwallet program can be in two possible states, either of which will require synchronization:

1. The resource is not created within Hyperwallet; or,
2. The resource is created within Hyperwallet but your application is not aware of the resource

To synchronize your Hyperwallet program with your application, simply retry the original request. To avoid creating a new resource, ensure that the same unique identifier is provided in this second request.

The following unique identifiers are used in the Hyperwallet endpoints:

* `clientUserId` in /users endpoint
* `clientPaymentId` in /payments endpoint
* `clientTransferId` in /transfers/spendback endpoint
* `clientRefundId` in /spendback-refunds endpoint

Upon submitting the second request:

* If the resource was not created within your Hyperwallet program on the original request, this second request will successfully create the resource.
* If the resource was created by the original request, this second request will not create a new resource but will rather cause a Duplicate Resource Error Response. This error response will contain the token identifying the original resource, enabling you to request the original resource through the API if necessary. You can see this type of response depicted in the provided example.

```json
    {
      "errors": [ {
        "message": "The value you provided for this field is already registered with another user usr-b7fbf0c4-d698-4cf5-8869-1836ea0eac69",
        "fieldName": "clientUserId",
        "code": "DUPLICATE_CLIENT_USER_ID",
        "relatedResources": [
          "usr-b7fbf0c4-d698-4cf5-8869-1836ea0eac69"
        ]
      } ]
    }

    {
      "errors": [ {
        "message": "Duplicate Client Reference Number",
        "fieldName": "clientPaymentId",
        "code": "CONSTRAINT_VIOLATIONS",
        "relatedResources": [
          "pmt-ce9b1c99-430d-4945-a2e7-d82e5e52bcaf"
        ]
      } ]
    }
```

### PUT Requests

All `PUT` requests to the Hyperwallet API are idempotent, so all subsequent requests to update the resource will leave the resource in the same state as the original `PUT` request. In these cases, simply retrying the original request is sufficient.

```json
{
    "errors" : [ {
    "message" : "The value you provided for this field is already registered with another user usr-ae836d14-f4f4-4d6d-9653-1ee03250df7b",
    "fieldName" : "clientUserId",
    "code" : "DUPLICATE_CLIENT_USER_ID",
    "relatedResources" : [ "usr-ae836d14-f4f4-4d6d-9653-1ee03250df7b" ]
    } ]
}
```

### GET Requests

All GET requests to the Hyperwallet API are idempotent. You can also use these calls to determine whether a previous POST request with 5xx error was successful or not. The unique identifier in the POST request needs to be used as a query parameter to access the object intended to be created.

The following unique identifiers are used in Hyperwallet endpoints:

* `clientUserId` in /users endpoint
* `clientPaymentId` in /payments endpoint
* `clientTransferId` in /transfers/spendback endpoint
* `clientRefundId` in /spendback-refunds endpoint

## API Throttling

API calls are limited based on the type of calls made over a period of a second and over a period of an hour (sliding window) per API user. The limits are applied to the rest API user and not per IP address.

Hyperwallet provides a single tier and API integrations (for all 3 [environments][hyperwallet-environments]) will need to work within the limits specified below.

Request Type | Per Second | Per Hour
--|--|--
`GET` | 5 | 7,500
`POST`/`PUT` | 30 | 50,000

### Exceeding the Limit
In the case that the limit is exceeded within the specified time period, error `429` (Too Many Requests) is returned and the requests are dropped. For example, if you have used all 7,500 `GET` requests between 7:35:00PM - 8:00:00PM,  all request between 8:00:01PM - 8:34:59PM will be dropped and error `429` is returned. You can send new requests starting at 8:35:00PM.

### Avoiding Limits
The following approaches can be used to reduce the number of API calls made within a given time period:
*	**Caching:** If the response of a request needs to be accessed frequently, store the results in the local cache of your application for easy access instead of sending a new request on each page load.
* 	**Use request parameters:** Use applicable request parameters on `GET` requests to obtain relevant information. For example, if you need to obtain a list of `ACTIVATED` users, use the appropriate parameter as opposed to retrieving results for the entire user list.
* 	**Webhook notifications:** For the majority of status changes, Hyperwallet encourages the use of [Webhook Notifications][webhooks] wherever possible. For example, when seeking the status of payment returns, establishing a Webhook Notification listener will greatly reduce polling.

## Error List

This section lists errors that Hyperwallet API endpoints return.

### Generic

These error codes are used by all Hyperwallet endpoints:

| Status Code and Error | Description |
| --- | --- |
| `401 JWT_ERROR` | The request includes an incorrect JSON Web Token (JWT). |
| `401 JWT_EXPIRED` | The request includes an expired JWT. Use a `POST` call to generate a new token. |
| `401 INCORRECT_LOGIN_CREDENTIALS` | The request includes incorrect credentials. Check your credentials and try again. |
| `401 FAILED_LOGIN_ERROR_104` | Authentication wasn't successful due to other reasons. |
| `403 FORBIDDEN` | Requestor doesn't have access to the resource. |
| `403 FORBIDDEN_REST_VERSION` | The request uses the wrong REST API version. Ensure you are using the REST API version configured for your program. |
| `500 SYSTEM_ERROR` | An unexpected error occurred. Try the request again. |
| `400 GENERAL_ERROR` | There was an error in the request. See the details below for a description based on the endpoint. |

### Users

The following tables show unique error codes for the [`/users`](/content/api/v4/resources/users) API endpoints.

##### Create a User

These error codes are unique to the [`POST /users`](/content/api/v4/resources/users/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of our user requirements here](/content/api/v4/resources/users/create). |
| `400 DUPLICATE_CLIENT_USER_ID` | The request includes a duplicate `clientUserId`. The `clientUserId` must be unique. |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The request includes a duplicate `email`. The `email` must be unique. |
| `400 INVALID_COUNTRY` | The request includes a country that is invalid, sanctioned, or restricted. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that is incorrect. [Read a list of expected values here](/content/api/v4/resources/users/create). |

##### Retrieve a User

These error codes are unique to the [`GET /users/{user-token}`](/content/api/v4/resources/users/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 INVALID_WALLET_STATUS` | The wallet status is invalid. [Read a list of valid wallet status options here](/content/api/v4/resources/users/retrieve). |
| `404 RESOURCE_NOT_FOUND` | This user doesn't exist in the system. Check the user token and try again.  |

##### Update a User

These error codes are unique to the [`PUT /users/{user-token}`](/content/api/v4/resources/users/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements.  [Read a list of user requirements here](/content/api/v4/resources/users/update). |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The request includes a duplicate `clientUserId`. The `clientUserId` must be unique. |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The request includes an `email` that is already registered in the system. The `email` must be unique. |
| `400 INVALID_COUNTRY` | The request includes a country that is invalid, sanctioned, or restricted. |
| `400 INVALID_ENUM_VALUE` | The request includes an incorrect value. [Read a list of expected values here](/content/api/v4/resources/users/create). |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to update a user. |

### Business Stakeholder

The following tables show unique error codes for the [`/users`](/content/api/v4/resources/users) API endpoints.

##### List Business Stakeholders

These error codes are unique to the [`GET /users/{user-token}/business-stakeholders`](/content/api/v4/resources/business-stakeholders/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again.  |

##### Create a Business Stakeholder

These error codes are unique to the [`POST /users/{user-token}/business-stakeholders`](/content/api/v4/resources/business-stakeholders/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/business-stakeholders/create). |
| `400 INVALID_COUNTRY` | The request includes a country that is invalid, sanctioned, or restricted. |

##### Update a Business Stakeholder

These error codes are unique to the [`PUT /users/{user-token}/business-stakeholders/{stakeholder-token}`](/content/api/v4/resources/business-stakeholders/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/business-stakeholders/update). |
| `400 INVALID_DOCUMENT_PARTS` | The request includes the wrong documents. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 MISSING_REQUEST_PART_FILE` | The request doesn't include a file required for this operation. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 VERIFICATION_NOT_REQUIRED` | The request includes a document when verification isn't required. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 INVALID_DOCUMENT_TYPE` | The request includes an incorrect document type. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 UNSUPPORTED_FILE_TYPE` | The request uploaded a file type that isn't supported. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 MISSING_COUNTRY_FOR_DOCUMENT` | 1 or more documents need to include a country or region. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 DOCUMENT_TYPE_REQUIRED` | You need to provide a document type for 1 or more documents. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 FILE_SIZE_EXCEEDS_MAXIMUM` | The file size exceeds the maximum allowable file size. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 INVALID_MESSAGE` | An application error caused the request to fail. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 EMPTY_FILE_UPLOADED` | The request includes an empty file. |
| `400 INVALID_PARAMETER` | The request includes a blank `type` parameter. [Read a list of requirements here](/content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 MAXIMUM_UPLOAD_FILES_EXCEEDED` | This request exceeds the maximum number of file uploads. |


### Bank Accounts

The following tables show unique error codes for the [`/bank-accounts`](/content/api/v4/resources/bank-accounts) API endpoints.

##### Create a Bank Account

These error codes are unique to the [`POST /users/{user-token}/bank-accounts`](/content/api/v4/resources/bank-accounts/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank account that doesn't exist in the system. Check the user or bank account token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/bank-accounts/create?profileType=Individual&accountType=BANK_ACCOUNT). |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds an account that is already in the Hyperwallet system. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. || `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 EXTERNAL_ACCOUNT_TYPE_NOT_SUPPORTED` | This transfer method is not configured for your program. Contact the customer support team if you would like this enabled. |

##### Retrieve a Bank Account

These error codes are unique to the [`GET /users/{user-token}/bank-accounts/{bank-account-token}`](/content/api/v4/resources/bank-accounts/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

##### Update a Bank Account

These error codes are unique to the [`PUT /users/{user-token}/bank-accounts/{bank-account-token}`](/content/api/v4/resources/bank-accounts/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/bank-accounts/create?profileType=Individual&accountType=BANK_ACCOUNT). |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds an account that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn't support updates. [Read the list of fields that can be updated](/content/api/v4/resources/bank-accounts/update?profileType=Individual&accountType=BANK_ACCOUNT&country=United+States&currency=USD). |


### Bank Cards

The following tables show unique error codes for the [`/bank-cards`](/content/api/v4/resources/bank-cards) API endpoints.

##### Create a Bank Card

These error codes are unique to the [`POST /users/{user-token}/bank-cards`](/content/api/v4/resources/bank-cards/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 CARD_NOT_SUPPORTED` | The request includes a card that we don't support. [Read a list of supported cards here](/content/transfer-methods/v1/bank-card#payee-availability) |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/bank-cards/create). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a card that is already in the Hyperwallet system. If this is a valid request, reach out to our customer support team to add the bank card. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `400 EXTERNAL_ACCOUNT_TYPE_NOT_SUPPORTED` | This transfer method is not configured for your program. Contact the customer support team if you would like this enabled. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |

##### Retrieve a Bank Card

These error codes are unique to the [`GET /users/{user-token}/bank-cards/{bank-card-token}`](/content/api/v4/resources/bank-cards/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank card that doesn't exist in the system. Check the user or bank card token and try again.  |

##### Update a Bank Card

These error codes are unique to the [`PUT /users/{user-token}/bank-cards/{bank-card-token}`](/content/api/v4/resources/bank-cards/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank card doesn't exist in the system. Check the user or bank card token and try again. |
| `400 CARD_NOT_SUPPORTED` | The request includes a card that we do not support. [Read a list of supported cards here](/content/transfer-methods/v1/bank-card#payee-availability). |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements.  [Read a list of requirements here](/content/api/v4/resources/bank-cards/update). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a card that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn't support updates. [Read the list of fields that can be updated](/content/api/v4/resources/bank-cards/update).  |

### PayPal Accounts

The following tables show unique error codes for the [`/paypal-accounts`](/content/api/v4/resources/paypal-accounts) API endpoints.

##### Create a PayPal Account

These error codes are unique to the [`POST /users/{user-token}/paypal-accounts`](/content/api/v4/resources/paypal-accounts/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](/content/api/v4/resources/paypal-accounts/create). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a transfer method that is already in the Hyperwallet system. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `400 EXTERNAL_ACCOUNT_TYPE_NOT_SUPPORTED` | This transfer method is not configured for your program. Contact the customer support team if you would like this enabled. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |

##### Retrieve a PayPal Account

These error codes are unique to the [`GET /users/{user-token}/paypal-accounts/{paypal-account-token}`](/content/api/v4/resources/paypal-accounts/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or PayPal account that doesn’t exist in the system. Check the user or PayPal account token and try again. |

##### Update a PayPal Account

These error codes are unique to the [`PUT /users/{user-token}/paypal-accounts/{paypal-account-token}`](/content/api/v4/resources/paypal-accounts/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or PayPal account that doesn’t exist in the system. Check the user or PayPal account token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](/content/api/v4/resources/paypal-accounts/create). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds an account that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn't support updates. [Read the list of fields that can be updated](/content/api/v4/resources/bank-cards/update). |

### Venmo Accounts

The following tables show unique error codes for the [`/venmo-accounts`](/content/api/v4/resources/venmo-accounts) API endpoints.

##### Create a Venmo Account

These error codes are unique to the [`POST /users/{user-token}/venmo-accounts`](/content/api/v4/resources/venmo-accounts/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](/content/api/v4/resources/venmo-accounts/create). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a Venmo account that is already in the Hyperwallet system. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `400 EXTERNAL_ACCOUNT_TYPE_NOT_SUPPORTED` | This transfer method is not configured for your program. Contact the customer support team if you would like this enabled. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |

##### Retrieve a Venmo Account

These error codes are unique to the [`GET /users/{user-token}/venmo-accounts/{venmo-account-token}`](/content/api/v4/resources/venmo-accounts/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or Venmo account that doesn’t exist in the system. Check the user or Venmo account token and try again. |

##### Update a Venmo Account

These error codes are unique to the [`PUT /users/{user-token}/venmo-accounts/{venmo-account-token}`](/content/api/v4/resources/venmo-accounts/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or Venmo account that doesn’t exist in the system. Check the user or Venmo account token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](/content/api/v4/resources/venmo-accounts/update). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a Venmo account that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn’t support updates. [Read the list of fields that can be updated](/content/api/v4/resources/bank-cards/update). |

### Prepaid Cards

The following tables show unique error codes for the [`/users/{user-token}/prepaid-cards`](/content/api/v4/resources/prepaid-cards) API endpoints.

##### List Prepaid Cards

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards`](/content/api/v4/resources/prepaid-cards/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

##### Create a Prepaid Card

These error codes are unique to the [`POST /users/{user-token}/prepaid-cards`](/content/api/v4/resources/prepaid-cards/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](/content/api/v4/resources/prepaid-cards/create). |
| `400 INVALID_PREPAID_CARD_PACKAGE` | The request includes an incorrect prepaid card package name or identifier. |
| `400 MAX_CARDS_PROGRAM_CONFIG` | This account already has a prepaid card associated with it. Your program configuration allows a maximum of 1 prepaid card per account. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/prepaid-cards/create). |
| `400 PENDING_ADD_CARD_REQUEST` | The request wasn't successful because this wallet has a pending request to add a prepaid card. |
| `400 ATTACH_CARD_CONNECTION_ERROR` | A connection error prevented this request from successfully adding a prepaid card to the wallet. Wait a few minutes and try your request again. |
| `400 ATTACH_CARD_ERROR` | An error prevented this request from successfully adding a prepaid card to the wallet. |


##### Replace a Prepaid Card

These error codes are unique to the [`POST /users/{user-token}/prepaid-cards`](/content/api/v4/resources/prepaid-cards/replace) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](/content/api/v4/resources/prepaid-cards/create). |
| `400 INVALID_PREPAID_CARD_PACKAGE` | The request includes an incorrect prepaid card package name or identifier. |
| `400 MAX_CARDS_PROGRAM_CONFIG` | This account already has a prepaid card associated with it. Your program configuration allows a maximum of 1 card request per account. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | A bank account registration request can't have more than 2 registrations. You can register a primary and a secondary card. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/prepaid-cards/create). |
| `400 PENDING_ADD_CARD_REQUEST` | The request wasn't successful because this wallet has a pending request to add a prepaid card. |
| `400 ATTACH_CARD_CONNECTION_ERROR` | A connection error prevented this request from successfully adding a prepaid card to the wallet. Wait a few minutes and try your request again. |
| `400 ATTACH_CARD_ERROR` | An error prevented this request from successfully adding a prepaid card to the wallet. |

##### Retrieve a Prepaid Card

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}`](/content/api/v4/resources/prepaid-cards/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or prepaid card that doesn’t exist in the system. Check the user or prepaid card token and try again. |

### Paper Checks

The following tables show unique error codes for the [`/users/{user-token}/paper-checks`](/content/api/v4/resources/paper-checks) API endpoints.

##### List Paper Checks

These error codes are unique to the [`GET /users/{user-token}/paper-checks`](/content/api/v4/resources/paper-checks/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

##### Create a Paper Check

These error codes are unique to the [`POST /users/{user-token}/paper-checks`](/content/api/v4/resources/paper-checks/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet our requirements. [Read a list of requirements here](/content/api/v4/resources/paper-checks/create). |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

##### Retrieve a Paper Check

These error codes are unique to the [`GET /users/{user-token}/paper-checks/{paper-check-token}`](/content/api/v4/resources/paper-checks/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or paper check that doesn’t exist in the system. Check the user or paper check token and try again. |

##### Update a Paper Check

These error codes are unique to the [`PUT /paper-checks/{paper-check-token}`](/content/api/v4/resources/paper-checks/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The user or the bank account doesn't exist. Check and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/bank-accounts/create?profileType=Individual&accountType=BANK_ACCOUNT). |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds an account that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn't support updates. [Read the list of fields that can be updated](/content/api/v4/resources/bank-accounts/update?profileType=Individual&accountType=BANK_ACCOUNT&country=United+States&currency=USD). |


### Transfer Methods

The following table shows unique error codes for the [`/users/{user-token}/transfer-methods`](/content/api/v4/resources/transfer-methods) API endpoint.

##### List Transfer Methods

These error codes are unique to the [`GET /users/{user-token}/transfer-methods`](/content/api/v4/resources/transfer-methods) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |


### Payments

The following tables show unique error codes for the [`/payments`](/content/api/v4/resources/payments) API endpoints.

##### Create a Payment

These error codes are unique to the [`POST /payments`](/content/api/v4/resources/payments/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | This request includes a user that doesn't exist in the system. Check the user token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](/content/api/v4/resources/payments/create). |
| `400 ACCOUNT_STATUS_FLAGGED` | The request issues a payment to an account that's flagged. Accounts are typically flagged for risk reasons. Review your request or provide another bank account. |
| `400 INCORRECT_FUNDING_PROGRAM` | This request is trying to initiate a payment from an incorrect funding program. Check the `programToken` and try again. |
| `400 INSUFFICIENT_FUNDS` | The funding account doesn't have sufficient funds for the requested payment amount. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 LIMIT_SUBCEEDED` | The amount is too low for the transfer method. |
| `400 LIMIT_SUCCEEDED` | The amount is too high for the transfer method. |
| `400 MINIMUM_CONVERSION_AMOUNT_NOT_REACHED` | The amount is too low for foreign exchange (FX) conversion. |

##### Retrieve a Payment

These error codes are unique to the [`GET /payments/{payment-token}`](/content/api/v4/resources/payments/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment token that doesn't exist. Check the payment token and try again. |

### Transfers

The following tables show unique error codes for the [`/transfers`](/content/api/v4/resources/transfers) API endpoints.

##### List Transfers

These error codes are unique to the [`GET /transfers`](/content/api/v4/resources/transfers/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a token or identifier that doesn't exist in the system. Check the request and try again. |

##### Create a Transfer

These error codes are unique to the [`POST /transfers`](/content/api/v4/resources/transfers/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 INVALID_SOURCE_ACCOUNT` | The request includes an incorrect source account. Check the `sourceToken` value and try again. |
| `400 INVALID_DESTINATION_TOKEN` | The request includes an incorrect destination token. Check the `destinationToken` value and try again. |
| `400 QUALIFIED_KYC_TAXATION_REQUIRED` | Taxpayer verification is required before processing a transfer for this recipient. |
| `400 INSUFFICIENT_FUNDS` | The account doesn't have enough money to cover the requested amount. |

##### Commit a Transfer

These error codes are unique to the [`POST /transfers/{transfer-token}/status-transitions`](/content/api/v4/resources/transfers/commit) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 INVALID_ENUM_VALUE` | The request includes a value that is incorrect. [Read a list of expected values here](/content/api/v4/resources/transfers/commit). |
| `400 EXPIRED_TRANSFER` | The transfer request expired. Create a new transfer and commit it before 120 seconds. |

##### Retrieve a Transfer

These error codes are unique to the [`GET /transfers/{transfer-token}`](/content/api/v4/resources/transfers/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The transfer token or other identifier doesn't exist in the system. Check the request and try again. |


### Spendback

The following tables show unique error codes for the [`/transfers`](/content/api/v4/resources/spendback) Spendback API endpoints.

##### List Spendbacks

These error codes are unique to the [`GET /transfers`](/content/api/v4/resources/spendback/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a token or identifier that doesn't exist in the system. Check the request and try again. |


##### Create a Spendback

These error codes are unique to the [`POST /transfers`](/content/api/v4/resources/spendback/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 INVALID_SOURCE_ACCOUNT` | The request includes an incorrect source account. Check the `sourceToken` value and try again. |
| `400 INVALID_DESTINATION_TOKEN` | The request includes an incorrect destination token. Check the `destinationToken` value and try again. |
| `400 QUALIFIED_KYC_TAXATION_REQUIRED` | Taxpayer verification is required to process a transfer. Verify or submit your tax information on the Hyperwallet home page. Hyperwallet sends you an email once it has been reviewed. |
| `400 INSUFFICIENT_FUNDS` | The account doesn't have enough money to cover the requested amount. |

##### Commit a Spendback

These error codes are unique to the [`POST /transfers/{transfer-token}/status-transitions`](/content/api/v4/resources/spendback/commit) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 INVALID_ENUM_VALUE` | The request includes a value that is incorrect. [Read a list of expected values here](/content/api/v4/resources/transfers/commit). |
| `400 EXPIRED_TRANSFER` | The transfer request expired. Create a new transfer and commit it before 120 seconds. |

##### Retrieve a Spendback

These error codes are unique to the [`GET /transfers/{transfer-token}`](/content/api/v4/resources/spendback/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The transfer token or other identifier doesn't exist in the system. Check the request and try again. |

### Spendback Refunds

The following tables show unique error codes for the [`/transfers`](/content/api/v4/resources/spendback-refunds) Spendback Refunds API endpoints.

##### Create a Spendback Refund

These error codes are unique to the [`POST /transfers/{transfer-token}/refunds`](/content/api/v4/resources/spendback-refunds/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `400 INVALID_SOURCE_ACCOUNT` | The request includes an incorrect source account. Check the `sourceToken` value and try again. |
| `400 INVALID_DESTINATION_TOKEN` | The request includes an incorrect destination token. Check the `destinationToken` value and try again. |
| `400 QUALIFIED_KYC_TAXATION_REQUIRED` | Taxpayer verification is required before processing a transfer. Verify or submit your tax information on the Hyperwallet home page. Hyperwallet sends you an email once it has been reviewed. |
| `400 INSUFFICIENT_FUNDS` | The account doesn't have enough money to cover the requested amount. |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

##### Retrieve a Spendback Refund

These error codes are unique to the [`GET /transfers/{transfer-token}/refunds/{refund-token}`](/content/api/v4/resources/spendback-refunds/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |


### Balances

The following tables show unique error codes for the [`/balances`](/content/api/v4/resources/balances) API endpoints.

##### List User Balances

These error codes are unique to the [`GET /users/{user-token}/balances`](/content/api/v4/resources/balances/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

##### List Account Balances

These error codes are unique to the [`GET /programs/{program-token}/accounts/{account-token}/balances`](/content/api/v4/resources/balances/accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a program or funding account that doesn’t exist in the system. Check the program or account token and try again. |

##### List Prepaid Card Balances

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}/balances`](/content/api/v4/resources/balances/prepaid-cards-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or prepaid card that doesn’t exist in the system. Check the user or prepaid card token and try again. |


### Receipts

The following tables show unique error codes for the [`/receipts`](/content/api/v4/resources/receipts) API endpoints.

##### List User Receipts

These error codes are unique to the [`GET /users/{user-token}/receipts`](/content/api/v4/resources/receipts/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

##### List Prepaid Card Receipts

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}/receipts`](/content/api/v4/resources/receipts/prepaid-cards-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or prepaid card that doesn’t exist in the system. Check the user or prepaid card token and try again. |

##### List Account Receipts

These error codes are unique to the [`GET  /programs/{program-token}/accounts/{account-token}/receipts`](/content/api/v4/resources/receipts/accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a program or account that doesn’t exist in the system. Check the program or account token and try again. |


### Programs

The following tables show unique error codes for the [`/programs`](/content/api/v4/resources/programs) API endpoints.

##### Retrieve a Program

These error codes are unique to the [`GET /programs/{program-token}`](/content/api/v4/resources/programs/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a program that doesn’t exist in the system. Check the program token and try again. |


### Accounts

The following tables show unique error codes for the [`/accounts`](/content/api/v4/resources/accounts) API endpoints.

##### Retrieve an account

These error codes are unique to the [`GET /programs/{program-token}/accounts/{account-token}`](/content/api/v4/resources/accounts/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a program or account that doesn’t exist in the system. Check the program or account token and try again. |


### Transfer Methods Configurations

The following tables show unique error codes for the [`/transfer-method-configurations`](/content/api/v4/resources/transfer-method-configurations) API endpoints.

##### List Transfer Method Configurations

These error codes are unique to the [`GET /transfer-method-configurations?userToken={userToken}`](/content/api/v4/resources/transfer-method-configurations/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

##### Retrieve a Transfer Method Configuration

These error codes are unique to the [`GET /transfer-method-configurations?userToken={userToken}&country={country}&currency={currency}&type={type}&profileType={profileType}`](/content/api/v4/resources/transfer-method-configurations/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |


### Webhook Notifications

The following tables show unique error codes for the [`/webhook-notifications`](/content/api/v4/resources/webhook-notifications) API endpoints.

##### List Webhook Notifications

[Click here](#generic) for a list of generic errors.


##### Retrieve a Webhook Notification

These error codes are unique to the [`GET /webhook-notifications/{webhook-notification-token}`](/content/api/v4/resources/webhook-notifications/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a webhook that doesn't exist in the system. Check the webhook token and try again. |


### Status Transitions

The following tables show unique error codes for the [`/status-transitions`](/content/api/v4/resources/status-transitions) API endpoints.

##### List Status Transitions for a User

These error codes are unique to the [`GET /users/{user-token}/status-transitions`](/content/api/v4/resources/status-transitions/users-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or status transition that doesn't exist in the system. Check the user or status transition token and try again. |

##### Create a User Status Transition

These error codes are unique to the [`POST /users/{user-token}/status-transitions`](/content/api/v4/resources/status-transitions/users-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 CHANGE_ACCOUNT_STATUS_CLOSE_ACCOUNT_APPROVAL` | This account cannot be closed. Contact customer support. |
| `400 CHANGE_ACCOUNT_STATUS_INVALID_PAYEE_ACCOUNT_STATUS` | This is an invalid account status transiton.  |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn't on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/status-transitions/users-create). |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. Check the account status and try again. |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a user status transition, for example, when it is `LOCKED` or `FROZEN`. Check the wallet status and try again. |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The request includes a duplicate `email`. The `email` must be unique. |
| `400 DUPLICATE_EXTRA_ID_TYPE` | The request includes a duplicate `ClientUserID`. The `ClientUserID` must be unique. |

##### Retrieve a User Status Transition

These error codes are unique to the [`GET /users/{user-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/users-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or status transition that doesn't exist in the system. Check the user or status transition token and try again. |

##### List Status Transitions for a Business Stakeholder

These error codes are unique to the [`GET /users/{user-token}/business-stakeholders/{stakeholder-token}/status-transitions`](/content/api/v4/resources/status-transitions/business-stakeholders-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or status transition that doesn't exist in the system. Check the user or status transition token and try again. |

##### Create a Business Stakeholder Status Transition

These error codes are unique to the [`POST /users/{user-token}/business-stakeholders `](/content/api/v4/resources/business-stakeholders/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 CHANGE_ACCOUNT_STATUS_CLOSE_ACCOUNT_APPROVAL` | This account cannot be closed. Contact customer support. |
| `400 CHANGE_ACCOUNT_STATUS_INVALID_PAYEE_ACCOUNT_STATUS` | This is an invalid account status transiton.  |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn't on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/business-stakeholders/create). |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status cannot be changed. Contact customer support. |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The transition request creates a duplicate `email` in the system. |

##### Retrieve a Business Stakeholder Status Transition

These error codes are unique to the [`GET /users/{user-token}/business-stakeholders/{stakeholder-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/business-stakeholders-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or status transition that doesn't exist in the system. Check the user or status transition token and try again. |

##### List Status Transitions for a Bank Account

These error codes are unique to the [`GET /users/{user-token}/bank-accounts/{bank-account-token}/status-transitions`](/content/api/v4/resources/status-transitions/bank-accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank account that doesn't exist in the system. Check the user or bank account token and try again. |

##### Create a Bank Account Status Transition

These error codes are unique to the [`POST /users/{user-token}/bank-accounts/{bank-account-token}/status-transitions`](/content/api/v4/resources/status-transitions/bank-accounts-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank account that doesn't exist in the system. Check the user or bank account token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/bank-accounts/create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a bank account status transition. Check the wallet status and try again. |

##### Retrieve a Bank Account Status Transition

These error codes are unique to the [`GET /users/{user-token}/bank-accounts/{bank-account-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/bank-accounts-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, bank account, or status transition that doesn't exist in the system. Check the user, bank account, or status transition token and try again. |

##### List Status Transitions for a Bank Card

These error codes are unique to the [`GET /users/{user-token}/bank-cards/{bank-card-token}/status-transitions`](/content/api/v4/resources/status-transitions/bank-cards-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank card that doesn't exist in the system. Check the user or bank card token and try again. |

##### Create a Bank Card Status Transition

These error codes are unique to the [`POST /users/{user-token}/bank-cards/{bank-card-token}/status-transitions`](/content/api/v4/resources/status-transitions/bank-cards-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank card that doesn't exist in the system. Check the user or bank card token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/status-transitions/bank-cards-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a bank card status transition. Check the wallet status and try again. |

##### Retrieve a Bank Card Status Transition

These error codes are unique to the [`GET /users/{user-token}/bank-cards/{bank-card-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/bank-cards-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, bank account, or status transition that doesn't exist in the system. Check the user, bank account, or status transition token and try again. |

##### List Status Transitions for a PayPal Account

These error codes are unique to the [`GET /users/{user-token}/paypal-accounts/{paypal-account-token}/status-transitions`](/content/api/v4/resources/status-transitions/paypal-accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or PayPal account that doesn't exist in the system. Check the user or PayPal account token and try again.  |

##### Create a PayPal Account Status Transition

These error codes are unique to the [`POST /users/{user-token}/PayPal-accounts/{paypal-account-token}/status-transitions`](/content/api/v4/resources/status-transitions/paypal-accounts-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or PayPal account that doesn't exist in the system. Check the user or PayPal account token and try again.  |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/status-transitions/paypal-accounts-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a PayPal account status transition. Check the wallet status and try again. |

##### Retrieve a PayPal Account Status Transition

These error codes are unique to the [`GET /users/{user-token}/PayPal-accounts/{paypal-account-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/paypal-accounts-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, PayPal account, or status transition that doesn't exist in the system. Check the user, PayPal account, or status transition token and try again. |

##### List Status Transitions for a Venmo Account

These error codes are unique to the [`GET /users/{user-token}/venmo-accounts/{venmo-account-token}/status-transitions`](/content/api/v4/resources/status-transitions/venmo-accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or Venmo account that doesn't exist in the system. Check the user or Venmo account token and try again. |

##### Create a Venmo Account Status Transition

These error codes are unique to the [`POST /users/{user-token}/venmo-accounts/{venmo-account-token}/status-transitions`](/content/api/v4/resources/status-transitions/venmo-accounts-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or Venmo account that doesn't exist in the system. Check the user or Venmo account token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/status-transitions/venmo-accounts-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a Venmo account status transition. Check the wallet status and try again. |

##### Retrieve a Venmo Account Status Transition

These error codes are unique to the [`GET /users/{user-token}/venmo-accounts/{venmo-account-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/venmo-accounts-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, Venmo account, or status transition that doesn't exist in the system. Check the user, Venmo account, or status transition token and try again. |


##### List Status Transitions for a Prepaid Card

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}/status-transitions`](/content/api/v4/resources/status-transitions/prepaid-cards-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank account that doesn't exist in the system. Check the user or bank account token and try again. |

##### Create a Prepaid Card Status Transition

These error codes are unique to the [`POST /users/{user-token}/prepaid-cards/{prepaid-card-token}/status-transitions`](/content/api/v4/resources/status-transitions/prepaid-cards-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or prepaid card that doesn't exist in the system. Check the user or bank account token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect transition. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/prepaid-cards/create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a prepaid card status transition. Check the wallet status and try again. |

##### Retrieve a Prepaid Card Status Transition

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/prepaid-cards-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, prepaid card, or status transition that doesn't exist in the system. Check the user, prepaid card, or status transition token and try again. |

##### List Status Transitions for a Paper Check

These error codes are unique to the [`GET /users/{user-token}/paper-checks/{paper-check-token}/status-transitions`](/content/api/v4/resources/status-transitions/paper-checks-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or paper check that doesn't exist in the system. Check the user or paper check token and try again. |

##### Create a Paper Check Status Transition

These error codes are unique to the [`POST /users/{user-token}/paper-checks/{paper-check-token}/status-transitions`](/content/api/v4/resources/status-transitions/paper-checks-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or paper check that doesn't exist in the system. Check the user or paper check token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/paper-checks/create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a paper check status transition. Check the wallet status and try again. |

##### Retrieve a Paper Check Status Transition

These error codes are unique to the [`GET /users/{user-token}/bank-accounts/{bank-account-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/bank-accounts-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, paper check, or status transition that doesn't exist in the system. Check the user, paper check, or status transition token and try again. |





##### List Status Transitions for a Payment

These error codes are unique to the [`GET /payments/{payment-token}/status-transitions`](/content/api/v4/resources/status-transitions/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment that doesn’t exist in the system. Check the payment token and try again. |

##### Create a Payment Status Transition

These error codes are unique to the [`POST /payments/{payment-token}/status-transitions`](/content/api/v4/resources/status-transitions/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment that doesn’t exist in the system. Check the payment token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/status-transitions/create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a payment status transition. Check the wallet status and try again. |

##### Retrieve a Payment Status Transition

These error codes are unique to the [`GET /payments/{payment-token}/status-transitions/{status-transition-token}`](/content/api/v4/resources/status-transitions/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment or status transition that doesn’t exist in the system. Check the payment or status transition token and try again. |

##### Create a PayPal Payment Status Transition

These error codes are unique to the [`POST /payments/{payment-token}/status-transitions`](/content/api/v4/resources/status-transitions/paypal-payment-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment that doesn’t exist in the system. Check the payment token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/status-transitions/paypal-payment-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a payment status transition. Check the wallet status and try again. |

##### Create a Venmo Payment Status Transition

These error codes are unique to the [`POST /payments/{payment-token}/status-transitions`](/content/api/v4/resources/status-transitions/venmo-payment-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment that doesn’t exist in the system. Check the payment token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](/content/api/v4/resources/status-transitions/venmo-payment-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a payment status transition. Check the wallet status and try again. |

### Authentication Token

The following table shows unique error codes for the [`/authentication-token/create`](/content/api/v4/resources/authentication-token/create) API endpoint.

##### Create Authentication Token

These error codes are unique to the [`POST /users/{user-token}/authentication-token`](/content/api/v4/resources/authentication-token/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status Code and Error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a request to create an authentication token. Check the wallet status and try again. |


## Pagination [/overview/pagination]

### Pagination [GET]

Each `GET` call to retrieve a list of resources will return a finite number of matching resources in the response, determined by the following arguments:

Argument | Description | Example
-------- | ----------- | -------
**limit** | Specifies the number of matching resources returned in the page. Ranges from 1 to 1000. By default, `limit=100`, i.e. each page of the response will include 100 matching resources. | `limit=15`

All list responses will include:

* `limit` - as supplied in the query
* `data` - an array containing matching resources
* `links` - an array of [HATEOAS][HATEOAS] links
* `hasNextPage` - boolean value indicating whether there are more pages after the current page. True for every page except the last page
* `hasPreviousPage` - boolean value indicating whether there are pages before the current page. True for every page except the first page

Additionally, if the result is larger than one page as set by `limit`, the `links` array will automatically include `next` and `previous` links for corresponding pages:

* The `previous` link will only appear if there is a page preceding the current one
* The `next` link will only appear if there is a page after the current one

The example request depicts a `GET` call to retrieve a list of transfers. Since `limit=2`, each page will have 2 matching resources per page. In this case, there are 7 total transfers, so this page returns 2 results.

+ Request

    curl -X "GET" "https://uat-api.paylution.com/rest/v4/transfers?limit=2" \
        -u "restapiuser@12345678:myAccPassw0rd" \
        -H "Accept: application/json"

+ Response 200 (application/json)

    {
      "hasNextPage" : false,
      "hasPreviousPage" : false,
      "limit" : 2,
      "data" : [ {
        "token" : "trf-6bf3b5b2-21b0-4148-8c0e-6a44919ce6f9",
        "status" : "SCHEDULED",
        "createdOn" : "2019-06-16T20:30:19",
        "clientTransferId" : "42556512",
        "sourceToken" : "trm-33374cd4-e84f-402e-8773-5539fbbe1897",
        "sourceAmount" : "10.01",
        "sourceFeeAmount" : "0.00",
        "sourceCurrency" : "CAD",
        "destinationToken" : "act-67b680fe-9ae8-46f2-953b-7057d8d9cf92",
        "destinationAmount" : "10.01",
        "destinationFeeAmount" : "0.75",
        "destinationCurrency" : "CAD",
        "notes" : "create CAD DDT via IS",
        "memo" : "Transfer123456",
        "purpose" : "OTHER"
      }, {
        "token" : "trf-3ff65674-a867-43f3-8893-5dff52342b09",
        "status" : "SCHEDULED",
        "createdOn" : "2019-07-24T12:16:52",
        "clientTransferId" : "16301803",
        "sourceToken" : "trm-1d2eb7d9-9a8e-4e7e-b2b4-49a9909ae25c",
        "sourceAmount" : "10.01",
        "sourceFeeAmount" : "0.00",
        "sourceCurrency" : "CAD",
        "destinationToken" : "act-67b680fe-9ae8-46f2-953b-7057d8d9cf92",
        "destinationAmount" : "10.01",
        "destinationFeeAmount" : "0.75",
        "destinationCurrency" : "CAD",
        "notes" : "create CAD DDT via IS",
        "memo" : "Transfer123456",
        "purpose" : "OTHER"
      } ],
      "links" : [ {
        "params" : {
          "rel" : "self"
        },
        "href" : "https://uat-api.paylution.com/rest/v4/transfers?after=trf-6bf3b5b2-21b0-4148-8c0e-6a44919ce6f9&limit=2"
      } ]
    }

## Sorting [/overview/sorting]

### Sorting [GET]

You can sort `GET` lists by providing a sortable attribute relevant to the resource. Additionally, lists can be sorted in ascending or descending order using the following parameter and prefixes:

Argument | Sorting Prefix | Description | Example
-------- | -------------- | ----------- | -------
**sortBy** | \+ | Sorts the result in ascending order of the `sortBy` attribute | `sortBy=+createdOn`
 | \- | Sorts the result in descending order of the `sortBy` attribute | `sortBy=-createdOn`

>  Note: sorting by + is functionally equivalent to omitting the + prefix.

Which attributes are sortable will depend on the queried resource. You can sort by at most one attribute per request.

The example request sorts a list of users in descending order of the date they were created (`-createdOn`). As depicted, the `sortBy` argument can be used alongside arguments specific to the resource or sub-resource (`status`) and those for [pagination][pagination] such as `limit`.

+ Request

    curl -X "GET" "https://uat-api.paylution.com/rest/v4/users?limit=2&sortBy=-createdOn" \
        -u "restapiuser@12345678:myAccPassw0rd" \
        -H "Accept: application/json"

+ Response 200 (application/json)

    {
      "hasNextPage" : true,
      "hasPreviousPage" : true,
      "limit" : 2,
      "data" : [ {
        "token" : "usr-0c3cacaf-408d-44b1-98a2-9bb3fea91bb3",
        "status" : "PRE_ACTIVATED",
        "createdOn" : "2019-12-15T05:23:25",
        "clientUserId" : "CSdgPhHRkR",
        "profileType" : "INDIVIDUAL",
        "firstName" : "John",
        "lastName" : "Smith",
        "dateOfBirth" : "1980-01-01",
        "email" : "johnsmith@emaill.com",
        "addressLine1" : "123 Main Street",
        "city" : "New York",
        "stateProvince" : "NY",
        "country" : "US",
        "postalCode" : "10016",
        "language" : "en",
        "programToken" : "prg-83836cdf-2ce2-4696-8bc5-f1b86077238c",
        "links" : [ {
          "params" : {
            "rel" : "self"
          },
          "href" : "https://uat-api.paylution.com/rest/v4/users/usr-0c3cacaf-408d-44b1-98a2-9bb3fea91bb3"
        } ]
      }, {
        "token" : "usr-b86ab524-2787-46e2-b536-5a70e37349f7",
        "status" : "PRE_ACTIVATED",
        "createdOn" : "2019-11-01T17:08:51",
        "clientUserId" : "CS2JkNbLIL",
        "profileType" : "INDIVIDUAL",
        "firstName" : "Joan",
        "lastName" : "Smith",
        "dateOfBirth" : "1980-01-01",
        "email" : "joansmith@email.com",
        "addressLine1" : "123 Main Street",
        "city" : "New York",
        "stateProvince" : "NY",
        "country" : "US",
        "postalCode" : "10016",
        "language" : "en",
        "programToken" : prg-83836cdf-2ce2-4696-8bc5-f1b86077238c",
        links" : [ {
          params" : {
            rel : "self
          },
          "href" : "https://uat-api.paylution.com/rest/v4/users/usr-b86ab524-2787-46e2-b536-5a70e37349f7"
        } ]
      } ],
      "links" : [ {
        "params" : {
          "rel" : "self"
        },
        "href" : "https://uat-api.paylution.com/rest/v4/users?limit=2&sortBy=-createdOn"
      }, {
        "params" : {
          "rel" : "next"
        },
        "href" : "https://uat-api.paylution.com/rest/v4/users?limit=2&sortBy=-createdOn"
      }, {
        "params" : {
          "rel" : "last"
        },
        "href" : "https://uat-api.paylution.com/rest/v4/users?limit=2&sortBy=-createdOn"
      } ]
    }

## HATEOAS [/overview/hateoas]

### HATEOAS [GET]

Responses will include an array of <a "http://en.wikipedia.org/wiki/HATEOAS" target="_blank">Hypermedia as the Engine of Application State</a> (HATEOAS) links that enable you to interact and construct an API flow without having to hard-code application logic. The `links` array will contain:

* `params` - this object includes a `rel` attribute describing how the link relates to the state of the requested resource
* `href` - this attribute points to the full URL of the current resource

Which links are returned will depend on the request. `POST`, `PUT` and `GET` calls will always include a `self` link for each returned resource. `GET` calls that retrieve a multi-page list will additionally include [pagination links][pagination].

+ Response 200 (application/json)

    {
      "links" : [ {
        "params" : {
          "rel" : "self"
        },
        "href" : "https://uat-api.paylution.com/rest/v4/users/usr-b86ab524-2787-46e2-b536-5a70e37349f7"
      } ]
    }

## What's New in V4 [overview/updates]

### What's New in V4 [GET]

Hyperwallet is pleased to announce the release of the new API version 4. This version hosts a variety of updates intended to make the APIs faster while providing more functionality for you.

> Note: This version cannot be used in conjunction with any other version, meaning all requests will need to be made using version 4.

## New Endpoints

API version 4 brings the functionality to verify your payees using REST requests. The new endpoints are as follows:

* [Create a Business Stakeholder](/content/api/v4/resources/business-stakeholders/create)
* [Update a Business Stakeholder](/content/api/v4/resources/business-stakeholders/update)
* [List Business Stakeholders](/content/api/v4/resources/business-stakeholders/list)

For more information about how to verify payees using API v4, see the [Verify Payee](/content/embedded-payout-experience/v1/verify-payee/api) section of the Embedded Payout Experience.

## Changes to Existing Endpoints

Updates have been made to the Create a User and Update a User endpoints to include extra verification statuses for use when verifying your payee. You can also upload documents, if required, in order to verify to a payee account.

* [Create a User](/content/api/v4/resources/users/create)
* [Update a User](/content/api/v4/resources/users/update)

## Changes to List Endpoints

The filters and sort clauses that can be used for any list endpoint have been updated in order to provide the most streamlined experience and to return the most relevant information you will need.

## Changes to SDKs

API v4 is supported by version 2 of the SDKs. API v3 is supported by version 1 of the SDKs.

| SDK | API v3<br>Supported | API v4<br>Supported |
| --- | --- | --- |
| Java | v1.x.x | v2.x.x |
| Node | v1.x.x | v2.x.x |
| PHP | v1.x.x | v2.x.x |
| Python | v1.x.x | - |

The Python SDK is not supported in API v4 but will continue to be supported in API v3.

## Changes to Business Stakeholders

API version 4 separates the process of adding a business profile and a business stakeholder.

You can't add a business profile and a business stakeholder in a single `POST` call to the [Create a User](/content/api/v4/resources/users/create) endpoint. When you pass `BUSINESS` as the `profileType` parameter in a Create a User API call, the API ignores:

* `firstName`
* `middleName`
* `lastName`
* `dateOfBirth`

Add a stakeholder to a business by making a `POST` call to the [Create a Business Stakeholder](/content/api/v4/resources/business-stakeholders/create) endpoint:

* Pass the business profile's `user-token` in the request path.
* Pass the stakeholder's information in the request body.

## Other Changes

The method of [pagination](/content/api/v4/overview/pagination) has been changed to a cursor based type which means that responses for all "List" endpoints are faster than ever especially for large datasets.

* List responses now contain Boolean values that indicate whether more records exist before and after the current page. If more records do exist, a link is included which directs to the next page of results. This method means that duplicate records will not be retrieved if new entries are added between requests for pages.
* Number of records returned has been increased to 1000 from 100
* Default number of records returned has been increased to 100 from 10 if no limit is set
* The count field has been removed from responses
* The offset field has been removed from responses

## Updating to API v4

In order to use API v4, an update to your program is required. Talk to your account manager or the Hyperwallet Production Support team to get started.
