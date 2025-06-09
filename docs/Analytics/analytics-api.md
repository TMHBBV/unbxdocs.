---
title: Analytics API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

<br />

Whether you’re a large enterprise or an SME (small-to-medium enterprise) online store owner, your resources are finite. As your business grows, your shoppers are looking for a retail experience that is intuitive and personalized.

Tracking visitor analytics and behaviour anonymously is critical to provide accurate and visitor-specific search and category page results.

To help us analyse and understand your shoppers better, Unbxd captures information for every visitor anonymously by creating the following three sets of cookies:

1. **userId**: An identifier for the shopper. This cookie never expires. For generating userId value, the below logic needs to be used to generate and store userId value in cookie.\
   This will ensure that it is generated in the right format and of correct length. UserId is a unique identifier for a shopper on a particular device which is generated only for a new user and should remain the same unless a user explicitly deletes this cookie.

```
var date = new Date();
var uid =  ‘uid-’ + date.getTime() + ‘-’ + Math.floor(Math.random() * 100000);
```

2. **visitId** : An identifier for the session/visit. This cookie expires when the shopper is idle for more than 30 minutes. If it is not defined for a new user, it should be created as per the logic mentioned in below code. Just modify the object name from Unbxd accordingly to what you want to use in the below code:

```
Unbxd.getVisitId = function getVisitId() {
      var visitId = Unbxd.readCookie(Unbxd.cookies.visitId);
      var now = new Date().getTime();
      var expire = new Date(now + 30 * 60000);
      if (!visitId) {
        visitId = 'visitId-' + now + '-' + Math.floor(Math.random() * 100000);
        Unbxd.setCookie(Unbxd.cookies.visitId, visitId, expire);
      } else {
        // extend visitId expire time if exists
        // visitId should expire on more than 30min inactivity
        Unbxd.setCookie(Unbxd.cookies.visitId, visitId, expire);
      }
      return visitId;
};
```

As mentioned above, visitId can be reset after shopper is idle for 30 mins and they should fire the visitor event again as in the below code for expire condition.

> 📘 Note
>
> It is mandatory is that you need to fire visitor event for Analytics, whenever the visitId is reset based on the expire logic. Session cookies have an inactivity timer. Sessions expire when they are idle for more than 30 minutes.

3. **visit** – This stores whether the visitor is a ‘first\_time’ or ‘repeat’ shopper. This cookie expires when the shopper is idle for more than 30 minutes.

The information within these cookies are used to create a non-identifiable persona that allows us to analyze your shopper’s past click-through behaviors, shopping history, and product preferences, in real time. We use this information to provide site-level aggregate reporting.

Unique tracking codes within site interactions help us measure the performance user interactions anonymously.

Anonymous shopper profiles help fetch personalized search results. It also helps in generating detailed reports.

In other words, information is aggregated and analysed for two purposes:

Providing relevant and personalised search & category pages results\
Generating reports
As a merchandiser or product manager you can make informed decisions and make your shopper’s experience a delightful one.

## Events

<br />

Events are any action a visitor takes on your eCommerce store.

Once deployed, the JS code tracks shopper events, using information stored within a cookie titled ‘unbxd.userId’. This file tracks, stores, and relays useful session-based information to Unbxd.

This section helps you understand more about the session-based events we track, like:

1. Visitor: Identifies new and returning shoppers.
2. Search Hit: Is the search query performed on the web page.
3. Search Impression: Is every time the search results page loads products on the PLP.
4. Product Click: Is when a shopper clicks on a product in the PLP.
5. Product View: Is the number of times a shopper has visited a specific Product Details Page (PDP).
6. Add to Cart: Is the number of times shoppers have added products to a cart. This event can be fired from both PDP and PLP.
7. Cart Removal: Is the number of times a shopper has removed a product from the cart.
8. Orders: Is the number of orders that have been successfully completed.

## API Integration

In this method, you integrate the API references for every event that you want Unbxd to track.

**NOTE: In case you are using a web browser, it is recommended that you use the Browser-based integration**

The calls have to be in the form of an http GET request to the url:

```
tracker.unbxdapi.com/v2/1p.jpg
```

Some of the common attributes used in the APIs are described below:

**referrer**: The url of the previous page, will be empty if the user opened that particular url directly.\
**uid**: The unique identifying number for shoppers. Usually we set the “uid” for a particular user in a particular browser. The “uid” is stored within the “uid” cookie, and we store this ID every time we need user-specific event information.
Every request needs to be passed with the following HTTP headers:

