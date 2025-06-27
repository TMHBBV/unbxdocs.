---
title: Recommendation SDK
deprecated: false
hidden: false
metadata:
  robots: index
---
Unbxd Recommendations SDK helps you integrate the Unbxd Recommendations and its functionalities.

With SDK documentation, you can optimize your layout of the recommendations widget. You can duplicate an Unbxd recommendation template and make changes to the JS-SDK configuration to render the appropriate HTML responses.

Version\
The Recommendations SDK Version 2.1.0 can be found here for different regions:

| Region         | SDK Version URL                                                                  |
| -------------- | -------------------------------------------------------------------------------- |
| US Customers   | `https://libraries.unbxdapi.com/recs-sdk/v2.1.0/unbxd_recs_template_sdk.js`      |
| UK Customers   | `https://libraries.unbxdapi.com/recs-sdk/v2.1.0/unbxd_recs_template_sdk_uk.js`   |
| APAC Customers | `https://libraries.unbxdapi.com/recs-sdk/v2.1.0/unbxd_recs_template_sdk_apac.js` |
| ANZ Customers  | `https://libraries.unbxdapi.com/recs-sdk/v2.1.0/unbxd_recs_template_sdk_anz.js`  |

> 📘 Note
>
> * Integration done through Recs SDK is only for AJAX customers.
> * Update: While v1.0 had just desktop template support, with v2.0 you get desktop as well as mobile template support.

## Quick Integration

To integrate Recommendations SDK onto your site quickly, follow these steps:

To enable Unbxd powered recommendation widgets, you need to include Unbxd recommendations SDK. This can be achieved by adding the JS CDN link in your index HTML page

```
 <script src="https://libraries.unbxdapi.com/recs-sdk/v2.1.0/unbxd_recs_template_sdk.js" async>
</script>
```

Create locator HTML div nodes on your page.

```
<div class="horizontal-section"><!-- First Horizontal template to be rendered here with unique id for the widget -->
<div id="recommendations1"> </div>
</div>
<div class="horizontal-section"><-- First Horizontal template to be rendered here with unique id for the widget -->
```

Invoke \_unbxd\_getRecommendations to fetch recommendations. This is the sample function for Home Page recommendations widget

```
window._unbxd_getRecommendations({
           widgets: {
               widget1: {
                   name: "home_recommendations1"
               },
               widget2: {
                   name: "home_recommendations2"
               },
               widget3: {
                   name: "home_recommendations3"
               }
           },
           userInfo: {
               userId: 'uidValue',
               siteKey: 'siteKeyValue',
               apiKey: 'apiKeyValue'
           },
           pageInfo: {
               pageType: 'HOME'
           },
           itemClickHandler: function (product) {
               //do what you want to do with product that has been clicked here
               alert(JSON.stringify(product));
           },
           dataParser: function (templateData) {
               // modify the data received from recommendation API
               // in case required       
               return templateData;
           }
       }); 
```

> 📘 NOTE
>
> You can know more about the details of keys by referring to our Search Documentation here.

## Installation

We will learn how to integrate the Unbxd Recommendations SDK to optimize and power the recommendations results in the display page on your site.

Include Recommendation SDK in your application\
To enable Unbxd powered recommendation widgets, you need to include Unbxd recommendations SDK. CDN link in the tag of the HTML code:

```
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>

    <!-- Include these scripts -->
    <!-- template sdk first, followed by template widget initialization -->
    <script src=“<unbxd template sdk url>”></script>
  </body>
</html>
```

## Create locator HTML div nodes

The web application on which the recommendation template will be displayed must contain HTML DIV nodes with well defined and unique IDs for the widget so that the SDK can fetch recommendations and display them at those positions.

```
<div class="horizontal-section"><!-- First Horizontal template to be rendered here with unique id. -->
<div id="recommendations1"> </div>
</div>
```

## Fetch Recommendations Results

The SDK has exposed a method (window\.getUnbxdRecommendations) to fetch the recommendations and display them. The method can be called from your website to fetch recommendation content and get it rendered on their page.

Function Details\
Function Name:window\.getUnbxdRecommendations

Function Argument: Context Object – Everything that the recommendation API needs from the merchandiser application to serve the relevant recommendation.

> 📘 NOTE
>
> If you are integrating this in the react single page application then, Invoke the recommendation parameter by placing the script in the index.html file and invoking window\.getUnbxdRecommendations in the mounting/updating phase of your components.

E.g In case of a react application the SDK can be implemented by invoking this method in the ‘componentDidMount’ method like this (in case of initial load):

```
componentDidMount(){
    new window.getUnbxdRecommendations({
	// context configuration here
     })
}
```

If you wish to show call the SDK when any update happens across the component the same call can be placed in ‘componentDidUpdate’ method:

```
componentDidUpdate(){
    new window.getUnbxdRecommendations({
	// context configuration here
     })
}
```

> 📘 Note
>
> window object needs to be used, otherwise the specific component won’t be able to access the recommendations call.