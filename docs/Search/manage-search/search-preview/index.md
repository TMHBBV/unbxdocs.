---
title: Search Preview
deprecated: false
hidden: false
metadata:
  robots: index
---
Enter a query to view product listings, understand performance metrics like clicks, carts, and orders, and evaluate search relevancy — all in one place.

The **Search Preview** feature lets you test how your customers will see products when they search on your website. It shows you the actual results, filters, and sorting logic before going live.

You can use this to:

* Check if the right products show up for the search terms.
* Validate sort order and filters.
* Preview your merchandising campaigns.

***

## How to Use Search Preview

1. On the Unbxd console, click **SEARCH PREVIEW** located in the top right corner.
2. Use the search bar at the top to type a keyword, for example, `dress` and press **Enter** or click the **search icon**. You can view the total number of products found and the preview of how products appear to shoppers.

In the top-right corner, you can switch between the view mode.

| View Mode    | Description                                           |
| ------------ | ----------------------------------------------------- |
| Default View | Standard shopper-facing display                       |
| Debug View   | Shows backend data like boost scores (for QA/testing) |

### Facets

On the left side, filter options to narrow down the results. You can test how filters will appear and work on your storefront.

| Available Filters (Facets) |
| -------------------------- |
| Price                      |
| Product Type               |
| Brand                      |
| Gender                     |
| Backstyle                  |
| Fit Type                   |
| Pattern                    |
| Color                      |
| Theme                      |
| Size                       |
| Material                   |

You can also collapse the filter panel using the **Hide Facets** button.

***

### Sort Options

You can sort the results using different criteria by clicking the **Sort by: Relevance** dropdown.

| Sort Option        | Description                         |
| ------------------ | ----------------------------------- |
| Relevance          | Default sort based on relevance     |
| Price: High to Low | Expensive products appear first     |
| Price: Low to High | Cheaper products appear first       |
| Title: A to Z      | Alphabetical order by product title |
| Title: Z to A      | Reverse alphabetical order          |

### Filters

Filters panel in Search Preview allows you to simulate different search scenarios by customizing ranking behaviors and user attributes.

| **Section**           | **Field/Option**                  | **Description**                                                                                            |
| --------------------- | --------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Filters**           | **Promotion**                     | Enables merchandising rules to boost products tied to promotions.                                          |
|                       | **Popularity**                    | Uses metrics like sales, views, or clicks to influence product ranking.                                    |
|                       | **Fallback**                      | Displays default fallback results when no direct matches are found.                                        |
|                       | **User Behavior**                 | Personalizes results based on user interaction history (views, clicks, etc.).                              |
| **Segment Attribute** | **User ID**                       | Enter a specific user ID to simulate personalized results for that user.                                   |
|                       | **Device**                        | Select a device type (e.g., Desktop, Mobile) to simulate device-specific output.                           |
| **Custom Attributes** | **Custom Attribute Name = Value** | Add up to 3 attribute-value pairs to test segment-specific behavior. \<br> Example: `loyaltyStatus = gold` |
| **Action Buttons**    | **Reset Filter**                  | Clears all selected toggles, user inputs, and attributes.                                                  |
|                       | **Apply**                         | Applies the current filter settings and updates the search results preview.                                |

Refer to the following documents to