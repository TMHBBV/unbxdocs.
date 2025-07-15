---
title: V2 Analytics Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
The following sections explain how Netcore Unbxd Analytics works and how to integrate it with your website. This document is **intended exclusively for customers who have integrated with our V2 integration method**. For details on versions of integrations, please refer to [ this documentation ](https://netcoreunbxd.com/docs/site-search/integration-documentation/introduction-analytics/) .

As part of our ongoing upgrade process, we are gradually transitioning all customers to the new and improved SDKs. Please note that we will eventually deprecate support for the older SDK versions. To ensure you have access to the latest features and enhancements, we strongly encourage you to plan your migration to the upgraded SDK.

<br />

## Why is it essential to set up Netcore Unbxd Analytics?

<br />

Analytics is crucial for maximizing the effectiveness of the Netcore Unbxd platform. By integrating Analytics, you add unique tracking codes to your store properties, which trigger interactions known as “events.” These events include actions like search queries, product clicks, impressions, cart additions, and orders, all of which are tracked for each visitor through browser cookies.\
This event data enables our AI/ML models to gain valuable insights and build detailed visitor profiles, highlighting their preferences for specific categories, brands, and prices.

<br />

These profiles are vital for:

* delivering personalized search results
  * enhancing recommendation algorithms for better product discovery
    * generating comprehensive reports
      <br />
      In summary, integrating Netcore Unbxd Analytics is crucial to achieving your conversion goals through precise personalization. Incomplete or broken analytics integration during or after onboarding leads to a diminished search experience, reduced relevance, and less effective personalized AI capabilities.
      <br />

## What are the types of events tracked?

<br />

The trackers will capture your users' behavior as they navigate and interact with your online touchpoints.

\<AccordionGroup>
&#x20; \<Accordion title="Global Events">
&#x20;   \<p>
&#x20;   These are standard interactions tracked across your entire site, such as Visitor, Page views, Product clicks, Product Cart, and Product Order.\</p>
&#x20; \</Accordion>
&#x20; \{" "}

&#x20; \<Accordion title="Feature-specific Events">
&#x20;   \<p>
&#x20;   These track user interactions with specific features of your platform, such as Search, Product Impressions, Autosuggest, Category Pages, Browse Impressions, and Recommendations.

&#x20;   \</p>
&#x20; \</Accordion>
&#x20; \{" "}
\</AccordionGroup>



<br />

## What are the events we track?

<br />

\<Tabs>
&#x20; \<Tab title="Visitor Event">
&#x20;   \<p>
&#x20;   The first event created when a shopper visits your site. It tracks and builds profiles using browser cookies for two types of visitors: first-time users and repeat users.\</p>

&#x20;   \<p>
&#x20;   Site-level information are stored as cookies and are titled as, \</p>

&#x20;   \<ul>
&#x20;   \<li>
&#x20;   User ID: \<code>
&#x20;   unbxd.userId\</code>

&#x20;   \</li>

&#x20;  &#x20;
&#x20;   \<li>
&#x20;   Visit ID: \<code>
&#x20;   unbxd.visitId\</code>

&#x20;   \</li>

&#x20;  &#x20;
&#x20;   \<li>
&#x20;   Visit Type: \<code>
&#x20;   unbxd.visit\</code>

&#x20;   \</li>

&#x20;   \</ul>
&#x20; \</Tab>
&#x20; \<Tab title="Search Hit">
&#x20;   \<p>
&#x20;   Triggered when a shopper uses the search bar to find a product on your site or selects one of the suggestions provided by Netcore Unbxd's Autosuggest widget.

&#x20;   It captures every query the shopper searches, even if no results are returned, providing insights into search effectiveness.

&#x20;   \</p>
&#x20; \</Tab>
&#x20; \<Tab title="Product Click">
&#x20;   \<p>
&#x20;   Triggered whenever a shopper clicks a product or product image from any Product Listing Page (PLP), Category page, or Recommendation widget. It will capture the clicked product’s unique ID and the page where the click activity occurred.

&#x20;   This data can be used to highlight ‘Popular Products’ and create personalized ‘Recommended For You’ lists, ensuring a more customized shopping experience.

&#x20;   \</p>
&#x20; \</Tab>
&#x20; \<Tab title="Add to Cart">
&#x20;   \<p>
&#x20;   Triggered each time a user adds a product to their cart, regardless of the originating page—whether it’s the Product Detail Page (PDP), Product Listing Page (PLP), historical orders, or any other page.
&#x20;   For users incrementally adding products, the event should fire once per product addition, and the \<code>
&#x20;   qty\</code>

&#x20;    parameter should reflect the quantity added during that specific action.

&#x20;   \</p>
&#x20; \</Tab>
&#x20; \<Tab title="Order">
&#x20;   \<p>
&#x20;    Triggered when a purchase is completed on your site. This event should be fired for each product in the order, capturing valuable data such as the product ID, quantity, and order details.\</p>
&#x20; \</Tab>
\</Tabs>