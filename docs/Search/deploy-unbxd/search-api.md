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

| Parameter           | Description                                                                                                                                                                           | Significance                                                                                           |
| :------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------------------- |
| unbxd-user-id       | Unique identification for the visitors. Example: uid-1466015353887-20419. The Unbxd Analytics JavaScript sets the userid in your browser cookie.                                      | If not passed, personalization, segmentation, and A/B testing of merchandising campaigns will not work |
| user-agent          | Browser identification information is passed to the web server with every HTTPS request.                                                                                              | If not passed, device-based merchandising campaigns will not work.                                     |
| unbxd-device-type\* | This header is an Unbxd custom header, which is required to identify if the request is coming from an app.                                                                            | If not passed, device-based merchandising campaigns cannot differentiate between browsers and apps.    |
| Accept-Encoding     | This header signifies the response's content encoding. Currently, Unbxd supports only gzip compression. To enable this, ‘gzip’ needs to be passed.                                    | If not passed, the response will not be compressed.                                                    |
| X-Forwarded-For     | This header signifies the end-user's IP address. It is primarily required if the integration is a backend, as Unbxd doesn’t get the IP of the end-user from the browser in that case. | If not passed, segmentation, A/B testing, and personalization will not work.                           |

#### \*unbxd-device-type:

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

* User can select multiple values from the filter:

```Text Sample Request
https://search.unbxd.io/fb853e3332f2645fac9d71dc63e09ec1/demo-unbxd700181503576558/search?q=dress&version=V2&filter=type_uFilter:”Shirt” OR ”type_uFilter=”Mini”&facet.multiselect=true
```

* User can select single values from multiple filters:

```Text Sample Request
https://search.unbxd.io/fb853e3332f2645fac9d71dc63e09ec1/demo-unbxd700181503576558/search?q=dress&version=V2&filter=type_uFilter:”Shirt”&filter=collar_uFilter:”Point”&facet.multiselect=true
```

* User can select multiple values from multiple filters:

```Text Sample Request
https://search.unbxd.io/fb853e3332f2645fac9d71dc63e09ec1/demo-unbxd700181503576558/search?q=dress&version=V2&filter=type_uFilter:”Shirt”&filter=collar_uFilter:”Point” OR collar_uFilter:”Spread”&facet.multiselect=true
```

* User can select range filter:

```Text Sample Request
https://search.unbxd.io/fb853e3332f2645fac9d71dc63e09ec1/demo-unbxd700181503576558/search?q=dress&filter=price:[0 TO 40]&version=V2
```

***

## Sorting

The sort parameter ranks the products based on specified fields in the specified order. It is an optional parameter. If not passed, products will be returned and ordered on the Unbxd relevancy algorithm.

**Sorting on a Single Field**: You can sort your search API results using a sort function as shown below:

E.g. for the first page of results, the start=0 and rows=20

For the next page of results, the start= 20 and rows=20.

```Text Sample Request
https://search.unbxd.io/fb853e3332f2645fac9d71dc63e09ec1/demo-unbxd700181503576558/search?q=dress&version=V2&sort=fieldname sort_order 
```

* **fieldname**: The field on which the sort is applied.
* **sort\_order**: The order in which the sort is applied. This value can be “asc” (for ascending) or “desc” (for descending)

For example, a visitor wants to sort results on price in ascending order, the API call below is made:

```Text Sample Request
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search?q=shirt&version=V2&sort=price%20asc
```

> 📘 NOTE
>
> There is a space between the field name and the sort\_order in the API call.

**Sorting on Multiple Fields**

To apply multiple sort rules, you need to make an API call as shown below:

```Text Sample Request
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/sort=field1 sort_order,field2 sort_order,field3 sort_order 
```

For example, to show results sorted on price and title the API call below is made:

```Text Sample Request
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search&q=mobile&filter=categoryPath"Mobiles & Tablets"&filter=brand_uFilter:"Apple"&filter=product_min_price:[35000 TO 37500]&version=V2&facet.multiselect=true 
```

> 📘 NOTE
>
> When multiple sort parameters are applied, the products will be sorted based on the first criteria passed in the request. Only in the case when multiple products have the same value for the first criteria, then the latter sorting criteria will be applied within those products.

***

## Banners

Banners can easily be configured from your dashboard during campaign creation. Once you have correctly configured your banner, the search API call will return the banner information as part of the catalog-based response.

This feature can be disabled from the HTTPS request using the ‘banner’ parameter.

```Text Custom Request
https://search.unbxd.io/<api-key>/<site-key>/search?q=<query>&banner=false&version=V2   
```

