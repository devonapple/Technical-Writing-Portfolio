# Group Supplemental Data

In 2018, China introduced a regulation that requires detailed reference data for each payment being delivered into China. Regulatory authorities use this underlying transaction data to understand the purpose for each payment.

Hyperwallet collects this supplemental data (SPD) for each payment sent to a local Chinese bank account. Hyperwallet doesn't process a payment into China until we have the supplemental data needed for that payment.

## Providing Supplemental Data

You can pass the supplemental data for a payment using our REST API, or by sending [batch files](https://docs.hyperwallet.com/content/batch/v2/cny-supplemental-data). This guide explains how to send this supplemental data through the REST API.

To provide the supplemental data via REST API, you need to make multiple API calls to pass the data.

1. Create a [supplemental data (SPD) group](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/data-group-create).
2. Create [SPD line items](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/line-items-create) for the SPD.
3. Create a [status transition](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/data-group-transition-create) on the SPD and its line items.

[Find out more about supplemental data](https://docs.hyperwallet.com/content/transfer-methods/v1/bank-account/cny-supplemental-data).

### Data Validation

Hyperwallet validates the SPD attached to all qualifying payments:

1. The supplemental data (SPD) includes all of [the mandatory fields for the industry](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data#industry-types) specified in the industry type field.
2. The SPD provided complies with the minimum and maximum length defined for each field.
3. The SPD provided uses the character set defined for each field.
4. The difference between the purchase amount and the other deductions amount given in the SPD for the payment needs to be equal to the Payment amount: **Payment amount = Purchase amount - Other Deductions**.

> Note: If multiple SPD line items have been passed for a payment, then the sum total of the purchase amounts for all of the line items is considered to be the total purchase amount.

5. If multiple SPD line items have been passed for a payment, then the currency specified in the "Purchase Currency" needs to be the same for all the line items under an SPD group.
6. The other deductions currency needs to be same as the payment amount currency and purchase amount currency.
7. The purchase currency of the SPD group needs to be same as the load currency for the payment.
8. The industry type mentioned in the SPD request can't be `INVALID`.
9. Hyperwallet doesn't accept duplicate SPD for a payment.

### Industry Types

This is a list of supported values for the `industryType` field:

* `Airlines`
* `Clinical Services`
* `eCommerce`
* `Freelancer`
* `Hotel`
* `Service`
* `Tour Services`

### Parameters

This API passes a core set of parameters for each request, as well as parameters for the [industry type](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data#industry-types).

#### Core parameters

This table shows the list of parameters used in all Supplemental Data API requests.

Field Name | Description | Min-Max Characters
---- | ---- | ----
`orderNumber` | Reference number for the order, invoice, or contract. | 1-32
`buyerId` | The client-assigned unique ID of the buyer in the client's system. | 1-32
`buyerName` | Name of the person purchasing the goods or services. | 1-64
`buyerCountryCode` | 3-letter country code (ISO alpha-3) where the buyer resides. | 3-3
`platformName` | Platform on which the payment was carried out. | 1-32
`platformCountry` | Country of the platform on which the payment took place. | 3-32
`orderDate` | Date order was placed by buyer in YYYY-MM-DD format. | 10-10
`orderTime` | Time order was placed by buyer in HH-MM-SS format. | 8-8
`purchaseCurrency` | 3-letter currency code for the payment, for example, the currency as shown in the order, invoice, or contract. | 3-3
`purchaseAmount` | Amount as shown in the order, invoice, or contract. | 1-15
`itemName` | Name of the goods or services. | 1-128
`itemsQuantity` | Quantity of each generic category of goods and services. | 1-9

#### Industry Parameters

This section shows the additional parameters needed for each [industry type](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data#industry-types) in Supplemental Data requests.

##### Airlines

This table shows the additional parameters for the `Airlines` industry type:

Field Name | Description | Min-Max Characters
---- | ---- | ----
`flightNumber` | Flight number. | 4-10
`takeOffTime` | Date of flight in YYYY-MM-DD format. | 10-10

##### Freelancer

This table shows the additional parameters for the `Freelancer` industry type:

Field Name | Description | Min-Max Characters
---- | ---- | ----
`goodsDescription` | Detailed itemized description of each good or service in the order. | 4-128
`startDate` | Start date of service. | 10-10

##### Clinical Services

This table shows the additional parameters for the `Clinical Services` industry type:

Field Name | Description | Min-Max Characters
---- | ---- | ----
`clinicalTrialName` | Name of the clinical trial performed. | 4-128
`startDate` | Date the clinical trial was performed. | 10-10

##### eCommerce

This table shows the additional parameters for the `eCommerce` industry type:

Field Name | Description | Min-Max Characters
---- | ---- | ----
`transportationPartnerName` | Name of the company responsible for delivering the goods. | 1-64

##### Hotel

This table shows the additional parameters for the `Hotel` industry type:

Field Name | Description | Min-Max Characters
---- | ---- | ----
`hotelName` | Name of the hotel. | 3-64
`startDate` | Date of check-in in YYYY-MM-DD format. | 10-10

##### Service

This table shows the additional parameters for the `Service` industry type:

Field Name | Description | Min-Max Characters
---- | ---- | ----
`serviceDetail` | Details of service provided. | 4-128
`serviceTime` | Date of service provided in YYYY-MM-DD format. | 10-10

##### Tour Services

This table shows the additional parameters for the `Tour Services` industry type:

Field Name | Description | Min-Max Characters
---- | ---- | ----
`lodgingCity` | Lodging city name. | 3-32
`startDate` | Start date of tour in YYYY-MM-DD format. | 10-10

## Troubleshooting

This documentation includes failure scenarios and a list of responses.

### Failure scenarios

This section describes two failure scenarios for the [Create Supplemental Data Group](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/data-group-create) and [Create Supplemental Data Line Items](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/line-items-create) endpoints.

#### Scenario 1

The supplemental data (SPD) group status is `INVALID`, and one or more line items under the SPD group have the `INVALID` status.

**Cause:** This happens when one or more SPD line items has incorrect data.

**Recommended action:** Correct the data provided for the SPD line items.

**Steps:** You can correct the SPD line items by using [Create Supplemental Data Line Items](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/line-items-create) to create a new line item under the SPD group. You can also use [Update Supplemental Data Line Item](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/line-items-update) on the incorrect SPD line item.

After all of the SPD line items have been corrected and submitted, perform a status transition on the SPD group by using [Create Status Transition for Supplemental Data Group](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/data-group-transition-create) to change the SPD group status to `PENDING_REVIEW`.

> **Note:** While performing validations on the SPD group, the system only considers the line items with a `VALID` status. For example, if 5 line items have been created under an SPD group, and one of the line items has the `INVALID` status, then the system performs the SPD group validation by considering the data for the 4 valid line items. In order to correct the data for the 5th SPD line item, either create a new SPD line item, or perform an update process on the line item with the `INVALID` status.

#### Scenario 2

The supplemental data (SPD) group status is `INVALID`, and all of the line items under the SPD group have the `VALID` status.

**Cause:** This happens when an error occurs during validation of the SPD group.

**Recommended action:** The action depends on the type of error response returned for the SPD group.

### Responses

This section provides details about API responses for supplemental data groups and supplemental data line items.

#### Supplemental data group messages

The tables in this section show the response messages and error codes that the Supplemental Data API returns for operations on supplemental data (SPD) groups.

Condition | Response code | Response description | Applicable for
---- | ---- | ---- | ----
Data Validation successful. | `SUCCESS` or `SPD_VALIDATION_FAILURES` | Data was successfully validated. | SPD group or line item
Mandatory information missing. | `VALIDATIONS_ERRORS` | **Presence:** Data requirements have not been met. **Field Name**: You need to provide a value for this field<br />**Regex:** Data requirements have not been met. **Field Name is Invalid**. | SPD group or line item
Supplemental Data amount < Payment Amount. | `PURCHASE_AMOUNT_LESS_THAN_PAYMENT_AMOUNT` | The total purchase amount provided in the supplemental data is less than the payment amount. | SPD group
Records under a supplemental data group have different currencies. | `PURCHASE_CURRENCY_MISMATCH_BETWEEN_LINE_ITEMS` | Records under the supplemental data group have more than 1 currency. Purchase currency needs to be the same for all of the line items under an SPD group. | SPD group
Order currency for the SPD group is different from the payment currency. | `PURCHASE_CURRENCY_DIFFERENT_FROM_PAYMENT_CURRENCY` | The purchase currency is different from the payment currency. | SPD group
Other deductions currency for the supplemental data group is different from the payment currency. | `OTHER_DEDUCTIONS_CURRENCY_DIFFERENT_FROM_PAYMENT_CURRENCY` | The currency of the other deductions is different from the payment currency. | SPD group
The following condition isn't satisfied: **Payment Amount = Purchase Amount - Other Deductions**. | `INCORRECT_AMOUNT_CALCULATION` | The total purchase amount minus the other deductions amount isn't equal to the payment amount. | SPD group

##### Immediate errors (Post Supplemental Data Group API Response Errors)

Condition | Response code | Response description | Applicable for
---- | ---- | ---- | ----
Invalid industry. | `INVALID_INDUSTRY` | The Industry provided is invalid. | SPD group
Other Deductions amount not provided. | `MISSING_OTHER_DEDUCTIONS_AMOUNT` | Provide a value for `otherDeductionsAmount`. | SPD group
Other Deductions currency not provided. | `MISSING_OTHER_DEDUCTIONS_CURRENCY` | Provide a value for `otherDeductionsCurrency`. | SPD group
Other Deductions amount invalid. | `INVALID_OTHER_DEDUCTIONS_AMOUNT` | Provide a value with a correct format for `otherDeductionsAmount`. | SPD group
Other Deductions currency invalid. | `INVALID_OTHER_DEDUCTIONS_CURRENCY` | The value under `otherDeductionsCurrency` isn't a valid currency. | SPD group
Supplemental data Industry not provided. | `MISSING_INDUSTRY` | Industry type isn't provided. | SPD group
Supplemental data for the payment already exists. | `DUPLICATE_SUPPLEMENTAL_DATA` | Industry type {0} isn't supported. | SPD group
Supplemental data can't be submitted in the current payment state.  | `INVALID_PAYMENT_STATE` | The payment state doesn't support the requested action. Payment state is {0}. | SPD group

#### Supplemental Line items messages:

The tables in this section show the response messages and error codes that the Supplemental Data API returns for operations on supplemental data (SPD) line items.

Condition | Response code | Response description | Applicable for
---- | ---- | ---- | ----
Data validation successful. | `SUCCESS` or `SPD_VALIDATION_FAILURES` | Data validated successfully. | SPD group or line item
Mandatory information missing. | `VALIDATIONS_ERRORS` |  | SPD group or line item

##### Immediate errors (Post Supplemental Data Group API Response Errors)

Condition | Response code | Response description | Applicable for
---- | ---- | ---- | ----
Supplemental data can't be submitted in the current payment state. | `INVALID_PAYMENT_STATE` | The payment state doesn't support the requested action. Payment state is {0}. | SPD line item
Supplemental data can't be submitted in the current group state. | `INVALID_SPD_GROUP_STATE` | The supplemental data group state doesn't support the requested action. Supplemental data group state is {0} | SPD line item
Supplemental data for the payment already exists | `DUPLICATE_SUPPLEMENTAL_DATA` | Supplemental data for this payment already exists. | SPD line item

## Endpoints

### Get Supplemental Data Group Details [GET]

Retrieve information about a payment's supplemental data (SPD) group by sending a `GET` request to `/payments/{payment-token}/supplemental-data`. This endpoint returns the `token` ID and other details about each SPD group.

### Create Supplemental Data Group [POST]

You need to create a supplemental data (SPD) group to pass the supplemental data for a payment. Create an SPD group by sending a `POST` request to `/payments/{payment-token}/supplemental-data`. Each payment needs one SPD group. This endpoint returns a unique `token` for each SPD group, with the prefix `spd-`

### Retrieve Supplemental Data Group Details [GET]

Get the details about a supplementary data (SPD) group by sending a `GET` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}`.

### Update Supplemental Data Group [PUT]

Update a supplemental data (SPD) group by sending a `PUT` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}`.

This endpoint can update an SPD group if the status of the group is `CREATED` or `INVALID`.

You can use this endpoint to update the `otherDeductionsAmount` and `otherDeductionsCurrency` fields of an SPD group.

> Note: You can't update the `industryType` field for an SPD group. If you need to change the `industryType`:
> * Cancel the SPD group using the [Create Status Transition for Supplemental Data Group](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/data-group-transition-create) endpoint.
> * Use the [Create Supplemental Data Group](https://docs.hyperwallet.com/content/api/v4/resources/supplemental-data/data-group-create) endpoint to create a new SPD group for the payment.

### Create Supplemental Data Line Items [POST]

Once you have a supplemental data (SPD) group for a payment, you need to create line items for that SPD group by sending a `POST` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items`. This endpoint returns a unique `token` for each SPD line item, with the prefix `spdl-`

You can send up to 500 SPD line items in a single call to this endpoint. If you have more than 500 line items to add to an SPD group, you need to send multiple calls.

### Retrieve Line Item Details [GET]

Get the details about a supplemental data (SPD) line item by sending a `GET` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}`.

### Update Supplemental Data Line Item [PUT]

Update a line item in a supplemental data (SPD) group by sending a `PUT` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}`.

You can update an SPD line item when its status is `CREATED`, `VALID`, or `INVALID`, and the status of its SPD group is `CREATED` or `INVALID`.

### List Status Transitions for Line Item [GET]

You can get a list of status transitions for a supplemental data (SPD) line item by sending a `GET` request to
`/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}/status-transitions`.

##### Supplemental Data Line Item Status Transitions

This table shows details about the available status transitions for an SPD line item. The "Applicable SPD Group status" column shows the SPD group status needed for each status transition.

From status | To status | Applicable SPD Group status | Notes
---- | ---- | ---- | ----
`CREATED` | `VALID` | `PENDING_REVIEW` | System-initiated status transition
`CREATED` | `INVALID` | `PENDING_REVIEW` | System-initiated status transition
`CREATED` | `CANCELLED` | `CREATED` | Merchant-initiated status transition
`VALID` | `CANCELLED` | `CREATED` or `INVALID` | Merchant-initiated status transition
`INVALID` | `CANCELLED` | `CREATED` or `INVALID` | Merchant-initiated status transition
`INVALID` | `CREATED` | `CREATED` or `INVALID` | System-initiated status transition

### Create Status Transition for Line Item [PUT]

You can create a status transition for a supplemental data (SPD) line item by sending a `POST` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}/status-transitions`. This endpoint returns a unique `token` for each status transition, with the prefix `sts-`.

This endpoint can apply the `CANCELLED` status to an SPD line item.

### Retrieve Status Transition for Line Item [GET]

You can retrieve a status transition for a supplemental data (SPD) line item by sending a `GET` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}/status-transitions/{status-transition-token}`.

### List Status Transitions for Supplemental Data Group [GET]

Retrieve a list of status transitions for a supplemental data (SPD) group by sending a `GET` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/status-transitions`.

##### Supplemental Data Group status Transitions

This table shows details about the available status transitions for an SPD group.

From status | To status | Notes |
---- | ---- | ---- |
`CREATED` | `PENDING_REVIEW` | Merchant-initiated status transition |
`CREATED` | `CANCELLED` | Merchant-initiated status transition |
`INVALID` | `PENDING_REVIEW` | Merchant-initiated status transition<br /><br />The merchant makes a status transition call to begin validation after updating supplemental data (SPD) line items or adding new line items under an SPD group. This doesn't change the SPD group data.<br /><br />Don't create this transition when the merchant updates the SPD group data.<br /><br />Scenario: If the user updates the SPD group immediately after creation, before doing a status transition to `PENDING_REVIEW`, then this triggers the group validations. SPD line items may or may not be created at this stage.  |
`PENDING_REVIEW` | `VALID` | System-initiated status transition |
`PENDING_REVIEW` | `INVALID` | System-initiated status transition |

### Create Status Transition for Supplemental Data Group [POST]

You can create a status transition for a supplemental data (SPD) group by sending a `POST` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/status-transitions`. This endpoint returns a unique `token` for each status transition, with the prefix `sts-`.

This endpoint can apply the `CANCELLED` or `PENDING_REVIEW` status to an SPD group.

### Retrieve Status Transition for Supplemental Data Group [GET]

You can retrieve a status transition for a supplemental data (SPD) group by sending a `GET` request to `payments/{payment-token}/supplemental-data/{spd-group-token}/status-transitions/{status-transition-token}`.