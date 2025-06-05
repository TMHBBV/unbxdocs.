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

<br />

## Authentication

Our APIs use an API\_KEY and a SITE\_KEY to authenticate search requests.

These keys are generated when account creation and can be accessed within Console at Manage -> Configure Site -> Keys.

## Headers

Unbxd requires some header parameters along with the search request in order to provide support for personalization and merchandising campaigns created on location, browser or device type. Headers need to be passed through the URL to process the actual response.

> 📘 Important Note
>
> For Search and Autosuggest API, we can enable personalization, segmentation, and A/B testing of the merchandising campaign. we recommend passing certain parameters as HTTPS headers.

The following parameters are available:

| Parameter           | Description                                                                                                                                      | Significance                                                                                           |
| :------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| unbxd-user-id       | Unique identification for the visitors. Example: uid-1466015353887-20419. The Unbxd Analytics JavaScript sets the userid in your browser cookie. | If not passed, personalization, segmentation, and A/B testing of merchandising campaigns will not work |
| user-agent          | Browser identification information is passed to the web server with every HTTPS request.                                                         | If not passed, device-based merchandising campaigns will not work.                                     |
| unbxd-device-type\* | This header is an Unbxd custom header which is required to identify if the request is coming from an app.                                        |                                                                                                        |