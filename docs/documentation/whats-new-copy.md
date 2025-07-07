---
title: What's New (COPY)
deprecated: false
hidden: false
metadata:
  robots: index
---
Netcore Unbxd continuously evolves to help you deliver more intelligent, personalized shopping experiences. In this section, you'll find the latest feature rollouts, performance enhancements, and platform updates designed to optimize product discovery, boost conversions, and elevate the customer journey.

# July 2025

1. **Elevate Your Search Game with Index Time Synonyms**

We’re thrilled to announce the Index Time Synonym feature, designed to supercharge your search experience! By adding synonym keywords to the search index during feed ingestion or re-indexing, this feature ensures that users find relevant products, even when using different terms in their queries. With this enhancement, searching has never been more intuitive and seamless! Read [here](https://unbxdocs.readme.io/docs/synonyms#/index-time-synonyms) to know more.

2. **Spellcheck Override**

We’re excited to introduce the Spellcheck Override feature, empowering you to control search suggestions more precisely! With this new functionality, you can easily override specific keywords to prevent the system from suggesting similar queries. This ensures users are directed exactly where they want to go, without confusing or displaying irrelevant alternatives. Refer to the [documentation](https://unbxdocs.readme.io/docs/spellcheck#/spellcheck-override) here.

3. **Attribute Enrichment: Supercharge Your Product Data for Better Search Results!**

We are thrilled to roll out Attribute Enrichment, a powerful feature designed to enhance your product data by adding valuable attributes during the indexing process. This improves product visibility and search relevance, helping users find the most relevant products faster and more accurately.

Attribute Enrichment enriches your product data by automatically adding relevant attributes based on predefined criteria, making your product catalog smarter and more insightful. Refer to the [documentation](https://unbxdocs.readme.io/docs/attribute-enrichment#/) to know more.

4. **Two-Factor Authentication (2FA) – Boost Your Security with an Extra Layer of Protection!**

We’re excited to introduce Two-Factor Authentication (2FA), a new security feature that adds an extra layer of protection to your Netcore Unbxd account. With 2FA enabled, users will need to verify their identity through a second authentication step, significantly enhancing account security and protecting sensitive data.

5. **Enhanced Filter & Boost Conditions**

We’re excited to introduce a new enhancement to your filter and boost conditions! You can now use >= (greater than or equal to) and \<= (less than or equal to) operators in your filter or boost conditions, providing you with even more flexibility and precision when refining search results. Refer [here](https://unbxdocs.readme.io/docs/ui-terminologies#/) to know more.

6. **Let AI Optimize Your User Experience using AI Suggested Redirects !**

We’re excited to launch AI Suggested Redirects, a feature that leverages the power of artificial intelligence to automatically recommend redirects for search queries. This ensures that users are directed to the most relevant pages, even when they type in incorrect or ambiguous search terms. Read the [documentation](https://unbxdocs.readme.io/docs/redirects#/set-up-ai-suggested-redirects) to know more.

# April 2025

OWASP Compliance for Search/Browse Console

We’re pleased to announce that the Unbxd Search and Browse Console is now fully compliant with the OWASP (Open Web Application Security Project) Top 10 standards.

This enhancement reflects our ongoing commitment to protecting customer data and improving the security of our platform.

No action is required from customers. These improvements have been implemented at the platform level and are automatically applied.

## V 1.22 : Release date: April

1. **Vector Search for Smarter Product Discovery**

We are excited to announce the release of Vector Search, a powerful AI-enabled feature designed to make product discovery more intuitive and accurate for shoppers on your eCommerce platform.

Unlike traditional keyword-based search, Vector Search understands the intent behind a user’s query and delivers results that match the meaning, not just the exact words.

Vector Search: Uses machine learning to understand semantic relationships between user queries and product data.

Hybrid Search Mode: Combines keyword-based results with semantically relevant results to enhance result quality.

Fallback Search Mode: Automatically activates Vector Search when traditional search shows limited or no results.

For more information, refer to Vector Search documentation

2. **Measurement Search**

Measurement Search is a new AI-powered search enhancement in the Unbxd platform that allows shoppers to find products based on specific, measurable dimensions such as size, weight, price, or pressure.

This feature supports more precise and intuitive search experiences for end users, especially for dimension-driven product categories like fashion, furniture, appliances, and hardware.

For more information, refer to Measurement Search documentation

3. **Website Preview for Enhanced Debugging Capabilities**

Website Preview is a powerful enhancement to the Unbxd Search platform that automatically enriches your product catalog by extracting key product attributes (such as color, material, fit, and style) using Artificial Intelligence.

Even if these attributes aren’t manually added to your catalog, the preview functionality can derive them from product titles, descriptions, and other content, ensuring your products appear accurately in search results and filters.

This works in synergy with the following Unbxd AI Models:

| **Model**          | **Function**                                                                                               |
| ------------------ | ---------------------------------------------------------------------------------------------------------- |
| **Content Model**  | Analyzes catalog data to structure and enrich it using attributes like title, color, size, brand, etc.     |
| **Intent Model**   | Understands the shopper’s true intent, even in natural language queries like “ergonomic chair under $200”. |
| **Ranking Model**  | Scores products based on relevance, user engagement, and availability to determine result order.           |
| **Fallback Model** | Uses semantic understanding to return related results when exact matches are unavailable.                  |

For more information, refer to the documentation.

4. **AI-Suggested Similar Queries**

We are excited to announce AI-Suggested Similar Queries to help improve the shopper experience by surfacing relevant, intent-driven search suggestions.\
What it does:

Recommends additional search terms and category-based suggestions based on past user behavior, search trends, and semantic understanding.

Helps users refine their search, discover products faster, and significantly reduce zero-result queries.

Example:\
 If a user searches for White Dresses, the system might suggest related queries like white dress, white shoes, white bag, or white sneakers.For more information, refer to the documentation.

5. **Visual Search**

We’re thrilled to announce the enhancement of Visual Search , a next-generation AI-driven feature that empowers shoppers to search for products using images instead of text.\
It has been significantly enhanced with improved capabilities and a refreshed user experience. This upgraded version delivers more accurate results, faster performance, and better integration, making it more powerful and intuitive than ever before.

***What it does?***

* Using Visual Search, users can easily find a product even if they dont know the exact product names.
* Visual Search allows users to:
* Upload an image or paste an image URL.
* Get real-time product recommendations that match visually with the input image.
* Interact with image markers (dots) to view similar items for specific products within a multi-item image (e.g., dress and shoes).

For more information, refer to the Visual Search documentation.

6. **Product Card Viewer**

We are pleased to announce the General Availability of Product Card Viewer, powerful visual tool that enables merchandisers and business teams to preview how products will appear to shoppers on Search and Browse pages.

This feature bridges the gap between data configuration and on-site presentation by linking specific product attributes (like title, price, and image) to how they are rendered in product listings.

***Why is it so important?***

The Product Card Viewer gives teams an at-a-glance preview of product listings directly in the Unbxd console. It ensures that key product information is prominently displayed, making merchandising more effective and product discovery smoother for shoppers.\
Refer the Product Card Mapping documentation to learn more.

7. **Bulk Export/Import Field Configurations**

We are excited to announce the General Availability of the Bulk Export/Import Field Configurations feature. This new capability allows users to export and import field configuration settings in bulk, making catalog setup and management faster, more scalable, and less error-prone.

Whether you're working across multiple environments or updating field properties for large product catalogs, this feature simplifies the process and ensures consistency in your configuration strategy.

Click here to know more.

8. **Bulk Upload for Searchable Fields**

We have introduced bulk upload and bulk download of searchable fields under Manage section.