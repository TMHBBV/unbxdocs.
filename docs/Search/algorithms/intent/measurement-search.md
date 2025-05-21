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

<Image align="center" border={true} caption="Set up Measurement Search" src="https://files.readme.io/bdb4e4041895b596d28027be519512a1995bca84864aa958e02406c6140cf446-image.png" width="80% " />

3. Strategy Selection: You can select either of the available strategy: Boost or Filter.
4. Boost Strategy: This strategy gives priority to products that are close to the measurement the user searched for even if they're not an exact match.For example : If a user searches for a "7 kg washing machine", and only 7.5 kg models are available, then the system will still show the 7.5 kg options at the top of the results.

It works best when shoppers are open to similar options or when exact matches are not available.

Filter Strategy: This strategy only shows products that exactly match the measurement in the search.For example,  If a user searches for a "7 kg washing machine", the system will show only washing machines that are exactly 7 kg. No 6.5 kg or 7.5 kg options will be included.

It works best when shoppers are looking for a specific size or fit, with no flexibility.

Configure Attributes: This section enables search using measurable attributes. You must select the attributes from the catalog and map the dimensions and units accordingly. You can add up to 5 attributes per dimension type. Currently, we support the following units: