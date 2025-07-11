---
title: Visual Search API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Integrate Visual Search Functionality with Unbxd Visual Search API

The Visual Search API allows you to seamlessly integrate with the Unbxd platform and effortlessly incorporate all functionalities related to visual search. It enables you to display search results for an image from the array of products that match the visual cues.

You can use the JSON /XML response format and leverage various built-in features. All API requests must be made over HTTPS.

```Text Post Sample Request
Reque

{  
curl -X POST 
'https://search.unbxd.io/v2.0/sites/{site_key}/images' 
-H 'Authorization: API Key' 
-H 'Content-Type: application/json'
}
```
```Text Get Sample
Request Method: Get

{  
curl -X GET "https://search.unbxd.io/v2.0/sites/(site_key)/images?imageUrl=https://some.site/images/image.png" \
-H "Authorization: API Key"
}
```

* **Authentication**\
  Authentication is done using API Keys and Sitekeys, which are generated during the account creation process and can be found in the Console under Manage -> Configure Site -> Keys.
* **Uploading Images** : Upload Using Public Image URL\
  Request Method: Post

```Text Request Method: Post
curl --location '/v2.0/sites/{site_key}/images' \  
\--header 'Content-Type: application/json' \
\--header 'Authorization: API Key' \
\--data '{ "imageUrl": "http://example.com/img/1.jpg" }'
```
```Text Request Method: Get
curl --location 'v2/sites/(site_key)/images?imageUrl=http%3A%2F%2Fexample.com%2Fimages%2F1.jpg' \\\
\--header 'Authorization: API Key'
```

* Image Uploaded as multipart/form-data

```
curl --location '/v2.0/sites/(site_key)/images' \\\
\--header 'Authorization: API Key' \
\--form 'image=@"./scripts/test/test.png"'
```

* Upload Image by sending Base64 Encoding

```
curl --location '/v2.0/sites/(site_key)/images' \\\
\--header 'Content-Type: image/png;base64' \
\--header 'Authorization: API Key' \
\--data 'iVBORw0KGgoAAAANSUhEUgAAAq4AAAIdCAYAAAD8of/......'
```

> 📘 Note
>
> Make sure you replace (site\_key) with your actual site key, and API Key with the API key you’re using for authorisation.
>
> Here is how an Image to Base64 Encoder splits out  data

```
data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/4QC2.....TP/9k=
```

Here’s how to read this data

```
data:<mime-type>,<raw-image-data>
</raw-image-data></mime-type>
```

When using this API, emit the mime-type within the content-type header as shown above, along with raw raw-image-data within the body.

Here are the supported mime types

```
image/jpeg;base64
image/png;base64
image/tiff;base64
```

### Headers

The following parameters are available:

| **Parameter**         | **Description**                                                                                                                                                 |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **unbxd-user-id**     | The Unbxd Analytics JavaScript sets a unique identifier in your browser’s cookie referred to as the user ID. Example: `uid-1466015353887-20419`.                |
| **user-agent**        | In each HTTPS request, the user-agent identification information is passed to the web server.                                                                   |
| **unbxd-device-type** | A custom Unbxd header that identifies if the request originated from an app.                                                                                    |
| **X-Forwarded-For**   | In this header, the IP address of the end user is identified. Crucial for backend integrations, since Unbxd cannot get the IP directly from the browser.        |
| **Content-Type**      | This header signifies the content type of the request being sent. Supported types include `application/json`, `image/*`, `base64image/*` (JPG/JPEG, PNG, TIFF). |

* unbxd-device-type:`{ "type":"tablet" , "os": "iOS" , "source": "app" }  
  possible values of “type” : “desktop”, “tablet”, “mobile”
  possible values of “os” : “android”, “ios”, “windows”
  possible values of “source” : “browser”, “app”`
* Supported Image Types:\
  PNG: image/png
  JPEG/JPG: image/jpg
  TIFF: image/tiff

### Request Parameters

The values of the request parameters are defined below:

| **Parameter**      | **Description**                                                                    | **Data Type** | **Possible Values / Format**                                                       |
| ------------------ | ---------------------------------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------- |
| **version**        | Specifies the API version. Always pass `v2` to access latest features.             | String        | Supported: `v2`                                                                    |
| **user-type**      | Indicates visit frequency of user.                                                 | String        | Format: \`"first-time"\`\<br>Values: \`first-time\`, \`frequent\`                  |
| **uid**            | Unique ID to identify visitors. Obtained from `unbxd.userId` cookie.               | String        | Format: `&uid=uid-1666356549013-78531`                                             |
| **format**         | Specifies response format.                                                         | String        | Format: \`\&format=xml\`\<br>Values: \`JSON\`, \`XML\`\<br>Default: \`JSON\`       |
| **start**          | Offsets the results by a specific number.                                          | Integer       | Format: \`\&start=2\`\<br>Default: \`0\`                                           |
| **page**           | Displays the right set of products per page (`rows` determines how many).          | Integer       | Format: `&page=2`                                                                  |
| **rows**           | Paginates query results OR sets number of buckets when used with bucketing.        | Integer       | Format: \`\&rows=2\`\<br>Default: \`10\`                                           |
| **variants**       | Displays variants of the same product.                                             | Boolean       | Format: \`\&variants=True\`\<br>Values: \`True\`, \`False\`\<br>Default: \`False\` |
| **variants.count** | Number of defined variants to show for a product.                                  | Integer       | Format: `&variants.count=5`                                                        |
| **fields**         | Defines which product attributes to return (e.g., color, size).                    | String        | Format: \`\&fields=color,size\`\<br>Default: returns all fields                    |
| **bucket.field**   | Groups products by a common field value into buckets.                              | String        | Format: `&bucket.field=brand`                                                      |
| **bucket.limit**   | Number of products to show in each bucket.                                         | Integer       | Format: \`\&bucket.limit=10\`\<br>Default: \`10\`                                  |
| **bucket.offset**  | Paginates to the next set of products within a bucket.                             | Integer       | Format: `&bucket.offset=10`                                                        |
| **analytics**      | Enables or disables tracking for analytics.                                        | String        | Default: Tracking is enabled                                                       |
| **stats**          | Returns product info with highest and lowest field values (numerical fields only). | –             | Format: `fieldName` (e.g., `price`, `rating`)                                      |

### API Response

```
"searchMeta"
...
"queryParams": { ... },
"image": {
"id": "ad85491c-9d2b-4cab-900a-df96aa11f0d9",
"boxes": [{
"id": 1089,
"vertices": [{
"x": 164.07107543945312,
"y": 352.81292724609375
},
{
"x": 188.38121032714844,
"y": 384.0833435058594
}
],
"url": "/v2.0/sites//images/ad85491c-9d2b-4cab-900a-df96aa11f0d9/boxes/1089"
}{
"id": 811,
"vertices": [{
"x": 147.3377685546875,
"y": 68.75267028808594
},
{
"x": 255.28317260742188,
"y": 340.2548522949219
}]
"url": "/v2.0/sites//images/ad85491c-9d2b-4cab-900a-df96aa11f0d9/boxes/811"
},
...
...
],
"selected": 1089
},
...
```

A search API response comprises of

* searchMetaData
* response
* And some other high level fields of the response.

The above JSON gets added in searchMetaData block, besides queryParams.

### Response Components

Unbxd returns the list of products that match the search criteria. The response would be in application/JSON or application/XML content type format.