1. X-Forwarded-For
2. user-agent

## Visitor

The Visitor event is the first event that gets created when a shopper visits your site. There are two types of shoppers we track:

1. First-time shoppers
2. Repeat shoppers

All shopper events are tracked against an anonymous User ID that is allotted to every shopper visiting your site.  Site-level information, like the “userID”, “siteName”, and “visitType” parameter, are stored in two cookies titled ‘unbxd.userId’ and ‘visitId’.

Both these files are created for the first time when a shopper visits your site for the first time. When a shopper does not have the ‘userID’ cookie or if the shopper has cleared the cookie from their device, that shopper is called as a ‘first-time shopper’. Conversely, when a shopper already has the ‘userID’ cookie, that shopper is a ‘repeat shopper’.

User ID is a random numerical value with the timestamp of the visit and is device/browser-specific.

For instance, a shopper accessing your site on Google Chrome and Mozilla Firefox on the same computer will have two sets of cookies for each browser.

> 📘 Note
>
> The ‘visitID’ cookie is set to expire after 30 continuous minutes of inactivity. If a shopper returns to your site after the cookie expires, that shopper will be a ‘first-time shopper’.

Here’s how a Visitor API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"url":"{{url-of-the-website}}","referrer":"{{reference-link}}","visit_type":"{{first-or-repeat}}","visitId":"{{visitId}}"}&UnbxdKey={{unbxd_sitekey}}&action=”visitor”&uid=”uid-1642414737751-2003”&t=”1662364656435|0.29442892143527755”
```

<br />

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        **Attribute Name**
      </th>

      <th>
        **Datatype**
      </th>

      <th>
        **What value to be passed**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **action**
      </td>

      <td>
        string
      </td>

      <td>
        Indicates the type of event. In this case, the value will be ‘visitor’
      </td>
    </tr>

    <tr>
      <td>
        **url**
      </td>

      <td>
        string
      </td>

      <td>
        Website URL where search is performed
      </td>
    </tr>

    <tr>
      <td>
        **visit\_type**
      </td>

      <td>
        string
      </td>

      <td>
        Either “first\_time” or “repeat”
      </td>
    </tr>

    <tr>
      <td>
        **UnbxdKey**
      </td>

      <td>
        string
      </td>

      <td>
        UnbxdSitekey value
      </td>
    </tr>

    <tr>
      <td>
        **uid**
      </td>

      <td>
        string
      </td>

      <td>
        Extracted from cookie `unbxd.userId` (unique shopper ID)
      </td>
    </tr>

    <tr>
      <td>
        **time**
      </td>

      <td>
        string
      </td>

      <td>
        This timestamp parameter should be according to the formula shared below

        t : current\_time | random number between 0 to 1

        t = new Date().getTime() + ‘|’ + Math.random();
      </td>
    </tr>

    <tr>
      <td>
        **referrer**
      </td>

      <td>
        string
      </td>

      <td>
        Link from where the page is opened (optional)
      </td>
    </tr>
  </tbody>
</Table>

## Search Hit

The Search event is generated every time a shopper uses the search bar to search for a product on your site.

Here’s how a Search API will look like.

```
http://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{search-query}}","url":"{{url-of-the-website}}","referrer":"","requestId":"{{unx-request-id}}","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}5&t=1662365253141|0.6835012308821242
```

> 📘 Note
>
> Action for this event will be “search”, as in the API above and does not need to be changed.

<Table>
  <thead>
    <tr>
      <th>
        **Attribute Name**
      </th>

      <th>
        **Datatype**
      </th>

      <th>
        **What value to be passed**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **action**
      </td>

      <td>
        string
      </td>

      <td>
        Indicates the type of event. In this case, the value will be ‘search’
      </td>
    </tr>

    <tr>
      <td>
        **query**
      </td>

      <td>
        string
      </td>

      <td>
        The search query entered by user
      </td>
    </tr>

    <tr>
      <td>
        **pid**
      </td>

      <td>
        string
      </td>

      <td>
        Unique id for the product, to be taken from API response, if relevantDocumentType=”parent”, In search api response, or null
      </td>
    </tr>

    <tr>
      <td>
        **url**
      </td>

      <td>
        string
      </td>

      <td>
        Website url where search is performed
      </td>
    </tr>

    <tr>
      <td>
        **requestId**
      </td>

      <td>
        string
      </td>

      <td>
        To be extracted from Unbxd search api response headers, from unx-request-id
      </td>
    </tr>

    <tr>
      <td>
        **visit\_type**
      </td>

      <td>
        string
      </td>

      <td>
        Can be either “first\_time” or “repeat”
      </td>
    </tr>

    <tr>
      <td>
        **UnbxdKey**
      </td>

      <td>
        string
      </td>

      <td>
        UnbxdSitekey value
      </td>
    </tr>

    <tr>
      <td>
        **uid**
      </td>

      <td>
        string
      </td>

      <td>
        Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers.
      </td>
    </tr>

    <tr>
      <td>
        **time**
      </td>

      <td>

      </td>

      <td>
        This timestamp parameter should be according to the formula shared below t : current\_time | random number between 0 to 1
        t = new Date().getTime() + ‘
      </td>
    </tr>

    <tr>
      <td>
        **referrer**
      </td>

      <td>
        string
      </td>

      <td>
        Link from where the page is opened (Optional)
      </td>
    </tr>
  </tbody>
</Table>

## Search Impression

A Search Impression (also known as Product Impressions) event is generated after a shopper gets a list of products on the search results page. This event is also generated every time a shopper refines the results by facets, filters, scroll-down or pagination. The productId of the products listed in the PLP will be sent as a payload.

Here’s how a Search Impression API will look like:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{search-query}}","pids_list":"{{list-of-products-uniqueId}}","url":"{{url-of-the-website}}","referrer":"","requestId":"{{unx-request-id}}","visit_type":"{{first_or_repeat}}",,,"visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search_impression&uid={{uid}}&t=1662366285967|0.7498946341398707  
```

