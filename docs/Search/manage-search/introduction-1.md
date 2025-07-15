---
title: Introduction
deprecated: false
hidden: false
metadata:
  robots: index
---
Netcore Unbxd's Merchandising Workbench is a robust tool for managing product visibility and enhancing user engagement by promoting specific products or categories. It provides a versatile, no-code Visual Editor, making it comfortable to create, configure, and fine-tune merchandising rules.

<Accordion title="What can I do with the Merchandising Workbench?">
  ### 1. Promote or Hide Products

  Easily prioritize specific products or remove less relevant items from search results based on keywords or customer preferences. By controlling product visibility, you guide shoppers toward the best-fit items. Learn how to do it ↗

  * Promote items relevant to the current season, like “winter coats” during colder months or “beachwear” in summer.
  * Prioritize visibility for newly launched products, ensuring they appear prominently in search results to drive awareness and engagement.
  * Temporarily hide products that are low on stock or in clearance to maintain shopper expectations around availability.

  ### 2. Pin Products to Specific Positions

  Pin selected products to designated spots in the search results of any query to ensure shoppers see the items you want to highlight. This helps increase visibility for new arrivals, high-margin items, or promotional products. Learn how to do it ↗

  * Pin high-profit products to prominent positions, increasing visibility for items with the best business interest.
  * Feature highly rated or reviewed products at the top of relevant search results to guide shoppers toward quality choices.

  ### 3. Run Campaigns with Banners and Landing Pages

  * Elevate your marketing initiatives by displaying banners for sales, events, or seasonal promotions. Learn how to do it ↗
    * Promote holiday sales with special offers.
    * Showcase banners for a new collection launch.
  * Create dedicated landing pages specific to a query for an engaging and cohesive shopping experience. Learn how to do it ↗
    * Showcase all discounted products together.
    * Curate a “Shopper Favorites” page that includes top-rated and best-selling items

  ### 4. Showcase Handpicked Product Collections

  Create curated collections that cater to specific shopper interests, such as “Top Picks for Summer” or “Gifts for Her,” providing an easy way to navigate high-interest items. Learn how to do it ↗

  * Create collections like “Eco-Friendly Essentials” or “Tech for Travelers” to help shoppers quickly find curated items for specific themes.
  * Create collections around special occasions (e.g., “Mother’s Day Gifts”) to guide shoppers toward popular gift ideas.

  ### 5. Instantly separate products that match set conditions

  Automatically filter and organize products based on specific criteria—such as pricing, stock levels, or shopper preferences—allowing for quick, dynamic adjustments in merchandising. Learn how to do it ↗

  * Create price-sensitive campaigns by quickly filtering products based on the price attribute.
  * Instantly filter all products based on color to run Christmas or St. Patrick’s Day campaigns.

  ### 6. Customize Facets for High-Conversion Filters

  Present high-impact filters to narrow search results and match shopper intent, such as “eco-friendly” or “popular brands,” enabling quick discovery of relevant products. Learn how to do it ↗

  * Feature filters for popular brands to make it easy for brand-loyal shoppers to navigate directly to their preferred options.
  * Highlight facets like “Eco-Friendly” or “Recyclable” for sustainability-focused shoppers.

  ### 7. Redirect Shoppers to Targeted URLs

  Guide users to relevant pages when they search for popular categories or keywords. For example, redirecting “customer support” queries to the help page ensures a smoother user experience. Learn how to do it ↗

  * Redirect searches like “new releases” to a dedicated page that showcases the latest product drops.
  * For out-of-stock popular items, redirect users to a similar collection page or “back-in-stock” alert page.

  ### 8. Merchandise Query Autosuggest

  Promote a specific suggestion/typeahead option and increase active campaign visibility. Learn how to do it ↗

  ### 9. Segment Shoppers and A/B Test Ideas

  * Leverage segmentation to personalize the shopping experience based on user behaviors or preferences. Learn how to do it ↗
  * Use A/B testing to measure the impact of merchandising adjustments on conversions. Learn how to do it ↗

  ### 10. Analyze Product and Campaign-Wise Shopper Behavior

  Get in-depth insights into how your shoppers engage with specific products, campaigns, or queries. Learn how to do it ↗

  * Track metrics like clicks and conversions to understand which campaigns (e.g., flash sales) perform best and refine future strategies accordingly.
  * Analyze engagement metrics for individual products to identify best-sellers and promote them for higher visibility.
  * Monitor shopper behavior patterns on category pages, identify popular items, and adjust merchandising strategies to cater to demand.
