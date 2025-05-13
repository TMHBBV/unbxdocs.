---
title: 'Search: Merchandising Features'
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