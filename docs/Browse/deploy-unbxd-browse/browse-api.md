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
| **unbxd-device-type\*** | This header is an Unbxd custom header which is required to identify if the request is coming from an app.                                                                                   | No        | If not passed, device-based merchandising campaigns will not be able to differentiate between browser and apps |
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

      </td>

      <td>

      </td>

      <td>

      </td>

      <td>

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