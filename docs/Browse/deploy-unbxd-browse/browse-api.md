---
title: Browse API
deprecated: false
hidden: false
metadata:
  robots: index
---
The Browse API lets you interact with the Unbxd platform and implement all category related functionality with ease. The API can customize your page experience by leveraging various built-in features of Browse. You can also power any type of page using this API, such as, Category, Brand, or any other attribute.This API can communicate over HTTP and HTTPS.

You can use the JSON /XML response format and customize your search experience by leveraging various built-in features of Search. This API can communicate over HTTP and HTTPS. However, we recommend using the HTTPS protocol.

# Browse Endpoint

Request Method: **GET**

`https://search.unbxd.io/<API-KEY>/<SITE-KEY>/category?`

```Text Sample Request
https://search.unbxd.io///category?p=&version=V2  
&pagetype=boolean&format=<xml|json>&start=&rows=&filter-id=&sort=asc|desc&uid=&<fields=comma separated list of fields>&selectedfacet=true
```
```
```

## Authentication

Our APIs use an API\_KEY and a SITE\_KEY to authenticate search requests.

These keys are generated at the time of account creation and can be accessed within Console at **Manage** -> **Configure Site** -> **Keys**.

# Headers

Unbxd requires some header parameters along with the search request in order to provide support for personalization and merchandising campaigns created on location, browser or device type. Headers need to be passed through the URL to process the actual response.

For Search and Autosuggest API, we can enable personalization, segmentation, and A/B testing of the merchandising campaign. we recommend passing certain parameters as HTTP headers.

The following parameters are available:

| Parameter             | Description                                                                                                                                                                                 | Mandatory | Significance                                                                                                   |
| :-------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------- | :------------------------------------------------------------------------------------------------------------- |
| **unbxd-user-id**     | Unique identification for the visitors. Example: uid-1466015353887-20419. The Unbxd Analytics javascript sets the userid in your browser cookie.                                            | No        | If not passed, personalization, segmentation, and A/B testing of merchandising campaigns will not work.        |
| **user-agent**        | Browser identification information passed to the webserver with every HTTP request                                                                                                          | No        | If not passed, device-based merchandising campaigns will not work.                                             |
| **unbxd-device-type** | This header is an Unbxd custom header which is required to identify if the request is coming from an app.                                                                                   | No        | If not passed, device-based merchandising campaigns will not be able to differentiate between browser and apps |
| **Accept-Encoding**   | This header signifies the content encoding of the response. Currently, Unbxd supports only gzip compression. To enable this, ‘gzip’ needs to be passed                                      | No        | If not passed, the response will not be compressed.                                                            |
| **X-Forwarded-For**   | This header signifies the IP address of the end-user. This is primarily required if the integration is a backend as Unbxd doesn’t get the IP of the end-user from the browser in that case. | No        | If not passed, segmentation, A/B testing and personalization will not work.                                    |

\*unbxd-device-type:

```
 { "type": , "os": , "source":  }
```

possible values of “type” : “desktop”, “tablet”, “mobile”

possible values of “os” : “android”, “ios”, “windows”

possible values of “source” : “browser”, “app”

## Error Codes (descriptive : calling out APIs applicable)

* **404**: The 404 error status code indicates that the REST API can’t map the client’s URI to a resource but may be available in the future. Subsequent requests by the client are permissible.
* **200**: The 200 status is a Success Code.

## Request Parameters

