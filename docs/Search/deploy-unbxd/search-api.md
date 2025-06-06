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
        Defines attributes for a product like color, size etc.
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

      </td>

      <td>

      </td>

      <td>

      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>