```Text Response for Hosted Banners
{
    "banner": {
        "banners": [{
            "imageUrl": "value",
            "landingUrl": "value",
            "bannerHtml": null
        }]
    }
}
```

```Text Response for Custom Banners
{
    "banner": {
        "banners": [{
            "imageUrl": null,
            "landingUrl": null,
            "bannerHtml": "value "
        }]
    }
}
{
    "banner": {
        "banners": [{
            "imageUrl": null,
            "landingUrl": null,
            "bannerHtml": "value "
        }]
    }
}
```

* **imageUrl**: The URL of the hosted banner image.
* **landingUrl**: The page URL visitors arrive at after clicking the banner.
* **bannerHtml**: The URL of the custom (HTML) banner image.

> 📘 NOTE
>
> The value of the response parameters will change to "null" according to the type of banner configuration.

For example, if a visitor searches a query, the banner response below will help you set up a hosted banner in your e-commerce site:

```Text Response for Hosted Banners
{
    "banner": {
        "banners": [{
"imageUrl":"http://www.myecommercewebsite.com/images/iphone-cases-banner.jpg",
"landingUrl":"http://www.myecommercewebsite.com/search?q=iphone%20cases",
            "bannerHtml": null
        }]
    }
}
```

***

## Redirects

Redirects visitors to a web page for the search query. This helps visitors navigate to the category pages as well as non-catalog-based information of the website, such as contact information, privacy policy, etc., right from your site’s search box. Redirects for a query can be configured from the Merchandising section of your Console.

By default, the value of redirects is enabled.

```Text Sample Request
https://search.unbxd.com/64a4a2592a648ac8415e13c561e44991/demosite-u1407617955968/search?q=iphone%20cases&redirect=false
```

```Text Response
{
    "searchMetaData": {
        "status": 0,
        "queryTime": 716,
        "queryParams": {
            "redirect": "false",
            "q": "iphone cases",
            "removeSpecialCharacters": "true",
            "escapeSpecialCharacters": "true",
            "boost": "sum(1,popularity(uniqueId))",
            "type": "interpreter",
            "personalization.recentlyViewed": "true",
            "queryTrimmer": "true"
        }
    },
    "response": {
        "numberOfProducts": 89,
        "start": 0,
        "products": [
            {
                "uniqueId": "5315b8565e4016e5737be4a7",
                "category": [
                    "women"
                ],
                "category_fq": [
                    "women"
                ],
                "test_fq": [
                    "women"
                ],
                "description": "A zebra with attitude lends new dimension to a sturdy holographic-print case that keeps your iPhone safe from scratches. Fits iPhone 5 and 5s.Polycarbonate.By MARC BY MARC JACOBS; imported.",
                "title": "'Zebra' Lenticular iPhone 5 & 5s Case",
                "color": [
                    "Orange Multi"
                ],
                "color_fq": [
                    "Orange Multi"
                ],
                "gender": "women",
                "imageUrl": [
                    "http://g.nordstromimage.com/imagegallery/store/product/Medium/1/_8493781.jpg"
                ],
                "image_link": "http://g.nordstromimage.com/imagegallery/store/product/Medium/1/_8493781.jpg",
                "catlevel1Name": "women",
                "pname": "'Zebra' Lenticular iPhone 5 & 5s Case",
                "price": 2803.0,
                "price_fq": 2803.0,
                "brand": "MARC BY MARC JACOBS",
                "brand_fq": "MARC BY MARC JACOBS",
                "test2_fq": "MARC BY MARC JACOBS",
                "categories": [
                    "Women"
                ],
                "cat_fq": [
                    "Women"
                ],
                "size": [
                    "NA"
                ],
                "size_fq": [
                    "NA"
                ]
            },
         {...}
```

> 📘 NOTE
>
> If you want to forcefully override redirect response with search response, set value to false.

***

## Fields

Defines attributes for a product like color, size, etc. The fields parameter specifies the set of fields to be returned, a comma-separated list of field names. Only fields in the list will be included when returning the results. It is an optional parameter; however, passing only the fields required in the response is recommended to reduce the response size and latency.

```Text Sample Request
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search?q=shirt&fields=title,vPrice&version=V2
```