The values of the request parameters are defined below:

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
        Data Types
      </th>

      <th>
        Possible Values/Format
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        p

        **Mandatory**
      </td>

      <td>
        Identifier of page being requested as Names.
      </td>

      <td>
        `String`
      </td>

      <td>
        n/a
      </td>
    </tr>

    <tr>
      <td>
        p-id

        **Mandatory**
      </td>

      <td>
        Identifier of page being requested as IDs.
      </td>

      <td>
        `Integer`
      </td>

      <td>
        n/a
      </td>
    </tr>

    <tr>
      <td>
        pagetype

        Mandatory
      </td>

      <td>
        Type of the page being requested.
      </td>

      <td>
        `String`
      </td>

      <td>
        n/a
      </td>
    </tr>

    <tr>
      <td>
        user-type

        **Mandatory**
      </td>

      <td>
        Number of times a user visits the site. Probable values can be: frequent,  first-time
      </td>

      <td>
        `String`
      </td>

      <td>
        Format:\
        “first-time”

        Supported Values: first-time, frequent
      </td>
    </tr>

    <tr>
      <td>
        uid

        Mandatory
      </td>

      <td>
        Unique identification id for visitors, value to pass can be obtained from unbxd.userId browser cookie
      </td>

      <td>
        `String`
      </td>

      <td>
        \&uid=uid-1666356549013-78531
      </td>
    </tr>

    <tr>
      <td>
        version

        Optional
      </td>

      <td>
        Version of the API.
      </td>

      <td>
        `String`
      </td>

      <td>
        Format:

        \&version=V2

        Supported Values: V1, V2
      </td>
    </tr>

    <tr>
      <td>
        format

        Optional
      </td>

      <td>
        Format of the response. This value can be: “xml” or “json”.
      </td>

      <td>
        `String`
      </td>

      <td>
        Format: \&format=xml

        Supported values: JSON, XML

        Default Value: JSON
      </td>
    </tr>

    <tr>
      <td>
        start

        Optional
      </td>

      <td>
        Offset in the complete result set.
      </td>

      <td>
        `Integer`
      </td>

      <td>
        Format: \&start=2

        Default Value: 0
      </td>
    </tr>

    <tr>
      <td>
        rows

        Optional
      </td>

      <td>
        Number of products in a single page. Set value as 0 if you don’t want products in the response.
      </td>

      <td>
        `Integer`
      </td>

      <td>
        Format: \&rows=2

        Default Value: 10
      </td>
    </tr>

    <tr>
      <td>
        variants

        Optional
      </td>

      <td>
        Enables or disables variants in the API response.
      </td>

      <td>
        `String`
      </td>

      <td>
        Format: \&variants=True

        Supported Values: True ,False

        Default value: False.
      </td>
    </tr>

    <tr>
      <td>
        variants.count

        Optional
      </td>

      <td>
        Number of variants to be sent in the API response.
      </td>

      <td>
        `Integer`
      </td>

      <td>
        Format: \&variants.count=5
      </td>
    </tr>

    <tr>
      <td>
        fields

        Optional
      </td>

      <td>
        Set of fields to be returned.
      </td>

      <td>
        `String`
      </td>

      <td>
        Format: \&fields=,

        Default Values: If not applied, returns all fields
      </td>
    </tr>

    <tr>
      <td>
        facet

        Optional
      </td>

      <td>
        Enables or disables displaying of facets in the UI. Note: All other parameters related to facet feature are mentioned in detail below.
      </td>

      <td>
        `String`
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        facet.multilevel

        Optional
      </td>

      <td>
        Enables or disables displaying multi-level facets in response.
      </td>

      <td>
        `String`
      </td>

      <td>
        n/a
      </td>
    </tr>

    <tr>
      <td>
        selectedfacet

        Optional
      </td>

      <td>
        Enables or disables sending selected facets in the API response.
      </td>

      <td>
        `String`
      </td>

      <td>
        false
      </td>
    </tr>

    <tr>
      <td>
        filter-id

        Optional
      </td>

      <td>
        Restrict the products based on criteria passed (using field-id).
      </td>

      <td>
        `Integer`
      </td>

      <td>
        n/a (no filter will be applied)
      </td>
    </tr>

    <tr>
      <td>
        filter

        Optional
      </td>

      <td>
        Restrict the products based on criteria passed (using field-name).
      </td>

      <td>
        `String`
      </td>

      <td>
        n/a (no filter will be applied)
      </td>
    </tr>

    <tr>
      <td>
        category-filter-id

        Optional
      </td>

      <td>
        Restrict the products based on category (using path comprised of category ID). Used only for multilevel-facets.
      </td>

      <td>
        `Integer`
      </td>

      <td>
        n/a (no filter will be applied)
      </td>
    </tr>

    <tr>
      <td>
        category-filter

        Optional
      </td>

      <td>
        Restrict the products based on category (using path comprised of category name). Used only for multilevel-facets.
      </td>

      <td>
        `String`
      </td>

      <td>
        n/a (no filter will be applied)
      </td>
    </tr>

    <tr>
      <td>
        sort

        Optional
      </td>

      <td>
        Rank products based on criteria passed.
      </td>

      <td>
        `String`
      </td>

      <td>
        n/a (default rank would be based on Unbxd relevancy)
      </td>
    </tr>

    <tr>
      <td>
        banner

        Optional
      </td>

      <td>
        Enables or disables displaying of banner set in the Console.
      </td>

      <td>
        `String`
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        analytics

        Optional
      </td>

      <td>
        Enables or disables tracking of the request by Unbxd analytics.
      </td>

      <td>
        `String`
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        stats

        Optional
      </td>

      <td>
        Specifies a field for which statistics should be generated.
      </td>

      <td>
        `String`
      </td>

      <td>
        n/a
      </td>
    </tr>
  </tbody>
