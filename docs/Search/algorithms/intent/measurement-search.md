---
title: Measurement Search
excerpt: >-
  Process any search query which has dimensions to it using Unbxd Measurement
  Search
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

This feature lets you run more accurate searches using specific product details like size, weight, price, or pressure. You can fine-tune search results by setting up a strategy and using product attributes that have measurable values and units.

For example, if you search for **28-inch denim jeans**, ***28 inches*** refers to a **measurable dimension**.

## How it works?

The system understands that the user is looking for jeans with a **waist measurement of 28 inches**. This is a clear, quantifiable search attribute (the waist size) that the system can use to filter and narrow down the results.

**Measurable Dimension**: A specific, quantifiable attribute of a product (such as size, weight, or price) that can be used to filter or refine search results based on exact values or units.

### Prerequisites

* You should have a valid UNBXD account with appropriate permissions to access the Self-Serve Console. The console allows you to configure various aspects of your search, product data, and system settings.
* Measurement Search must be enabled on your UNBXD account. This could be enabled by clicking on the toggle button.

### Impact of Meaurement Search

1. **Refined Search Results**:\
   By setting exact dimensions like width, weight, and price, you can narrow down the search to products that meet all your specific needs.
2. **Saves Time**:\
   Instead of browsing through irrelevant products, this method allows users to find exactly what they need faster by applying filters based on exact measurements.
3. **Personalized Results**:\
   Users can specify exact sizes, weights, and prices, making the search process more personalized and tailored to their preferences.
4. **Better Shopping Experience**:\
   By focusing on specific product attributes, customers can quickly find items that match their exact requirements, leading to a smoother and more satisfying shopping experience.

## Set up Measurement Search

Log in to Netcore Unbxd console page.

1. Navigate to **Algorithm** > **Intent** > **Measurement Search**
2. Click on the **CTA button** to enable the Measurement Search.

<Image align="center" border={true} caption="Set up Measurement Search" src="https://files.readme.io/b20fd27e1d9e7bb9d96f807bbb67390386c18a95f784832df6b4c7ed420fe0d3-MEasurementsearchGIF.mp4-ezgif.com-crop.gif" width="80% " />

3. **Strategy Selection**: You can select either of the available strategy: **Boost or Filter**.

* **Boost Strategy**: This strategy gives priority to products that are close to the measurement the user searched for even if they're not an exact match.For example : If a user searches for a "7 kg washing machine", and only 7.5 kg models are available, then the system will still show the 7.5 kg options at the top of the results.

It works best when shoppers are open to similar options or when exact matches are not available.

* **Filter Strategy**: This strategy only shows products that exactly match the measurement in the search.For example,  If a user searches for a "7 kg washing machine", the system will show only washing machines that are exactly 7 kg. No 6.5 kg or 7.5 kg options will be included.

It works best when shoppers are looking for a specific size or fit, with no flexibility.

4. **Configure Attributes** This section enables search using measurable attributes. You must select the attributes from the catalog and map the dimensions and units accordingly. You can add up to 5 attributes per dimension type. Currently, we support the following units:

| **Dimension**    | **Unit**                                                                                                         |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Price**        | usd, aud, cad, sgd, gbp, cent, $, €, £, ₹                                                                        |
| **Size**         | mm, cm, m, mi, in, ft, mm², cm², m², mi², in², ft², mm³, cm³, m³, mi³, in³, ft³, l, fl oz, gal, qt, pt, bbl, tsp |
| **Weight**       | mg, g, kg, lb, oz                                                                                                |
| **Pressure**     | pa, kpa, atm, torr, bar, psi, mmhg, psia, psig, ksi                                                              |
| **Product Info** | b, kb, mb, gb, tb, pb, eb, ib, kib, mib, gib, tib, pib, eib                                                      |

<br />

5. **Default Configuration**: This is used to power the queries that do not have a dimension attribute.\
   For example, your search query is "red shirt under 10". Here, the user/merchandiser must set up a default dimension (Price or Size, in this case) so that the search result displays products with a price less than $10 or products with a size less than ten.
6. **Tolerance configuration**: It is a flexibility factor that gives you better search results. Currently, the query builder follows a configurable normalization range of ±10%.

After the type of strategy is decided, click Save configuration and click Sync to add measurement search configurations to your search.

### Use Case

A user searches for a coffee table, the user enters search query: "Coffee table 48x24x18" (48 inches long, 24 inches wide, 18 inches high).

The search engine would parse these dimensions and query for products where:

**Length** = **48 inches**

**Width** = **24 inches**

**Height** = **18 inches**

Measurement-based search in Netcore Unbxd helps users find products that meet specific criteria based on measurable dimensions (size, weight, pressure, etc.). It improves the overall shopping experience by allowing precise searches and delivering highly relevant results based on the user's needs.

## Troubleshoot & FAQs

<Accordion title="How does Measurement Search improve the shopping experience?">
  It delivers more accurate and relevant results by understanding and applying measurable product dimensions.   This helps shoppers quickly find products that fit their specific needs (e.g., size, capacity, or budget).
</Accordion>

<Accordion title="What is the difference between Boost and Filter strategies?">
  Boost Strategy: Prioritizes products within or close to the specified measurement range (e.g., 7.5 kg washing  machine when 7 kg is searched).

  Filter Strategy: Only shows exact matches for the specified measurement (e.g., only 7 kg models when 7 kg is searched).
</Accordion>

<Accordion title="How many attributes can I map per dimension type?">
  You can map up to 5 attributes per dimension type from your product catalog (e.g., waist, chest, and inseam under size).
</Accordion>

<Accordion title="What happens if a user enters a query without units?">
  The system attempts to infer the context based on the product type and attribute configuration. However, best results are achieved when units are specified.
</Accordion>