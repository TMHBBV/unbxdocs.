---
title: 'Search API '
deprecated: false
hidden: false
metadata:
  robots: index
---
# Search API

The Search API lets you easily interact with the Unbxd platform and implement all search-related functionality. It allows you to provide search results to a query from the list of products matching search criteria. It also provides relevant facets and filters, pagination option, sorting option, spell check suggestion functionality catering to the search query.

You can use the JSON /XML response format and customize your search experience by leveraging various built-in features of Search. All API requests must be made over HTTPS.

## Search Endpoint

```Text Sample Request
ccurl -X GET \
'https://search.unbxd.io/<API Key>/<SITE Key>/search?q=query&version=V2&user-type=repeat'
  -H 'unbxd-device-type: {"type":"mobile","os":"windows","source":"app"}'
 -H 'User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; HTC; Windows Phone 8X by HTC)'
 -H 'X-forwarded-for: 192.168.1.1, 192.168.1.101'
 -H 'unbxd-user-id: uid-1499941737191-79890'
```

## Authentication

Our APIs use an API\_KEY and a SITE\_KEY to authenticate search requests.

These keys are generated when an account is created and can be accessed within the Console at Manage -> Configure Site -> Keys.

## Headers

Unbxd requires some header parameters along with the search request in order to provide support for personalization and merchandising campaigns created on location, browser or device type. Headers need to be passed through the URL to process the actual response.

> 📘 Important Note
>
> For Search and Autosuggest API, we can enable personalization, segmentation, and A/B testing of the merchandising campaign. we recommend passing certain parameters as HTTPS headers.

The following parameters are available:

| Parameter         | Description                                                                                                                                                                           | Significance                                                                                           |
| :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------------------- |
| unbxd-user-id     | Unique identification for the visitors. Example: uid-1466015353887-20419. The Unbxd Analytics JavaScript sets the userid in your browser cookie.                                      | If not passed, personalization, segmentation, and A/B testing of merchandising campaigns will not work |
| user-agent        | Browser identification information is passed to the web server with every HTTPS request.                                                                                              | If not passed, device-based merchandising campaigns will not work.                                     |
| unbxd-device-type | This header is an Unbxd custom header, which is required to identify if the request is coming from an app.                                                                            | If not passed, device-based merchandising campaigns cannot differentiate between browsers and apps.    |
| Accept-Encoding   | This header signifies the response's content encoding. Currently, Unbxd supports only gzip compression. To enable this, ‘gzip’ needs to be passed.                                    | If not passed, the response will not be compressed.                                                    |
| X-Forwarded-For   | This header signifies the end-user's IP address. It is primarily required if the integration is a backend, as Unbxd doesn’t get the IP of the end-user from the browser in that case. | If not passed, segmentation, A/B testing, and personalization will not work.                           |

#### unbxd-device-type:

```
 { "type":"tablet" , "os": "iOS" , "source": "app" }
```

possible values of “type” : “desktop”, “tablet”, “mobile”

possible values of “os” : “android”, “ios”, “windows”

possible values of “source” : “browser”, “app”

## Error Codes

* 404 (Not Found): Indicates the requested resource doesn’t exist. In the browser, this means the URL is not recognized. This can also mean that the endpoint is valid in an API, but the resource does not exist.
* 400 (Bad Request): Indicates the request was unacceptable, often due to missing a required parameter.
* 401 (Unauthorized): No valid API key provided.
* 200 (OK): Indicates that everything worked as expected.

## Request Parameters