</Table>

# Response Components

Unbxd returns the list of products that match the search criteria. The response would be in application/JSON or application/XML content type format.

| **Component**        | **Description**                                                                                                                        |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **status**           | Response status code defines if it is Ok (code 200), Not Found (code 404), Internal server error (code 500), and many more             |
| **queryTime**        | Time taken to process the shopper’s request                                                                                            |
| **queryParams**      | Parameters sent as a part of the request                                                                                               |
| **numberOfProducts** | Total number of products returned for the page                                                                                         |
| **start**            | Offset in the complete result set of products for the page                                                                             |
| **products**         | Product details sent as a result that matches the request query. The structure will be the same as passed in the feed                  |
| **relevantDocument** | Mentions if the parent or the variant for a particular product needs to be displayed in the UI. It can be either “parent” or “variant” |
| **facets**           | Filters displayed in the UI to allow visitors to narrow down the result set based on product fields                                    |
| **breadcrumb**       | Position in the field hierarchy                                                                                                        |
| **selected**         | Filters which are selected in the UI                                                                                                   |
| **banner**           | Banner response for the query                                                                                                          |

# Component Description

The aforementioned table provided as with the default values of the request parameters. Let’s dwell deep and understand the API calls of each parameter individually.

### Page Parameters

* **p-id**: Identifier of the page being requested as IDs. It is an optional parameter and has the following form p-id=field-id:value-id. For category page, field-id is “categoryPathId” and value-id is the corresponding category path comprised of category IDs. Example, p-id=categoryPathId:”J>J00157>J00158”. For any other page, field-id is corresponding field ID as passed in the feed and value-id is the corresponding value ID. Example, p-id=1:9357, p-id=12224:18010.
* **p**: Identifier of the page being requested as Names. It is an optional parameter and has the following form.

  p=fieldname:”fieldvalue”: Page rules in the console should be created as this)\
  p=\<value> (Field name is not specified): Page rules in console should be created with the name  \<value> . By using categoryPath as the default field.
  For category page, fieldname is “categoryPath” and fieldvalue is the corresponding category path comprised of category names. Example, p=categoryPath:”Jewelery>Necklaces>Beaded Necklaces”. For any other page, fieldname is corresponding field as passed in the feed and fieldvalue is the corresponding value. Example, p=Brand:”Nike”, p=Events:”40 Years of Innovation”

```Text Sample request
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:"Fashion>Shoes"&pagetype=boolean&rows=1&version=V2  
```

### Sample Response