```Text Response
{
    "searchMetaData": {
        "status": 0,
        "queryTime": 20,
        "queryParams": {
            "log.response": "false",
            "original.q": "*",
            "module.exclude": "personalization",
            "alternate.op": "true",
            "req.rm.asterix": "true",
            "q.op": "AND",
            "version": "V2",
            "enableTaxonomy": "false",
            "q": "*",
            "req.rm.promotionEngine": "true",
            "user.behaviour": "true",
            "fields": "title,vPrice",
            "enablePopularity": "true"
        }
    },
    "response": {
        "numberOfProducts": 7,
        "start": 0,
        "products": [
            {
                "vPrice": [
                    150.0
                ],
                "uniqueId": "parent-id-2_child-5",
                "title": "Oxford Formal Shoes"
            },
            {
                "vPrice": [
                    150.0
                ],
                "uniqueId": "parent-id-2_child-4",
                "title": "Oxford Formal Shoes"
            },
            {
                "uniqueId": "parent-id-2",
                "title": "Oxford Formal Shoes"
            },
            {
                "vPrice": [
                    50.0
                ],
                "uniqueId": "parent-id-1_child-3",
                "title": "Ralph Lauren formal shirt"
            },
            {
                "vPrice": [
                    45.0
                ],
                "uniqueId": "parent-id-1_child-2",
                "title": "Ralph Lauren formal shirt"
            },
            {
                "vPrice": [
                    50.0
                ],
                "uniqueId": "parent-id-1_child-1",
                "title": "Ralph Lauren formal shirt"
            },
            {
                "uniqueId": "parent-id-1",
                "title": "Ralph Lauren formal shirt"
            }
        ]
    }
}
```

***

## Fallback

Visitors may misspell when searching for an item on your website. The site must be able to autocorrect the misspelled words and display the most relevant search results without waiting for the customer to request results for the correctly spelled search query.

The fallback flag will spellcheck the search query and display results for the autocorrected search query.

Spellcheck can also be enabled or disabled in a request.

By default, `spellcheck=true`, so spellcheck is enabled.

```Text Sample Request
https://search.unbxd.com/64a4a2592a648ac8415e13c561e44991/demosite-u1407617955968/search?q=shits&fallback=true&fallback.method=spellcheck
```

```Text Reponse
{
    "searchMetaData": {
        "status": 0,
        "queryTime": 470,
        "queryParams": {
            "q": "shits",
            "removeSpecialCharacters": "true",
            "escapeSpecialCharacters": "true",
            "fallback.method": "spellcheck",
            "boost": "sum(1,popularity(uniqueId))",
            "type": "interpreter",
            "amp;fallback": "true",
            "personalization.recentlyViewed": "true",
            "queryTrimmer": "true"
        }
    },
    "response": {
        "numberOfProducts": 0,
        "start": 0,
        "products": []
    },
    "facets": {
        "price_fq": {
            "type": "facet_ranges",
            "values": {
                "counts": [],
                "gap": 100.0,
                "start": 100.0,
                "end": 1000.0
            },
            "position": 1,
            "displayName": "price_fq"
        },
        "category_fq": {
            "type": "facet_fields",
            "values": [],
            "position": 2,
            "displayName": "category_fq"
        },
        "color_fq": {
            "type": "facet_fields",
            "values": [],
            "position": 3,
            "displayName": "color_fq"
        },
        "brand_fq": {
            "type": "facet_fields",
            "values": [],
            "position": 4,
            "displayName": "brand_fq"
        },
        "size_fq": {
            "type": "facet_fields",
            "values": [],
            "position": 5,
            "displayName": "size_fq"
        },
        "cat_fq": {
            "type": "facet_fields",
            "values": [],
            "position": 6,
            "displayName": "cat_fq"
        },
        "test_fq": {
            "type": "facet_fields",
            "values": [],
            "position": 7,
            "displayName": "test_fq"
        },
        "test1_fq": {
            "type": "facet_fields",
            "values": [],
            "position": 8,
            "displayName": "test1_fq"
        },
        "test2_fq": {
            "type": "facet_fields",
            "values": [],
            "position": 9,
            "displayName": "test2_fq"
        }
    },
    "didYouMean": [
        {
            "suggestion": "shirt",
            "frequency": "1101"
        }
    ]
}
         {...}
```

***

## Relevant Document

When the user enters a query where the keyword matches more with the variant product, the search API shows the attribute “`relevantDocument`” with the value “`variants`” and the first variant available in the “`variants`” array in the API response is the relevant variant. In other cases, the “`relevantDocument`” is “parent” when the master product matches the query.

***

## Format

The format parameter specifies the format for generating the response result. Possible values are ‘JSON’ or ‘XML’. It is an optional parameter, and the default value is ‘JSON’.

```Text Sample request to get JSON response
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search?q=shirt&format=json&version=V2
```

```Text Sample JSON Response
{
    "searchMetaData": {
        "status": 0,
        "queryTime": 27,
        "queryParams": {
            "log.response": "false",
            "original.q": "shoes",
            "module.exclude": "personalization",
            "format": "json",
            "alternate.op": "true",
            "req.rm.asterix": "true",
            "q.op": "AND",
            "version": "V2",
            "enableTaxonomy": "false",
            "q": "shoes",
            "req.rm.promotionEngine": "true",
            "user.behaviour": "true",
            "enablePopularity": "true"
        }
    },
    "response": {
        "numberOfProducts": 0,
        "start": 0,
        "products": []
    }
}
```

