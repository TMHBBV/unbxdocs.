---
title: GTM Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
# GTM Integration

Tracking visitor analytics and behavior are essential in order to provide accurate and visitor-specific search and category page results. UNBXD analyzes visitor events, such as product clicks, products added to cart, orders, etc. These events are tracked using browser cookies. With this information, a profile is built for every visitor, based on his/her affinity to different categories, brands, or prices.

This information is then aggregated and analyzed for two purposes:

Generating reports

Providing relevant and personalized search & category pages results

When visitors browse through your store, the integrated trackers log everything visitors do – the products they visit, orders, even the various store properties they interact with. We take that information, analyze it, and assemble a detailed profile of the visitor. We know their browsing patterns, preferences and can even determine susceptibility to merchandising campaigns. The trackers are unique tracking codes that must be configured onto the store properties that yield an interaction. We call this interaction as an “event”, for example, click on the “Add to Cart” button.

The visitor profiles help fetch relevant and personalized products as search results. It also helps in generating detailed reports.

NOTE: For Unbxd E-commerce Search to function correctly on your site, Unbxd Analytics must be configured.

## Introduction to GTM

Google Tag Manager is a free tool that allows you to manage and deploy marketing tags (snippets of code or tracking pixels) on your website (or mobile app) without having to modify the code.

Here’s a very simple example of how GTM works. Information from one data source (your website) is shared with another data source (Analytics) through Google Tag Manager. GTM becomes very handy when you have lots of tags to manage because all the code is stored in one place.

### Basic components of GTM

Following are the basic components within Google Tag Manager:

* Tags – Tags are tracking codes and code fragments that tell GTM what action to take on that page.

For example: Sending searched query to Unbxd analytics.

* Triggers – Triggers specify the conditions under which a Tag should fire.For example: A trigger with a condition to only fire a Tag when a user views URLs containing the path /search/.
* Variables – Variables are values used in triggers and tags to filter when a specific tag should fire. GTM provides built-in variables and allows you to create custom user-defined variables. For example: A ‘click’ class variable has a value name (such as a word string) assigned to buttons on the website.
* DataLayer – The dataLayer is a JSON that contains name value pairs of data points you wish to pass from your website into GTM. (And GTM can then, in turn, pass on to any tags that are managed in GTM, including Unbxd tags.)

## Requirements for Unbxd tracking through GTM

Unbxd analytics scripts need to be loaded across all the pages. We require a tag which will need to be loaded on all the pages. Below is the required code block for Unbxd analytics script. This should be loaded before other Unbxd tracking scripts and is mandatory to be added on all pages.

```
// Container ID is present in GTM-XXXX format in GTM Dashboard
// HTML ID can be found in the url. Eg:
// containers/422XXXX/workspaces/20 , 20 is the HTML ID

<script type = "text/javascript" >
   /* * * CONFIGURATION * * */
   // Replace the value with the Unbxd Site Key and API Key.

   var UnbxdSiteName = "{{UNBXD_SITE_NAME}}";
   var UnbxdApiKey = "{{UNBXD_API_KEY}}";

   /* * * DON'T EDIT BELOW THIS LINE * * */
   (function() {
   var ubx = document.createElement('script');
   ubx.type = 'text/javascript';
   ubx.async = true; ubx.src='//d21gpk1vhmjuf5.cloudfront.net/unbxdAnalytics.js';
   ubx.addEventListener('load', function() {
   window.google_tag_manager[{{Container ID}}].onHtmlSuccess({{HTML ID}}); });
   (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(ubx);
   })();
</script>
```

The above JS snippet needs to be added in a tag and also enable Built-In Variables, i.e.,

Container ID and HTML ID without fail.

TagName: UnbxdAnalyticsScript

TagType: Custom HTML Tag

Trigger: AllPagesPageView

## Search Query Tracker

A Search hit event is tracked to understand the query and intent of your visitors. Each search query is tracked to enable per-query analytics of the visitor. A typical search hit event involves:

* SearchQueryTrigger

Through GTM to integrate this event we need to follow below approach:

* Create Trigger in GTM to catch the search Query on form hit.\
  Trigger Configuration:
  * TriggerName: UnbxdSearchQueryTrigger
  * Trigger Type: Custom Event
  * Event Name: SearchQuery