Payload details:

<Table>
  <thead>
    <tr>
      <th>
        **Attribute Name**
      </th>

      <th>
        **Datatype**
      </th>

      <th>
        **What value to be passed**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **action**
      </td>

      <td>
        string
      </td>

      <td>
        Indicates the type of event. In this case, the value will be ‘search\_impression’
      </td>
    </tr>

    <tr>
      <td>
        **query**
      </td>

      <td>
        string
      </td>

      <td>
        The search query entered by user
      </td>
    </tr>

    <tr>
      <td>
        **url**
      </td>

      <td>
        string
      </td>

      <td>
        Website url where search is performed
      </td>
    </tr>

    <tr>
      <td>
        **pids\_list**
      </td>

      <td>
        string
      </td>

      <td>
        List of unique id of products loaded with current request. If zero products are returned, pass an empty list(array).
      </td>
    </tr>

    <tr>
      <td>
        **requestId**
      </td>

      <td>
        string
      </td>

      <td>
        To be extracted from Unbxd search api response headers, from unx-request-id
      </td>
    </tr>

    <tr>
      <td>
        **visit\_type**
      </td>

      <td>
        string
      </td>

      <td>
        Can be either “first\_time” or “repeat”
      </td>
    </tr>

    <tr>
      <td>
        **UnbxdKey**
      </td>

      <td>
        string
      </td>

      <td>
        UnbxdSitekey value
      </td>
    </tr>

    <tr>
      <td>
        **uid**
      </td>

      <td>
        string
      </td>

      <td>
        Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers
      </td>
    </tr>

    <tr>
      <td>
        **time**
      </td>

      <td>

      </td>

      <td>
        This timestamp parameter should be according to the formula shared below t : current\_time | random number between 0 to 1
        t = new Date().getTime() + ‘
      </td>
    </tr>

    <tr>
      <td>
        **referrer**
      </td>

      <td>
        string
      </td>

      <td>
        Link from where the page is opened (Optional)
      </td>
    </tr>
  </tbody>
</Table>

## Product Click

The Product Click event is generated every time a shopper clicks on a product in a Product Listing Page (PLP) or in a recommendation widget.

This helps us understand your shoppers’ search preferences. This information is analyzed to list and promote ‘Popular Products’ and display personalized ‘Recommended For You’ lists.