```Text json
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

<br />

> 📘 Important Points
>
> It is mandatory to pass either “p” or “p-id”. If both are passed together, “p” would be ignored and results would be shown as per “p-id”.\
> The value passed under “p-id” (or “p”) is displayed in the Console and reports as-it-is.
> IMPORTANT: In the tracker api, the following parameters need to be passed:
>
> page: Pass the exact value as passed under “p-id” (or “p”).\
> page\_type: Always pass “BOOLEAN”.
> If you have a categorypath containing “&”, you will need to encode it in the request.
>
> Example,“Fashion>Shoes>Sneakers & Athletic shoes” will be encoded to“Fashion%3EShoes%3ESneakers%20%26%20Athletic%20shoes”
>
> pagetype
>
> The pagetype is a mandatory parameter and has the value “boolean”.
>
> NOTE: The values passed in the API should be encoded, when required, for correct interpretation.

# Format

The format parameter specifies the format in which the response result will be generated. Possible values are ‘JSON’ or ‘XML’. It is an optional parameter and the default value is ‘JSON’.

### Sample request to get JSON response

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&format=json&version=V2
```

### Sample JSON Response

```json
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

### Sample request to get XML response

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&format=xml&version=V2
```

### XML Response

```xml
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

# Fields

Defines attributes for a product like color, size etc. Fields parameter is used to specify the set of fields to be returned. The set of fields to be returned can be specified as a comma-separated list of field names. When returning the results, only fields in the list will be included. It is an optional parameter; however, it is recommended to pass only the fields required in the response to reduce the response size and latency.

### Sample request

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&fields=product_name&version=V2
```

### Response

```json
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

# Banners

Banners can be easily configured from your dashboard during campaign creation. Once you have correctly configured your banner, the category page API call will return the banner information as a part of the catalog-based response.

This feature can be disabled from the HTTP request using the ‘banner’ parameter. The default value of this parameter would be true.

### Sample request

```
http://search.unbxd.io///category?p=&pagetype=boolean&banner=false&version=V2
```

### Response for ‘Hosted Banners’

```json
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

### Response for ‘Custom Banners’

```json
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

```json
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

**imageUrl**: The URL of the hosted banner image.\
**landingUrl**: The URL of the page your visitors arrives after clicking the banner.
**bannerHtml**: The URL of the custom (HTML) banner image.

**NOTE**: The value of the response parameters will change to "null" according to the type of banner configuration.

For example, a visitor searched a query, the banner response below will help you set up a hosted banner in your eCommerce site:

### Response for ‘Hosted Banners’

```json
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

# Analytics

The analytics parameter enables or disables tracking the query hit for analytics. By default, tracking is enabled. To disable tracking, set value to false.

### Sample request

```
http://search.unbxd.io/<api-key>/<site-key>/category?p=<page>&pagetype=boolean&analytics=false&version=V2
```

### Response

```json
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
            }
         ]
    }
}
```

# Stats

Gives information about the products with highest and lowest field value. Applicable only on fields with numeric or decimal values.

To apply stats on the price field make the below API call:

### Sample request

```
http://search.unbxd.io/<api-key>/<site-key>/category?p=<page>&pagetype=boolean&stats=price&version=V2
```

### Response

```json
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
            }
         ]
    }
}
```

***

# Pagination

To get the paginated response in the search API, specify the value of the parameter “start”, and “rows”. The “start” parameter defines the position of the product in the response. The “rows” attribute defines the number of products required per API call.

E.g. for the first page of results, the start=0 and rows=20

For the next page of results, the start= 20 and rows=20.

## start

It indicates offset in the complete result set of the products.

### Sample Request

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&start=40&version=V2
```

This request will fetch all the results starting with the offset 5 for the result set of the query red.

## rows

The row parameter is used to paginate the results of listing in a category page. It indicates number of products in a single page. It is an optional parameter and the default value is 10, maximum value is 100.

