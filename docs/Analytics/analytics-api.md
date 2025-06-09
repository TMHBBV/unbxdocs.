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