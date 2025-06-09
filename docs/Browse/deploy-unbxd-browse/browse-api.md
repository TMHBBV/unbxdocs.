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

```Text Sample Request
https://search.unbxd.io///category?p=&version=V2  
&pagetype=boolean&format=<xml|json>&start=&rows=&filter-id=&sort=asc|desc&uid=&<fields=comma separated list of fields>&selectedfacet=true
```

## Authentication

Our APIs use an API\_KEY and a SITE\_KEY to authenticate search requests.

These keys are generated at the time of account creation and can be accessed within Console at **Manage** -> **Configure Site** -> **Keys**.

# Headers

Unbxd requires some header parameters along with the search request in order to provide support for personalization and merchandising campaigns created on location, browser or device type. Headers need to be passed through the URL to process the actual response.

For Search and Autosuggest API, we can enable personalization, segmentation, and A/B testing of the merchandising campaign. we recommend passing certain parameters as HTTP headers.

The following parameters are available:

| Parameter               | Description                                                                                                                                                                                 | Mandatory | Significance                                                                                                   |
| :---------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------- | :------------------------------------------------------------------------------------------------------------- |
| **unbxd-user-id**       | Unique identification for the visitors. Example: uid-1466015353887-20419. The Unbxd Analytics javascript sets the userid in your browser cookie.                                            | No        | If not passed, personalization, segmentation, and A/B testing of merchandising campaigns will not work.        |
| **user-agent**          | Browser identification information passed to the webserver with every HTTP request                                                                                                          | No        | If not passed, device-based merchandising campaigns will not work.                                             |
| **unbxd-device-type**\* | This header is an Unbxd custom header which is required to identify if the request is coming from an app.                                                                                   | No        | If not passed, device-based merchandising campaigns will not be able to differentiate between browser and apps |
| **Accept-Encoding**     | This header signifies the content encoding of the response. Currently, Unbxd supports only gzip compression. To enable this, ‘gzip’ needs to be passed                                      | No        | If not passed, the response will not be compressed.                                                            |
| **X-Forwarded-For**     | This header signifies the IP address of the end-user. This is primarily required if the integration is a backend as Unbxd doesn’t get the IP of the end-user from the browser in that case. | No        | If not passed, segmentation, A/B testing and personalization will not work.                                    |

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

  p=fieldname:”fieldvalue”: Page rules in the console should be created as this) &#x20;
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