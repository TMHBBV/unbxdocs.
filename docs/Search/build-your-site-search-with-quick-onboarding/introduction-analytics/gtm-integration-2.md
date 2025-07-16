---
title: GTM Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
## GTM Integration

Tracking visitor analytics and behavior are essential in order to provide accurate and visitor-specific search and category page results. UNBXD analyzes visitor events, such as product clicks, products added to cart, orders, etc. These events are tracked using browser cookies. With this information, a profile is built for every visitor, based on his/her affinity to different categories, brands, or prices.

This information is then aggregated and analyzed for two purposes:

* Generating reports
* Providing relevant and personalized search & category pages results

When visitors browse through your store, the integrated trackers log everything visitors do – the products they visit, orders, even the various store properties they interact with. We take that information, analyze it, and assemble a detailed profile of the visitor. We know their browsing patterns, preferences and can even determine susceptibility to merchandising campaigns. The trackers are unique tracking codes that must be configured onto the store properties that yield an interaction. We call this interaction as an “event”, for example, click on the “Add to Cart” button.

The visitor profiles help fetch relevant and personalized products as search results. It also helps in generating detailed reports.

> 📘 NOTE
>
> For Unbxd E-commerce Search to function correctly on your site, Unbxd Analytics must be configured.

## Introduction to GTM

Google Tag Manager is a free tool that allows you to manage and deploy marketing tags (snippets of code or tracking pixels) on your website (or mobile app) without having to modify the code.

Here’s a very simple example of how GTM works. Information from one data source (your website) is shared with another data source (Analytics) through Google Tag Manager. GTM becomes very handy when you have lots of tags to manage because all the code is stored in one place.

### Basic components of GTM

Following are the basic components within Google Tag Manager:

* Tags – Tags are tracking codes and code fragments that tell GTM what action to take on that page.

For example: Sending searched query to Unbxd analytics.

* Triggers – Triggers specify the conditions under which a Tag should fire.For example: A trigger with a condition to only fire a Tag when a user views URLs
* containing the path /search/.
* Variables – Variables are values used in triggers and tags to filter when a specific tag should fire. GTM provides built-in variables and allows you to create custom user-defined variables. For example: A ‘click’ class variable has a value name (such as a word string) assigned to buttons on the website.
* DataLayer – The dataLayer is a JSON that contains name value pairs of data points you wish to pass from your website into GTM. (And GTM can then, in turn, pass on to any tags that are managed in GTM, including Unbxd tags.)

### Requirements for Unbxd tracking through GTM

Unbxd analytics scripts need to be loaded across all the pages. We require a tag which will need to be loaded on all the pages. Below is the required code block for Unbxd analytics script. This should be loaded before other Unbxd tracking scripts and is mandatory to be added on all pages.