Here’s how a Product Click API will look like:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueId-of-the-product}}","query":"{{search-query}}","pr":"","requestId":"{{unx-request-id}}","url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=click&uid={uid}}&t=1662365583875|0.7442797542869459
```

Payload details:

<Table>
  <thead>
    <tr>
      <th>
        **Attribute Name**
      </th>

      <th>
        **Datatype**
      </th>

      <th>
        **What value to be passed**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **action**
      </td>

      <td>
        string
      </td>

      <td>
        Indicates the type of event. In this case, the value will be ‘click’
      </td>
    </tr>

    <tr>
      <td>
        **query**
      </td>

      <td>
        string
      </td>

      <td>
        The search query entered by user
      </td>
    </tr>

    <tr>
      <td>
        **pid**
      </td>

      <td>
        string
      </td>

      <td>
        Unique id for the product, to be taken from API response, if relevantDocumentType=”parent”, In search api response, or null
      </td>
    </tr>

    <tr>
      <td>
        **url**
      </td>

      <td>
        string
      </td>

      <td>
        Website url where product is clicked
      </td>
    </tr>

    <tr>
      <td>
        **requestId**
      </td>

      <td>
        string
      </td>

      <td>
        To be extracted from Unbxd search api response headers, from unx-request-id
      </td>
    </tr>

    <tr>
      <td>
        **visit\_type**
      </td>

      <td>
        string
      </td>

      <td>
        Can be either “first\_time” or “repeat”
      </td>
    </tr>

    <tr>
      <td>
        **UnbxdKey**
      </td>

      <td>
        string
      </td>

      <td>
        UnbxdSitekey value
      </td>
    </tr>

    <tr>
      <td>
        **uid**
      </td>

      <td>
        string
      </td>

      <td>
        Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers
      </td>
    </tr>

    <tr>
      <td>
        **time**
      </td>

      <td>

      </td>

      <td>
        This timestamp parameter should be according to the formula shared below
        t : current\_time | random number between 0 to 1
        t = new Date().getTime() + ‘
      </td>
    </tr>

    <tr>
      <td>
        **referrer**
      </td>

      <td>
        string
      </td>

      <td>
        Link from where the page is opened (Optional)
      </td>
    </tr>
  </tbody>
</Table>

## Product View

Product View indicates the number of times a shopper has visited a specific Product Details Page (PDP).

Here’s how a Product View API will look like:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueid-of-the-product}}","referrer":"","url":"{{url-of-the-website}}","visit_type":"{{first-or-repeat}}","requestId":”{{request-id}},”UnbxdKey”=”{{unbxd-sitekey}}&action=product_view,”uid”:”{{uid}}”&t={{time-spent}}
```

<br />

<Table>
  <thead>
    <tr>
      <th>
        **Attribute Name**
      </th>

      <th>
        **Datatype**
      </th>

      <th>
        **What value to be passed**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        action
      </td>

      <td>
        string
      </td>

      <td>
        Indicates the type of event. In this case, the value will be ‘product\_view’
      </td>
    </tr>

    <tr>
      <td>
        url
      </td>

      <td>
        string
      </td>

      <td>
        URL of product display page (PDP), on which product is viewed.
      </td>
    </tr>

    <tr>
      <td>
        pid
      </td>

      <td>
        string
      </td>

      <td>
        Unique id of the product viewed.
      </td>
    </tr>

    <tr>
      <td>
        requestId
      </td>

      <td>
        string
      </td>

      <td>
        To be extracted from Unbxd search api response headers, from unx-request-id
      </td>
    </tr>

    <tr>
      <td>
        visit\_type
      </td>

      <td>
        string
      </td>

      <td>
        Can be either “first\_time” or “repeat”
      </td>
    </tr>

    <tr>
      <td>
        UnbxdKey
      </td>

      <td>
        string
      </td>

      <td>
        UnbxdSitekey value
      </td>
    </tr>

    <tr>
      <td>
        action
      </td>

      <td>
        string
      </td>

      <td>
        Indicates the type of event. In this case, the value will be ‘product\_view’
      </td>
    </tr>

    <tr>
      <td>
        uid
      </td>

      <td>
        string
      </td>

      <td>
        Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers
      </td>
    </tr>

    <tr>
      <td>
        time
      </td>

      <td>

      </td>

      <td>
        This timestamp parameter should be according to the formula shared below t : current\_time | random number between 0 to 1
        t = new Date().getTime() + ‘
      </td>
    </tr>

    <tr>
      <td>
        referrer
      </td>

      <td>
        string
      </td>

      <td>
        Link from where the page is opened (Optional)
      </td>
    </tr>
  </tbody>
</Table>

## Add to Cart