The value of the request parameters is defined below:

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Description
      </th>

      <th>
        Data Type
      </th>

      <th>
        Possible Values/Format
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        q

        Mandatory
      </td>

      <td>
        The main query parameter passed in the request is the search term a shopper enters in the e-commerce site's search box.
      </td>

      <td>
        String
      </td>

      <td>
        `Format: ?q={search_query}`
      </td>
    </tr>

    <tr>
      <td>
        version

        Mandatory
      </td>

      <td>
        The version parameter specifies the version of the API. To get the latest API features, you should always pass “\&version=V2” in every API call. The facet response changes in V1 as compared to V2.
      </td>

      <td>
        String
      </td>

      <td>
        Format: `&version=V2`

        <br />

        Supported Values: V1, V2
      </td>
    </tr>

    <tr>
      <td>
        user-type

        Mandatory
      </td>

      <td>
        Number of times a user visits the site. Probable values can be: frequent,  first-time.
      </td>

      <td>
        String
      </td>

      <td>
        Format: “first-time”

        <br />

        Supported Values: first-time, frequent
      </td>
    </tr>

    <tr>
      <td>
        uid

        Mandatory
      </td>

      <td>
        Unique identification ID for visitors, with value to pass, can be obtained from Unbxd. userId browser cookie
      </td>

      <td>
        String
      </td>

      <td>
        `&uid=uid-1666356549013-78531`
      </td>
    </tr>

    <tr>
      <td>
        format

        Optional
      </td>

      <td>
        The format parameter specifies the format for generating the response result.
      </td>

      <td>
        String
      </td>

      <td>
        Format: `&format=xml`

        <br />

        Supported values: JSON, XML

        <br />

        Default Value: JSON
      </td>
    </tr>

    <tr>
      <td>
        start

        Optional
      </td>

      <td>
        The start parameter is used to offset the results by a specific number.
      </td>

      <td>
        Integer
      </td>

      <td>
        Format: `&start=2`

        <br />

        Default Value: 0
      </td>
    </tr>

    <tr>
      <td>
        page

        optional
      </td>

      <td>
        Displays the right set of products with respect to the number of products shown on one page(rows parameter).
      </td>

      <td>
        Integer
      </td>

      <td>
        Format: `&page=2`
      </td>
    </tr>

    <tr>
      <td>
        rows

        optional
      </td>

      <td>
        Paginate the results of a query
      </td>

      <td>
        Integer
      </td>

      <td>
        Format: `&rows=2`

        Default Value: 10
      </td>
    </tr>

    <tr>
      <td>
        variants
      </td>

      <td>
        Displays variants of the same product
      </td>

      <td>
        Boolean
      </td>

      <td>
        Format: `&variants.count=5`
      </td>
    </tr>

    <tr>
      <td>
        variants.count
      </td>

      <td>
        Displays multiple defined variants of a product.
      </td>

      <td>
        Integer
      </td>

      <td>
        Format: `&variants.count=5`
      </td>
    </tr>

    <tr>
      <td>
        fields
      </td>

      <td>
        Defines attributes for a product like color, size, etc.
      </td>

      <td>
        String
      </td>

      <td>
        Format: \&fields=,

        <br />

        Default Values: If not applied, returns all fields
      </td>
    </tr>

    <tr>
      <td>
        bucket.field
      </td>

      <td>
        It allows you to group products with a common field value into groups known as buckets, returning the top products per bucket.
      </td>

      <td>
        String
      </td>

      <td>
        Format: `&bucket.field=,`
      </td>
    </tr>

    <tr>
      <td>
        bucket.limit
      </td>

      <td>
        Determines the number of products in a bucket.
      </td>

      <td>
        Integer
      </td>

      <td>
        Format: `&bucket.limit=10`

        Default Value: 10
      </td>
    </tr>

    <tr>
      <td>
        bucket.offset
      </td>

      <td>
        To Paginate to the next 5 products of the group
      </td>

      <td>
        Integer
      </td>

      <td>
        Format: `&bucket.offset=10`
      </td>
    </tr>

    <tr>
      <td>
        rows
      </td>

      <td>
        Determines the number of buckets displayed at a time in case bucketing is done on a field.
      </td>

      <td>
        Integer
      </td>

      <td>
        Format: `&rows=10`
      </td>
    </tr>

    <tr>
      <td>
        analytics
      </td>

      <td>
        Enables or disables tracking the query hit for analytics.
      </td>

      <td>
        String
      </td>

      <td>
        Default value: Tracking is enabled
      </td>
    </tr>

    <tr>
      <td>
        stats
      </td>

      <td>
        It gives information about the products with the highest and lowest field values.
      </td>

      <td>

      </td>

      <td>
        Format: `fieldName`\
        (only numerical fields)
      </td>
    </tr>

    <tr>
      <td>
        fallback
      </td>

      <td>
        Spell checks the search query and displays results for the autocorrected search query.
      </td>

      <td>
        Boolean
      </td>

      <td>
        Default fallback: `True`
      </td>
    </tr>

    <tr>
      <td>
        banners
      </td>

      <td>
        Creates sales/promotional images to promote a brand or occasion.
      </td>

      <td>
        Boolean
      </td>

      <td>
        Default value: `True`
      </td>
    </tr>

    <tr>
      <td>
        redirect
      </td>

      <td>
        Redirects visitors to a web page for the search query
      </td>

      <td>

      </td>

      <td>
        Default Value: Enabled
      </td>
    </tr>
  </tbody>
</Table>

## Response Components

Unbxd returns the list of products that match the search criteria. The response would be in application/JSON or application/XML content types format.

| Component        | Description                                                                                                                                 |
| :--------------- | :------------------------------------------------------------------------------------------------------------------------------------------ |
| status           | The response status code defines whether it is OK(code 200), Not Found(code 404), Internal Server Error(code 500), or many other types.     |
| queryTime        | Time is taken to process the shopper's request.                                                                                             |
| queryParams      | Parameters sent as part of the request.                                                                                                     |
| numberOfProducts | The total number of products returned for the page.                                                                                         |
| start            | Offset in the complete result set of products for the page.                                                                                 |
| products         | Product details are sent as a result that matches the request query. The structure will be the same as passed in the feed.                  |
| relevantDocument | Mention whether the parent or the variant for a particular product needs to be displayed in the UI. It can be either "parent" or "variant". |
| facets           | Filters that are displayed in the UI allow visitors to narrow down the result set based on product fields.                                  |
| breadcrumb       | Position in the field hierarchy.                                                                                                            |
| selected         | Filters that are selected for the query.                                                                                                    |
| redirect         | Redirect response for the query.                                                                                                            |
| didYouMean       | Spellcheck response with a query suggestion.                                                                                                |
| banner           | Banner response for the query.                                                                                                              |

