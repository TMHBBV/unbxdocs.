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

<br />

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

## Category Page

A category page event is tracked to understand the browse/category interests of your visitors, as in which all category pages are visited by user. Each browse results page is tracked to enable per category page analytics of the visitor. A typical category page event involves:

UnbxdCategoryPageTrigger

Through GTM to integrate this event we need to follow below approach:

Create Trigger in GTM to catch the CategoryPath on browse results page load.\
Trigger Configuration:

* TriggerName: UnbxdCategoryPageTrigger
* Trigger Type: Custom Event
* Event Name: CategoryPage
* TriggerFiresOn: All custom events

<Image align="center" width="80% " src="https://files.readme.io/4a75e6039100961d7b2dd832bde188d4380f6d33d77f4101c00b3f9361e3aaf9-image.png" />

<br />

Create Variable in GTM, to fetch the query from the dataLayer.\
Variable Configuration:

Variable Name: UnbxdCategoryPagePayload

Variable Variable Type: Data Layer Variable

Data Layer Variable Name: CategoryPagePayload

HTML Content:

<Image align="center" width="80% " src="https://files.readme.io/440a6e6049fd4d2e37ff9873d3ff4272d8b515f44305d204f80cc445cc5226ac-image.png" />

<br />

Create a Javascript tag with the below details.

Tag Configuration:

Tag Name: UnbxdSearchQueryTag

Tag Type: Custom HTML

HTML Content:

/