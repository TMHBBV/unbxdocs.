---
title: Attribute Enrichment
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The **Attribute Enrichment** in the console aims to enhance catalog completeness for optimal search performance. This dashboard facilitates the identification of missing or incomplete attributes in product catalogs, providing detailed metrics and allowing merchandisers to prioritize enrichment efforts. It presents various attributes, their status, and their impact on search performance.

## Why is this Useful?

Below are the benefits of using Attribute Enrichment:

* **Analyze Your Data:** Use Unbxd’s tools to assess the quality of your product data and search results.
* **Manage Attributes:** Access an intuitive dashboard to review and control enriched attributes.
* **Optimize Continuously:** Monitor key performance indicators (KPIs) and refine enrichment rules as needed to maximize impact.

### How It Works

Our attribute enrichment technology combines advanced AI techniques with your merchandising expertise to:

* Augment existing product attributes.
* Generate new attributes and categories where data is missing.
* Standardize and correct inconsistent product information.

### Benefits

* **Improved Product Discovery:** Enriched attributes enable more relevant search results, helping shoppers find the right products faster.
* **Increased Revenue:** Better search relevance drives higher Revenue Per Visitor (RPV) and Average Order Value (AOV).
* **Efficiency for Merchandisers:** Automating manual data tasks frees up valuable time, allowing merchandisers to focus on strategic initiatives.
* **Continuous Improvement:** Easily review, manage, and analyze enriched product data to optimize search performance and key metrics over time.

## How to Get Started

Log in to Netcore Unbxd Dashboard and navigate to **Manage** > **Catalog** > **Attribute Enrichment**

<Image align="center" border={true} caption="Navigate to Attribute Enrichment" src="https://files.readme.io/4dac8cf8173b238cc8e531f14d089772e618331133cb30e58c3e82a7177229d9-Attribute_Enrichment.gif" width="80% " />

1. Initial Setup: Map product attributes to Google Category taxonomy (e.g., Product Title, Category, Brand) using the "Target Field" column.
2. Track Completeness: Ensure the "Completeness" column accurately reflects the percentage of attributes populated for each product category.
3. Define Metrics: Set up calculation formulas for the "Missing" and "Search Impact" columns based on product data and search analytics.
4. Monitor Progress: Use the "Status" and "Mapping" columns to monitor the enrichment process and track the lifecycle of each attribute.
5. Prioritize Action: Use the "Actions" column to trigger appropriate actions (enrich, publish, review) based on the status of each attribute.

Leverage Attribute Enrichment to boost your e-commerce platform’s search experience and overall conversion metrics. For a personalized walkthrough, consider booking a demo or requesting a search experience audit through your Unbxd account.

## Dashboard Keywords and Their Functionality

Below are the functionality present on the Netcore Unbxd Console.

| **Keyword**         | **Functionality**                                                                                                                                                      | Use Case                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Target Field**    | Displays standardized attribute names based on Google Category taxonomy. Shows the ideal attributes for optimal catalog completeness.                                  | **For Example**: For a motorsports customer with a diverse product selection (e.g., trousers, tires, helmet gears, e-bikes), the Target Field "closure" is only applicable for relevant categories like trousers, not for irrelevant ones like tires or helmets. Metrics like completeness, missing values, and search impact are calculated based on products in the relevant category. The details section displays product and category-related information based on the identified relevant categories. |
| **Completeness**    | Shows the percentage of products with populated attribute values. Displays a progress bar with color coding (red, orange, green) to indicate coverage levels.          | **For Example:** For a motorsports customer with 100 products in the "trousers" category, if only 60 out of 100 products have the "closure" attribute filled, the completeness for this attribute is 60%. This metric is calculated based on products in the relevant category (e.g., trousers) and does not include irrelevant categories like tires, helmets, or e-bikes. This ensures that the completeness metric is category-specific.                                                                 |
| **Missing**         | Displays the count of products lacking attribute values. Sortable and clickable for detailed product lists. Helps prioritize enrichment based on missing values.       | **For Example:** Using the same motorsports example, if the "closure" attribute is missing for 40 out of 100 trouser products, the "Missing" column would show "40". This gives merchandisers a clear count of products that need attention, allowing them to prioritize enrichment efforts based on the volume of missing data.                                                                                                                                                                            |
| **Search Impact**   | Shows the potential improvement in search performance if missing attributes were enriched. Calculated using a specific formula and displayed as a percentage.          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Status**          | Tracks the lifecycle status of each attribute (Unmapped, Mapped, Enriching, Enriched). Visual indicators (color coding) represent the current stage of each attribute. |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Mapping**         | Displays the actual catalog field mapped to the Google Category attribute. Shows the connection between standard and internal fields.                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Actions**         | Provides contextual action buttons based on the attribute's current status. Options include "Enrich," "Publish," "Review," and "Analyze Impact."                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Category Picker** | A dropdown menu allowing users to select categories. Categories are sorted based on the number of products. Helps in filtering by relevant categories.                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Search Bar**      | Allows users to search for attributes and displays them dynamically as users type. Facilitates easy navigation to relevant attributes.                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Refresh**         | A button to update completeness, missing, and search impact metrics in real-time, ensuring data accuracy.                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **View Details**    | An expandable option to view detailed information about the attributes, showing product and category-related details for enrichment decisions.                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Sort Order**      | Controls the order in which attributes are displayed on the landing page. Options include completeness, missing & search impact, and status.                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Advance Filters** | A set of filters to narrow down data based on specific criteria. Used to refine the view of attributes.                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

### Next Steps

Leverage Attribute Enrichment to boost your e-commerce platform’s search experience and overall conversion metrics. For a personalized walkthrough, consider booking a demo or requesting a search experience audit through your Unbxd account.