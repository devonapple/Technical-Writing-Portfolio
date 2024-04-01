# Operation API

- [Operation endpoint](#operation-endpoint)   
   - [Get a resource using the operation endpoint](#get-a-resource-using-the-operation-endpoint)   
- [Asset library](#asset-library)   
   - [Objects](#objects)   
      - [date_standard](#date_standard)   
      - [url](#url)   
   - [Enumerated values (ENUM)](#enums)   
      - [mode](#mode)   
      - [query_mode](#query_mode)   
      - [status_code](#status_code)   

## Operation endpoint

The operation API returns resource details from local, market, and global lists. You can select a summary or a full report.

**URI** `POST server/operation-network/operation/{resource_id}`

Shows details about a resource in the system of record (SOR). Use `query_mode` to limit the information returned and change the format of the response. The [query_mode table](#mode_query_tables) has a list of available modes.

This endpoint returns `HTTP 201` and the resource details when the request is successful. The endpoint returns `HTTP 200` when the system already has a pending operation request for the `operation_id`.

<a name="operation_request_unique_id"></a>

### Get a resource using the operation endpoint

**Path**

 | Parameter | Description | Type | Required | Notes |
 | :--- | :--- | :--- | :--- | :--- |
 | `resource_id` | The unique identifier of the resource in the system. | string | Required | <p>Minimum length: `1`</p><p>Maximum length: `100`</p> |

**Query**

 | Parameter | Description | Type | Required | Notes |
 | :--- | :--- | :--- | :--- | :--- |
 | `query_mode` | The query mode for this request. | string | &nbsp; | <p>Minimum length: `1`</p><p>Maximum length: `100`</p><p>Pattern: `^[0-9A-Z_]+$`</p><p>ENUM: [query_mode](#mode_query_tables)</p><p>Default: `LOCAL`</p> |

**Request**

 | Element | Description | Type | Required | Notes |
 | :--- | :--- | :--- | :--- | :--- |
 | `operation_id` | The unique idempotent identifier of this operation. | string | Required | <p>Minimum length: `0`</p><p>Maximum length: `100`</p> |
 | `mode` | The operation mode for this request. | string | Required | <p>Minimum length: `1`</p><p>Maximum length: `100`</p><p>Pattern: `^[0-9A-Z_]+$`</p><p>ENUM: [mode](#mode_common_assets) |

**Response**

 | Element | Description | Type | Required | Notes |
 | :--- | :--- | :--- | :--- | :--- |
 | `operation_id` | The unique idempotent identifier of this operation. | string | &nbsp; | <p>Minimum length: `0`</p><p>Maximum length: `100`</p> |
 | `id` | The unique identifier of the resource in the system. | string | Required | <p>Minimum length: `0`</p><p>Maximum length: `100`</p> |
 | `status` | The status of the resource. | string | &nbsp; | <p>Minimum length: `1`</p><p>Maximum length: `255`</p><p>Pattern: `^[0-9A-Z_]+$`</p><p>ENUM: [status_code](#status_code_common_assets) |
 | `retry_availability` | The number of remaining operation attempts supported by this resource. | integer | &nbsp; | <p>Minimum: `0`</p><p>Maximum: `256`</p> |
 | `retry_count` | The number of times that the system has attempted to re-initiate the operation. | integer | &nbsp; | <p>Minimum: `0`</p><p>Maximum: `256`</p> |
 | `time_on` | The date and time when the resource was initiated, in [Internet date and time format](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | [date_standard](#date_standard_common_assets) | &nbsp; | &nbsp; |
 | `time_released` | The date and time when the resource was released, in [Internet date and time format](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | [date_standard](#date_standard_common_assets) | &nbsp; | &nbsp; |
 | `urls` | An array of Hypermedia as the Engine of Application State (HATEOAS) links associated with this resource. | array of [urls](#url_common_assets) | &nbsp; | <p>Minimum items: `1`</p><p>Maximum items: `30`</p> |
 | `mode` | This echoes the operation mode for the original request. | string | &nbsp; | <p>Minimum length: `1`</p><p>Maximum length: `100`</p><p>Pattern: `^[0-9A-Z_]+$`</p><p>ENUM: [mode](#mode_common_assets) |


## Asset library

This resource defines the parameter objects and enum lists that the operation API uses.


<a name="objects"></a>

### Objects

This section defines the parameter objects for this API.

<a name="date_standard_common_assets"></a>

#### date_standard

The date and time in [Internet date and time format](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6).

| Element | Description | Type | Required | Notes |
| :--- | :--- | :--- | :--- | :--- |
| `date` | A valid date-time representation as defined by [RFC 3339 Section 5.6](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). Seconds are required while fractional seconds are optional. | string | &nbsp; | <p>Minimum length: `20`</p><p>Maximum length: `64`</p><p>Pattern: `^([0-9]+)-(0[1-9]|1[012])-(0[1-9]|[12][0-9]|3[01])[Tt]([01][0-9]|2[0-3]):([0-5][0-9]):([0-5][0-9]|60)(\.[0-9]+)?(([Zz])|([\+|\-]([01][0-9]|2[0-3]):[0-5][0-9]))$`</p> |


<a name="url_common_assets"></a>

#### url

The request-related information for a Hypermedia as the Engine of Application State (HATEOAS) link.

 | Element | Description | Type | Required | Notes |
 | :--- | :--- | :--- | :--- | :--- |
 | `href` | The complete target URL. To make the related call, combine the method with this [URI Template-formatted](https://datatracker.ietf.org/doc/html/rfc6570) link. | string | Required | &nbsp; |
 | `rel` | The [link relation type](https://datatracker.ietf.org/doc/html/rfc5988#section-4), which serves as an ID of a link that unambiguously describes the semantics of the link. | string | Required | &nbsp; |
 | `method` | The HTTP method needed to make the related call. | string | &nbsp; | Default: `POST` |
 | `title` | The link title. | string | &nbsp; | &nbsp; |
 | `media_type` | The media type, as defined by [RFC 2046](https://datatracker.ietf.org/doc/html/rfc2046). This describes the link target. | string | &nbsp; | &nbsp; |


<a name="enums"></a>

### Enumerated values (ENUM)

This section defines the enumerator objects for this API.


<a name="mode_common_assets"></a>

#### mode

The mode determines the priority for the operation.

 | Value | Description | Notes |
 | :--- | :--- | :--- |
 | `EXPEDITED` | A realtime request. The request is queued for immediate action. An expedited request takes up to 30 seconds. | &nbsp; |
 | `BATCH` | The operation is submitted to the end-of-day batch server. A batch request takes up to 24 hours. | &nbsp; |
 | `MONTHEND` | The operation is added to the batch request. The server processes month-end operations on the 28th of the month. | &nbsp; |


<a name="mode_query_tables"></a>

#### query_mode

 The query mode determines how much information an operation returns.

 | Value | Description | Notes |
 | :--- | :--- | :--- |
 | `LOCAL` | Returns data for the local region. | The local region is passed by the server based on the IP address of the operation caller. |
 | `LIGHT` | Returns summarized information for the local region. | The local region is passed by the server based on the IP address of the operation caller. |
 | `MARKET` | Returns results for the market region. | The market region is passed by the server based on the IP address of the operation caller. |
 | `MARKET_LIGHT` | Returns summarized information for the market region. | The market region is passed by the server based on the IP address of the operation caller. |
 | `GLOBAL` | Returns results for all regions. | &nbsp; |
 | `GLOBAL_LIGHT` | Returns summarized information for all regions in the organization. | &nbsp; |


<a name="status_code_common_assets"></a>

#### status_code

The status code for a resource.

 | Value | Description | Notes |
 | :--- | :--- | :--- |
 | `AVAILABLE` | The resource is available for operations. | &nbsp; |
 | `CLOSED` | The resource doesn't support operations. | &nbsp; |
 | `PENDING` | The resource is temporarily unavailable for operations. | You can retry in 30 seconds. |