<br />

## How to work with Search APIs

The table, as mentioned above, provides the default values of the request parameters.

Let’s delve deeper and understand the API calls of each parameter individually.

## Querying

The q (query) parameter in the search API defines the query a visitor searches for in your store. This process of searching is also known as querying.

For instance, you searched for “red dress“, in the API call, the query will look like this:

```Text Sample
q=red%20dress
```

Querying is URL-based, i.e., all queries are URL-encoded. Here, %20 represents the word space in the URL-encoded API call.

### Quick Tips for Handling Special Characters

Unbxd strives to better understand your visitor queries by translating commonly used punctuation while querying. However, our algorithm treats special characters differently.

For example, a query typed within double quotation marks, “red dress,” allows the algorithm to recognize the query as a phrase and tokenize it as one single token to be indexed, instead of indexing the words red and dress separately.

To escape these special characters in a query, use a trailing slash before the character. For example, the special characters in a query (jeans+shirt)\*2? can be escaped as shown below:

```
\(jeans\+shirt\)\*2\?
```

#### The current list of special characters are:

```
+  -  &&  ||  !  (  )  {  }  [  ]  ^  "  ~  *  ?  :  \
```

#### Sample request to get JSON response

```
https://search.unbxd.io/fb853e3332f2645fac9d71dc63e09ec1/demo-unbxd700181503576558/search?q=dress&version=V2
```

#### Sample JSON Response

```
{
searchMetaData: {
status: 0,
queryTime: 32,
queryParams: {
log.response: "false",
original.q: "dog",
module.exclude: "personalization",
alternate.op: "true",
req.rm.asterix: "true",
q.op: "AND",
enableTaxonomy: "false",
q: "dog",
req.rm.promotionEngine: "true",
promotion.fields: [
"color_uFilter",
"gender_uFilter",
"category_uFilter"
],
enablePf: "false",
user.behaviour: "true",
enablePopularity: "true"
}
},
response: {
numberOfProducts: 0,
start: 0,
products: [ ]
},
didYouMean: [
{
suggestion: "dot",
frequency: "100"
}
]
}
```

***

## Pagination

To get the paginated response in the search API, specify the value of the parameters “start”, “rows”, “page”, and “maxRows”. The “start” parameter defines the product's position in the response. The “rows” attribute defines the number of products required per API call.

E.g. for the first page of results, the start=0 and rows=20

For the next page of results, the start= 20 and rows=20.

```Text Sample Request
https://search.unbxd.io/fb853e3332f2645fac9d71dc63e09ec1/demo-unbxd700181503576558/search?q=dress&version=V2&start=0&rows=20
```

**start**: It indicates offset in the complete result set of the products.

```Text Sample Request
https://search.unbxd.io/c85ec9e6c53e6522f2d0f88c4a214717/hsn-com700091495001458/search?&q=red&start=5&rows=5
```

This request will fetch all the results starting with the offset 5 for the result set of the query red.

**page**: Call the ‘page’ parameter when you want the correct set of products to be returned concerning the number of products shown on one page(rows parameter).

If you specify the page value as 2, with rows as 20, then the products with the offset 40 will be returned for the results.

```Text Sample Request
http://search.unbxd.io/c85ec9e6c53e6522f2d0f88c4a214717/hsn-com700091495001458/search?&q=red&page=5&rows=5
```

**page**: The ‘rows’ parameter is used to paginate the results of a query. It indicates the number of products displayed on a single page.

```
http://search.unbxd.io/c85ec9e6c53e6522f2d0f88c4a214717/hsn-com700091495001458/search?&q=red&start=5&rows=5
```

This request will fetch a total of 5 products.

> 📘 NOTE
>
> If the products are not required in the response, the parameter needs to be set to 0.

**maxRows**: Parameter to override the maximum rows returned by the rows parameter, i.e, 100. Fetching more products in the API response can adversely impact the latency; hence, the maxRows parameter should be used only where necessary.

```Text Sampel Request
http://search.unbxd.io/c85ec9e6c53e6522f2d0f88c4a214717/hsn-com700091495001458/search?&q=red&rows=500&maxRows=500&fields=uniqueId
```

This request will return 500 products.

***

## Filtering

Filters are applied to fetch only the details you need, reducing the latency time. To use a filter on the search result page, specify the filter attribute and value in the "filter" parameter. The API supports multiple types of filters.

* User can select a single value from a filter:

```Text Sample Request 
https://search.unbxd.io/fb853e3332f2645fac9d71dc63e09ec1/demo-unbxd700181503576558/search?q=dress&version=V2&filter=gender_uFilter:”women”
```