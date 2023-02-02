# 1. Introduction
This document or guidelines are the standard practise of LTS' development in which to promote the consistency of REST API implementation across all system within LTS' software/service implementations.

With this in mind, we encourage API First as our key engineering principles. We encourage our teams and vendors to follow them to ensure that our APIs:
- are easy to learn and understand
- have a common look and feel
- follow a consistent RESTful style and syntax

# 2. Principles

## API design principles

- We prefer REST-based APIs with data exchange using JSON
- We prefer the API to be RESTful
- API as a Product
- API needs to be secured

- Additional Reads
    - Refer to <a href="https://cloud.google.com/files/apigee/apigee-api-best-practices-ebook.pdf" target="_blank">APIGee API documentation</a>

# 3. General Guidelines

- Documentation
    - Provide description of the end point and describe the special logic if any.
    - Provide example of the request payload
    - Specify the possible Error Message and HTTP Status Codes from response
    - Recommended to use <a href="https://swagger.io" target="_blank">Swagger</a> as API Endpoint documentation. <a href="https://petstore.swagger.io/" target="_blank">Swagger Example</a>

# 4. REST Guidelines

## 4.1 Meta Information

The API should contain versioning. Ideally the version should be placed in the URI path for easy identification.
    - e.g. /v1/employees

The hostname should follow standardize naming convention and ensuring naming are consistent across all environments. e.g.
- https&#58;//portal.&lt;domain&gt;.sg
- https&#58;//portal-api.&lt;domain&gt;.sg
- https&#58;//uat-portal.&lt;domain&gt;.sg
- https&#58;//uat-portal-api.&lt;domain&gt;.sg

## 4.2 Security

Every API endpoint must be protected and armed with authentication and authorization. As part of the API definition you must specify how you protect your API using either the http typed bearer or oauth2 typed security schemes defined in the <a href="https://swagger.io/docs/specification/authentication/" target="_blank">OpenAPI Authentication Specification</a>.

## 4.3 Data Formats

Use the Open API defined data types supported by the JSON schema specification draft. 

JSON consists of 6 data types:
1. string
2. number
3. boolean
4. null
5. object
6. array

Use Base 64 encoding for binary data.

Use dates without a zone offset (UTC) consistently. Localization to be done on services which provide user interfaces.

## 4.4 URLs

Think API as resources, it should have pluralize naming. Should not have verbs in URL naming for resource. Avoid action naming whenever possible.

API naming resources should be **Nouns** collections
- **GET** /user (Bad)
- **GET** `/users (Good)`

Avoid use of verbs in name collections
- **GET** /getAllEmployees (Bad)
- **GET** `/employees (Good)`
- **POST** /createEmployees (Bad)
- **POST** `/employees (Good)`

If there is resource nesting:
- Try to limit not more than 3 level of nesting
    - **GET** /customers/{cid}/orders/{oid}/items/{oiid}

## 4.5 JSON Payload

Use **JSON** as request and response body
- Use camel case for attribute names
- Wrap actual data in data field
- Use query string for optional parameters

## 4.6 HTTP Requests
Use HTTP Methods correctly.

Verbs should clearly specify the intention of the API. In LTS, we would suggest the use of these 4 API verbs.

- **GET** - Use to retrive a representation of a resource
- **POST** - Use to create a new resource
- **PUT** - Use to update an existing resource
- **DELETE** - Use to delete an existing resource

## 4.7 HTTP Status Codes
Use standard HTTP Status Codes for success and error handling <a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes" target="_blank">List of codes</a>
- Information (100 - 199)
- Success (200 - 299)
- Redirection (300 - 399)
- Client Error (400 - 499)
- Server Error (500 - 599)

Do not include sensitive information (e.g. method/class names) in the error response message.

## 4.8 HTTP Headers
We may use standard headers as defined in the <a href="https://en.wikipedia.org/wiki/List_of_HTTP_header_fields" target="_blank">list</a>.

**You should also use Content-{name} headers correctly.**

Content or entity headers are headers with a **Content-** prefix. They describe the content of the body of the message and they can be used in both, HTTP requests and responses. Commonly used content headers include but are not limited to:

- **Content-Disposition** can indicate that the representation is supposed to be saved as a file, and the proposed file name.
- **Content-Encoding** indicates compression or encryption algorithms applied to the content.
- **Content-Length** indicates the length of the content (in bytes).
- **Content-Type** indicates the media type of the body content.

Custom headers should be kebab case with upper case separate words for readability and consistency.

``` code
X-Tenant-Code
X-Rate-Limit
Auth-Type
```

## 4.9 Performance
Should cache GET and HEAD requests.

Use GZIP Compression

Compress the payload of your API’s responses with gzip, unless there’s a good reason not to — for example, you are serving so many requests that the time to compress becomes a bottleneck. This helps to transport data faster over the network (fewer bytes) and makes frontends respond faster.

## 4.10 Pagination
When fetching a collection of data, do use  pagination for data retrieval. To standardize the naming convention and terms for paging in LTS for REST API, the parameter/properties name to be used

| Property | Type | Description
| -------- | ---- | -----------
| **start** | (params) | The record starting row instead of using *pageNumber*, *row*, *etc*.
| **size** | (params) | The size of record collection to be fetched instead of using *pageSize*, *offset*, *etc*.
| **total** | (response) | The total collection available in the resource.
| **items** | (response) | The collection array.

*Example: Fetching a list of customers starting from row 1, with page size of 25. The database contains 101 records of customers.*

``` json
GET /customers?start=1&size=25 

HTTP/1.1 200 OK
Content-Type: application/json
{
  "total": 101,
  "items": [
    {
        "id": 1,
        "dateOfBirth": "2000-01-01T08:00:00.000Z",
        "fullname": "John Doe",
        "creditBalance": 9.99,
        "isAdministrator": false
    }, ...
    {
        "id": 25,
        "dateOfBirth": "1969-08-28T16:00:00.000Z",
        "fullname": "Jack Black",
        "creditBalance": 9999.99,
        "isAdministrator": true
    }
  ]
}
```


## 4.11 Compatibility
While we support changes of APIs, but we need to ensure that all API consumer does not break due to the change of API behaviour. API consumer usually have it's own release lifecycle and may not provide additional attributes that is required.

APIs must be backward compatible. If there are breaking changes, introduce a new API version.

Backward compatible:
- add only optional fields
- use only JSON object as top level response

Validation:
- Unknown input fields should not be ignored.
- Check constraints and return dedicated error information.

## 4.12 Deprecation
Any deprecation of API should be communicated in advance and must obtain approval/consent from LTS before API removal.
- Reflect the deprecation in the API specification and HTTP header.
- Ensure external partner consent on deprecation time span before discontinuing deprecated API.

# 5. Others
More information here on things that is not above topic.
