---
title: Merchandising Features
excerpt: 'Managing Search involves settings to configure your site and search. '
deprecated: false
hidden: false
metadata:
  robots: index
---
The Unbxd Site Search solution provides an advanced search engine designed to enhance the eCommerce user experience. It offers a variety of features aimed at improving product discovery, eliminating irrelevant results, and personalizing search outcomes to meet the shopper's needs. This documentation outlines the key features of the **Unbxd search engine**, including merchandising, system capabilities, and relevancy features.

## 1. Merchandising Features

Merchandising features in Unbxd’s site search solution are designed to enhance the shopper experience by effectively displaying and organizing products. These features focus on improving the search results, making them more relevant and user-friendly, which ultimately drives better engagement and conversion rates. Below are the key merchandising features:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Feature
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Facets**
      </td>

      <td>
        Facets help shoppers refine their search results by narrowing down the product options based on specific attributes. When a shopper searches for a product, facets allow them to filter results according to categories like brand, size, color, etc. Facets improve the user experience by making it easier for shoppers to find their desired product. For instance:

        * For a cosmetic query, facets may include brands, color, and ratings.
        * For a dress search, facets may include size, color, type, and brand.
      </td>
    </tr>

    <tr>
      <td>
        **Variants**
      </td>

      <td>
        Variants define different attributes of the same product, such as color or size. For example, a product like a dress can have multiple color variants but share the same product ID. Shoppers can see the different variations available (e.g., different colors of a dress) while keeping the product ID the same. When a shopper hovers over the product, they can select their preferred variant (e.g., color) and add it directly to the cart.
      </td>
    </tr>

    <tr>
      <td>
        **Multi-Value**
      </td>

      <td>
        Multi-value refers to when a product has multiple images, such as different angles of the same product. For example, a shopper searching for a MacBook can view different images of the product (e.g., front, side, and back view) for a clearer understanding before making a purchase decision.
      </td>
    </tr>

    <tr>
      <td>
        **Typo Tolerance**
      </td>

      <td>
        Typo tolerance, including features like 'Did you mean', ensures that shoppers still find relevant results even if they make spelling mistakes. Instead of showing a 'No Results Found' message, the system displays alternative spelling suggestions along with 2-3 product suggestions that are close to the original query. This feature uses context-aware algorithms to offer more accurate and relevant search results based on frequent misspelled queries.
      </td>
    </tr>

    <tr>
      <td>
        **Synonyms**
      </td>

      <td>
        Synonyms help shoppers find products even when they use different words to describe the same item. For example, ‘flip-flops’ is considered a synonym for ‘slippers’, and ‘pants’ for ‘trousers’. Synonyms also account for geolocation to better understand regional language differences. This prevents zero results for common queries and improves the overall search experience.
      </td>
    </tr>

    <tr>
      <td>
        **Bucketing**
      </td>

      <td>
        Bucketing allows grouping products with common attributes into buckets. This feature helps display the most relevant products in a specific group. Buckets allow for better organization of search results, making it easier for shoppers to find related products based on certain criteria. Each bucket must also be defined as a facet field in your store
      </td>
    </tr>

    <tr>
      <td>
        **Pagination**
      </td>

      <td>
        Pagination splits search results across multiple pages, allowing for more manageable viewing. The following parameters help control pagination:

        * **start**: Offsets the results by a specified number.
        * **rows**: Defines the number of products displayed per page.
      </td>
    </tr>

    <tr>
      <td>
        **Sorting**
      </td>

      <td>
        Sorting allows products to be organized based on specific fields, either in ascending or descending order. For example, products can be sorted by price, popularity, or newest arrivals, helping shoppers find products according to their preferences.
      </td>
    </tr>

    <tr>
      <td>
        **Banners / Redirects**
      </td>

      <td>
        Event-driven banners or redirects allow you to display promotional images on your site during special events, like a sale or holiday season. These banners can be linked to specific product categories, attracting shoppers to a targeted set of products based on the event.
      </td>
    </tr>
  </tbody>
</Table>

<br />

## 2. Console / Site Features

The Console / Site Features are designed to provide comprehensive monitoring, multi-language support, and other functionalities that enhance your site's performance and user experience. Below are the key features:

1. **System Health / Monitoring Dashboard**

The Monitoring Dashboard provides detailed reports and insights into the status of the uploaded catalog and API integration. It helps ensure that all the functionalities are working correctly and allows for proactive troubleshooting. Key Features includes:

* Real-Time Monitoring: You can track the performance of the catalog and APIs to ensure everything is running smoothly.
* Error Indicators: If certain functionalities are not integrated correctly, such as the Auto Suggest feature, the relevant section will appear grayed out with no statistics displayed, signaling that action is required.

This feature helps keep track of integrations and provides transparency on the system’s health.

2. **Multi-Language Support**

Unbxd now supports multi-language capabilities, allowing shoppers to search in a variety of languages. This feature ensures that language barriers do not hinder shoppers from finding the products they are looking for. Currently we support the below languages:

* French
* Spanish
* German
* Bahasa
* Italian
* Swedish
* Portuguese
* Dutch
* Danish
* Polish

> 📘 Note
>
> Shoppers can conduct searches in any of these languages, and Unbxd will handle the search functionality in the background, ensuring accurate and relevant results. This multi-language feature helps create a global eCommerce experience for customers across different regions.

## 3. Features