Whenever a user adds any product to cart or shopping bag, the add to cart will get fired. This helps us further improve the products appearing in the Recommendation widget.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueid-of-the-product}}","qty":”{{no-of-units}}","variantId":"{{variantId-of-the-variant}}","url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first-or-repeat}}"&UnbxdKey=”{{unbxd-sitekey}}&action=cart&uid={{uid}}&t={{time-spent}}
```

Payload details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                                                                                                                     |                        |
| ------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| action             | string       | Indicates the type of event. In this case, the value will be ‘cart’                                                                                                                             |                        |
| qty                | string       | The number of units added to the cart. This should be the string value of the quantity added. For example, if 2 quantities of a product is added then its value would be “2” (instead of 2).    |                        |
| url                | string       | Url of the page where product is added to cart.                                                                                                                                                 |                        |
| pid                | string       | Unique id of the product viewed.                                                                                                                                                                |                        |
| visit\_type        | string       | Can be either “first\_time” or “repeat”                                                                                                                                                         |                        |
| UnbxdKey           | string       | UnbxdSitekey value                                                                                                                                                                              |                        |
| uid                | string       | Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers                                                                                              |                        |
| t                  |              | This timestamp parameter should be according to the formula shared below \<br>\<br> \*\*t : current\\\_time \| random number between 0 to 1\*\* \<br>\<br> \\\*\\\*t = new Date().getTime() + ‘ | ’ + Math.random();\*\* |
| referrer           | string       | Link from where the page is opened (Optional)                                                                                                                                                   |                        |

## Cart Removal

The Remove From Cart event tracks every instance a product is removed from cart as well. Information it helps us better understand the visitor’s preferences.

When a product with variants is removed from the cart, here’s how the API will look like.

Payload details:

<Table>
  <thead>
    <tr>
      <th>
        **Attribute Name**
      </th>

      <th>
        **Datatype**
      </th>

      <th>
        **What value to be passed**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        action
      </td>

      <td>
        string
      </td>

      <td>
        Indicates the type of event. In this case, the value will be ‘cartRemoval’
      </td>
    </tr>

    <tr>
      <td>
        pid
      </td>

      <td>
        string
      </td>

      <td>
        Unique id of the product viewed.
      </td>
    </tr>

    <tr>
      <td>
        qty
      </td>

      <td>
        string
      </td>

      <td>
        Quantity being removed by the user as string.
      </td>
    </tr>

    <tr>
      <td>
        url
      </td>

      <td>
        string
      </td>

      <td>
        Url of the page where product is removed from cart.
      </td>
    </tr>

    <tr>
      <td>
        visit\_type
      </td>

      <td>
        string
      </td>

      <td>
        Can be either “first\_time” or “repeat”
      </td>
    </tr>

    <tr>
      <td>
        UnbxdKey
      </td>

      <td>
        string
      </td>

      <td>
        UnbxdSitekey value
      </td>
    </tr>

    <tr>
      <td>
        uid
      </td>

      <td>
        string
      </td>

      <td>
        Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers
      </td>
    </tr>

    <tr>
      <td>
        time
      </td>

      <td>

      </td>

      <td>
        This timestamp parameter should be according to the formula shared below t : current\_time | random number between 0 to 1
        t = new Date().getTime() + ‘
      </td>
    </tr>

    <tr>
      <td>
        variantId
      </td>

      <td>
        string
      </td>

      <td>
        VariantId of the variant-product. It is necessary only if variants are present. (optional)
      </td>
    </tr>

    <tr>
      <td>
        referrer
      </td>

      <td>
        string
      </td>

      <td>
        Link from where the page is opened (Optional)
      </td>
    </tr>
  </tbody>
</Table>

## Orders

The Orders event is pushed for every product that is purchased on your site.

Here’s how an Order API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueId-of-the-product}}","qty":"{{quantity-selected}}","price":"{{unit-price-for-product}}","url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","requestId":"{{unx-request-id}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=order&uid={{uid}}1658904085468-92302&t=1662367087116|0.07798836811209986
```

Payload Details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                                                 |
| ------------------ | ------------ | --------------------------------------------------------------------------------------------------------------------------- |
| action             | string       | Indicates the type of event. In this case, the value will be ‘order’                                                        |
| query              | string       | The search query entered by user                                                                                            |
| pid                | string       | Unique id for the product, to be taken from API response, if relevantDocumentType=”parent”, In search api response, or null |
| price              | string       | Unit price of the product (variant, if variant is selected)                                                                 |
| url                | string       | Url of the order success page where the API for order event is fired                                                        |
| requestId          | string       | To be extracted from Unbxd search api response headers, from unx-request-id                                                 |
| visit\_type        | string       | Can be either “first\_time” or “repeat”                                                                                     |
| UnbxdKey           | string       | UnbxdSitekey value                                                                                                          |
| uid                | string       | Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers                          |
| referrer           | string       | Link from where the page is opened (Optional)                                                                               |

## Facets

A Facet event tracks the guided navigation on the Product Listing Page. The event query will list the specific filters the shopper has selected to narrow down the results on the search results page.