### Sample Request

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&rows=20&version=V2
```

> 📘 NOTE
>
> If the products are not required in the response, the parameter needs to be set to 0.

***

# Sorting

The sort parameter is used to rank the products based on specified fields in the specified order. It is an optional parameter. If not passed, products would be returned ordered on Unbxd relevancy algorithm.

## Sorting on Single Field

You can sort your search API results using a sort function as shown below:

E.g. for the first page of results, the start=0 and rows=20

For the next page of results, the start= 20 and rows=20.

### Sample Request

```
http://search.unbxd.io/<api-key>/<site-key>/category?p=<page>&version=V2&sort=fieldname sort_order
```

* **fieldname**: The field on which the sort is applied.
* **sort\_order**: The order in which the sort is applied. This value can be “asc” (for ascending) or “desc” (for descending)

For example, a visitor wants to sort results on price in ascending order, the API call below is made:

### Sample Request

```
http://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&sort=price%20asc&version=V2
```

**NOTE**: There is a space between the field name and the sort\_order in the API call.

## Sorting on Multiple Fields

To apply multiple sort rules, you need to make an API call as shown below:

### Sample Request

```
http://search.unbxd.io///category?p=&verison=V2&sort=field1 sort_order,field2 sort_order,field3 sort_order
```

For example, to show results sorted on price and title the API call below is made:

```
http://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&sort=price%20asc&sort=title%20desc&version=V2
```

> 📘 NOTE
>
> When multiple sort parameters are applied, the products will be sorted based on the first criteria passed in the request. Only in the case when multiple products have the same value for the first criteria, then the latter sorting criteria will be applied within those products.

***

# Facets

Faceting helps your shoppers narrow down search results by selecting filter values as needed. Every time a user clicks a facet value, the set of results is reduced to only the items that have that value. Additional clicks continue to narrow down the search—the previous facet values are remembered and applied again.

Facets can be easily configured from the Manage -> Configure Search -> Configure Facet section of the Console.

### Sample Request

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&facet=false&version=V2
```

### Sample Response

```json
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

Here, when a search API is fired, “facet” is received in response.

Facet response contains different types of facets (for example, Categories, Brand , Color, Price etc..) that are configured by client with respective values and count of those values. For example, if Brand is configured for faceting, response will look like:

```json
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

Response contains Facet Name: Brand, Value: Samsung and Count of products with filter Samsung = 663.

***

# Common Features across all Facets

## 1. MultiSelect Facet

Multi-select facet is the option to enable or disable the customers to select more than one facet at a time for a query.

### Sample Request

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/search?&q=mobile&filter=categoryPath"Mobiles & Tablets"&filter=brand_uFilter:"Apple"&filter=product_min_price:[35000 TO 37500]&version=V2&facet.multiselect=true
```

### Response

```json
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

## 2. SelectedFacet

This displays the values of a single selected facet or multiple selected facets. If you select the facet ‘brand’ then the values ‘Apple’, ‘Samsung’, and so are displayed.

### Sample Request

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&filter-id=76678:5001&selectedfacet=true&version=V2
```

### Response

```json
{
    "selected": [
        {
            "facetName": "u_5110_unbxdMap",
            "displayName": "Color",
            "values": [
                "5335"
            ],
            "id": "5110",
            "position": 785,
            "filterField": "ShopbyColor_uFilter"
        },
        {
            "facetName": "u_2707_unbxdMap",
            "displayName": "Price",
            "values": [
                "6666"
            ],
            "id": "2707",
            "position": 784,
            "filterField": "ShopbyPrice_uFilter"
        }
    ]
}
```

***

# Multilevel Facet

You can build a hierarchy in your facet values to enable multi-level navigation and filtering. This pattern is great for very long lists of values and to improve discoverability: your users will be able to browse up and down in the levels to refine their searches.

### Property Descriptions

| Property    | Description                                                                 |
| ----------- | --------------------------------------------------------------------------- |
| multilevel  | Hierarchical facets configured on the hierarchical field(s).                |
| list        | Array of hierarchical facets as configured on the hierarchical fields.      |
| values      | All the unique values for the sub categories available for query and count. |
| level       | Depth of multilevel field                                                   |
| filterField | Field on which hierarchical facet is created                                |
| breadcrumb  | Position within the hierarchical field where the results appear             |

The `facet.multilevel` parameter is used to enable multi-level facets in the API response. It takes a fixed value `categoryPath` if you want multi-level facets in the response. If not passed, multi-level facets will not appear in the response.

### Sample Request

```
https://search.unbxd.io/63e6578fcb4382aee0eea117aba3a227/docs-unbxd700181508846765/category?p=categoryPath:%22Fashion%22&pagetype=boolean&facet.multilevel=categoryPath&version=V2
```

### Response

```json
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
```