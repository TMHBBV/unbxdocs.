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

## Invoke function to register hooks on before and after template rendered

Function Name:

`_unbxd_RegisterHook(“beforeTemplateRender”, beforeTemplateRenderer);`

`_unbxd_RegisterHook(“afterTemplateRender”, afterTemplateRenderer);`

Function Argument: Event name (beforeTemplateRender/ afterTemplateRender) & callback function which gets called when the event triggers in SDK. Prior to this, templateRenderer callback can be used to modify the recommendation items received from the Recommendation API. afterTemplateRendered gets called after every time the widget/template gets rendered. afterTemplateRendered callback is called with a parameter “isVertical” which can be used to distinguish between horizontal and vertical rendered templates.

```
 beforeTemplateRenderer = function(templateData){
           // modify the data received from recommendation API in case required.
          console.log("template data");
          return templateData;
       }
 
            //Perform activity after template render
       afterTemplateRenderer = function(isVertical){
         if(!isVertical){
               console.log("Horizontal Template Rendered");
         } else {
               console.log("Vertical Template Rendered");
         }
      }
 
      window._unbxd_registerHook("beforeTemplateRender", beforeTemplateRenderer);
      window._unbxd_registerHook("afterTemplateRender", afterTemplateRenderer);
```

<br />

Context Object Details\
It is a Javascript object which would have following keys:

## widgets

\*REQUIRED

At least one of the keys among ‘widget1’, ‘widget2’ and ‘widget3’ has to be provided along with its configuration. The description of these keys can be found below

| **Key**          | **Type**          | **Description**                                                |
| ---------------- | ----------------- | -------------------------------------------------------------- |
| `widget1`        | JavaScript Object | Configuration for widget 1                                     |
| `widget1 > name` | String            | Unique Target DOM element ID where widget 1 will be displayed. |
| `widget2`        | Object            | Configuration for widget 2                                     |
| `widget2 > name` | String            | Target DOM element ID where widget 2 will be displayed.        |
| `widget3`        | Object            | Configuration for widget 3                                     |
| `widget3 > name` | String            | Target DOM element ID where widget 3 will be displayed.        |

Sample Value

```
<span style="font-size: 16px;">widgets: {
                widget1: {
                    name: "home_recommendations1"
                },
                widget2: {
                    name: "home_recommendations2"
                },
                widget3: {
                    name: "home_recommendations3"
                }
            }</span>
```

## userInfo

\*REQUIRED

userInfo must contain following key value pairs:

| **Key**   | **Type** | **Description**                                              |
| --------- | -------- | ------------------------------------------------------------ |
| `userId`  | String   | User tracking ID to be used for personalized recommendations |
| `siteKey` | String   | Site key shared by UNBXD                                     |
| `apiKey`  | String   | API key shared by UNBXD                                      |

> 📘 NOTE
>
> You can fetch the key details from the Search documentation.

Sample Code:

```
<span style="font-size: 16px;">userInfo: {
                userId: 'uid',
                siteKey: 'site-key',
                apiKey: 'apiKey''
},</span>
```

<br />

pageInfo\
\*REQUIRED

pageInfo must contain values for the following keys:

| **Key**         | **Type** | **Description**                                                                                                                            |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `pageType`      | String   | Must be one of ‘HOME’, ‘PRODUCT’, ‘CART’, ‘CATEGORY’.                                                                                      |
| `productIds`    | Array    | An array of a list of product ids of String type. This field is required only when the `pageType` is ‘PRODUCT’ or ‘CART’.                  |
| `catlevel1Name` | String   | Defines the first level of category filter. This field is required only when the `pageType` is ‘CATEGORY’.                                 |
| `catlevel2Name` | String   | Defines the second level of category filter. This is an optional field which needs to be mentioned only when the `pageType` is ‘CATEGORY’. |
| `catlevel3Name` | String   | Defines the third level of category filter. This is an optional field which needs to be mentioned only when the `pageType` is ‘CATEGORY’.  |
| `catlevel4Name` | String   | Defines the fourth level of category filter. This is an optional field which needs to be mentioned only when the `pageType` is ‘CATEGORY’. |

Category Level values must be in continuous order starting with catlevel1Name.

For instance:

‘catlevel1Name’: ‘Women’,

‘catlevel2Name’: ‘Clothes’,

‘catlevel3Name’: ‘Top’,

‘catlevel4Name’: ‘Denim’

catlevel1Name is REQUIRED for the Category page.