```Text Sample request to get XML response
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search?q=shirt&format=xml&version=V2
```

```Text XML Response
<?xml version="1.0" encoding="UTF-8”?>
<response>
    <lst name="searchMetaData">
        <int name="status">0</int>
        <long name="queryTime">26</long>
        <lst name="queryParams">
            <str name=“log.response”>false</str>
           <str name=“original.q”>shoes</str>
            <str name=“module.exclude”>personalization</str>
            <str name=“format”>xml</str>
            <str name=“alternate.op”>true</str>
            <str name=“req.rm.asterix”>true</str>
            <str name=“q.op”>AND</str>
            <str name=“version”>V2</str>
            <str name=“enableTaxonomy”>false</str>
            <str name=“q”>shoes</str>
            <str name=“req.rm.promotionEngine”>true</str>
            <str name=“user.behaviour”>true</str>
            <str name=“enablePopularity”>true</str>
        </lst>
    </lst>
    <result name="response" numberOfProducts="0" start="0">
</result>
    <lst name="facets"/>
</response>
```

***

## Bucketing

Bucketing allows you to group products with a common field value into groups known as buckets, returning the top products per bucket, and the top buckets based on what documents are in the groups. It is necessary that every bucket field is also the facet field in your e-commerce store. To use bucketing feature, you need to use bucket.field, bucket.limit and bucket.offset parameters to define the field name on which bucketing has to be done, the number of products that should be returned per bucket and bucket.offset parameter to define the starting position of the product returned in each bucket. The rows parameter controls the number of buckets that should be returned.

For example, a search at your site for a common term such as DVD, will show the top 3 results for each category (“TVs & Video”,”Movies”,”Computers”, etc).

```Text Sample request
https://search.unbxdapi.io/<API-KEY>/<SITE-KEY>/search?q=Shirts&format=<xml|json>&& bucket.field=<bucket.field>&<rows=42><bucket.limit=5>&&<bucket.offset=5> &<sort>&bucket.sortByCount=desc&sort=<sort field>desc  
```

```Text Response
"buckets":{
                "totalProducts":22331,
                "numberOfBuckets":386,
                "":{"numberOfProducts":168,"start":0,"products":[
                                {
                                        product_1
                                },
                                .
                                .
                                .
                                {
                                        product_N
                                }]
                },
                "":{"numberOfProducts":4098,"start":0,"products":[
                                {
                                        product_1
                                },
                                .
                                .
                                .
                                {
                                        product_N
                                }]
                },
                "":{"numberOfProducts":1370,"start":0,"products":[
                                {
                                        product_1
                                },
                                .
                                .
                                .
                                {
                                        product_N
                                }]
                }
        }
```

***

## Analytics

The analytics parameter is used specifically for enabling visual autosuggest. It enables or disables tracking the query hit for analytics. By default, tracking is enabled. To disable tracking, set the value to false.

```Text Sample request
https://search.unbxd.com/64a4a2592a648ac8415e13c561e44991/demosite-u1407617955968/search?q=&analytics=false&version=V2
```

```Text Response
{
    "searchMetaData": {
        "status": 0,
        "queryTime": 727,
        "queryParams": {
            "analytics": "false",
            "q": "shirts",
            "removeSpecialCharacters": "true",
            "escapeSpecialCharacters": "true",
            "boost": "sum(1,popularity(uniqueId))",
            "type": "interpreter",
            "version": "V2",
            "personalization.recentlyViewed": "true",
            "queryTrimmer": "true"
        }
    },
    "response": {
        "numberOfProducts": 1101,
        "start": 0,
        "products": [
            {
                "uniqueId": "5315b8565e4016e5737bef50",
                "category": [
                    "Sport Shirts"
                ],
                "category_fq": [
                    "Sport Shirts"
                ],
                "test_fq": [
                    "Sport Shirts"
                ],
                "productDescription": "Button-down point collar. Applied buttoned placket.Long sleeves with barrel cuffs. Curved hem.Split back yoke for smooth, contoured shoulders. Our signature embroidered pony accents the left chest. 100% cotton. Machine washable. Imported.",
                "title": "Custom-Fit Tattersall Shirt",
                "url": "http://www.ralphlauren.com/product/index.jsp?productId=23840006",
                "gender": "men",
                "imageUrl": [
                    "http://www.ralphlauren.com/graphics/product_images/pPOLO2-16755537_standard_t240.jpg"
                ],
                "brand": "Ralph Lauren",
                "brand_fq": "Ralph Lauren",
                "test2_fq": "Ralph Lauren",
                "taxID": "11",
                "image_link": "http://www.ralphlauren.com/graphics/product_images/pPOLO2-16755537_standard_t240.jpg",
                "color": [
                    "Blue/Navy"
                ],
                "color_fq": [
                    "Blue/Navy"
                ],
                "catlevel1Name": "Sport Shirts",
                "pname": "Custom-Fit Tattersall Shirt",
                "price": 89.5,
                "price_fq": 89.5,
                "id": "product-23840006"
            },
         {...}
```

