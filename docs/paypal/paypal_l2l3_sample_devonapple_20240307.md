# Level 2/Level 3 processing

## What are Level 2 and 3 card payment transactions?

Card payment processing has 3 levels: Level 1, Level 2, and Level 3. The levels differ in the amount of information required to complete the payment as a Level 1, Level 2, or Level 3 eligible transaction. Level 1 requires less information and therefore generally incurs higher interchange fees compared to transactions processed with Level 2 and Level 3 data. Most businesses can operate at Level 1, however, when processing corporate and purchase credit cards, IC++ merchants can benefit from reduced interchange fees by providing additional transaction information called Level 2 and Level 3 data.

## Which types of card payments qualify?

Corporate and purchase credit cards are eligible for Levels 2 and 3 processing if the required information is provided. Consumer cards are only eligible for Level 1 processing.

Level 2 and Level 3 cost optimization benefits do not apply to debit cards.

## Which card networks support Level 2 and 3 processing?

Visa and Mastercard offer Levels 2 and 3 processing. American Express offers Level 2, and Discover offers only Level 1 processing.

## How does a payment qualify?

To qualify for Levels 2 and 3 processing, merchants must send the following information. However, the card network and cardholder issuing bank ultimately make the determination of whether a transaction qualifies for Level 2 or Level 3 processing:

### Level 2 data

* Card number, expiration, billing address, shipping address, and invoice number.
* Customer Code or PO number: a unique reference ID for the order.
* Tax amount: an amount must be submitted separately from the total transaction amount.

### Level 3 data

* Level 2 data, and,
* Unit amount or unit price.
* Unit of measure.
* Freight or shipping amount: the total shipping and handling charges.
* Duty amount: the total charges for any import or export duties.
* Discount amount.
* Item commodity code.
* Item description.
* Item product code.
* Item quantity.
* Unit tax amount.
* Unit discount amount.
* Ship-from ZIP code.

> **Note:** The partner, merchant, or other initiating party needs to provide the Level 2 and 3 payment details when using the <a href="https://developer.paypal.com/docs/api/orders/v2/" target="_blank">Orders v2 API</a> to start a payment.

## Create Order request

This code sample shows Level 2 and 3 data in the body of a `POST` call to the <a href="https://developer.paypal.com/docs/api/orders/v2/#orders_create" target="_blank">Create order</a> endpoint of the Orders v2 API. This request creates a new order and completes the payment in a single step by declaring the `intent` as `CAPTURE`:

```javascript
curl -v -X POST https://api-m.sandbox.paypal.com/v2/checkout/orders \
-H 'Content-Type: application/json' \
-H 'PayPal-Request-Id: REQUEST-ID' \
-H 'Authorization: Bearer ACCESS-TOKEN' \
-d '{
   "intent": "CAPTURE",
   "payer": {
      "name": {
         "given_name": "Firstname",
         "surname": "Lastname"
      },
      "address": {
         "address_line_1": "123 Main St.",
         "admin_area_2": "Anytown",
         "admin_area_1": "CA",
         "postal_code": "12345",
         "country_code": "US"
      }
   },
   "purchase_units": [
      {
         "reference_id": "Reference_ID_L2L32",
         "description": "Description of PU",
         "custom_id": "Custom-ID",
         "soft_descriptor": "Purchase Descriptor",
         "invoice_id": "INV_202302011234",
         "supplementary_data": {
            "card": {
               "level_2": {
                  "invoice_id": "INV_202302011234",
                  "tax_total": {
                     "currency_code": "USD",
                     "value": "5.20"
                  }
               },
               "level_3": {
                  "shipping_amount": {
                     "currency_code": "USD",
                     "value": "1.17"
                  },
                  "duty_amount": {
                     "currency_code": "USD",
                     "value": "1.16"
                  },
                  "discount_amount": {
                     "currency_code": "USD",
                     "value": "1.15"
                  },
                  "shipping_address": {
                     "address_line_1": "123 Main St.",
                     "admin_area_2": "Anytown",
                     "admin_area_1": "CA",
                     "postal_code": "12345",
                     "country_code": "US"
                  },
                  "ships_from_postal_code": "12345",
                  "line_items": [
                     {
                        "name": "Item1",
                        "description": "Description of Item1",
                        "upc": {
                           "type": "UPC-A",
                           "code": "001004697"
                        },
                        "unit_amount": {
                           "currency_code": "USD",
                           "value": "9.50"
                        },
                        "tax": {
                           "currency_code": "USD",
                           "value": "5.12"
                        },
                        "discount_amount": {
                           "currency_code": "USD",
                           "value": "1.11"
                        },
                        "total_amount": {
                           "currency_code": "USD",
                           "value": "95.10"
                        },
                        "unit_of_measure": "POUND_GB_US",
                        "quantity": "10",
                        "commodity_code": "98756"
                     }
                  ]
               }
            }
         },
         "amount": {
            "currency_code": "USD",
            "breakdown": {
               "item_total": {
                  "currency_code": "USD",
                  "value": "90.20"
               },
               "tax_total": {
                  "currency_code": "USD",
                  "value": "10.10"
               },
               "shipping": {
                  "currency_code": "USD",
                  "value": "10.00"
               },
               "discount": {
                  "currency_code": "USD",
                  "value": "10.00"
               }
            }
         },
         "items": [
            {
               "name": "Item1",
               "description": "Description of Item1",
               "sku": "SKU - 0",
               "url": "http: //example.com",
               "unit_amount": {
                  "currency_code": "USD",
                  "value": "45.10"
               },
               "tax": {
                  "currency_code": "USD",
                  "value": "5.05"
               },
               "quantity": "2",
               "category": "PHYSICAL_GOODS"
            }
         ],
         "shipping": {
            "address": {
               "address_line_1": "123 Main St.",
               "admin_area_2": "Anytown",
               "admin_area_1": "CA",
               "postal_code": "12345",
               "country_code": "US"
            }
         }
      }
   ]
}'
```

* Lines 25-31 declare a `level_2` object inside `purchase_units.supplementary_data.card`, including the invoice ID and the taxes charged for the payment.
* Lines 32-82 declare a `level_3` object inside `purchase_units.supplementary_data.card`. Data includes shipping, duty, and discount amounts, as well as line-item information and units of measure.

## See also

See the Level 2 and Level 3 Processing <a href="https://www.paypal.com/us/cshelp/article/ts2278" target="_blank">FAQ</a>.