> 📘 NOTE
>
> If a category level value is skipped, the next level values will be ignored i.e. if ‘‘catlevel2Name’ value is not set, then ‘‘catlevel3Name’ and ‘‘catlevel4Name’ will be ignored by SDK. They will not be used to fetch recommendations.

### itemClickHandler

OPTIONAL

Description for this handler can be found below:

| **Key**            | **Type** | **Description**                                                                                                                                                                                                   |
| ------------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `itemClickHandler` | Function | Callback method that will be called when the recommendation item is clicked in the widget. The callback is called with one argument that contains all the product attributes sent by the recommendation platform. |

dataParser\
OPTIONAL

| **Key**      | **Type** | **Description**                                                                                                                                                                                                                                                                                                                                                     |
| ------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `dataParser` | Function | Callback method that will be called just before feeding the data to the dot template with original recommendations data. You can modify the original data based on your requirement and return the modified data to be passed to the template. This is useful when you are using your custom template and you don’t want to write parsing logic in a template file. |

## Sample function calls for each Page Type

Sample function calls for each page type\
HOMEPAGE

```
_unbxd_getRecommendations({
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
                userId: 'uidValue'',
                siteKey: 'siteKeyValue',
                apiKey: 'apiKeyValue''
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

**Product Page**

```
_unbxd_getRecommendations({
            widgets: {
                widget1: {
                    name: "product_recommendations1"
                },
                widget2: {
                    name: "product_recommendations2"
                },
                widget3: {
                    name: "product_recommendations3"
                }
            },
           userInfo: {
                userId: 'uidValue'',
                siteKey: 'siteKeyValue',
                apiKey: 'apiKeyValue''
            },
            pageInfo: {
                pageType: 'PRODUCT',
                productIDs: ['uniqueId1', 'uniqueId2']
            },
            itemClickHandler: function (product) {
                // product information will be provided here
                alert(JSON.stringify(product));
            },
            dataParser: function (templateData) {
             // modify the data received from recommendation API 
             // in case required        
            return templateData;
            }
    });
```

**CART PAGE**

```
_unbxd_getRecommendations({
            widgets: {
                widget1: {
                    name: "product_recommendations1"
                },
                widget2: {
                    name: "product_recommendations2"
                },
                widget3: {
                    name: "product_recommendations3"
                }
            },
            userInfo: {
                userId: 'uidValue'',
                siteKey: 'siteKeyValue',
                apiKey: 'apiKeyValue''
            },
            pageInfo: {
                pageType: 'CART',
                productIDs: ['uniqueId1', 'uniqueId2']
            },
            itemClickHandler: function (product) {
                // product information will be provided here
                alert(JSON.stringify(product));
            },
            dataParser: function (templateData) {
              //modify the data received from recommendation API
              //in case required        
            return templateData;
            },
    });
```

**CATEGORY PAGE**

```
_unbxd_getRecommendations({
            widgets: {
                widget1: {
                    name: "product_recommendations1"
                },
                widget2: {
                    name: "product_recommendations2"
                },
                widget3: {
                    name: "product_recommendations3"
                }
            },
            userInfo: {
                userId: 'uidValue'',
                siteKey: 'siteKeyValue',
                apiKey: 'apiKeyValue''
            },
            pageInfo: {
                pageType: 'CATEGORY',
                catlevel1Name: 'MENS',
            catlevel2Name: 'FORMALS',
            catlevel3Name: 'SHIRTS',
            catlevel4Name: 'NEW ARRIVALS'
            },
            itemClickHandler: function (product) {
                // product information will be provided here
                alert(JSON.stringify(product));
            },
              dataParser: function (templateData) {
             //modify the data received from recommendation 
             // API in case required        
            return templateData;
            },
    });
```

<br />

## Default Template

Under the recommendations section, you have the option to select Unbxd’s default templates for displaying recommendations. The display of widgets varies with the device type and screen resolution. So, it’s important to choose templates for specific devices.

The template selection is specifically defined for all device types which are primarily divided into:

Desktop\
Mobile
Let’s look at the various template types available for each device type.

Desktop\
Selecting a template for the desktop version defines how would the recommendation widget be displayed across the portrait orientations.

To see the desktop templates, navigate to Manage > Templates.

You can select either a Horizontal or Vertical template display for the products.

**Horizontal**: Horizontal template displays products in a single plane, next to each other. Such a display makes it easier for customers to look at multiple products in one sight.

![](https://files.readme.io/6c83465fdc3879ca20caa3a6429f1dee0a85cd9edd138c228df36cb8c151de38-image.png)

**Vertical**: Vertical template displays products in a line one after another. In this shoppers see one product at a time.