***

## Stats

Gives information about the products with highest and lowest field value. Applicable only on fields with numeric or decimal values.

To apply stats on the price field make the below API call:

```Text Sample Request
https://search.unbxd.com/64a4a2592a648ac8415e13c561e44991/demosite-u1407617955968/search?q=shirts&stats=price&version=V2
```

```Text Response
{
    "searchMetaData": {
        "status": 0,
        "queryTime": 726,
        "queryParams": {
            "q": "shirts",
            "removeSpecialCharacters": "true",
            "escapeSpecialCharacters": "true",
            "stats": "price",
            "boost": "sum(1,popularity(uniqueId))",
            "type": "interpreter",
            "version": "V2",
            "personalization.recentlyViewed": "true",
            "queryTrimmer": "true"
        }
    },
    "response": {
        "numberOfProducts": 1101,
        "start": 0,
        "products": [
            {
                "uniqueId": "5315b8565e4016e5737bef50",
                "category": [
                    "Sport Shirts"
                ],
                "category_fq": [
                    "Sport Shirts"
                ],
                "test_fq": [
                    "Sport Shirts"
                ],
                "productDescription": "Button-down point collar. Applied buttoned placket.Long sleeves with barrel cuffs. Curved hem.Split back yoke for smooth, contoured shoulders. Our signature embroidered pony accents the left chest. 100% cotton. Machine washable. Imported.",
                "title": "Custom-Fit Tattersall Shirt",
                "url": "http://www.ralphlauren.com/product/index.jsp?productId=23840006",
                "gender": "men",
                "imageUrl": [
                    "http://www.ralphlauren.com/graphics/product_images/pPOLO2-16755537_standard_t240.jpg"
                ],
                "brand": "Ralph Lauren",
                "brand_fq": "Ralph Lauren",
                "test2_fq": "Ralph Lauren",
                "taxID": "11",
                "image_link": "http://www.ralphlauren.com/graphics/product_images/pPOLO2-16755537_standard_t240.jpg",
                "color": [
                    "Blue/Navy"
                ],
                "color_fq": [
                    "Blue/Navy"
                ],
                "catlevel1Name": "Sport Shirts",
                "pname": "Custom-Fit Tattersall Shirt",
                "price": 89.5,
                "price_fq": 89.5,
                "id": "product-23840006"
            },
         {...}
```

***

## Variants

Variants cover all the parameters related to the variants feature. To integrate any functionality, we have to set variants=true (to enable variants).

The feed defines variants for a product. If the product doesn’t have variants, the variants parameter is disabled in the API response, and if it does, it is defined as enabled.

It can have two values, viz. True or False.

* If “variants” is set to true, all the variants for a product are clubbed together.
* If “variants” is set to false, all the variants are sent separately as different products.

> 📘 NOTE
>
> The default value is set to false.

```Text Request with variants enabled
https://search.unbxd.com/64a4a2592a648ac8415e13c561e44991/demosite-u1407617955968/search?q=dress&variants=true
```

```Text Request with variants disabled
https://search.unbxd.com/64a4a2592a648ac8415e13c561e44991/demosite-u1407617955968/search?q=dress&variants=false
```

## Variants Count

This parameter limits the number of variants that must be returned per product. This is equivalent to the rows parameter.

* This is an integer parameter, if not specified, is set to default value of 1
* When there is a need to enable all the variants, specify variants.count=\*. Please avoid using this value, as this would lead to performance degradation.

If you want to get more than one variant in the API response, you can use this parameter.

```Text Request with variants count
http://search.unbxd.io/c85ec9e6c53e6522f2d0f88c4a214717/hsn-com700091495001458/search?q=dress&variants=true&variants.count=1
```

