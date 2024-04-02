# Hyperwallet Error Handling

## Error List

This section lists errors that Hyperwallet API endpoints return.

<a name="generic"></a>

### Generic

These error codes are used by all Hyperwallet endpoints:

| Status code and error | Description |
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

The following tables show unique error codes for the [`/users`](https://docs.hyperwallet.com//content/api/v4/resources/users) API endpoints.

#### Create a User

These error codes are unique to the [`POST /users`](https://docs.hyperwallet.com//content/api/v4/resources/users/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of our user requirements here](https://docs.hyperwallet.com//content/api/v4/resources/users/create). |
| `400 DUPLICATE_CLIENT_USER_ID` | The request includes a duplicate `clientUserId`. The `clientUserId` must be unique. |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The request includes a duplicate `email`. The `email` must be unique. |
| `400 INVALID_COUNTRY` | The request includes a country that is invalid, sanctioned, or restricted. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that is incorrect. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/users/create). |

#### Retrieve a User

These error codes are unique to the [`GET /users/{user-token}`](https://docs.hyperwallet.com//content/api/v4/resources/users/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 INVALID_WALLET_STATUS` | The wallet status is invalid. [Read a list of valid wallet status options here](https://docs.hyperwallet.com//content/api/v4/resources/users/retrieve). |
| `404 RESOURCE_NOT_FOUND` | This user doesn't exist in the system. Check the user token and try again.  |

#### Update a User

These error codes are unique to the [`PUT /users/{user-token}`](https://docs.hyperwallet.com//content/api/v4/resources/users/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements.  [Read a list of user requirements here](https://docs.hyperwallet.com//content/api/v4/resources/users/update). |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The request includes a duplicate `clientUserId`. The `clientUserId` must be unique. |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The request includes an `email` that is already registered in the system. The `email` must be unique. |
| `400 INVALID_COUNTRY` | The request includes a country that is invalid, sanctioned, or restricted. |
| `400 INVALID_ENUM_VALUE` | The request includes an incorrect value. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/users/create). |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to update a user. |

### Business Stakeholder

The following tables show unique error codes for the [`/users`](https://docs.hyperwallet.com//content/api/v4/resources/users) API endpoints.

#### List Business Stakeholders

These error codes are unique to the [`GET /users/{user-token}/business-stakeholders`](https://docs.hyperwallet.com//content/api/v4/resources/business-stakeholders/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again.  |

#### Create a Business Stakeholder

These error codes are unique to the [`POST /users/{user-token}/business-stakeholders`](https://docs.hyperwallet.com//content/api/v4/resources/business-stakeholders/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/business-stakeholders/create). |
| `400 INVALID_COUNTRY` | The request includes a country that is invalid, sanctioned, or restricted. |

#### Update a Business Stakeholder

These error codes are unique to the [`PUT /users/{user-token}/business-stakeholders/{stakeholder-token}`](https://docs.hyperwallet.com//content/api/v4/resources/business-stakeholders/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/business-stakeholders/update). |
| `400 INVALID_DOCUMENT_PARTS` | The request includes the wrong documents. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 MISSING_REQUEST_PART_FILE` | The request doesn't include a file required for this operation. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 VERIFICATION_NOT_REQUIRED` | The request includes a document when verification isn't required. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 INVALID_DOCUMENT_TYPE` | The request includes an incorrect document type. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 UNSUPPORTED_FILE_TYPE` | The request uploaded a file type that isn't supported. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 MISSING_COUNTRY_FOR_DOCUMENT` | 1 or more documents need to include a country or region. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 DOCUMENT_TYPE_REQUIRED` | You need to provide a document type for 1 or more documents. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 FILE_SIZE_EXCEEDS_MAXIMUM` | The file size exceeds the maximum allowable file size. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 INVALID_MESSAGE` | An application error caused the request to fail. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 EMPTY_FILE_UPLOADED` | The request includes an empty file. |
| `400 INVALID_PARAMETER` | The request includes a blank `type` parameter. [Read a list of requirements here](https://docs.hyperwallet.com//content/embedded-payout-experience/v1/verify-payee/api/business-payee). |
| `400 MAXIMUM_UPLOAD_FILES_EXCEEDED` | This request exceeds the maximum number of file uploads. |


### Bank Accounts

The following tables show unique error codes for the [`/bank-accounts`](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts) API endpoints.

#### Create a Bank Account

These error codes are unique to the [`POST /users/{user-token}/bank-accounts`](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank account that doesn't exist in the system. Check the user or bank account token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/create?profileType=Individual&accountType=BANK_ACCOUNT). |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds an account that is already in the Hyperwallet system. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. || `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 EXTERNAL_ACCOUNT_TYPE_NOT_SUPPORTED` | This transfer method is not configured for your program. Contact the customer support team if you would like this enabled. |

#### Retrieve a Bank Account

These error codes are unique to the [`GET /users/{user-token}/bank-accounts/{bank-account-token}`](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

#### Update a Bank Account

These error codes are unique to the [`PUT /users/{user-token}/bank-accounts/{bank-account-token}`](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/create?profileType=Individual&accountType=BANK_ACCOUNT). |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds an account that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn't support updates. [Read the list of fields that can be updated](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/update?profileType=Individual&accountType=BANK_ACCOUNT&country=United+States&currency=USD). |


### Bank Cards

The following tables show unique error codes for the [`/bank-cards`](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards) API endpoints.

#### Create a Bank Card

These error codes are unique to the [`POST /users/{user-token}/bank-cards`](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 CARD_NOT_SUPPORTED` | The request includes a card that we don't support. [Read a list of supported cards here](https://docs.hyperwallet.com//content/transfer-methods/v1/bank-card#payee-availability) |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards/create). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a card that is already in the Hyperwallet system. If this is a valid request, reach out to our customer support team to add the bank card. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `400 EXTERNAL_ACCOUNT_TYPE_NOT_SUPPORTED` | This transfer method is not configured for your program. Contact the customer support team if you would like this enabled. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |

#### Retrieve a Bank Card

These error codes are unique to the [`GET /users/{user-token}/bank-cards/{bank-card-token}`](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank card that doesn't exist in the system. Check the user or bank card token and try again.  |

#### Update a Bank Card

These error codes are unique to the [`PUT /users/{user-token}/bank-cards/{bank-card-token}`](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank card doesn't exist in the system. Check the user or bank card token and try again. |
| `400 CARD_NOT_SUPPORTED` | The request includes a card that we do not support. [Read a list of supported cards here](https://docs.hyperwallet.com//content/transfer-methods/v1/bank-card#payee-availability). |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements.  [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards/update). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a card that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn't support updates. [Read the list of fields that can be updated](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards/update).  |

### PayPal Accounts

The following tables show unique error codes for the [`/paypal-accounts`](https://docs.hyperwallet.com//content/api/v4/resources/paypal-accounts) API endpoints.

#### Create a PayPal Account

These error codes are unique to the [`POST /users/{user-token}/paypal-accounts`](https://docs.hyperwallet.com//content/api/v4/resources/paypal-accounts/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/paypal-accounts/create). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a transfer method that is already in the Hyperwallet system. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `400 EXTERNAL_ACCOUNT_TYPE_NOT_SUPPORTED` | This transfer method is not configured for your program. Contact the customer support team if you would like this enabled. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |

#### Retrieve a PayPal Account

These error codes are unique to the [`GET /users/{user-token}/paypal-accounts/{paypal-account-token}`](https://docs.hyperwallet.com//content/api/v4/resources/paypal-accounts/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or PayPal account that doesn’t exist in the system. Check the user or PayPal account token and try again. |

#### Update a PayPal Account

These error codes are unique to the [`PUT /users/{user-token}/paypal-accounts/{paypal-account-token}`](https://docs.hyperwallet.com//content/api/v4/resources/paypal-accounts/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or PayPal account that doesn’t exist in the system. Check the user or PayPal account token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/paypal-accounts/create). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds an account that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn't support updates. [Read the list of fields that can be updated](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards/update). |

### Venmo Accounts

The following tables show unique error codes for the [`/venmo-accounts`](https://docs.hyperwallet.com//content/api/v4/resources/venmo-accounts) API endpoints.

#### Create a Venmo Account

These error codes are unique to the [`POST /users/{user-token}/venmo-accounts`](https://docs.hyperwallet.com//content/api/v4/resources/venmo-accounts/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/venmo-accounts/create). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a Venmo account that is already in the Hyperwallet system. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `400 EXTERNAL_ACCOUNT_TYPE_NOT_SUPPORTED` | This transfer method is not configured for your program. Contact the customer support team if you would like this enabled. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |

#### Retrieve a Venmo Account

These error codes are unique to the [`GET /users/{user-token}/venmo-accounts/{venmo-account-token}`](https://docs.hyperwallet.com//content/api/v4/resources/venmo-accounts/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or Venmo account that doesn’t exist in the system. Check the user or Venmo account token and try again. |

#### Update a Venmo Account

These error codes are unique to the [`PUT /users/{user-token}/venmo-accounts/{venmo-account-token}`](https://docs.hyperwallet.com//content/api/v4/resources/venmo-accounts/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or Venmo account that doesn’t exist in the system. Check the user or Venmo account token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/venmo-accounts/update). |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds a Venmo account that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn’t support updates. [Read the list of fields that can be updated](https://docs.hyperwallet.com//content/api/v4/resources/bank-cards/update). |

### Prepaid Cards

The following tables show unique error codes for the [`/users/{user-token}/prepaid-cards`](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards) API endpoints.

#### List Prepaid Cards

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards`](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

#### Create a Prepaid Card

These error codes are unique to the [`POST /users/{user-token}/prepaid-cards`](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/create). |
| `400 INVALID_PREPAID_CARD_PACKAGE` | The request includes an incorrect prepaid card package name or identifier. |
| `400 MAX_CARDS_PROGRAM_CONFIG` | This account already has a prepaid card associated with it. Your program configuration allows a maximum of 1 prepaid card per account. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/create). |
| `400 PENDING_ADD_CARD_REQUEST` | The request wasn't successful because this wallet has a pending request to add a prepaid card. |
| `400 ATTACH_CARD_CONNECTION_ERROR` | A connection error prevented this request from successfully adding a prepaid card to the wallet. Wait a few minutes and try your request again. |
| `400 ATTACH_CARD_ERROR` | An error prevented this request from successfully adding a prepaid card to the wallet. |


#### Replace a Prepaid Card

These error codes are unique to the [`POST /users/{user-token}/prepaid-cards`](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/replace) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/create). |
| `400 INVALID_PREPAID_CARD_PACKAGE` | The request includes an incorrect prepaid card package name or identifier. |
| `400 MAX_CARDS_PROGRAM_CONFIG` | This account already has a prepaid card associated with it. Your program configuration allows a maximum of 1 card request per account. |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | A bank account registration request can't have more than 2 registrations. You can register a primary and a secondary card. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/create). |
| `400 PENDING_ADD_CARD_REQUEST` | The request wasn't successful because this wallet has a pending request to add a prepaid card. |
| `400 ATTACH_CARD_CONNECTION_ERROR` | A connection error prevented this request from successfully adding a prepaid card to the wallet. Wait a few minutes and try your request again. |
| `400 ATTACH_CARD_ERROR` | An error prevented this request from successfully adding a prepaid card to the wallet. |

#### Retrieve a Prepaid Card

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}`](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or prepaid card that doesn’t exist in the system. Check the user or prepaid card token and try again. |

### Paper Checks

The following tables show unique error codes for the [`/users/{user-token}/paper-checks`](https://docs.hyperwallet.com//content/api/v4/resources/paper-checks) API endpoints.

#### List Paper Checks

These error codes are unique to the [`GET /users/{user-token}/paper-checks`](https://docs.hyperwallet.com//content/api/v4/resources/paper-checks/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

#### Create a Paper Check

These error codes are unique to the [`POST /users/{user-token}/paper-checks`](https://docs.hyperwallet.com//content/api/v4/resources/paper-checks/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don’t meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/paper-checks/create). |
| `400 BANK_ACCOUNT_REGISTRATION_LIMIT_EXCEEDED` | This account already has the maximum number of allowed transfer methods. |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

#### Retrieve a Paper Check

These error codes are unique to the [`GET /users/{user-token}/paper-checks/{paper-check-token}`](https://docs.hyperwallet.com//content/api/v4/resources/paper-checks/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or paper check that doesn’t exist in the system. Check the user or paper check token and try again. |

#### Update a Paper Check

These error codes are unique to the [`PUT /paper-checks/{paper-check-token}`](https://docs.hyperwallet.com//content/api/v4/resources/paper-checks/update) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The user or the bank account doesn't exist. Check and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/create?profileType=Individual&accountType=BANK_ACCOUNT). |
| `400 ACCOUNT_STATUS_FLAGGED` | The account is flagged, typically for risk reasons. |
| `400 DUPLICATE_EXTERNAL_ACCOUNT_CREATION` | This request adds an account that is already in the Hyperwallet system. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 NON_UPDATEABLE_FIELD` | The request passes a value to a field that doesn't support updates. [Read the list of fields that can be updated](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/update?profileType=Individual&accountType=BANK_ACCOUNT&country=United+States&currency=USD). |


### Transfer Methods

The following table shows unique error codes for the [`/users/{user-token}/transfer-methods`](https://docs.hyperwallet.com//content/api/v4/resources/transfer-methods) API endpoint.

#### List Transfer Methods

These error codes are unique to the [`GET /users/{user-token}/transfer-methods`](https://docs.hyperwallet.com//content/api/v4/resources/transfer-methods) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |


### Payments

The following tables show unique error codes for the [`/payments`](https://docs.hyperwallet.com//content/api/v4/resources/payments) API endpoints.

#### Create a Payment

These error codes are unique to the [`POST /payments`](https://docs.hyperwallet.com//content/api/v4/resources/payments/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | This request includes a user that doesn't exist in the system. Check the user token and try again. |
| `400 CONSTRAINT_VIOLATIONS` | The request includes values that don't meet our requirements. [Read a list of requirements here](https://docs.hyperwallet.com//content/api/v4/resources/payments/create). |
| `400 ACCOUNT_STATUS_FLAGGED` | The request issues a payment to an account that's flagged. Accounts are typically flagged for risk reasons. Review your request or provide another bank account. |
| `400 INCORRECT_FUNDING_PROGRAM` | This request is trying to initiate a payment from an incorrect funding program. Check the `programToken` and try again. |
| `400 INSUFFICIENT_FUNDS` | The funding account doesn't have sufficient funds for the requested payment amount. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support requests to add a transfer method. A wallet should be in an `OPEN` status to register a transfer method. |
| `400 LIMIT_SUBCEEDED` | The amount is too low for the transfer method. |
| `400 LIMIT_SUCCEEDED` | The amount is too high for the transfer method. |
| `400 MINIMUM_CONVERSION_AMOUNT_NOT_REACHED` | The amount is too low for foreign exchange (FX) conversion. |

#### Retrieve a Payment

These error codes are unique to the [`GET /payments/{payment-token}`](https://docs.hyperwallet.com//content/api/v4/resources/payments/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment token that doesn't exist. Check the payment token and try again. |

### Transfers

The following tables show unique error codes for the [`/transfers`](https://docs.hyperwallet.com//content/api/v4/resources/transfers) API endpoints.

#### List Transfers

These error codes are unique to the [`GET /transfers`](https://docs.hyperwallet.com//content/api/v4/resources/transfers/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a token or identifier that doesn't exist in the system. Check the request and try again. |

#### Create a Transfer

These error codes are unique to the [`POST /transfers`](https://docs.hyperwallet.com//content/api/v4/resources/transfers/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 INVALID_SOURCE_ACCOUNT` | The request includes an incorrect source account. Check the `sourceToken` value and try again. |
| `400 INVALID_DESTINATION_TOKEN` | The request includes an incorrect destination token. Check the `destinationToken` value and try again. |
| `400 QUALIFIED_KYC_TAXATION_REQUIRED` | Taxpayer verification is required before processing a transfer for this recipient. |
| `400 INSUFFICIENT_FUNDS` | The account doesn't have enough money to cover the requested amount. |

#### Commit a Transfer

These error codes are unique to the [`POST /transfers/{transfer-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/transfers/commit) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 INVALID_ENUM_VALUE` | The request includes a value that is incorrect. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/transfers/commit). |
| `400 EXPIRED_TRANSFER` | The transfer request expired. Create a new transfer and commit it before 120 seconds. |

#### Retrieve a Transfer

These error codes are unique to the [`GET /transfers/{transfer-token}`](https://docs.hyperwallet.com//content/api/v4/resources/transfers/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The transfer token or other identifier doesn't exist in the system. Check the request and try again. |


### Spendback

The following tables show unique error codes for the [`/transfers`](https://docs.hyperwallet.com//content/api/v4/resources/spendback) Spendback API endpoints.

#### List Spendbacks

These error codes are unique to the [`GET /transfers`](https://docs.hyperwallet.com//content/api/v4/resources/spendback/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a token or identifier that doesn't exist in the system. Check the request and try again. |


#### Create a Spendback

These error codes are unique to the [`POST /transfers`](https://docs.hyperwallet.com//content/api/v4/resources/spendback/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 INVALID_SOURCE_ACCOUNT` | The request includes an incorrect source account. Check the `sourceToken` value and try again. |
| `400 INVALID_DESTINATION_TOKEN` | The request includes an incorrect destination token. Check the `destinationToken` value and try again. |
| `400 QUALIFIED_KYC_TAXATION_REQUIRED` | Taxpayer verification is required to process a transfer. Verify or submit your tax information on the Hyperwallet home page. Hyperwallet sends you an email once it has been reviewed. |
| `400 INSUFFICIENT_FUNDS` | The account doesn't have enough money to cover the requested amount. |

#### Commit a Spendback

These error codes are unique to the [`POST /transfers/{transfer-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/spendback/commit) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 INVALID_ENUM_VALUE` | The request includes a value that is incorrect. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/transfers/commit). |
| `400 EXPIRED_TRANSFER` | The transfer request expired. Create a new transfer and commit it before 120 seconds. |

#### Retrieve a Spendback

These error codes are unique to the [`GET /transfers/{transfer-token}`](https://docs.hyperwallet.com//content/api/v4/resources/spendback/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The transfer token or other identifier doesn't exist in the system. Check the request and try again. |

### Spendback Refunds

The following tables show unique error codes for the [`/transfers`](https://docs.hyperwallet.com//content/api/v4/resources/spendback-refunds) Spendback Refunds API endpoints.

#### Create a Spendback Refund

These error codes are unique to the [`POST /transfers/{transfer-token}/refunds`](https://docs.hyperwallet.com//content/api/v4/resources/spendback-refunds/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `400 INVALID_SOURCE_ACCOUNT` | The request includes an incorrect source account. Check the `sourceToken` value and try again. |
| `400 INVALID_DESTINATION_TOKEN` | The request includes an incorrect destination token. Check the `destinationToken` value and try again. |
| `400 QUALIFIED_KYC_TAXATION_REQUIRED` | Taxpayer verification is required before processing a transfer. Verify or submit your tax information on the Hyperwallet home page. Hyperwallet sends you an email once it has been reviewed. |
| `400 INSUFFICIENT_FUNDS` | The account doesn't have enough money to cover the requested amount. |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

#### Retrieve a Spendback Refund

These error codes are unique to the [`GET /transfers/{transfer-token}/refunds/{refund-token}`](https://docs.hyperwallet.com//content/api/v4/resources/spendback-refunds/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |


### Balances

The following tables show unique error codes for the [`/balances`](https://docs.hyperwallet.com//content/api/v4/resources/balances) API endpoints.

#### List User Balances

These error codes are unique to the [`GET /users/{user-token}/balances`](https://docs.hyperwallet.com//content/api/v4/resources/balances/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

#### List Account Balances

These error codes are unique to the [`GET /programs/{program-token}/accounts/{account-token}/balances`](https://docs.hyperwallet.com//content/api/v4/resources/balances/accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a program or funding account that doesn’t exist in the system. Check the program or account token and try again. |

#### List Prepaid Card Balances

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}/balances`](https://docs.hyperwallet.com//content/api/v4/resources/balances/prepaid-cards-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or prepaid card that doesn’t exist in the system. Check the user or prepaid card token and try again. |


### Receipts

The following tables show unique error codes for the [`/receipts`](https://docs.hyperwallet.com//content/api/v4/resources/receipts) API endpoints.

#### List User Receipts

These error codes are unique to the [`GET /users/{user-token}/receipts`](https://docs.hyperwallet.com//content/api/v4/resources/receipts/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

#### List Prepaid Card Receipts

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}/receipts`](https://docs.hyperwallet.com//content/api/v4/resources/receipts/prepaid-cards-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or prepaid card that doesn’t exist in the system. Check the user or prepaid card token and try again. |

#### List Account Receipts

These error codes are unique to the [`GET  /programs/{program-token}/accounts/{account-token}/receipts`](https://docs.hyperwallet.com//content/api/v4/resources/receipts/accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a program or account that doesn’t exist in the system. Check the program or account token and try again. |


### Programs

The following tables show unique error codes for the [`/programs`](https://docs.hyperwallet.com//content/api/v4/resources/programs) API endpoints.

#### Retrieve a Program

These error codes are unique to the [`GET /programs/{program-token}`](https://docs.hyperwallet.com//content/api/v4/resources/programs/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a program that doesn’t exist in the system. Check the program token and try again. |


### Accounts

The following tables show unique error codes for the [`/accounts`](https://docs.hyperwallet.com//content/api/v4/resources/accounts) API endpoints.

#### Retrieve an account

These error codes are unique to the [`GET /programs/{program-token}/accounts/{account-token}`](https://docs.hyperwallet.com//content/api/v4/resources/accounts/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a program or account that doesn’t exist in the system. Check the program or account token and try again. |


### Transfer Methods Configurations

The following tables show unique error codes for the [`/transfer-method-configurations`](https://docs.hyperwallet.com//content/api/v4/resources/transfer-method-configurations) API endpoints.

#### List Transfer Method Configurations

These error codes are unique to the [`GET /transfer-method-configurations?userToken={userToken}`](https://docs.hyperwallet.com//content/api/v4/resources/transfer-method-configurations/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |

#### Retrieve a Transfer Method Configuration

These error codes are unique to the [`GET /transfer-method-configurations?userToken={userToken}&country={country}&currency={currency}&type={type}&profileType={profileType}`](https://docs.hyperwallet.com//content/api/v4/resources/transfer-method-configurations/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |


### Webhook Notifications

The following tables show unique error codes for the [`/webhook-notifications`](https://docs.hyperwallet.com//content/api/v4/resources/webhook-notifications) API endpoints.

#### List Webhook Notifications

[Click here](#generic) for a list of generic errors.


#### Retrieve a Webhook Notification

These error codes are unique to the [`GET /webhook-notifications/{webhook-notification-token}`](https://docs.hyperwallet.com//content/api/v4/resources/webhook-notifications/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a webhook that doesn't exist in the system. Check the webhook token and try again. |


### Status Transitions

The following tables show unique error codes for the [`/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions) API endpoints.

#### List Status Transitions for a User

These error codes are unique to the [`GET /users/{user-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/users-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or status transition that doesn't exist in the system. Check the user or status transition token and try again. |

#### Create a User Status Transition

These error codes are unique to the [`POST /users/{user-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/users-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 CHANGE_ACCOUNT_STATUS_CLOSE_ACCOUNT_APPROVAL` | This account cannot be closed. Contact customer support. |
| `400 CHANGE_ACCOUNT_STATUS_INVALID_PAYEE_ACCOUNT_STATUS` | This is an invalid account status transiton.  |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn't on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/users-create). |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. Check the account status and try again. |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a user status transition, for example, when it is `LOCKED` or `FROZEN`. Check the wallet status and try again. |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The request includes a duplicate `email`. The `email` must be unique. |
| `400 DUPLICATE_EXTRA_ID_TYPE` | The request includes a duplicate `ClientUserID`. The `ClientUserID` must be unique. |

#### Retrieve a User Status Transition

These error codes are unique to the [`GET /users/{user-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/users-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or status transition that doesn't exist in the system. Check the user or status transition token and try again. |

#### List Status Transitions for a Business Stakeholder

These error codes are unique to the [`GET /users/{user-token}/business-stakeholders/{stakeholder-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/business-stakeholders-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or status transition that doesn't exist in the system. Check the user or status transition token and try again. |

#### Create a Business Stakeholder Status Transition

These error codes are unique to the [`POST /users/{user-token}/business-stakeholders `](https://docs.hyperwallet.com//content/api/v4/resources/business-stakeholders/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 CHANGE_ACCOUNT_STATUS_CLOSE_ACCOUNT_APPROVAL` | This account cannot be closed. Contact customer support. |
| `400 CHANGE_ACCOUNT_STATUS_INVALID_PAYEE_ACCOUNT_STATUS` | This is an invalid account status transiton.  |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn't on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/business-stakeholders/create). |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status cannot be changed. Contact customer support. |
| `400 DUPLICATE_EMAIL_REGISTRATION` | The transition request creates a duplicate `email` in the system. |

#### Retrieve a Business Stakeholder Status Transition

These error codes are unique to the [`GET /users/{user-token}/business-stakeholders/{stakeholder-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/business-stakeholders-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or status transition that doesn't exist in the system. Check the user or status transition token and try again. |

#### List Status Transitions for a Bank Account

These error codes are unique to the [`GET /users/{user-token}/bank-accounts/{bank-account-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/bank-accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank account that doesn't exist in the system. Check the user or bank account token and try again. |

#### Create a Bank Account Status Transition

These error codes are unique to the [`POST /users/{user-token}/bank-accounts/{bank-account-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/bank-accounts-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank account that doesn't exist in the system. Check the user or bank account token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/bank-accounts/create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a bank account status transition. Check the wallet status and try again. |

#### Retrieve a Bank Account Status Transition

These error codes are unique to the [`GET /users/{user-token}/bank-accounts/{bank-account-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/bank-accounts-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, bank account, or status transition that doesn't exist in the system. Check the user, bank account, or status transition token and try again. |

#### List Status Transitions for a Bank Card

These error codes are unique to the [`GET /users/{user-token}/bank-cards/{bank-card-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/bank-cards-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank card that doesn't exist in the system. Check the user or bank card token and try again. |

#### Create a Bank Card Status Transition

These error codes are unique to the [`POST /users/{user-token}/bank-cards/{bank-card-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/bank-cards-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank card that doesn't exist in the system. Check the user or bank card token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/bank-cards-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a bank card status transition. Check the wallet status and try again. |

#### Retrieve a Bank Card Status Transition

These error codes are unique to the [`GET /users/{user-token}/bank-cards/{bank-card-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/bank-cards-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, bank account, or status transition that doesn't exist in the system. Check the user, bank account, or status transition token and try again. |

#### List Status Transitions for a PayPal Account

These error codes are unique to the [`GET /users/{user-token}/paypal-accounts/{paypal-account-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/paypal-accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or PayPal account that doesn't exist in the system. Check the user or PayPal account token and try again.  |

#### Create a PayPal Account Status Transition

These error codes are unique to the [`POST /users/{user-token}/PayPal-accounts/{paypal-account-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/paypal-accounts-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or PayPal account that doesn't exist in the system. Check the user or PayPal account token and try again.  |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/paypal-accounts-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a PayPal account status transition. Check the wallet status and try again. |

#### Retrieve a PayPal Account Status Transition

These error codes are unique to the [`GET /users/{user-token}/PayPal-accounts/{paypal-account-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/paypal-accounts-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, PayPal account, or status transition that doesn't exist in the system. Check the user, PayPal account, or status transition token and try again. |

#### List Status Transitions for a Venmo Account

These error codes are unique to the [`GET /users/{user-token}/venmo-accounts/{venmo-account-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/venmo-accounts-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or Venmo account that doesn't exist in the system. Check the user or Venmo account token and try again. |

#### Create a Venmo Account Status Transition

These error codes are unique to the [`POST /users/{user-token}/venmo-accounts/{venmo-account-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/venmo-accounts-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or Venmo account that doesn't exist in the system. Check the user or Venmo account token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/venmo-accounts-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a Venmo account status transition. Check the wallet status and try again. |

#### Retrieve a Venmo Account Status Transition

These error codes are unique to the [`GET /users/{user-token}/venmo-accounts/{venmo-account-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/venmo-accounts-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, Venmo account, or status transition that doesn't exist in the system. Check the user, Venmo account, or status transition token and try again. |


#### List Status Transitions for a Prepaid Card

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/prepaid-cards-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or bank account that doesn't exist in the system. Check the user or bank account token and try again. |

#### Create a Prepaid Card Status Transition

These error codes are unique to the [`POST /users/{user-token}/prepaid-cards/{prepaid-card-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/prepaid-cards-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or prepaid card that doesn't exist in the system. Check the user or bank account token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect transition. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/prepaid-cards/create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a prepaid card status transition. Check the wallet status and try again. |

#### Retrieve a Prepaid Card Status Transition

These error codes are unique to the [`GET /users/{user-token}/prepaid-cards/{prepaid-card-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/prepaid-cards-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, prepaid card, or status transition that doesn't exist in the system. Check the user, prepaid card, or status transition token and try again. |

#### List Status Transitions for a Paper Check

These error codes are unique to the [`GET /users/{user-token}/paper-checks/{paper-check-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/paper-checks-list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or paper check that doesn't exist in the system. Check the user or paper check token and try again. |

#### Create a Paper Check Status Transition

These error codes are unique to the [`POST /users/{user-token}/paper-checks/{paper-check-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/paper-checks-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user or paper check that doesn't exist in the system. Check the user or paper check token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/paper-checks/create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a paper check status transition. Check the wallet status and try again. |

#### Retrieve a Paper Check Status Transition

These error codes are unique to the [`GET /users/{user-token}/bank-accounts/{bank-account-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/bank-accounts-retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user, paper check, or status transition that doesn't exist in the system. Check the user, paper check, or status transition token and try again. |





#### List Status Transitions for a Payment

These error codes are unique to the [`GET /payments/{payment-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/list) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment that doesn’t exist in the system. Check the payment token and try again. |

#### Create a Payment Status Transition

These error codes are unique to the [`POST /payments/{payment-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment that doesn’t exist in the system. Check the payment token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a payment status transition. Check the wallet status and try again. |

#### Retrieve a Payment Status Transition

These error codes are unique to the [`GET /payments/{payment-token}/status-transitions/{status-transition-token}`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/retrieve) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment or status transition that doesn’t exist in the system. Check the payment or status transition token and try again. |

#### Create a PayPal Payment Status Transition

These error codes are unique to the [`POST /payments/{payment-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/paypal-payment-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment that doesn’t exist in the system. Check the payment token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/paypal-payment-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a payment status transition. Check the wallet status and try again. |

#### Create a Venmo Payment Status Transition

These error codes are unique to the [`POST /payments/{payment-token}/status-transitions`](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/venmo-payment-create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a payment that doesn’t exist in the system. Check the payment token and try again. |
| `400 INVALID_FIELD_VALUE` | The request includes an incorrect value. |
| `400 INVALID_ENUM_VALUE` | The request includes a value that isn’t on the list of correct values. [Read a list of expected values here](https://docs.hyperwallet.com//content/api/v4/resources/status-transitions/venmo-payment-create). |
| `400 INVALID_STATUS_TRANSITION` | The request includes an incorrect value. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a payment status transition. Check the wallet status and try again. |

### Authentication Token

The following table shows unique error codes for the [`/authentication-token/create`](https://docs.hyperwallet.com//content/api/v4/resources/authentication-token/create) API endpoint.

#### Create Authentication Token

These error codes are unique to the [`POST /users/{user-token}/authentication-token`](https://docs.hyperwallet.com//content/api/v4/resources/authentication-token/create) endpoint. [Click here](#generic) for a list of generic errors.

| Status code and error | Description |
| --- | --- |
| `404 RESOURCE_NOT_FOUND` | The request includes a user that doesn’t exist in the system. Check the user token and try again. |
| `400 INVALID_WALLET_STATUS` | The wallet status doesn’t support a request to create an authentication token. Check the wallet status and try again. |