# Group Supplemental Data

In 2018, China introduced a regulation that requires detailed reference data for each payment being delivered into China. Regulatory authorities use this underlying transaction data to understand the purpose for each payment.

Hyperwallet collects this supplemental data (SPD) for each payment sent to a local Chinese bank account. Hyperwallet doesn't process a payment into China until we have the supplemental data needed for that payment.

**Table of contents**

- [Providing Supplemental Data](#providing-supplemental-data)
   - [Data Validation](#data-validation)
   - [Industry Types](#industry-types)
   - [Parameters](#parameters)
- [Troubleshooting](#troubleshooting)
   - [Failure scenarios](#failure-scenarios)
   - [Responses](#responses)
- [Endpoints](#endpoints)
   - [Get Supplemental Data Group Details [GET]](/content/api/v4/resources/supplemental-data/data-group-get)
   - [Create Supplemental Data Group [POST]](/content/api/v4/resources/supplemental-data/data-group-create)
   - [Retrieve Supplemental Data Group Details [GET]](/content/api/v4/resources/supplemental-data/data-group-retrieve)
   - [Update Supplemental Data Group [PUT]](/content/api/v4/resources/supplemental-data/data-group-update)
   - [Create Supplemental Data Line Items [POST]](/content/api/v4/resources/supplemental-data/line-items-create)
   - [Retrieve Line Item Details [GET]](/content/api/v4/resources/supplemental-data/line-items-retrieve)
   - [Update Supplemental Data Line Item [PUT]](/content/api/v4/resources/supplemental-data/line-items-update)
   - [List Status Transitions for Line Item [GET]](/content/api/v4/resources/supplemental-data/line-items-status-list)
   - [Create Status Transition for Line Item [PUT]](/content/api/v4/resources/supplemental-data/line-item-status-create)
   - [Retrieve Status Transition for Line Item [GET]](/content/api/v4/resources/supplemental-data/line-item-status-retrieve)
   - [List Status Transitions for Supplemental Data Group [GET]](/content/api/v4/resources/supplemental-data/data-group-transition-list)
   - [Create Status Transition for Supplemental Data Group [POST]](/content/api/v4/resources/supplemental-data/data-group-transition-create)
   - [Retrieve Status Transition for Supplemental Data Group [GET]](/content/api/v4/resources/supplemental-data/data-group-transition-retrieve)


## Providing Supplemental Data

You can pass the supplemental data for a payment using our REST API, or by sending [batch files](/content/batch/v2/cny-supplemental-data). This guide explains how to send this supplemental data through the REST API.

To provide the supplemental data via REST API, you need to make multiple API calls to pass the data.

1. Create a [supplemental data (SPD) group](/content/api/v4/resources/supplemental-data/data-group-create).
2. Create [SPD line items](/content/api/v4/resources/supplemental-data/line-items-create) for the SPD.
3. Create a [status transition](/content/api/v4/resources/supplemental-data/data-group-transition-create) on the SPD and its line items.

[Find out more about supplemental data](/content/transfer-methods/v1/bank-account/cny-supplemental-data).

### Data Validation

Hyperwallet validates the SPD attached to all qualifying payments:

1. The supplemental data (SPD) includes all of [the mandatory fields for the industry](/content/api/v4/resources/supplemental-data#industry-types) specified in the industry type field.
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

This API passes a core set of parameters for each request, as well as parameters for the [industry type](/content/api/v4/resources/supplemental-data#industry-types).

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

This section shows the additional parameters needed for each [industry type](/content/api/v4/resources/supplemental-data#industry-types) in Supplemental Data requests.

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

This section describes two failure scenarios for the [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create) and [Create Supplemental Data Line Items](/content/api/v4/resources/supplemental-data/line-items-create) endpoints.

#### Scenario 1

The supplemental data (SPD) group status is `INVALID`, and one or more line items under the SPD group has the `INVALID` status.

**Cause:** This happens when one or more SPD line items has incorrect data.

**Recommended action:** Correct the data provided for the SPD line items.

**Steps:** You can correct the SPD line items by using [Create Supplemental Data Line Items](/content/api/v4/resources/supplemental-data/line-items-create) to create a new line item under the SPD group. You can also use [Update Supplemental Data Line Item](/content/api/v4/resources/supplemental-data/line-items-update) on the incorrect SPD line item.

After all of the SPD line items have been corrected and submitted, perform a status transition on the SPD group by using [Create Status Transition for Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-transition-create) to change the SPD group status to `PENDING_REVIEW`.

> **Note:** While performing validations on the SPD group, the system only considers the line items with a `VALID` status. For example, if 5 line items have been created under an SPD group, and one of the line items has the `INVALID` status, then the system performs the SPD group validation by considering the data for the 4 valid line items. In order to correct the data for the 5th SPD line item, either create a new SPD line item, or perform an update process on the line item with the `INVALID` status.


#### Scenario 2

The supplemental data (SPD) group status is `INVALID`, and all of the line items under the SPD group has the `VALID` status.

**Cause:** This happens when an error occurs during validation of the SPD group.

**Recommended action:** The action depends on the type of error response returned for the SPD group.

### Responses

This section provides details about API responses for supplemental data groups and supplemental data line items.

#### Supplemental data group messages

The tables in this section show the response messages and error codes that the Supplemental Data API returns for operations on supplemental data (SPD) groups.

Condition | Response Code | Response Description | Applicable for
---- | ---- | ---- | ----
Data Validation successful. | `SUCCESS` or `SPD_VALIDATION_FAILURES` | Data was successfully validated. | SPD group or line item
Mandatory information missing. | `VALIDATIONS_ERRORS` | **Presence:** Data requirements have not been met. **Field Name**: You need to provide a value for this field<br />**Regex:** Data requirements have not been met. **Field Name is Invalid**. | SPD group or line item
Supplemental Data amount < Payment Amount. | `PURCHASE_AMOUNT_LESS_THAN_PAYMENT_AMOUNT` | The total purchase amount provided in the supplemental data is less than the payment amount. | SPD group
Records under a supplemental data group have different currencies. | `PURCHASE_CURRENCY_MISMATCH_BETWEEN_LINE_ITEMS` | Records under the supplemental data group have more than 1 currency. Purchase currency needs to be the same for all of the line items under an SPD group. | SPD group
Order currency for the SPD group is different from the payment currency. | `PURCHASE_CURRENCY_DIFFERENT_FROM_PAYMENT_CURRENCY` | The purchase currency is different from the payment currency. | SPD group
Other deductions currency for the supplemental data group is different from the payment currency. | `OTHER_DEDUCTIONS_CURRENCY_DIFFERENT_FROM_PAYMENT_CURRENCY` | The currency of the other deductions is different from the payment currency. | SPD group
The following condition isn't satisfied: **Payment Amount = Purchase Amount - Other Deductions**. | `INCORRECT_AMOUNT_CALCULATION` | The total purchase amount minus the other deductions amount isn't equal to the payment amount. | SPD group

##### Immediate errors (Post Supplemental Data Group API Response Errors)

Condition | Response Code | Response Description | Applicable for
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

Condition | Response Code | Response Description | Applicable for
---- | ---- | ---- | ----
Data validation successful. | `SUCCESS` or `SPD_VALIDATION_FAILURES` | Data validated successfully. | SPD group or line item
Mandatory information missing. | `VALIDATIONS_ERRORS` |  | SPD group or line item

##### Immediate errors (Post Supplemental Data Group API Response Errors)

Condition | Response Code | Response Description | Applicable for
---- | ---- | ---- | ----
Supplemental data can't be submitted in the current payment state. | `INVALID_PAYMENT_STATE` | The payment state doesn't support the requested action. Payment state is {0}. | SPD line item
Supplemental data can't be submitted in the current group state. | `INVALID_SPD_GROUP_STATE` | The supplemental data group state doesn't support the requested action. Supplemental data group state is {0} | SPD line item
Supplemental data for the payment already exists | `DUPLICATE_SUPPLEMENTAL_DATA` | Supplemental data for this payment already exists. | SPD line item

## Endpoints

## Supplemental Data Collection [/payments/{payment-token}/supplemental-data]

+ Parameters

    + `payment-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The payment token ID of the supplemental data (SPD) group.


### Get Supplemental Data Group Details [GET]

Retrieve information about a payment's supplemental data (SPD) group by sending a `GET` request to `/payments/{payment-token}/supplemental-data`. This endpoint returns the `token` ID and other details about each SPD group.

+ Response 200 (application/json)

    [
      {
        "industryType": "airlines",
        "otherDeductionsAmount": "200",
        "otherDeductionsCurrency": "CNY",
        "status": "INVALID",
        "createdOn": "2021-06-01T22:28:27.809Z",
        "token": "spd-5a30ae30-c980-11eb-b8bc-0242ac130003",
        "responseCode": "PURCHASE_CURRENCY_MISMATCH_BETWEEN_LINE_ITEMS",
        "responseDescription": "Records under the supplemental data group have more than 1 currency.Purchase currency should be same for all the line items under a supplemental data group.",
        "links": [
            {
              "params": {
                  "rel": "self"
              },
              "href": "https://uat-api.paylution.com/rest/v4/payments/pmt-9826c53c-c0e5-4663-a9ac-e6526fd67998/supplemental-data/spd-5a30ae30-c980-11eb-b8bc-0242ac130003"
            }
          ]
      },
      {
        "industryType": "airlines",
        "otherDeductionsAmount": "200",
        "otherDeductionsCurrency": "CNY",
        "status": "CREATED",
        "createdOn": "2021-06-01T23:28:27.809Z",
        "token": "spd-3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "links": [
            {
              "params": {
                  "rel": "self"
              },
              "href": "https://uat-api.paylution.com/rest/v4/payments/pmt-9826c53c-c0e5-4663-a9ac-e6526fd67998/supplemental-data/spd-3fa85f64-5717-4562-b3fc-2c963f66afa6"
            }
          ]
      }
    ]



### Create Supplemental Data Group [POST]

You need to create a supplemental data (SPD) group to pass the supplemental data for a payment. Create an SPD group by sending a `POST` request to `/payments/{payment-token}/supplemental-data`. Each payment needs one SPD group. This endpoint returns a unique `token` for each SPD group, with the prefix `spd-`

+ Attributes

    + `industryType`: `airlines` (string)

        The type of industry for the payment, such as `airlines` or `service`.

    + `otherDeductionsAmount`: `200` (string)

        The combined total of any deductions for this payment.

    + `otherDeductionsCurrency`: `CNY` (string)

        The currency of the payment deductions.

+ Request 200 (application/json)

    {
      "industryType": "airlines",
      "otherDeductionsAmount": "200",
      "otherDeductionsCurrency": "CNY"
    }

+ Response 200 (application/json)

    {
      "industryType": "airlines",
      "otherDeductionsAmount": "200",
      "otherDeductionsCurrency": "CNY",
      "status": "CREATED",
      "createdOn": "2021-06-01T22:28:27.809Z",
      "token": "spd-3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "links": [
          {
            "params": {
                "rel": "self"
            },
            "href": "https://uat-api.paylution.com/rest/v4/payments/pmt-9826c53c-c0e5-4663-a9ac-e6526fd67998/supplemental-data/spd-3fa85f64-5717-4562-b3fc-2c963f66afa6"
            }
        ]
    }

## Supplemental Data Group Collection [/payments/{payment-token}/supplemental-data/{spd-group-token}]

+ Parameters

    + `payment-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The payment token ID of the supplemental data (SPD) group.

    + `spd-group-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The token ID of the SPD group. This ID is returned in the `token` field when you make a successful [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create#create-supplemental-data-group) call.


### Retrieve Supplemental Data Group Details [GET]

Get the details about a supplementary data (SPD) group by sending a `GET` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}`.

+ Response 200 (application/json)

    {
        "industryType": "airlines",
        "otherDeductionsAmount": "200",
        "otherDeductionsCurrency": "CNY",
        "status": "VALID",
        "createdOn": "2021-06-01T22:28:27.809Z",
        "token": "spd-3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "responseCode": "SUCCESS",
        "responseDescription": "Supplemental data group validated successfully.",
        "links": [
            {
                "params": {
                    "rel": "self"
                },
                "href": "https://uat-api.paylution.com/rest/v4/payments/pmt-9826c53c-c0e5-4663-a9ac-e6526fd67998/supplemental-data/spd-3fa85f64-5717-4562-b3fc-2c963f66afa6"
            }
        ]
    }


### Update Supplemental Data Group [PUT]

Update a supplemental data (SPD) group by sending a `PUT` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}`.

This endpoint can update an SPD group if the status of the group is `CREATED` or `INVALID`.

You can use this endpoint to update the `otherDeductionsAmount` and `otherDeductionsCurrency` fields of an SPD group.

> Note: You can't update the `industryType` field for an SPD group. If you need to change the `industryType`:
> * Cancel the SPD group using the [Create Status Transition for Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-transition-create) endpoint.
> * Use the [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create) endpoint to create a new SPD group for the payment.

+ Request 200 (application/json)

    {
        "industryType": "airlines",
        "otherDeductionsAmount": "200",
        "otherDeductionsCurrency": "CNY"
    }

+ Response 200 (application/json)

    {
        "industryType": "airlines",
        "otherDeductionsAmount": "200",
        "otherDeductionsCurrency": "CNY",
        "status": "CREATED",
        "createdOn": "2021-06-01T22:28:27.809Z",
        "token": "spd-3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "links": [
            {
                "params": {
                    "rel": "self"
                },
                "href": "https://uat-api.paylution.com/rest/v4/payments/pmt-9826c53c-c0e5-4663-a9ac-e6526fd67998/supplemental-data/spd-3fa85f64-5717-4562-b3fc-2c963f66afa6"
            }
        ]
    }


## Supplemental Data Line Item Collection [/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items]

+ Parameters

    + `payment-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The payment token ID of the supplemental data (SPD) group.

    + `spd-group-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The token ID of the SPD group. This ID is returned in the `token` field when you make a successful [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create) call.


### Create Supplemental Data Line Items [POST]

Once you have a supplemental data (SPD) group for a payment, you need to create line items for that SPD group by sending a `POST` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items`. This endpoint returns a unique `token` for each SPD line item, with the prefix `spdl-`

You can send up to 500 SPD line items in a single call to this endpoint. If you have more than 500 line items to add to an SPD group, you need to send multiple calls.

+ Request 201 (application/json)

    [
      {
        "orderNumber": "123456",
        "orderDate": "12/11/2018",
        "orderTime": "2/15/2018",
        "itemName": "shoes",
        "itemsQuantity": "2",
        "purchaseCurrency": "CAD",
        "purchaseAmount": "100",
        "buyerId": "1231",
        "buyerCountryCode": "HKG",
        "buyerName": "PeterHayden",
        "platformName": "Amazon",
        "platformCountry": "HKG",
        "flightNumber": "AB123",
        "takeOffTime": "12/15/2018"
      },
      {
        "orderNumber": "123457",
        "orderDate": "12/11/2018",
        "orderTime": "2/15/2018",
        "itemName": "shoes",
        "itemsQuantity": "2",
        "purchaseCurrency": "CAD",
        "purchaseAmount": "100",
        "buyerId": "1231",
        "buyerCountryCode": "HKG",
        "buyerName": "PeterHayden",
        "platformName": "Amazon",
        "platformCountry": "HKG",
        "flightNumber": "AB123",
        "takeOffTime": "12/15/2018"
      }
    ]


+ Response 201 (application/json)

    [
        {
            "orderNumber": "123456",
            "status": "CREATED",
            "createdOn": "2021-06-03T16:13:26.277Z",
            "token": "spdl-3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "links": [
                {
                    "params": {
                        "rel": "self"
                    },
                    "href": "https://api.paylution.com:8181/rest/v4/payments/pmt-12d343f1-3adb-455d-b92c-8d6c168a664a/supplemental-data/spd-40d539c6-2b17-436c-94da-e4088f624ee4/line-items/spdl-3fa85f64-5717-4562-b3fc-2c963f66afa6"
                }
            ]
        },
        {
            "orderNumber": "123456",
            "status": "CREATED",
            "createdOn": "2021-06-03T16:13:26.277Z",
            "token": "spdl-5a30ae30-c980-11eb-b8bc-0242ac130003",
            "links": [
                {
                    "params": {
                        "rel": "self"
                    },
                    "href": "https://api.paylution.com:8181/rest/v4/payments/pmt-12d343f1-3adb-455d-b92c-8d6c168a664a/supplemental-data/spd-40d539c6-2b17-436c-94da-e4088f624ee4/line-items/spdl-5a30ae30-c980-11eb-b8bc-0242ac130003"
                }
            ]
        }
    ]


## Supplemental Data Line Item Details Collection [/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}]

+ Parameters

    + `payment-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The payment token ID of the supplemental data (SPD) group.

    + `spd-group-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The token ID of the SPD group. This ID is returned in the `token` field when you make a successful [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create) call.

    + `spd-line-item-token`: `spdl-5a30ae30-c980-11eb-b8bc-0242ac130003` (string)

        The token ID of the SPD line item. This value is returned in the `token` field by a successful [Create Supplemental Data Line Items](/content/api/v4/resources/supplemental-data/line-items-create) call.


### Retrieve Line Item Details [GET]

Get the details about a supplemental data (SPD) line item by sending a `GET` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}`.

+ Response 200 (application/json)

    {
      "orderNumber": "123456",
      "orderDate": "12/11/2018",
      "orderTime": "2/15/2018",
      "itemName": "shoes",
      "itemsQuantity": "2",
      "purchaseCurrency": "CAD",
      "purchaseAmount": "100",
      "buyerId": "1231",
      "buyerCountryCode": "HKG",
      "buyerName": "PeterHayden",
      "platformName": "Amazon",
      "platformCountry": "HKG",
      "flightNumber": "AB123",
      "takeOffTime": "12/15/2018",
      "status": "VALID",
      "createdOn": "2021-06-03T16:13:26.277Z",
      "token": "spdl-5a30ae30-c980-11eb-b8bc-0242ac130003",
      "responseCode": "0",
      "responseDescription": "Supplemental data line item validated successfully",
      "links": [
            {
                "params": {
                    "rel": "self"
                },
                "href": "https://api.paylution.com:8181/rest/v4/payments/pmt-12d343f1-3adb-455d-b92c-8d6c168a664a/supplemental-data/spd-40d539c6-2b17-436c-94da-e4088f624ee4/line-items/spdl-5a30ae30-c980-11eb-b8bc-0242ac130003"
            }
        ]
    }

### Update Supplemental Data Line Item [PUT]

Update a line item in a supplemental data (SPD) group by sending a `PUT` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}`.

You can update an SPD line item when its status is `CREATED`, `VALID`, or `INVALID`, and the status of its SPD group is `CREATED` or `INVALID`.

+ Request 202 (application/json)

    {
        "orderNumber": "123456",
        "orderDate": "12/11/2018"
    }

+ Response 202 (application/json)

    {
        "orderNumber": "123456",
        "orderDate": "12/11/2018",
        "orderTime": "2/15/2018",
        "itemName": "shoes",
        "itemsQuantity": "2",
        "purchaseCurrency": "CAD",
        "purchaseAmount": "100",
        "buyerId": "1231",
        "buyerCountryCode": "HKG",
        "buyerName": "PeterHayden",
        "platformName": "Amazon",
        "platformCountry": "HKG",
        "flightNumber": "AB123",
        "takeOffTime": "12/15/2018",
        "status": "CREATED",
        "createdOn": "2021-06-03T16:13:26.277Z",
        "token": "spdl-5a30ae30-c980-11eb-b8bc-0242ac130003",
        "links": [
            {
                "params": {
                    "rel": "self"
                },
                "href": "https://api.paylution.com:8181/rest/v4/payments/pmt-12d343f1-3adb-455d-b92c-8d6c168a664a/supplemental-data/spd-40d539c6-2b17-436c-94da-e4088f624ee4/line-items/spdl-5a30ae30-c980-11eb-b8bc-0242ac130003"
            }
        ]
    }


## Supplemental Data Line Item Status Transitions Collection [/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}]

+ Parameters

    + `payment-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The payment token ID of the supplemental data (SPD) group.

    + `spd-group-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The token ID of the SPD group. This ID is returned in the `token` field when you make a successful [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create) call.

    + `spd-line-item-token`: `spdl-5a30ae30-c980-11eb-b8bc-0242ac130003` (string)

        The token ID of the SPD line item. This value is returned in the `token` field by a successful [Create Supplemental Data Line Items](/content/api/v4/resources/supplemental-data/line-items-create) call.

### List Status Transitions for Line Item [GET]

You can get a list of status transitions for a supplemental data (SPD) line item by sending a `GET` request to
`/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}/status-transitions`.

##### Supplemental Data Line Item Status Transitions

This table shows details about the available status transitions for an SPD line item. The "Applicable SPD Group Status" column shows the SPD group status needed for each status transition.

From Status | To Status | Applicable SPD Group Status | Notes
---- | ---- | ---- | ----
`CREATED` | `VALID` | `PENDING_REVIEW` | System-initiated status transition
`CREATED` | `INVALID` | `PENDING_REVIEW` | System-initiated status transition
`CREATED` | `CANCELLED` | `CREATED` | Merchant-initiated status transition
`VALID` | `CANCELLED` | `CREATED` or `INVALID` | Merchant-initiated status transition
`INVALID` | `CANCELLED` | `CREATED` or `INVALID` | Merchant-initiated status transition
`INVALID` | `CREATED` | `CREATED` or `INVALID` | System-initiated status transition

+ Response 200 (application/json)

      {
        "count": 1,
        "offset": 0,
        "limit": 10,
        "data": [
          {
            "token": "sts-4f790461-2e07-45e8-852f-40229421b4d4",
            "createdOn": "2017-11-16T01:55:34",
            "transition": "CANCELLED",
            "fromStatus": "VALID",
            "toStatus": "CANCELLED",
            "notes": "CANCELLING THE LINE ITEM",
            "links": [
              {
                "params": {
                  "rel": "self"
                },
                "href": "https://uat-api.paylution.com/rest/v4/payments/{payment-token}/supplemental-data/spdg-83836cdf-2ce2-4696-8bc5-f1b86077238c/supplemental-data-record/spdr-87939c73-ff0a-4011-970e-3de855347ea7/status-transitions/sts-4f790461-2e07-45e8-852f-40229421b4d4"
              }
            ]
          }
        ],
        "links": [
          {
            "params": {
              "rel": "self"
                },
                "href": "https://uat-api.paylution.com/rest/v4/payments/pmt-2c059341-8281-4d30-a65d-a49d8e2a9b0f/supplemental-data/spd-83836cdf-2ce2-4696-8bc5-f1b86077238c/supplemental-data-record/spl-87939c73-ff0a-4011-970e-3de855347ea7/status-transitions?offset=0&limit=10"
            }
          ]
      }

### Create Status Transition for Line Item [PUT]

You can create a status transition for a supplemental data (SPD) line item by sending a `POST` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}/status-transitions`. This endpoint returns a unique `token` for each status transition, with the prefix `sts-`.

This endpoint can apply the `CANCELLED` status to an SPD line item.

+ Request 201 (application/json)

    {
      "transition": "CANCELLED",
      "notes": "status transition notes"
    }

+ Response 201 (application/json)

    {
      "token": "sts-4647533a-8f45-4fa8-ba7a-31982054b85c",
      "createdOn": "2021-06-14T12:45:43",
      "transition": "CANCELLED",
      "fromStatus": "CREATED",
      "toStatus": "CANCELLED",
      "notes": "status transition notes",
      "links": [
        {
          "params": {
            "rel": "self"
          },
          "href": "https://api.paylution.com:8181/rest/v4/payments/pmt-606d6ada-9b7c-4938-be1a-4d02e37153fe/supplemental-data/spd-4bf748f5-a073-44fa-84e1-bf4f35639236/line-items/spdl-87afbbf4-673b-4eea-97f9-76f3d2375e76/status-transitions/sts-4647533a-8f45-4fa8-ba7a-31982054b85c"
        }
      ]
}


## Supplemental Data Line Item Status Transitions Collection [/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}/status-transitions/{status-transition-token}]

+ Parameters

    + `payment-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The payment token ID of the supplemental data (SPD) group.

    + `spd-group-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The token ID of the SPD group. This ID is returned in the `token` field when you make a successful [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create) call.

    + `spd-line-item-token`: `spdl-5a30ae30-c980-11eb-b8bc-0242ac130003` (string)

        The token ID of the SPD line item. This value is returned in the `token` field by a successful [Create Supplemental Data Line Items](/content/api/v4/resources/supplemental-data/line-items-create) call.

    + `status-transition-token`: `sts-4647533a-8f45-4fa8-ba7a-31982054b85c` (string)

        The status transition token ID for the SPD line item. This ID is returned in the `token` field when you make a successful [Create Status Transition for Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-transition-create) or [Create Status Transition for Line Item](/content/api/v4/resources/supplemental-data/line-item-status-create) call.


### Retrieve Status Transition for Line Item [GET]

You can retrieve a status transition for a supplemental data (SPD) line item by sending a `GET` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/line-items/{spd-line-item-token}/status-transitions/{status-transition-token}`.


+ Response 200 (application/json)

    {
      "token" : "sts-4647533a-8f45-4fa8-ba7a-31982054b85c",
      "createdOn" : "2021-06-14T12:45:43",
      "transition" : "PENDING_REVIEW",
      "fromStatus" : "CREATED",
      "toStatus" : "PENDING_REVIEW",
      "notes" : "status transition notes",
      "links" : [ {
        "params" : {
          "rel" : "self"
        },
        "href" : "https://api.paylution.com:8181/rest/v4/payments/pmt-606d6ada-9b7c-4938-be1a-4d02e37153fe/supplemental-data/spd-4bf748f5-a073-44fa-84e1-bf4f35639236/line-items/spdl-87afbbf4-673b-4eea-97f9-76f3d2375e76/status-transitions/sts-4647533a-8f45-4fa8-ba7a-31982054b85c"
        } ]
    }


## Supplemental Data Group Status Transitions Collection [/payments/{payment-token}/supplemental-data/{spd-group-token}/status-transitions]

+ Parameters

    + `payment-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The payment token ID of the supplemental data (SPD) group.

    + `spd-group-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The token ID of the SPD group. This ID is returned in the `token` field when you make a successful [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create) call.


### List Status Transitions for Supplemental Data Group [GET]

Retrieve a list of status transitions for a supplemental data (SPD) group by sending a `GET` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/status-transitions`.

##### Supplemental Data Group Status Transitions

This table shows details about the available status transitions for an SPD group.

From Status | To Status | Notes |
---- | ---- | ---- |
`CREATED` | `PENDING_REVIEW` | Merchant-initiated status transition |
`CREATED` | `CANCELLED` | Merchant-initiated status transition |
`INVALID` | `PENDING_REVIEW` | Merchant-initiated status transition<br /><br />The merchant makes a status transition call to begin validation after updating supplemental data (SPD) line items or adding new line items under an SPD group. This doesn't change the SPD group data.<br /><br />Don't create this transition when the merchant updates the SPD group data.<br /><br />Scenario: If the user updates the SPD group immediately after creation, before doing a status transition to `PENDING_REVIEW`, then this triggers the group validations. SPD line items may or may not be created at this stage.  |
`PENDING_REVIEW` | `VALID` | System-initiated status transition |
`PENDING_REVIEW` | `INVALID` | System-initiated status transition |


+ Response 200 (application/json)

  [
      {
          "token": "sts-4647533a-8f45-4fa8-ba7a-31982054b85c",
          "createdOn": "2021-06-14T12:45:43",
          "transition": "PENDING_REVIEW",
          "fromStatus": "CREATED",
          "toStatus": "PENDING_REVIEW",
          "notes": "status transition notes",
          "links": [
              {
                  "params": {
                      "rel": "self"
                  },
                  "href": "https://api.paylution.com:8181/rest/v4/payments/pmt-606d6ada-9b7c-4938-be1a-4d02e37153fe/supplemental-data/spd-4bf748f5-a073-44fa-84e1-bf4f35639236/status-transitions/sts-4647533a-8f45-4fa8-ba7a-31982054b85c"
              }
          ]
      },
      {
          "token": "sts-87afbbf4-673b-4eea-97f9-76f3d2375e76",
          "createdOn": "2021-06-14T13:45:43",
          "transition": "VALID",
          "fromStatus": "PENDING_REVIEW",
          "toStatus": "VALID",
          "notes": "status transition notes",
          "links": [
              {
                  "params": {
                      "rel": "self"
                  },
                  "href": "https://api.paylution.com:8181/rest/v4/payments/pmt-606d6ada-9b7c-4938-be1a-4d02e37153fe/supplemental-data/spd-4bf748f5-a073-44fa-84e1-bf4f35639236/status-transitions/sts-87afbbf4-673b-4eea-97f9-76f3d2375e76"
              }
          ]
      }
  ]


### Create Status Transition for Supplemental Data Group [POST]

You can create a status transition for a supplemental data (SPD) group by sending a `POST` request to `/payments/{payment-token}/supplemental-data/{spd-group-token}/status-transitions`. This endpoint returns a unique `token` for each status transition, with the prefix `sts-`.

This endpoint can apply the `CANCELLED` or `PENDING_REVIEW` status to an SPD group.

+ Request 201 (application/json)

    {
      "transition": "PENDING_REVIEW",
      "notes": "status transition notes"
    }

+ Response 201 (application/json)

    {
      "token": "sts-4647533a-8f45-4fa8-ba7a-31982054b85c",
      "createdOn": "2021-06-14T12:45:43",
      "transition": "PENDING_REVIEW",
      "fromStatus": "CREATED",
      "toStatus": "PENDING_REVIEW",
      "notes": "status transition notes",
      "links": [
        {
          "params": {
            "rel": "self"
          },
          "href": "https://api.paylution.com:8181/rest/v4/payments/pmt-606d6ada-9b7c-4938-be1a-4d02e37153fe/supplemental-data/spd-4bf748f5-a073-44fa-84e1-bf4f35639236/status-transitions/sts-4647533a-8f45-4fa8-ba7a-31982054b85c"
        }
      ]
    }




## Supplemental Data Group Status Transition Collection [/payments/{payment-token}/supplemental-data/{spd-group-token}/status-transitions/{status-transition-token}]

+ Parameters

    + `payment-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The payment token ID of the supplemental data (SPD) group.

    + `spd-group-token`: `spd-3fa85f64-5717-4562-b3fc-2c963f66afa6` (string)

        The token ID of the SPD group. This ID is returned in the `token` field when you make a successful [Create Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-create) call.

    + `status-transition-token`: `sts-4647533a-8f45-4fa8-ba7a-31982054b85c` (string)

        The status transition token ID for the SPD group. This ID is returned in the `token` field when you make a successful [Create Status Transition for Supplemental Data Group](/content/api/v4/resources/supplemental-data/data-group-transition-create) call.


### Retrieve Status Transition for Supplemental Data Group [GET]

You can retrieve a status transition for a supplemental data (SPD) group by sending a `GET` request to `payments/{payment-token}/supplemental-data/{spd-group-token}/status-transitions/{status-transition-token}`.

+ Response 200 (application/json)

    {
      "token" : "sts-4647533a-8f45-4fa8-ba7a-31982054b85c",
      "createdOn" : "2021-06-14T12:45:43",
      "transition" : "PENDING_REVIEW",
      "fromStatus" : "CREATED",
      "toStatus" : "PENDING_REVIEW",
      "notes" : "status transition notes",
      "links" : [ {
        "params" : {
          "rel" : "self"
        },
        "href" : "https://api.paylution.com:8181/rest/v4/payments/pmt-606d6ada-9b7c-4938-be1a-4d02e37153fe/supplemental-data/spd-4bf748f5-a073-44fa-84e1-bf4f35639236/status-transitions/sts-4647533a-8f45-4fa8-ba7a-31982054b85c"
        } ]
    }