<Image align="center" width="% " src="https://files.readme.io/f8f2b4f02d78f8c8c11205ee1037759272c17c63c727b92af97dabcdf8c63a28-image.png" />

<br />

2. Create Variable in GTM, to fetch the query from the dataLayer.

   Variable Configuration:
   * Variable Name: UnbxdSearchQueryPayload
   * Variable Variable Type: Data Layer Variable
   * Data Layer Variable Name: SearchQueryPayload
   HTML Content:

![](https://files.readme.io/71b93703e04f4e7b455b5cc327e27f9540aac23ec3f606b254f8325bd9cc39fd-image.png)

3. Create a Javascript tag with the below details.

   Tag Configuration:

   Tag Name: UnbxdSearchQueryTag

   Tag Type: Custom HTML

   HTML Content:

```
// Pass payload to Unbxd.track function
// to call the tracker API

<script type="text/javascript">
   var u_payload = {{UnbxdSearchQueryPayload}};
   if (Unbxd && typeof Unbxd.track === 'function'
       && u_payload.hasOwnProperty("query")) {
       Unbxd.track("search", u_payload);
   } else {
       console.error('unbxdAnalytics.js is not loaded or payload incorrect!')
   }
</script>
```

Pushing the event to the dataLayer through a search query.

```
// Add payload to Datalayer variable SearchQueryPayload
// Should be triggered on search form submit
// Please change selectors for form and input box

<script​ ​type=​"text/javascript"​>
jQuery('#input_form_id').on("submit", function(){
       var searchQuery = jQuery("#myInput").val();
       if (searchQuery.length >= 1) {
           window.dataLayer = window.dataLayer || [];
               dataLayer.push(
               {
                   'event': 'SearchQuery',
                   'SearchQueryPayload':
                   {
                     'requestId' : '{{unbxd-request-id}}',
                     'query' : '{{searchQuery}}'
                    }
               }
           );
       }
   });
</script>
```

Payload Details

| Attribute | Datatype | Value to be passed                                                          |
| --------- | -------- | --------------------------------------------------------------------------- |
| requestId | string   | To be extracted from Unbxd search API response headers, from unx-request-id |
| query     | string   | The search query used by user                                               |

3. Create a javascript tag with the below details.

Tag Configuration:

Tag Name: UnbxdExperienceImpressionTag

Tag Type: Custom HTML

HTML Content:

Tag Configuration:

HTML Content:

```
// Pass payload to Unbxd.track() function
// to call the tracker API

<script type="text/javascript">
 var u_payload = {{UnbxdExperienceImpressionPayload}};
 if (Unbxd && typeof Unbxd.track === 'function'
      && u_payload.hasOwnProperty("experience_pagetype")
      && u_payload.hasOwnProperty("experience_widget")) {
          Unbxd.track('experience_impression', u_payload);
  } else {
 console.error('ERRNO-001: unbxdAnalytics.js is not loaded or payload incorrect!')
}
</script>
```

4. Pushing event to the dataLayer when the recommendation results loads.

Push payload to Datalayer:

```
// Add payload to Datalayer variable ExperienceImpressionPayload
// Should be triggered on category page load
// Payload will contain page and page_type instead of query

<script type="text/javascript">
 window.dataLayer = window.dataLayer || [];
 dataLayer.push(
   {
    'event': 'ExperienceImpression',
    'ExperienceImpressionPayload':
     {
       'requestId' : '{{unbxd-request-id}}',
       'pids_list': [LIST OF UNIQUE ID OF PRODUCTS],
       'experience_pagetype': '{{recs-pagetype}}',
       'experience_widget': '{{recs-widget}}'
     }
   });
</script>
```

Payload details:

| **Attribute Name**    | **Datatype** | **What value to be passed**                                                                                                             |
| --------------------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `requestId`           | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                                                      |
| `pids_list`           | String       | List of unique IDs of products loaded with the current request. If zero products are returned, pass an empty list (array).              |
| `experience_pagetype` | String       | Pagetype for the widget should be either Home, Product, Category, Cart, or Brand based on the type of page on which the widget is used. |
| `experience_widget`   | String       | Widget type, either WIDGET1, WIDGET2, or WIDGET3.                                                                                       |

Events Flow will be:

As soon as the ‘ExperienceImpression’ event got pushed to the dataLayer.\
This initiates the trigger UnbxdExperienceImpressionTrigger which we created in the step-1.
UnbxdExperienceImpressionTrigger executes the tag UnbxdExperienceImpressionTag: ​which we created in step-3.
Inside UnbxdExperienceImpressionTag we have added an Unbxd analytics experience impression tag.
Experience tracker code gets the data from the variable UnbxdExperienceImpressionPayload ​which we created in step-2.
Finally, UnbxdExperienceImpressionTrigger event data will be updated in the Unbxd analytics database for the particular site key.

## Product Click

1. Create Trigger in GTM to catch the Product Click event on product in recs results.

Trigger Configuration:

TriggerName: UnbxdProductClickTrigger

TriggerType: Custom Event

EventName: ProductClick

TriggerFiresOn: All Custom Events

![](https://files.readme.io/f4ced616aeae258cdb1c50a96c14102bf2ba03505a59fb9ea8e46d269565db39-image.png)

2. Create Variable in GTM, to fetch the product details from the dataLayer.

Variable Configuration:

VariableName: UnbxdProductClickPayload

Variable Type: Data Layer Variable

Data Layer Variable Name: ProductClickPayload

![](https://files.readme.io/5ba23246f92530d750e5c5cf6cd68dae3525334f5bbda89fae53c3bd2c1acc91-image.png)

3. Create a Javascript tag with the below details.

Tag Configuration:

Tag Name: UnbxdProductClickTag

Tag Type: Custom HTML

HTML Content:

```
// Pass payload to Unbxd.track function
// to call the tracker API

<script type="text/javascript">
   var u_payload = {{UnbxdProductClickPayload}};
   if (Unbxd && typeof Unbxd.track === 'function'
      && u_payload.hasOwnProperty("experience_pagetype")
      && u_payload.hasOwnProperty("experience_widget")) {
       Unbxd.track('click', u_payload);
     } else {
       console.error('ERRNO-004: unbxdAnalytics.js is not loaded or payload incorrect!')
   }
</script>
```

4. Pushing the event to the Data Layer through the Product Click.

Push payload to Datalayer

```
// Add payload to Datalayer variable ProductClickPayload
// Should be triggered on product click on browse results page

<script type="text/javascript">
  window.dataLayer = window.dataLayer || [];
  dataLayer.push(
    {
     'event': 'ProductClick',
     'ProductClickPayload':
      {
        'requestId': 'REQUEST ID',
        'pid': 'PRODUCT ID',
        'variantId': 'VARIANT ID OF SELECTED VARIANT',
        'prank': 'RANK',
        'experience_pagetype': '{{recs-pagetype}}',
        'experience_widget': '{{recs-widget}}'
      }
    });
</script>
```

Parameter details:

| **Attribute Name**    | **Datatype** | **What value to be passed**                                                                                                             |
| --------------------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `requestId`           | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                                                      |
| `pid`                 | String       | Unique ID for the product.                                                                                                              |
| `variantId`           | String       | VariantId of the selected product variant, if `relevantDocumentType="variant"`, in the search API response, or `null`.                  |
| `prank`               | String       | The rank (position) of the product in the response.                                                                                     |
| `experience_pagetype` | String       | Pagetype for the widget should be either Home, Product, Category, Cart, or Brand based on the type of page on which the widget is used. |
| `experience_widget`   | String       | Widget type, either WIDGET1, WIDGET2, or WIDGET3.                                                                                       |

Events Flow will be:

As soon as the ‘ProductClick’ event got pushed to the dataLayer.\
This initiates the trigger UnbxdProductClickTrigger which we created in step-1.
UnbxdProductClickTrigger executes the tag UnbxdProductClickTag: ​which we created in step-3.
Inside UnbxdProductClickTrigger we have added an Unbxd analytics recs impression tag.
Recs tracker code gets the data from the variable UnbxdProductClickPayload ​which we created in step-2.
Finally, UnbxdProductClickTrigger event data will be updated in the Unbxd analytics database for the particular siteKey.
Product View
​​Product Page View indicates the total number of visits that has been made to the product details page (PDP) by the visitor irrespective of the source (search result page, category page, search engine, email, marketing campaigns, etc). This can be tracked by passing the product ID in the payload.

To integrate this event through GTM, we need to follow the below approach:

1. Create a Trigger in GTM to catch the product view.

Trigger Configuration:

TriggerName: UnbxdProductViewTrigger

TriggerType: Custom Event

EventName: ProductView

TriggerFiresOn: All Custom Events

![](https://files.readme.io/b1349b4d673a33fb2919de5fae4dfbef65c406aa63289b86b783440803f5fe2a-image.png)

2. Create a Variable in GTM to fetch the product ID from the dataLayer.

Variable Configuration:

VariableName: UnbxdProductViewPayload

Variable Type: Data Layer Variable

Data Layer Variable Name: ProductViewPayload

![](https://files.readme.io/49a503950a5b1c86227e84fb2a21c4b1f99481178468617f73ac44ac629aba09-image.png)

3. Create a Javascript tag with the below details

Tag Configuration:

Tag Name: UnbxdProductViewTag

Tag Type: Custom HTML

HTML Content:

```
// Pass payload to Unbxd.track function
// to call the tracker API

<script type="text/javascript">
   var u_payload = {{UnbxdProductViewPayload}};
   if (Unbxd && typeof Unbxd.track === 'function'
       && u_payload.hasOwnProperty("pid")){
       Unbxd.track('product_view', u_payload);
     } else {
       console.error('ERRNO-005: unbxdAnalytics.js is not loaded or payload incorrect!')
   }
</script>
```

4. Pushing the event to the dataLayer through a product view.

Push payload to Datalayer

// Add payload to Datalayer variable ProductViewPayload\
// Should be triggered when a user lands on product page

```
// Add payload to Datalayer variable ProductViewPayload
// Should be triggered when a user lands on product page

<script type="text/javascript">
   window.dataLayer = window.dataLayer || [];
   dataLayer.push(
     {
      'event': 'ProductView',
      'ProductViewPayload':
       {
         'requestId': 'REQUEST ID',
         'pid': 'PRODUCT ID',
         'variantId': 'VARIANT ID OF SELECTED VARIANT'
       }
     });
</script>
```

Parameter Details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                                            |
| ------------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------- |
| `requestId`        | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                                     |
| `pid`              | String       | Unique ID for the product.                                                                                             |
| `variantId`        | String       | VariantId of the selected product variant, if `relevantDocumentType="variant"`, in the search API response, or `null`. |

Events Flow will be:

As soon as the ‘Productview\` event got pushed to the dataLayer.\
This initiates the trigger UnbxdProductViewTrigger which we created in the step-1.
UnbxdProductViewTrigger executes the tag UnbxdProductViewTag: which we created in step-3.
Inside UnbxdProductViewTrigger we have added an Unbxd analytics product view tag.
Product view tracker code gets the data from the variable UnbxdProductViewPayload which we created in step-2.
Finally, UnbxdProductViewTrigger event data will be updated in the Unbxd analytics database for the particular siteKey.
Add to Cart
Tracking products added to the cart help us further improve product ranks for a search query.

1. Create Trigger in GTM to catch the uniqueId of product on product add to cart.

Trigger Configuration:

Trigger Name: UnbxdProductAddToCartTrigger

Trigger Type: Custom Event

Event Name:  ProductCarted (Use regex matching)

TriggerFiresOn: All Custom Events

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/9235fcc8d12b3c1b0d480cc3f331d9a16ddf198c55d743ae88857c822a078d64-image.png" />

2. Create Variable in GTM, to fetch the product details from the dataLayer.

Variable Configuration:

Variable Name: UnbxdProductCartedPayload

Variable Type: Data Layer Variable

Data Layer Variable Name: ProductCartedPayload

![](https://files.readme.io/0c66ffc76cfc57379f8ba3a45c2ea0cafa98a05ca164919c02516c617ef67cbf-image.png)

3. Create Create a Javascript tag with the below details.

Tag Configuration:

Tag Name: UnbxdProductCartedTag

Tag Type: Custom HTML

HTML Content:

```
// Pass payload to Unbxd.track function
// to call the tracker API

<script type="text/javascript">
   var u_payload = {{UnbxdProductCartedPayload}};
   if (Unbxd && typeof Unbxd.track === 'function') {
      Unbxd.track("addToCart", u_payload);
   } else {
       console.error('ERRNO-006: unbxdAnalytics.js is not loaded or payload incorrect!')
   }
</script>
```

Push payload to Datalayer:

```
// Add payload to Datalayer variable ProductCartedPayload
// Should be triggered on add to cart button onclick() event
// when product is added to cart

<script type="text/javascript">
   window.dataLayer = window.dataLayer || [];
   dataLayer.push(
     {
      'event': 'ProductCarted',
      'ProductCartedPayload':
       {
           'requestId': 'REQUEST ID',
           'pid': 'PRODUCT ID',
           'variantId': 'VARIANT ID OF SELECTED VARIANT',
           'qty': 'QUANTITY SELECTED',
           'price': 'UNIT PRICE FOR PRODUCT'
       }
     });
</script>
```

Payload details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                                            |
| ------------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------- |
| `requestId`        | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                                     |
| `pid`              | String       | Unique ID for the product.                                                                                             |
| `variantId`        | String       | VariantId of the selected product variant, if `relevantDocumentType="variant"`, in the search API response, or `null`. |
| `qty`              | String       | Quantity being added to the cart by the user.                                                                          |
| `price`            | String       | Unit price of the product (variant, if variant is selected).                                                           |

## Cart Removal

Like “Cart Additions”, tracking “Cart Removal” is also important as it helps us better understand the visitor’s preferences. To track the “Cart Removal”, customer needs to call the Unbxd API on the cart Removal event.

1. Create Trigger in GTM to catch the uniqueId of the product if a product is removed from cart page.

Trigger Configuration:

Trigger Name: RemoveFromCartTrigger

Trigger Type: Custom Event

Event Name: CartRemoved (Use regex matching)

TriggerFiresOn: All Custom Events

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/d49ed1ccc16e67ad267e5b4280a34928375b9df4052aea7d8db234a7f71d1a51-image.png" />

2. Create Variable in GTM, to fetch the product details from the dataLayer.

Variable Configuration:

Variable Name: RemoveProductFromCart

Variable Type:  Data Layer VariableData Layer

Variable Name: CartRemovedPayload

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/aabb40f731071d4c9924c9923196cb926d5fe7f84af2b1b7d5e752a22cbe11b9-image.png" />

3. Create a Javascript tag with the below details.

Tag Configuration:

Tag Name: RemoveCartTag

Tag Type: Custom HTML

HTML Content:

```
// Pass payload to Unbxd.track function
// to call the tracker API

<script type="text/javascript">
   var u_payload = {{RemoveProductFromCart}};
   if (Unbxd && typeof Unbxd.track === 'function') {
      Unbxd.track("cartRemoval", u_payload);
   } else {
       console.error('ERRNO-007: unbxdAnalytics.js is not loaded or payload incorrect!')
   }
</script>
```

Push payload to Datalayer:

```
// Add payload to Datalayer variable CartRemovedpayload
// Should be triggered when a product is removed
// from cart

<script type="text/javascript">
   window.dataLayer = window.dataLayer || [];
   dataLayer.push(
     {
      'event': ' 'CartRemoved',
      'CartRemovedPayload':
       {
           'requestId': 'REQUEST ID',
           'pid': 'PRODUCT ID',
           'variantId': 'VARIANT ID OF SELECTED VARIANT',
           'qty': 'QUANTITY SELECTED',
           'price': 'UNIT PRICE FOR PRODUCT'
       }
     });
</script>
```

Payload details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                                            |
| ------------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------- |
| `requestId`        | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                                     |
| `pid`              | String       | Unique ID for the product.                                                                                             |
| `variantId`        | String       | VariantId of the selected product variant, if `relevantDocumentType="variant"`, in the search API response, or `null`. |
| `qty`              | String       | Quantity being added to the cart by the user.                                                                          |
| `price`            | String       | Unit price of the product (variant, if variant is selected).                                                           |

### Order

Unbxd analytics also track orders placed by the visitor from your eCommerce store.

1. Create Trigger in GTM to catch the products details on order confirmation.

Trigger Configuration:

Trigger Name: UnbxdProductOrderTrigger

Trigger Type: Custom Event

Event Name: ProductOrder (Use regex matching)

TriggerFiresOn: All Custom Events

![](https://files.readme.io/6c2478fc821ac36c7497973e227d3317924515f4787a60d72534481521485610-image.png)

2. Create Variable in GTM, to fetch the products data from the dataLayer.

Variable Configuration:

Variable Name: UnbxdProductsOrderedPayload

Variable Type:  Data Layer VariableData Layer

Variable Name: ProductsOrderedPayload

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/348adfb7147530e54667b26aedc127b36d9ddd113f7042143f64108294b7d90d-image.png" />

3. **Create a Javascript tag with the below details.**

Tag Configuration:

Tag Name: UnbxdProductsOrderedTag

Tag Type: Custom HTML

HTML Content:

Individually for each product

Tag Configuration:

HTML Content:

```
// Pass payload to Unbxd.track function
// to call the tracker API

<script type="text/javascript">
   var u_payload = {{UnbxdProductsOrderedPayload}};
   if( Unbxd && typeof Unbxd.track === 'function' &&
       u_payload.hasOwnProperty("pid") &&
       u_payload.hasOwnProperty("price") &&
       u_payload.hasOwnProperty ("qty")){
       Unbxd.track('order', u_payload);
   } else {
       console.error('ERRNO-008: unbxdAnalytics.js is not loaded or payload incorrect!')
   }
</script>
```

Push payload to Datalayer:

```
// Add payload to Datalayer variable ProductOrderedPayload
// Should be triggered individually for all the products on
// order success page

<script  type="text/javascript">
   window.dataLayer = window.dataLayer || [];
   dataLayer.push(
     {
      'event': 'ProductOrder',
      'ProductsOrderedPayload':
       {
           'requestId': 'REQUEST ID',
           'pid': 'PRODUCT ID',
           'variantId': 'VARIANT ID OF SELECTED VARIANT',
           'qty': 'QUANTITY SELECTED',
           'price': 'UNIT PRICE FOR PRODUCT'
       }
     });
</script>
```

Payload Details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                        |
| ------------------ | ------------ | ---------------------------------------------------------------------------------- |
| `requestId`        | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`. |
| `pid`              | String       | Unique ID for the product.                                                         |
| `variantId`        | String       | VariantId of the selected product variant (if variant), or `null`.                 |
| `qty`              | String       | Quantity of the product being ordered.                                             |
| `price`            | String       | Unit price of the product (variant, if variant is selected).                       |

trackMultiple

```
// Pass payload to Unbxd.track function
// to call the tracker API

<script type="text/javascript">
   var u_payload = {{UnbxdProductsOrderedPayload}};
   if( Unbxd && typeof Unbxd.track === 'function'
       && typeof(u_payload) == "object"
       && u_payload.length > 1){
       Unbxd.trackMultiple('order', u_payload);
   } else {
       console.error('unbxdAnalytics.js is not loaded or payload incorrect!')
   }
</script>
```

Push payload to Datalayer:

```
// Add payload to Datalayer variable ProductOrderedPayload
// Should be triggered on order success page
// for all products in order added to a list

<script  type="text/javascript">
   window.dataLayer = window.dataLayer || [];
   dataLayer.push(
     {
      'event': 'ProductOrder',
      'ProductsOrderedPayload':
       [{
           'requestId': 'REQUEST ID',
           'pid': 'PRODUCT ID',
           'variantId': 'VARIANT ID OF SELECTED VARIANT',
           'qty': 'QUANTITY SELECTED',
           'price': 'UNIT PRICE FOR PRODUCT'
       },
       {
           'requestId': 'REQUEST ID',
           'pid': 'PRODUCT ID',
           'variantId': 'VARIANT ID OF SELECTED VARIANT',
           'qty': 'QUANTITY SELECTED',
           'price': 'UNIT PRICE FOR PRODUCT'
       },
       {
           'requestId': 'REQUEST ID',
           'pid': 'PRODUCT ID',
           'variantId': 'VARIANT ID OF SELECTED VARIANT',
           'qty': 'QUANTITY SELECTED',
           'price': 'UNIT PRICE FOR PRODUCT'
       }]
     });
</script>
```