---
title: AI-Meta-Data
excerpt: >-
  AI Metadata in Unbxd enriches your product catalog by automatically extracting
  and enhancing product attributes using AI
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

**AI Metadata** is a smart feature in Unbxd that automatically adds important information (called attributes) to your product listings using **Artificial Intelligence**.\
It decodes complex search queries to help shoppers find exactly what they want. It looks at your product titles, descriptions, and other content to figure out things like: **Color, Material, Style**, **Fit**, **Occasion,** and so on.

For example, if a product is titled “**white dress for summer brunch**”, Unbxd’s AI will automatically extract:

* **Color**: White
* **Occasion**: Brunch
* **Season**: Summer
* **Style**: Casual / Daywear (based on content patterns)

**Solution with AI Metadata:**\
Unbxd's AI Metadata automatically extracts these attributes are enriched in the product metadata, enabling the system to match the search intent and surface the most relevant white dresses. The customer is shown perfectly suited products for a summer brunch in white. This leads to better user satisfaction, quicker product discovery, and increased conversions.

These attributes get added to your catalog as **metadata**, which helps improve how this product shows up in search or filtering. Even if this info isn’t manually added to your product catalog, **AI Metadata can detect it automatically.**

<Image align="center" border={true} caption="Navigate to Insights" src="https://files.readme.io/773730c21015350e1b6ead9af45034c8eefb9c08eb44c80362c62ffc12235d83-Insights.gif" width="80% " />

## Impact of AI-Meta Data

* With the help of AI Meta Data search results become more accurate.
* **Filters and Facets** (like "color" or "material") give better results.
* It makes it easier for users to find the right product.
* Time is saved by reducing manual data entry.
* It improves product recommendations and SEO.

## Use AI-Meta Data

1. Navigate to **Search Preview** on the Unbxd console.
2. Click **Debug View** from the drop-down.

<Image align="center" border={true} caption="Viewing Debug View" src="https://files.readme.io/d3504b1f19a41f0a3dbe4fc47347c8575cb3da6aac1e028b984ef6cb3fa5b8f0-debugview.png" width="80% " />

In Debug view, you would be able to see the below:

* **Site Perfomance**: It measures how fast and efficiently the site responds to search requests.*For example*: Search results loaded in 130ms.
* **Query Performace**: This tracks how well a specific search query performs in terms of speed and relevance.*For example*: if a user searches for “leather boots” the webite took 120ms and returned 25 results. 120ms & 25 results are the attribules of Query performance
* **Relevancy**: Indicates how closely a product matches the user's search intent and query terms. *For\_example*: A product has 4/5 relevancy score for “wireless earbuds”.
* **Performance** (if enabled) : Displays user engagement metrics like clicks, add-to-cart, and conversions per product.\_ For example:A product has a 5% conversion rate from searches in the last 7 days.

These factors collectively contribute to the **Score** (final product score), which determines the product's ranking in search results.

## AI Models: Models that Influence the Overall Search Result

Click Insights to understand how shoppers are interacting with Search and Browse.

1. **Content Model**: The Content Model analyzes your product catalog to understand what each product is, based on its attributes like title, description, brand, color, size, material, and so on.\
   It structures and enriches product data to improve discoverability.
   For example: If a product title is "Slim Fit Cotton Shirt – Blue, Medium". The Content Model will extract the below:

   * *Category*: Shirt
   * *Fit*: Slim Fit
   * *Material*: Cotton
   * *Color*: Blue
   * *Size*: Medium

   This will help the system surface the product when users search for any of those attributes.
2. **Intent Model**: The Intent Model interprets what the shopper *really* means when they type a search query even if it’s not phrased perfectly. Refer here for details of Intent Model. For example:  If a user searches for \_“office chair for back pain under $200”. \_The Intent Model will understands:
   * *Product type*: Office Chair
   * *Use case*: Ergonomic / back support
   * *Price filter*: Less than $200\
     This model helps in showing ergonomic chairs with lumbar support within the price range.
   * Intent Model uses below algorithms to understand the purpose of the search query.\
     -**Named entity recognition**: It detects and tags important keywords in a search query, like brand, color, size, or product typ,to better understand user intent.
     -**Measurement Search:** It allows shoppers to search using specific dimensions (like size, weight, or price), and returns products that match those exact measurable values.
     -**Vector Search**: IT uses AI to understand the *meaning* behind a search query, returning relevant products even when exact keywords aren’t used.
3. **Ranking Model**: The Ranking Model decides the order in which products appear in search results. It scores products based on factors like relevance, user engagement, popularity, availability, and business rules. It ensures the most relevant and high-performing products show up at the top.\
   For example: If a user searches for "\_wireless headphones" and \_ two products matches the search query, the Ranking Model will boost **Product A** higher in the search results because:

   * Product A has a higher click-through rate and better reviews.
   * Product B is new with little engagement.

   <Image align="center" border={true} src="https://files.readme.io/bf0bc347c1fd423ae4b9103ba12f4372a92e18499b0393f9af15d5b7f04048af-Rankingmodel.png" width="80% " />
4. **Fallback Model**: If none of the primary models — **Content**, **Intent**, or **Ranking** — are able to return strong or relevant results for a search query, the **Fallback Model** steps in to support the search. The Fallback Model ensures users **never hit a dead-end** by retrieving semantically related products using **Vector Search**, even when exact matches are missing.\
   For example: Example: If a user searches for: \_“shoes for muddy trails” and \_no product contains this exact phrase or Content & Intent models can't map it clearly then **Fallback Model** uses vector search to surface results like:
   * *“Trail running shoes”*
   * *“Hiking boots”*
   * *“Waterproof outdoor shoes*

## Conclusion

AI Metadata in Unbxd is a powerful tool that enhances product discoverability and search accuracy by automatically enriching product data using Artificial Intelligence. It extracts key attributes like color, material, size, and style from product content—saving time and reducing manual effort.

By combining AI Metadata with advanced models like **Content**, **Intent**, **Ranking**, and **Fallback**, Unbxd ensures:

* **More relevant and personalized search results**
* **Smarter filtering and facet generation**
* **Improved product rankings and engagement**
* **Fewer dead ends and better shopper experiences**

Ultimately, AI Metadata helps merchandisers gain deeper visibility into search performance while enabling shoppers to quickly and easily find exactly what they’re looking for.

## Troubleshooting & FAQ's

<Accordion title="How does AI Metadata improve search results?" icon="sparkles">
  It adds enriched product attributes which improve filtering, facets, and ranking in search results. This helps users find relevant products faster.
</Accordion>

<Accordion title="Do I need to manually tag attributes like color or size?" icon="sparkles">
  No, the AI engine automatically extracts this data from product titles, descriptions, and other content—even if it’s not already part of your catalog.
</Accordion>

<Accordion title="How does AI Metadata improve search results?" icon="sparkles">
  It adds enriched product attributes which improve filtering, facets, and ranking in search results. This helps users find relevant products faster.
</Accordion>

<Accordion title="Does AI Metadata help with SEO?" icon="sparkles">
  Yes. Enriched product attributes improve on-site search relevance and external discoverability, indirectly boosting SEO.
</Accordion>

<Accordion title="Search results are irrelevant despite correct metadata." icon="sparkles">
  * **Check:** Look at the scores in Debug View.
  * **Fix:** Check if other models (like Ranking or Intent) are influencing results.
  * **Action:** Adjust weights or rules in the ranking strategy if needed.
</Accordion>