```Text Response
{
    "searchMetaData": {
        "status": 0,
        "queryTime": 42,
        "queryParams": {
            "log.response": "false",
            "module.exclude": "none",
            "alternate.op": "true",
            "enableTrendingProducts": "true",
            "q.op": "AND",
            "variants": "true",
            "variants.count": "1",
            "f.categoryPath.facet.limit": "100",
            "f.categoryPath.position": "1",
            "req.rm.promotionEngine": "true",
            "f.categoryPath.nameId": "true",
            "original.q": "dress",
            "req.rm.asterix": "true",
            "enableTaxonomy": "false",
            "version": "V2",
            "f.categoryPath.displayName": "Category",
            "q": "dress",
            "f.categoryPath.max.depth": "4",
            "promotion.fields": [
                "categoryPath1_uFilter",
                "categoryPath2_uFilter",
                "Brand_uFilter"
            ],
            "facet.multilevel": "categoryPath",
            "user.behaviour": "true",
            "fallback": "true",
            "fallback.response": "false",
            "enablePopularity": "true"
        }
    },
    "response": {
        "numberOfProducts": 0,
        "start": 0,
        "products": []
    },
    "redirect": {
        "type": "url",
        "value": "https://www.hsn.com/shop/dresses/fa0283"
    }
}
```

***

## Facets Overview

Faceting helps your shoppers narrow down search results by selecting filter values as needed. Every time a user clicks a facet value, the results are reduced to only the items with that value. Additional clicks continue to narrow down the search—the previous facet values are remembered and applied again.

Facets can be easily configured from the **Manage** -> **Configure Search** -> **Configure Facet** section of the Console.

```Text Sample Request
https://search.unbxd.io/<api_key>/<site_key>/search?q=samsung&facet.multiselect=true
```

```Text Sample Request
{
    "facets": {
        "multilevel": {
            "list": [{
                "filterField": "productType",
                "level": 2,
                "id": "100",
                "displayName": "Product Type",
                "position": 1,
                "values": [{
                        "id": "HO001",
                        "name": "Decor",
                        "count": 15
                    },
                    {
                        "id": "Ho002",
                        "name": "Outdoors",
                        "count": 16
                    }
                ],
                "breadcrumb": {
                    "filterField": "productType",
                    "values": [{
                        "id": "HO",
                        "name": "Home"
                    }],
                    "level": 1
                }

            }]
        },
        "range": {
            "list": []
        },
        "text": {
            "list": []
        }
    }
}
```

<br />

Here, when a search API is fired, “facet” is received in response.

Facet response contains different types of facets (for example, Categories, Brand , Color, Price etc..) that are configured by client with respective values and count of those values. For example, if Brand is configured for faceting, response will look like:

```
{
  "facets": {
    "text": {
      "list": [
        {
          "facetName": "brand_uFilter",
          "filterField": "brand_uFilter",
          "values": [
            "Samsung",
            663
          ],
          "displayName": "brand",
          "position": 3
        }
      ]
    }
  }
}
```

Response contains Facet Name: Brand, Value: Samsung, and Count of products with filter Samsung = 663.

If integrated, the website will look like:

<Image align="center" className="border" border={true} width="50% " src="https://files.readme.io/4f8b47c0f6f7715a51bb9e83fe07e2fbf585cfa852182656deedfc322c827d0b-facet-exam.png" />

***

## Common Feature Across all Facets

### 1. MultiSelect Facet

Multi-select facet is the option to enable or disable the customers to select more than one facet at a time for a query.

```Text Sample Request
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search?&q=mobile&filter=categoryPath"Mobiles & Tablets"&filter=brand_uFilter:"Apple"&filter=product_min_price:[35000 TO 37500]&version=V2&facet.multiselect=true 
```
```Text Response
{
  "facets": {
    "multilevel": {},
    "range": {
      "list": [
        {
          "facetName": "product_min_price",
          "values": {
            "counts": [
              "35000.0",
              1,
              "37500.0",
              3,
              "40000.0",
              5
            ],
            "gap": 2500,
            "start": 0,
            "end": 2635000
          },
          "displayName": "price",
          "position": 1
        }
      ]
    },
    "text": {
"list": [
        {



          "facetName": "brand_uFilter",
          "filterField": "brand_uFilter",
          "values": [
            "Apple",
            1,
            "LG",
            4,
            "Samsung",
            9,
            "Sony Xperia",
            3
          ],
          "displayName": "brand",
          "position": 3
        }
      ]
    }
  }
}
```

<br />

### 2. SelectedFacet

This displays the values of a single facet or multiple selected facets. If you selecet the facet 'brand' then the values 'Apple', 'Samsung', and so are displayed.