Here is how the API call will look like when facets are clicked on search page:

```
http://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{search-query}}","facets":{“facet-name”:[value],},"url":"{{url-of-the-website}}","referrer":"","requestId":"{{unx-request-id}}","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}5&t=1662365253141|0.6835012308821242
```

> 📘 Note
>
> Action for this event will be “search”, as in the API above and does not need to be changed.

<Table>
  <thead>
    <tr>
      <th>
        **Attribute Name**
      </th>

      <th>
        **Datatype**
      </th>

      <th>
        **What value to be passed**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        action
      </td>

      <td>
        string
      </td>

      <td>
        Indicates the type of event. In this case, the value will be ‘search’
      </td>
    </tr>

    <tr>
      <td>
        query
      </td>

      <td>
        string
      </td>

      <td>
        The search query entered by user
      </td>
    </tr>

    <tr>
      <td>
        facets
      </td>

      <td>
        string
      </td>

      <td>
        Will contain the key value pair of `:<value>`. For eg: “facets”:\{“flavour\_uFilter”:\[“Orange”,”Cola”],”goal\_categoryPath\_uFilter”:\[“Daily Wellness”]}
      </td>
    </tr>

    <tr>
      <td>
        pid
      </td>

      <td>
        string
      </td>

      <td>
        Unique id for the product, to be taken from API response, if relevantDocumentType=”parent”, In search api response, or null
      </td>
    </tr>

    <tr>
      <td>
        url
      </td>

      <td>
        string
      </td>

      <td>
        Website url where search is performed
      </td>
    </tr>

    <tr>
      <td>
        requestId
      </td>

      <td>
        string
      </td>

      <td>
        To be extracted from Unbxd search api response headers, from unx-request-id
      </td>
    </tr>

    <tr>
      <td>
        visit\_type
      </td>

      <td>
        string
      </td>

      <td>
        Can be either “first\_time” or “repeat”
      </td>
    </tr>

    <tr>
      <td>
        UnbxdKey
      </td>

      <td>
        string
      </td>

      <td>
        UnbxdSitekey value
      </td>
    </tr>

    <tr>
      <td>
        uid
      </td>

      <td>
        string
      </td>

      <td>
        Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers.
      </td>
    </tr>

    <tr>
      <td>
        time
      </td>

      <td>

      </td>

      <td>
        This timestamp parameter should be according to the formula shared below
        t : current\_time | random number between 0 to 1
        t = new Date().getTime() + ‘
      </td>
    </tr>

    <tr>
      <td>
        referrer
      </td>

      <td>
        string
      </td>

      <td>
        Link from where the page is opened (Optional)
      </td>
    </tr>
  </tbody>
</Table>

## Autosuggest

If the autocomplete feature on store is powered by Unbxd, then events originating from Unbxd Autosuggest Widget should pass additional metadata. This enables us to improve autocomplete suggestions over time. It is also used to generate reports on how well different types of suggestions are doing.

Events from Autosuggest

In this section we will give examples of events which may originate from the user’s interaction with Autosuggest widget and hence should send suggestion related metadata with payload. This will cover Javascript based approach for integrating the events.

Search

Whenever a user selects any suggestion from Autosuggest widget and hits the form submit, this event should be tracked. It should also send additional information about the suggestion using autosuggestParams field in the payload.

For instance in case of infield suggestion like below:

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/71f91c1a21c86a90234f1508f51ff08a33c402655969eb0d52c53019c497879c-image.png" />

On submitting the form (irrespective of mouse or keyboard) any of the options (including popular products) from the autocomplete box should trigger a search event which should provide autosuggest related metadata. The image beacon looks like this when selecting the “Batman” option from the suggestion list.

<br />

The Unbxd.track API call will look like this:

1. In case, it is an IN\_FIELD suggestion which is selected and submitted:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{suggested-query}}","autosuggest_data":{"autosuggest_type":"IN_FIELD","autosuggest_suggestion":"{{suggested-query}}","field_value":null,"field_name":null,"src_field":null,"pid":null,"internal_query":"{{original-query}}"},"url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}&t=1666830840426|0.12139712486982823
```

Payload Details:

| **Attribute Name**      | **Datatype** | **What value to be passed**                                                                                                               |
| ----------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| autosuggest\_type       | string       | IN\_FIELD autosuggest type is selected and submitted for search, usually the same as the value of doctype field in Unbxd autosuggest API. |
| autosuggest\_suggestion | string       | Suggested query in infield.                                                                                                               |
| field\_name             | string       | The name of the field which is used for IN\_FIELD suggestion.                                                                             |
| field\_value            | string       | The value of the field, which is the suggestion                                                                                           |
| internal\_query         | string       | The typed query in searchbox, which led to the suggestions in autosuggest                                                                 |
| query                   | string       | Suggested query in Infield.                                                                                                               |
| url                     | string       | Website url where search is performed                                                                                                     |
| requestId               | string       | To be extracted from Unbxd search api response headers, from unx-request-id                                                               |
| visit\_type             | string       | Can be either “first\_time” or “repeat”                                                                                                   |
| UnbxdKey                | string       | UnbxdSitekey value                                                                                                                        |
| uid                     | string       | Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers                                        |
| referrer                | string       | Link from where the page is opened (Optional)                                                                                             |

2. In case, it is POPULAR\_PRODUCTS suggestion which is selected and submitted:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{suggested-query}}","autosuggest_data":{"autosuggest_type":"POPULAR_PRODUCTS","autosuggest_suggestion":"{{suggested-query}}","field_value":null,"field_name":null,"src_field":null,"pid":"{{uniqueId-of-the-product}}","unbxdprank":"{{rank-of-product}}","internal_query":"{{original-query}}"},"url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}&t=1666851030913|0.2127782620243308
```

Payload Details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                                                      |
| ------------------ | ------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| autosuggest\_type  | string       | POPULAR\_PRODUCTS depending on the type of suggestion, usually the same as the value of doctype field in Unbxd autosuggest API.. |
| pid                | string       | UniqueId of the selected product.                                                                                                |
| unbxdprank         | string       | In case of POPULAR\_PRODUCTS suggestions, the rank of the product.                                                               |
| internal\_query    | string       | The typed query in searchbox, which led to the suggestions in autosuggest                                                        |
| query              | string       | Suggested query in keyword or infield, can be null if POPULAR\_PRODUCTS is selected.                                             |
| url                | string       | Website url where search is performed                                                                                            |
| pid                | string       | Unique id of the product viewed.                                                                                                 |
| requestId          | string       | To be extracted from Unbxd search api response headers, from unx-request-id                                                      |
| visit\_type        | string       | Can be either “first\_time” or “repeat”                                                                                          |
| UnbxdKey           | string       | UnbxdSitekey value                                                                                                               |
| uid                | string       | Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers                               |
| referrer           | string       | Link from where the page is opened (Optional)                                                                                    |

3. In case, it is an KEYWORD\_SUGGESTIONS which is selected and submitted:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{suggested-query}}","autosuggest_data":{"autosuggest_type":"KEYWORD_SUGGESTION","autosuggest_suggestion":"{{suggested-query}}","field_value":null,"field_name":null,"src_field":null,"pid":null,"unbxdprank":"{{rank-of-product}}","internal_query":"{{original-query}}"},"url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}&t=1666830840426|0.12139712486982823
```

Payload Details:

| **Attribute Name**      | **Datatype** | **What value to be passed**                                                                                                                         |
| ----------------------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| autosuggest\_type       | string       | KEYWORD\_SUGGESTION autosuggest type is selected and submitted for search, usually the same as the value of doctype field in Unbxd autosuggest API. |
| autosuggest\_suggestion | string       | Suggested query in infield.                                                                                                                         |
| field\_name             | string       | The name of the field which is used for KEYWORD\_SUGGESTION.                                                                                        |
| field\_value            | string       | The value of the field, which is the suggestion                                                                                                     |
| internal\_query         | string       | The typed query in searchbox, which led to the suggestions in autosuggest                                                                           |
| query                   | string       | Suggested query in Infield.                                                                                                                         |
| url                     | string       | Website url where search is performed                                                                                                               |
| requestId               | string       | To be extracted from Unbxd search api response headers, from unx-request-id                                                                         |
| visit\_type             | string       | Can be either “first\_time” or “repeat”                                                                                                             |
| UnbxdKey                | string       | UnbxdSitekey value                                                                                                                                  |
| uid                     | string       | Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers                                                  |
| referrer                | string       | Link from where the page is opened (Optional)                                                                                                       |

## Click

This event should be tracked (along with search) whenever any popular product option is clicked on the autocomplete box.

The Unbxd.track API call will look like this and will be based on the selection type:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{suggested-query}}","autosuggest_data":{"autosuggest_type":"{{autosuggest-type}}","autosuggest_suggestion":"{{suggested-query}}","field_value":null,"field_name":{{suggestion-field-name}},"src_field":{{src-field}},"pid":"{{uniqueId-of-the-product}}","unbxdprank":"{{rank-of-product}}","internal_query":"{{original-query}}"},"url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=click&uid={{uid}}&t=1666851030913|0.2127782620243308
```