</Accordion>

## How to access the Merchandising Workbench?

1. Log in to Netcore Unbxd’s [self-serve console](https://console.unbxd.io/) ↗
2. From the **Site Key Picker**, click the site you want to apply a merchandising strategy.
3. After selecting the appropriate site key, navigate to **Merchandising** > **Search**. The options under search are: **Promotions**, **Banners**, **Facets**, and **Redirects**.

<Image align="center" border={true} caption="Highlight Your Products Through Merchandising Search" src="https://files.readme.io/c9083d3fc592bc0dcbb7f2fdaaba31ef433197d9acb109b06c7df363eac9e984-Search_Merchandising.gif" width="80% " />

## What are the Netcore Unbxd UI terminologies you should know?

<Accordion title="Attributes">
  In an ecommerce catalog, attributes are the characteristics or properties that describe a product. These attributes can be textual or numerical and help effectively organize, filter, and display products.

  **Example:** Attributes like Color, Price, and Brand define key traits of a product.
</Accordion>

<Accordion title="Values">
  Values represent the specific details or data points associated with an attribute. These values define the characteristics that an attribute describes.

  * **Example:**
    * The attribute Color might have values like *Red*, *Blue*, or *Green*.
    * The attribute Price might have values like *50*, *100*, or *150*.
    * The attribute Brand might have values like *Nike* or *Adidas*.
</Accordion>

<Accordion title="Operators">
  Conditions allow you to create rules by comparing attributes and their values. These conditions determine how products are filtered, boosted, or buried.

  1. Equals (=)
     The attribute value must exactly match the specified value.
     **Example:**
     Brand = Nike will include only products with the brand "Nike." Products like "Nike Limited Edition" will not be included because it's not an exact match.

  2. Not Equals (≠)
     The attribute value must not exactly match the specified value.
     **Example:**
     Color ≠ Red will exclude products that have "Red" as their color. However, products like "Dark Red" or "Red Velvet" will still be included because they are not an exact match for "Red."

  3. Contains (⊂)
     The attribute value must include the specified keyword or text.
     **Example:**
     Brand ⊂ "Nike" will include products where the brand contains the word "Nike," such as "Nike" or "Nike Limited Edition."

  4. Does Not Contain (⊄)
     The attribute value must not contain the specified keyword or text.
     **Example:**
     Color ⊄ "Red" will exclude all products with "Red" anywhere in the color description, such as "Dark Red" or "Red Velvet."

  5. Logical Operators

  **AND**: All conditions must be true for the rule to apply. This operator is used to combine multiple conditions where all must be met. **Example:** Brand = Nike AND Color = Red will include only products that are both "Nike" and "Red."

  **OR**: At least one of the conditions must be true for the rule to apply. This operator is used to broaden the scope of the condition. **Example:**  Brand = Nike OR Brand = Adidas will include products from either "Nike" or "Adidas," but not necessarily both.

  **THEN**: This operator is used to define the sequence of rules. If the first condition is met, the second rule will apply. It is typically used when you want to create a layered, sequential set of rules. **Example:** Sort by Price Ascending THEN Sort by Rating Descending means that the products will first be sorted by price from low to high. If products are at the same price, they will be sorted by rating them high or low.
</Accordion>

## How to combine rules to create a cohesive merchandising strategy?

Netcore Unbxd Workbench supports using multiple merchandising rules, enabling retailers to create a cohesive shopping experience.

Here’s a simple example for a search query **back-to-school** campaign:

| Action                  | Description                                                                                                                   |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Segment shoppers        | Divide shoppers based on behaviors, preferences, or demographic data.                                                         |
| Run a banner            | Display a banner on the homepage, category pages, and search query listing pages promoting the "**back-to-school**" campaign. |
| Create a landing page   | Apply filters for specific items such as stationery, lunch bags, or water bottles to create a campaign landing page.          |
| Redirect users          | Guide users to the landing page dedicated to back-to-school products and deals.                                               |
| Boost and bury products | Highlight new arrivals and highly rated items for each segment, while burying products with lower ratings.                    |
| Pin popular items       | Pin products from popular brands in the top 1 to 10 positions on the search results page.                                     |
| Analyze performance     | Evaluate the campaign's success and analyze shoppers' journeys to improve future campaigns.                                   |

# Field Rule

Field rules are used to create facets and banners for a specific page. By default, facet under Site Rule is inherited to all the pages, however, you can override them by creating a field rule for that particular page.

Field rules allow you to show banners and facets when more than 80% of the products satisfy field rule criteria. While facets under Site Rules are displayed for all queries, Field Rules allow you to override the facets defined in site-rule based on product-type/category, etc.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/6929e510039c66d43ae2b84ac1a93306f788ecc6ea1f85b58ff857aad71f8c85-image.png" />

When a query has multiple Field Rules – where more than 80% of retrieved products can map to two different Field Rules – the creation date of Field Rules is considered. Older Field Rules will take precedence over newer Field Rules. While facets under Site Rules are displayed for all queries, Field Rules allow you to override them for queries for certain type/category.

For example, if a field rule is created for ‘Hybrid Cycles’ and when a shopper searches for ‘Cycles’, and 80% of the search results are ‘Hybrid Cycles’, then the ‘Hybrid Cycles’ field rule will be applied.

Field Rules created in Search and Browse are exclusive of each other and will not overlap.

> 📘 Note
>
> In case of conflicts in facet settings, field rules are given preference over site-rules.

## Create a Field Rule

To add a field rule follow the mentioned process :

1. Navigate to Merchandising → Browse → Field Rule.
2. To add fields, do the following:
   1. Click  .
   2. Select the fields you want to use. You can also search for the fields.\
      Note: You can select a maximum of five fields.
   3. Click Apply.\
      The selected fields appear in the Create Field Rule window.
3. Click  .The Create Field Rule window appears.
4. Select the field you want to use.
5. Select the respective field value.
6. Click Create Field Rule.The new field rule is added to the Field Rule tab.
7. Click the field rule you want to publish.
8. To set up banner using an image url, do the following:

a. Click Image url.

b. Enter the url of an existing banner image.

c. Enter the corresponding landing page url.

9. To set up a banner using HTML, click HTML, and then paste your banner HTML code.
10. Click the Facets tab. You can navigate to Manage → Configure Site to configure facets. For more information on configuring facets, see Configure Facets.
11. To reposition a facet, do the following:
    1. Hover on the faceting row you want to reposition. The reposition icon  appears.
    2. Click , and then drag the facet to a new position.
    3. If you want to show the facet on your site, in the Show column, select the respective facet checkbox.
    4. Click  to save the repositioning changes.

## Edit a Field Rule

To modify a facet, edit using the mentioned process :

1. Click the facet for which you want to edit the values.
2. Click .
3. Type the new facet length.
4. Select sort order for your facet. You can sort either by product count or alphabetically.
5. Click Save.
6. To go to the previous screen, click  PREV.
7. Click PUBLISH.

## Delete a Field Rule

To Delete a field rule follow the mentioned process :

1. Within the console, navigate to Merchandising > Browse > Field Rule.
2. Click Field Rule.
3. Click the delete icon for the required Rule.
4. You’ve successfully deleted the field rule.

> ❗️ CAUTION
>
> Deleting will permanently remove the Rule. You cannot recover a deleted field rule.