The Enhanced Relevancy Features in Unbxd’s search solution are focused on delivering the most relevant product results based on shopper behavior, product interactions, and personalized experiences. These features ensure that the search results not only meet the shopper’s expectations but also improve overall engagement, conversion rates, and inventory management. The key components of these enhanced relevancy features include:

1. **Algorithmic Ranking**\
   Unbxd’s ranking algorithms use shopper behavior data to optimize product rankings in search results. The system automatically adjusts rankings based on product traction, conversion rates, and overall shopper interactions. This ensures that products receiving higher engagement are ranked higher, improving the conversion rate and ensuring relevancy.
2. **Personalization**\
   Personalization involves tailoring the product suggestions based on the individual shopper's behavior. By tracking shoppers’ past interactions, preferences, and browsing habits, Unbxd uses AI-driven models to recommend products that best match each shopper’s interests and previous activity on the site.
3. **Stock Keeping Unit Search (SKU Search)**\
   The SKU search feature enables you to search products using their unique stock-keeping unit (SKU) to help manage inventory and monitor stock levels. This feature is particularly useful for quickly locating a product within your catalog based on its SKU.

## What can I do with Merchandising Workbench?

It allows you to optimize product visibility by promoting or demoting products in the search results, aligning them with business goals or seasonal campaigns. You can

1. **Promote or Hide Products**\
   Easily prioritize specific products or remove less relevant items from search results based on keywords or customer preferences. By controlling product visibility, you guide shoppers toward the best-fit items.  Promote items relevant to the current season, like **winter coats** for the winter months or **beachwear** in summer.
   Prioritize visibility for newly launched products, ensuring they appear prominently in search results to drive awareness and engagement or temporarily hide products that are low on stock or in clearance to maintain shopper expectations around availability.
2. **Pin Products to Specific Positions**\
   Pin selected products to designated spots in the search results of any query to ensure shoppers see the items you want to highlight. This helps increase visibility for new arrivals, high-margin items, or promotional products. Pin high-profit products to prominent positions, increasing visibility for items with the best business interest.
   Feature highly rated or reviewed products at the top of relevant search results to guide shoppers toward quality choices.​
3. **Run Campaigns with Banners and Landing Pages**\
   Elevate your marketing initiatives by displaying banners for sales, events, or seasonal promotions. Promote holiday sales with special offers. Showcase banners for a new collection launch or create dedicated landing pages specific to a query for an engaging and cohesive shopping experience. You can showcase all discounted products together. Curate a **Shopper Favorites** page that includes top-rated and best-selling items
4. **Showcase Handpicked Product Collections**\
   Create curated collections that cater to specific shopper interests, such as **Top Picks for Summer** or **Gifts for Her**, providing an easy way to navigate high-interest items. You can also create collections like **Eco-Friendly Essential**s or **Tech for Travelers** to help shoppers quickly find curated items for specific themes. or create collections around special occasions like **Mother’s Day Gifts** to guide shoppers toward popular gift ideas.
5. **Instantly separate products that match set conditions**\
   Automatically filter and organize products based on specific criteria such as pricing, stock levels, or shopper preferences allowing for quick, dynamic adjustments in merchandising. Create price-sensitive campaigns by quickly filtering products based on the price attribute. You can instantly filter all products based on color to run Christmas or St. Patrick’s Day campaigns.
6. **Customize Facets for High-Conversion Filters**\
   Present high-impact filters to narrow search results and match shopper intent, such as **eco-friendly** or **popular brands**, enabling quick discovery of relevant products. Feature filters for popular brands to make it easy for brand-loyal shoppers to navigate directly to their preferred options.
7. **Redirect Shoppers to Targeted URLs**\
   Guide users to relevant pages when they search for popular categories or keywords. For example, redirecting customer support queries to the help page ensures a smoother user experience. Creating redirect searches like **new releases** to a dedicated page that showcases the latest product drops or for out-of-stock popular items, redirect users to a similar collection page or **back-in-stock** alert page.
8. **Merchandise Query Autosuggest**\
   Promote a specific suggestion/typeahead option and increase active campaign visibility.​
9. **Segment Shoppers and A/B Test Ideas**\
   Leverage segmentation to personalize the shopping experience based on user behaviors or preferences. Learn
   Use A/B testing to measure the impact of merchandising adjustments on conversions.​
10. **Analyze Product and Campaign-Wise Shopper Behavior**\
    Get in-depth insights into how your shoppers engage with specific products, campaigns, or queries.

* Track metrics like clicks and conversions to understand which campaigns (e.g., flash sales) perform best and refine future strategies accordingly.
* Analyze engagement metrics for individual products to identify best-sellers and promote them for higher visibility.
* Monitor shopper behavior patterns on category pages, identify popular items, and adjust merchandising strategies to cater to demand.

## Use Case

Netcore Unbxd Workbench supports using multiple merchandising rules, enabling retailers to create a cohesive shopping experience. For a search query **back-to-school** campaign, using workbench, you can

1. Segment shoppers.
2. Run a banner to advertise the campaign on the home page, category pages, and search query listing pages.
3. Create a landing page by applying filters for stationery, lunch bags, or water bottles.
4. Redirect users to the landing page dedicated to back-to-school products and deals.
5. Boost new arrivals and highly rated items unique to each segment and bury products with lower ratings.Pin
6. items from popular brands in positions 1 to 10 on the search result page.
7. Analyze the campaign’s performance and the shoppers’ journeys.