Payload Details:

| **Attribute Name**      | **Datatype** | **What value to be passed**                                                                                              |
| ----------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------ |
| autosuggest\_type       | string       | POPULAR\_PRODUCT depending on the type of suggestion which is selected and submitted for search.                         |
| autosuggest\_suggestion | string       | Suggested query in keyword or infield, can be null if POPULAR PRODUCT is selected.                                       |
| field\_name             | string       | In case of IN\_FIELD suggestions, the name of the field which is used for suggestion, null in popular product selection. |
| field\_value            | string       | In case of IN\_FIELD suggestions, the value of the field, which is the suggestion, null in popular products.             |
| pid                     | string       | In case of popular product getting selected, we need to pass uniqueId of the selected product.                           |
| unbxdprank              | string       | In case of POPULAR\_PRODUCT suggestions, the rank (1 based index) of the product.                                        |
| internal\_query         | string       | The typed query in searchbox, which led to the suggestions in autosuggest                                                |
| query                   | string       | Suggested query in keyword or infield, can be null if POPULAR PRODUCT is selected.                                       |
| url                     | string       | Website url where search is performed                                                                                    |
| pid                     | string       | Unique id of the product viewed.                                                                                         |
| requestId               | string       | To be extracted from Unbxd search api response headers, from unx-request-id                                              |
| visit\_type             | string       | Can be either “first\_time” or “repeat”                                                                                  |
| UnbxdKey                | string       | UnbxdSitekey value                                                                                                       |
| uid                     | string       | Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers                       |
| referrer                | string       | Link from where the page is opened (Optional)                                                                            |

## Add to Cart

This event should be tracked whenever any product is added to cart directly from the autocomplete box.

The Unbxd.track call will look like below:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueId-of-the-product}}","qty":”{{no-of-units}}","variantId":"{{variantId-of-the-variant}}",”price”:”{{price-of-the-product}}”,"autosuggest_data":{"autosuggest_type":"POPULAR_PRODUCTS","autosuggest_suggestion":"{{suggested-query}}""field_name":{{fiel-name}},"field_value":{{field-value}},"src_field":null,"pid":"{{uniqueId-of-the-product}}","unbxdprank":null,"internal_query":null}",url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first-or-repeat}}","requestId":"{{request-id}}"&UnbxdKey=”{{unbxd-sitekey}}&action=cart&uid={{uid}}&t={{time-spent}}
```

Payload Details:

| **Attribute Name**      | **Datatype** | **What value to be passed**                                                                                                                                       |
| ----------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| autosuggest\_type       | string       | Can be either IN\_FIELD, KEYWORD\_SUGGESTION or POPULAR\_PRODUCT depending on the type of suggestion which is selected and submitted for search.                  |
| autosuggest\_suggestion | string       | Suggested query in keyword or infield, can be null if POPULAR PRODUCT is selected.                                                                                |
| field\_name             | string       | In case of IN\_FIELD suggestions, the name of the field which is used for suggestion, null in popular product selection.                                          |
| field\_value            | string       | In case of IN\_FIELD suggestions, the value of the field, which is the suggestion, null in popular products.                                                      |
| pid                     | string       | Here, it is null since it is not the POPULAR PRODUCT SUGGESTION. (In case of popular product getting selected, we need to pass uniqueId of the selected product.) |
| unbxdprank              | string       | Here, it will be null. In case of POPULAR\_PRODUCT suggestions, the rank (1 based index) of the product.                                                          |
| internal\_query         | string       | The typed query in searchbox, which led to the suggestions in autosuggest                                                                                         |
| query                   | string       | Suggested query in keyword or infield, can be null if POPULAR PRODUCT is selected.                                                                                |
| url                     | string       | Website url where search is performed                                                                                                                             |
| pid                     | string       | Unique id of the product viewed.                                                                                                                                  |
| requestId               | string       | To be extracted from Unbxd search api response headers, from unx-request-id                                                                                       |
| visit\_type             | string       | Can be either “first\_time” or “repeat”                                                                                                                           |
| UnbxdKey                | string       | UnbxdSitekey value                                                                                                                                                |
| uid                     | string       | Need to be extracted from cookie, unbxd.userId. This is the unique identifying number for shoppers                                                                |
| referrer                | string       | Link from where the page is opened (Optional)                                                                                                                     |