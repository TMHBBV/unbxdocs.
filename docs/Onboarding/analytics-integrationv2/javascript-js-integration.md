---
title: JavaScript (JS) Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📘 Note
>
> This method should primarily be used when the client prefers to manage the process directly or if the event integration has failed through other recommended approaches.

The Unbxd Search JS Library is an SDK for adding search and product discovery features to e-commerce websites. It is written in Vanilla JavaScript and provides a JavaScript API for configuring and managing search requests.

The SDK has no external dependencies, making it lightweight and straightforward to integrate. To use it, a script tag is added to the relevant webpage. Developers can customize and extend its functionality through JavaScript methods and callbacks.

# How to do the JS-based Analytics integration?

Add the following `<script>` tag at the end of your site's HTML body.

```
<script type="text/javascript" defer charset="utf-8"
  src="https://libraries.unbxdapi.com/sdk-clients/PROD_SITEKEY/ua/ua.js">
</script>
```

# What are the event payload data required?

## Search

This tracks user search queries, including those using the Autosuggest widget. It is important to capture all search queries, including ones with zero results.

### Payload details

| Attribute Name | Type   | Value to Pass                            |
| :------------- | :----- | :--------------------------------------- |
| `query`        | String | The search query entered by the shopper. |

Refer to the following code snippet to call the Unbxd.track function to trigger the search event.

```
 <script type="text/javascript">
   	var payload = {
   	query: '{{search-query}}',
   	}


   	if(Unbxd && typeof Unbxd.track === 'function') {
   		Unbxd.track('search', payload)
   	} else {
   		console.error('unbxdAnalytics.js is not loaded!')
   	}
   </script>
```

# Visual Search

## Payload details

| Attribute Name | Datatype | What Value to be Passed                                                                                                 |
| :------------- | :------- | :---------------------------------------------------------------------------------------------------------------------- |
| `imageId`      | String   | Id of the image, to be retrieved from the response of visualSearch API                                                  |
| `boxId`        | String   | Optional, the ID of the bounding box that has been selected. Look for the selected key in the visualSearch API response |

Refer to the following code snippet to call the `Unbxd.track` function to trigger the `visualSearch` event.

```
<script type="text/javascript">
   	var payload = {
   	imageId: 'ad85491c-9d2b-4cab-900a-df96aa11f0d9',
     	boxId: '1089',
   	}


   	if(Unbxd && typeof Unbxd.track === 'function') {
   		Unbxd.track('visualSearch', payload)
   	} else {
   		console.error('unbxdAnalytics.js is not loaded!')
   	}
   </script>
```