```
// Container ID is present in GTM-XXXX format in GTM Dashboard
// HTML ID can be found in the url. Eg:
// containers/422XXXX/workspaces/20 , 20 is the HTML ID

<script type="text/javascript">
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

<br />

The above JS snippet needs to be added in a tag and also enable Built-In Variables, i.e., Container ID and HTML ID without fail.

* TagName: UnbxdAnalyticsScript
* TagType: Custom HTML Tag
* Trigger: AllPagesPageView

## Search Query Tracker

A Search hit event is tracked to understand the query and intent of your visitors. Each search

query is tracked to enable per-query analytics of the visitor. A typical search hit event involves:

**SearchQueryTrigger**: Through GTM to integrate this event we need to follow below approach:

1. Create Trigger in GTM to catch the search Query on form hit.\
   Trigger Configuration:
   * TriggerName: UnbxdSearchQueryTrigger
   * Trigger Type: Custom Event
   * Event Name: SearchQuery                                                                                                                                TriggerFiresOn: All custom events

<Image align="center" width="80% " src="https://files.readme.io/ace8019cb8b49f1efb5412038cd7547d35a65b94dbcc82f02432691e4b5ef4e8-image.png" />

2. Create Variable in GTM, to fetch the query from the dataLayer.

Variable Configuration:

* Variable Name: UnbxdSearchQueryPayload
* Variable Variable Type: Data Layer Variable
* Data Layer Variable Name: SearchQueryPayload

HTML Content:

<Image align="center" width="80% " src="https://files.readme.io/d635d029ba4fd4d1cf4cea1b4b7d4020e4e702fe7d031ff091dbe3fe3354cd62-image.png" />

3. Create a Javascript tag with the below details.

   Tag Configuration:
   * Tag Name: UnbxdSearchQueryTag
   * Tag Type: Custom HTML
   * HTML Content:

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

On a search query, please pass the searched query to the dataLayer as shown above. The event flow will be:

* As soon as the `SearchQuery` event got pushed data layer.
* This initiates the trigger UnbxdSearchQueryTrigger which we created in the step-1.
* UnbxdSearchQueryTrigger executes the tag: UnbxdSearchQueryTag which we created in step-3.
* Inside UnbxdSearchQueryTag we have added Unbxd analytics search tracker code.
* Search tracker code get the searched query from variable UnbxdSearchQueryPayload which we created in step-2.
* Finally searched query will be updated in Unbxd analytics database for the particular siteKey.

## Product Click Unbxd Tracker

Tracking product clicks of visitors helps our search engine to understand their preferences over other products on the listing page. This information is used to compute popular products and render relevant and personalized results. It needs to be tracked in case of search and navigation pages. It is also integrated if customer is using the recommendation widgets.

Through GTM to integrate this event we need to follow the below approach:

Create a Trigger in GTM to catch the click event.

Trigger Configuration:

* TriggerName: UnbxdProductClickTrigger
* TriggerType: Custom Event
* EventName: ProductClick
* TriggerFiresOn: All Custom Events

<Image align="center" width="80% " src="https://files.readme.io/1dc01a993470a27e86d16c1a25d74ed5d9d353acb4651bd0072bb78ed3c24e64-image.png" />

Create Variable in GTM, to fetch the product details from the dataLayer. Variable Configuration:

VariableName: UnbxdProductClickPayload

Variable Type: Data Layer Variable

Data Layer Variable Name: ProductClickPayload

<Image align="center" width="80% " src="https://files.readme.io/97d98ce6a8c01f9dd12311650921890c5b69c0089dac752cce45c11dc65661d6-image.png" />

3. Create a Javascript tag with the below details.

   Tag Configuration:
   * Tag Name: UnbxdProductClickTag
   * Tag Type: Custom HTML
   * HTML Content:
   ```
   // Pass payload to Unbxd.track function
   // to call the tracker API

   <script type="text/javascript">
      var u_payload = {{UnbxdProductClickPayload}};
      if (Unbxd && typeof Unbxd.track === 'function'
          && u_payload.hasOwnProperty("pid")
          && u_payload.hasOwnProperty ("prank")){
          Unbxd.track('click', u_payload);
        } else {
          console.error('unbxdAnalytics.js is not loaded or payload incorrect!')
      }
   </script>
   ```
   Pushing the event to the Data Layer through the Product Click.

```
// Add payload to Datalayer variable ProductClickPayload
// Should be triggered on product click

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
         'query': 'SEARCH QUERY'
       }
     });
</script>
```

Payload Details

| Attribute | Datatype | Value to be passed                                                                                    |
| --------- | -------- | ----------------------------------------------------------------------------------------------------- |
| requestId | string   | To be extracted from Unbxd search API response headers, from unx-request-id                           |
| pid       | string   | Unique id for the product, to be taken from API response, if relevantDocumentType = "parent", or null |
| variantId | string   | The variantId of the selected product variant, if relevantDocumentType = "variant", or null           |
| prank     | string   | Number aka rank of product in response                                                                |
| query     | string   | Search query for search listing page                                                                  |