```Text Sample Request 
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search?&q=mobile&filter=brand_uFilter:%22Apple%22&facet.multiselect=true&selectedfacet=true
```
```Text Response
{
  "response": {
    "numberOfProducts": 47,
    "products": []
  },
  "searchMetaData": {},
  "facets": {
    "text": {
      "list": [
        {
          "facetName": "brand_uFilter",
          "filterField": "brand_uFilter",
          "values": [
            "Acer",
            1,
            "Apple",
            47,
            "Gionee",
            28,
            "Google",
            10,
            "HTC",
            20
          ],
          "displayName": "brand",
 "position": 0
        },
        {
          "facetName": "color_uFilter",
          "filterField": "color_uFilter",
          "values": [
            "Black",
            99,
            "Gold",
            80,
            "White",
            48,
            "Silver",
            31,
            "Grey",
            24
          ],
          "displayName": "color",
          "position": 1
        },
        {
"selected": [
            {
              "facetName": "brand_uFilter",
              "position": 3,
              "filterField": "brand_uFilter",
              "displayName": "brand",
              "values": [
                "Apple"
              ]
            }
          ]
        }
      ]
    }
}
}
```

<br />

### 3. Disabling Facet

If facets are not needed, we can disable them. Value of facets can be either 'false' or 'true'. Facet: Disabled in response

```Text Sample Request
http://search.unbxd.io/c85ec9e6c53e6522f2d0f88c4a214717/hsn-com700091495001458/search?&q=mobile&facet=false
```
```Text Response
{
  "response": {
    "numberOfProducts": 490,
    "start": 0,
    "products": []
  },
  "searchMetaData": {}
}
```

<br />

***

## Multilevel Facet

You can build a hierarchy in your facet values to enable multi-level navigation and filtering. This pattern is great for very long lists of values and to improve discoverability: your users will be able to browse up and down in the levels to refine their searches.

| Property    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| :---------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| multilevel  | Hierarchical facets configured on the hierarchical field(s). Facets are grouped under their respective types, so that it is easy to deserialize them. Currently, we support “multilevel” (MultiLevel Facets), “text” (Text Facets), “range” (Range Facets).                                                                                                                                                                                                                                                            |
| list        | Array of hierarchical facets as configured on the hierarchical fields in Unbxd Console.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| values      | All the unique values for the sub categories available for query and their count. For example, for query “mobile” , values are “Mobiles & Tablets”(300) , “Smartphones” (36) and so on.. This means for query mobile , under multilevel facet we have Mobiles & Tablets, Smartphones as filters ( values) and total number of products available with that value is also available. Shopper can select any value among ( Mobiles & Tablets , Smartphones ..) and that value will be applied as filter in search query. |
| level       | Depth of multilevel field.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| filterField | Field on which hierarchical facet is created                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| breadcrumb  | Position within the hierarchical field where the results appear.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

<br />

### 1. When no Facet is selected

When no facets are selected (or no filters are passed), API is going to respond with facets belonging to the first level of the field.

```Text Sample Request
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search?&q=mobile&version=V2
```
```Text Response
{
"searchMetaData": {...},
"response": {...},
"facets":
 {
    "multilevel": {
        "list": [{
                "filterField": "productType",
                "level": 1,
                "id": "100",
                "displayName": "Product Type",
                "position": 1,
                "values": [{
                        "id": "HO",
                        "name": "Home",
                        "count": 31
                    },
                    {
                        "id": "J",
                        "name": "Jewelry",
                        "count": 22
                    }
                ],
                "breadcrumb": {}
            },
            {
                "filterField": "theme",
                "level": 1,
                "id": "200",
                "displayName": "Theme",
                "position": 2,
                "values": [{
                        "id": "12",
                        "name": "Animals",
                        "count": 34
                    },
                    {
                        "id": "13",
                        "name": "Birds",
                        "count": 21
                    }
                ],
                "breadcrumb": {}
            }
        ]
    }
}
}
```

### 2. When first level of facets are selected

When first level of facets are selected, the API will respond with the second level of field values.

```Text Sample Request
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/
search?&q=mobile&version=V2&filter=productType:"Home"
```
```Text Response 
{
"searchMetaData": {...},
"response": {...},
"facets":
{
    "multilevel": {
        "list": [{
                "filterField": "productType",
                "level": 2,
                "id": "100",
                "displayName": "Product Type",
                "position": 1,
                "values": [{
                        "id": "HO001",
                        "name": "Decor",
                        "count": 15
                    },
                    {
                        "id": "HO002",
                        "name": "Outdoors",
                        "count": 16
                    }
                ],
                "breadcrumb": {
                    "filterField": "productType",
                    "values": [{
                        "id": "HO",
                        "name": "Home"
                    }],
                    "level": 1
                }

            },
            {
                "filterField": "theme",
                "level": 1,
                "id": "200",
                "displayName": "Theme",
                "position": 2,
                "values": [{
                        "id": "12",
                        "name": "Animals",
                        "count": 34
                    },
                    {
                        "id": "13",
                        "name": "Birds",
                        "count": 21
                    }
                ],
                "breadcrumb": {
                    "filterField": "theme",
                    "values": [{
                        "id": "21",
                        "name": "MNP"
                    }],
                    "child": {
                        "filterField": "theme",
                        "values": [{
                            "id": "23",
                            "name": "ZZZ"
                        }],
                        "level": 2
                    },
                    "level": 1
                }
            }
        ]
    }
}
}
```

