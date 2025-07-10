---
title: 'Integrate Netcore Unbxd Analytics '
excerpt: V2 Analytics Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
The following sections explain how Netcore Unbxd Analytics works and how to integrate it with your website. This document is intended exclusively for customers who have integrated with our V2 integration method. For details on versions of integrations, please refer to [this documentation](doc:introduction-analytics).

<Accordion title="Upgrade Notice: Transition to New SDKs Underway" icon="fa-info-circle">
  As part of our ongoing upgrade process, we are gradually transitioning all customers to the new and improved SDKs. Please note that we will eventually deprecate support for the older SDK versions. To ensure you have access to the latest features and enhancements, we strongly encourage you to plan your migration to the upgraded SDK.
</Accordion>

## Why is it essential to set up Netcore Unbxd Analytics?

Analytics is crucial for maximizing the effectiveness of the **Netcore Unbxd** platform. By integrating Analytics, you add unique tracking codes to your store properties, which trigger interactions known as “events.” These events include actions like search queries, product clicks, impressions, cart additions, and orders, all of which are tracked for each visitor through browser cookies. This event data enables our AI/ML models to gain valuable insights and build detailed visitor profiles, highlighting their preferences for specific categories, brands, and prices.

These profiles are vital for:

* delivering personalized search results
* enhancing recommendation algorithms for better product discovery
* generating comprehensve reports

In summary, integrating Netcore Unbxd Analytics is crucial to achieving your conversion goals through precise personalization. Incomplete or broken analytics integration during or after onboarding leads to a diminished search experience, reduced relevance, and less effective personalized AI capabilities.

## What are the types of events tracked?

The trackers will capture your users’ behavior as they navigate and interact with your online touchpoints.

<Accordion title="Global Events" icon="fa-info-circle">
  These are standard interactions tracked across your entire site, such as Visitor, Page views, Product clicks, Product Cart, and Product Order.
</Accordion>

<Accordion title="Feature-specific Events" icon="fa-info-circle">
  These track user interactions with specific features of your platform, such as Search, Product Impressions, Autosuggest, Category Pages, Browse Impressions, and Recommendations
</Accordion>

## What are the events we track?

<Tabs>
  <Tab title="Visitor Event">
    The first event created when a shopper visits your site. It tracks and builds profiles using browser           cookies for two types of visitors: first-time users and repeat users.
    Site-level information are stored as cookies and are titled as,

    1. User ID: `unbxd.userId`
    2. Visit ID: `unbxd.visitId`
    3. Viit Type: `unbxd.visit`
  </Tab>

  <Tab title="Search Hit">
    Triggered when a shopper uses the search bar to find a product on your site or selects one of the             suggestions provided by Netcore Unbxd’s Autosuggest widget.

    It captures every query the shopper searches, even if no results are returned, providing insights into         search effectiveness.
  </Tab>

  <Tab title="Product Click">
    Triggered whenever a shopper clicks a product or product image from any Product Listing Page (PLP),           Category page, or Recommendation widget. It will capture the clicked product’s unique ID and the page         where the click activity occurred.

    This data can be used to highlight ‘Popular Products’ and create personalized ‘Recommended For You’ lists,     ensuring a more customized shopping experience.
  </Tab>

  <Tab title="Add to Cart">
    Triggered each time a user adds a product to their cart, regardless of the originating page—whether it’s the   Product Detail Page (PDP), Product Listing Page (PLP), historical orders, or any other page. For users         incrementally adding products, the event should fire once per product addition, and the `qty` parameter       should reflect the quantity added during that specific action.
  </Tab>

  <Tab title="Order">
    Triggered when a purchase is completed on your site. This event should be fired for each product in the       order, capturing valuable data such as the product ID, quantity, and order details.
  </Tab>
</Tabs>