### 3. When second level of facets are selected

When the second level of facets are selected, API will respond with the third level of field values.

```Text Sample Request 
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/
search?&q=mobile&version=V2&&filter=productType:"Home>Decor"
```
```Text Response
{
"searchMetaData": {...},
"response": {...},
"facets":
{
{
    "multilevel": {
        "list": [{
                "filterField": "productType",
                "level": 3,
                "id": "100",
                "displayName": "Product Type",
                "position": 1,
                "values": [{
                        "id": "HO011",
                        "name": "Wall Decor",
                        "count": 10
                    },
                    {
                        "id": "Ho012",

                        "name": "Floor Decor",
                        "count": 5
                    }
                ],
                "breadcrumb": {
                    "filterField": "productType",
                    "values": [{
                        "id": "HO",
                        "name": "Home"
                    }],
                    "child": {
                        "filterField": "productType",
                        "values": [{
                            "id": "HO001",
                            "name": "Decor"
                        }],
                        "level": 2
                    },
                    "level": 1
                }

            },
            {
                "filterField": "theme",
                "level": 1,
                "id": "200",
                "displayName": "Theme",
                "position": 2,
                "values": [{
                        "id": "12",
                        "name": "Animals",
                        "count": 34
                    },
                    {
                        "id": "13",
                        "name": "Birds",
                        "count": 21
                    }
                ],
                "breadcrumb": {
                    "filterField": "theme",
                    "values": [{
                        "id": "21",
                        "name": "MNP"
                    }],
                    "child": {

                        "filterField": "theme",
                        "values": [{
                            "id": "23",
                            "name": "ZZZ"
                        }],
                        "level": 2
                    },
                    "level": 1
                }
            }
        ]
    }
}
```

<br />

### 4. When the value from the last level is selected

When the value from the last level is selected, API will respond back with the sibling field values from the last level

Sample Request

Here is the API when the “*Home>Decor>Wall Decor*” is selected:

```Text Sample Response 
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/
search?&q=mobile&version=V2&filter=productType:"Home>Decor>Wall Decor"  
```
```Text Reponse 
{
"searchMetaData": {...},
"response": {...},
"facets":
{
{
    "multilevel": {
        "list": [{
                "filterField": "productType",
                "level": 3,
                "id": "100",
                "displayName": "Product Type",
                "position": 1,
                "values": [{
                        "id": "HO011",
                        "name": "Wall Decor",
                        "count": 10
                    },
                    {
                        "id": "Ho012",
                        "name": "Floor Decor",
                        "count": 5
                    }
                ],
                "breadcrumb": {
                    "filterField": "productType",
                    "values": [{
                        "id": "HO",
                        "name": "Home"
                    }],
                    "child": {
                        "filterField": "productType",
                        "values": [{
                            "id": "HO001",
                            "name": "Decor"
                        }],
                        "child": {
                            "filterField": "productType",
                            "values": [{
                                "id": "HO011",
                                "name": "Wall Decor"
                            }],
                            "level": 3
                        },
                        "level": 2
                    },
                    "level": 1      }],

                    "child": {
                        "filterField": "productType",
                        "values": [{
                            "id": "HO001",
                            "name": "Decor"
                        }],
                        "child": {
                            "filterField": "productType",
                            "values": [{
                                "id": "HO011",
                                "name": "Wall Decor"
                            }],
                            "level": 3
                        },
                        "level": 2
                    },
                    "level": 1
                }
            },
            {
                "filterField": "theme",
                "level": 1,
                "id": "200",
                "displayName": "Theme",
                "position": 2,
                "values": [{
                        "id": "12",
                        "name": "Animals",
                        "count": 34
                    },
                    {
                        "id": "13",
                        "name": "Birds",
                        "count": 21
                    }
                ],
                "breadcrumb": {
                    "filterField": "theme",
                    "values": [{
                        "id": "21",
                        "name": "MNP"
                    }],

                    "child": {
                        "filterField": "theme",
                        "values": [{
                            "id": "23",
                            "name": "ZZZ"
                        }],
                        "level": 2
                    },
                    "level": 1
                }
            }
        ]
    }
}
}
```