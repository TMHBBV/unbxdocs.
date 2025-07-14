---
title: Customised Facets and Navigations
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Facets are essential tools that help shoppers narrow down search results on an e-commerce site. When searching for products, the Product Listing Page (PLP) can quickly become overwhelming if many products are returned for a single query. By using product attributes as facets, you can effectively narrow down the listing, which improves the overall shopping experience.

## Advantages of Using Faceted Search

1. **Increases Product Discoverability** : Faceted navigation improves the shopping experience by reducing the overwhelming task of scrolling through hundreds of products.

Facets help shoppers refine their search quickly, increasing the likelihood of finding the right products faster.

2. **Fewer Clicks to Desired Products**: Facets help users skip the task of scrolling through multiple pages.

Users can quickly find the desired product with minimal clicks and navigate easily between different options.

3. **Higher Conversion Rate** : By reducing the time and effort spent searching, faceted search helps users make quicker purchase decisions.

The simplified process facilitates a smoother shopping experience, increasing the chances of a completed purchase.

### Types of Facets

| **FacetType**    | **Description**                                                             | **Examples**                  | **Attributes**                                          |
| ---------------- | --------------------------------------------------------------------------- | ----------------------------- | ------------------------------------------------------- |
| **Text**         | Used for attributes that have text-based values.                            | Brand, Color                  | Text values (e.g., "Nike", "Red")                       |
| **Range**        | Used for attributes with numeric values, allowing filtering within a range. | Price, Date                   | Range Start, Range End, Range Gap                       |
| **Multi\_level** | Based on attributes with hierarchical information.                          | Product Categories, Locations | Hierarchical categories (e.g., "Electronics > Laptops") |

## Facets Configuration in Unbxd Console

<Image align="center" border={true} caption="Add A New Facet" src="https://files.readme.io/7891cb0f1e455a07c274885bd7bb570373e34734972f9927b0871a4b5184c83b-AddNewFacet.gif" width="80% " />

To configure facets, follow these steps:

1. Log in to the Unbxd console. Navigate to **Manage** > **Search** > **Facets** to access the facet settings page.
2. Review existing facets or click Add New Facet to create a new one.
3. Enable global facets and control their rankings under **Merchandising** > **Search** > **Facet**.

> 📘 Note
>
> Only facets with status **Enable** will appear on the site’s Product Listing Page (PLP). Facets with ‘Disabled’ status won’t be shown on website.

### Types of Facet Merchandising Available

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        **Facet Type**
      </th>

      <th>
        **Description**
      </th>

      <th>
        **Examples**
      </th>

      <th>
        **Key Characteristics**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **All Queries Facet**
      </td>

      <td>
        Applied universally across all search queries and shopper segments.
      </td>

      <td>
        Price: Filter by price range across all product categories. Brand: Filter by brand for all searches.  Customer Ratings: Filter by customer ratings across products.
      </td>

      <td>
        * Only one rule can exist per site. Automatically generated during site setup.  Applies to all searches.
      </td>
    </tr>

    <tr>
      <td>
        **Field-based Facets**
      </td>

      <td>
        Dynamically adapt based on the search results.
      </td>

      <td>
        Filters for product attributes like Color, Size, etc., based on the search query.
      </td>

      <td>
        * Displayed only when 80% or more of products match the condition. Take precedence over “All Queries” rule.
      </td>
    </tr>
  </tbody>
</Table>

### Create and Edit Facets

1. To add a Text Facet: Navigate to **Manage** > **Search** > **Facets**. Click **Add New Facet**. Fill in the following details:

<Table>
  <thead>
    <tr>
      <th>
        **Attribute Name**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Name of the Product Attribute**
      </td>

      <td>
        Name of the product attribute defined in the catalog.
      </td>
    </tr>

    <tr>
      <td>
        **Select Attributes to Create a Facet**
      </td>

      <td>
        Choose the product attribute from the catalog.
      </td>
    </tr>

    <tr>
      <td>
        **Display Name**
      </td>

      <td>
        The name of the attribute as it should appear on the site.
      </td>
    </tr>

    <tr>
      <td>
        **Facet Type**
      </td>

      <td>
        Choose either "Text" or "Range".
      </td>
    </tr>

    <tr>
      <td>
        **Sort Order**
      </td>

      <td>
        Choose how to sort the facet values:

        * Product Count: Sort by the number of products.
        * Alphabetically: Sort alphabetically.
      </td>
    </tr>

    <tr>
      <td>
        **Facet Length**
      </td>

      <td>
        The maximum number of facet values to display.
      </td>
    </tr>

    <tr>
      <td>
        **Status**
      </td>

      <td>
        Set to "Enable" to display the facet on the site.
      </td>
    </tr>
  </tbody>
</Table>

### Edit and Manage Facets

To edit a facet, click **Edit** next to the selected facet. Modify the necessary fields, such as **Display Name**, **Sort Order**, or **Status**. Click **Save** to apply changes.

> 📘 Note
>
> If the facet is enabled at multiple places, some fields like Display Name or Field Name might not be editable.

### Delete a Facet

To delete a facet, click **Delete** next to the facet. Confirm the deletion by clicking **Yes** in the pop-up message.

> ❗️ Warning
>
> Once a facet is deleted, it cannot be recovered. If you simply don’t want to display a facet, consider disabling it instead of deleting it.

### Change the Ranking of Facets

To adjust the order of facets, click the three dots next to a facet under the Ranking column. Set the new ranking position in the pop-up box. Click **OK** to save the changes.

> 📘 Note
>
> You can view the facet configuration in a graphical format to easily adjust the ranking.

## AI Recommendations for Facets

Unbxd’s AI recommendations automatically suggest probable facets based on tracking your catalog. To enable AI recommendations:

1. Click **Apply AI recommendations** to view the list of recommended facets. If you’ve added new fields to your catalog, click **Refresh AI recommendations** to update the list.

### Facet Features

**Multiselect Facet:** Allows users to select multiple values within a facet or across facets, refining the search results.

1. **AND**: Filters products matching all selected conditions.
2. **OR**: Filters products matching at least one selected condition.

**Displaying Exact Value Count of Facets** The facet algorithm shows the exact count of values for each facet, allowing customers to know how many products are present in each facet.

**Sorting in Facet**: You can configure facets to be sorted by:

1. Product Count
2. Alphabetical Order

**Flexibility to Modify Facet Position**: Use drag-and-drop to change the order of facets on the site to match business needs.

**Different Facets for Different Category Pages**: Customize facets based on the category. For example, facets for "shirts" may include brand, size, and price, while facets for "smartphones" may include brand, RAM, and OS.

**Breadcrumbs**:Display the position of search results within the category hierarchy.

**Disabling Facets**: If you don’t want a facet to be displayed on your site, change the status to "Disable" instead of deleting it. You can enable it again later.

## Edit and Publish Facet Rules

1. To Edit the “All Queries” Rule, navigate to **Merchandising** > **Search** > **Facets** in the console. Click the **Edit** icon next to the "**All Queries**" rule. Modify the facets as needed (e.g., Display Name, Sort Order). Click **Apply Changes,** then **Publish Rule** to make the changes live.
2. To Create a Field-based Facet Rule: Navigate to Field Settings and select the attributes you want to merchandise.
   * Set Up the Campaign: Choose the attributes for the condition (e.g., "Sneakers") and specify facet items.
   * Configure the Facets: Define properties like Display Name, Facet Length, and Sort Order.
   * Publish the Rule: Click Save for a draft or Publish Rule to make it live.
3. View and Manage Facet Campaigns, navigate to **Merchandising** > **Search** > **Facets**. The Facets Overview page shows all campaigns (draft or live). Use filters to find campaigns based on criteria like **Status**, **Created By**, or **Query**.
4. Additional Actions for Facet Campaigns

* Stop Active Campaigns: Temporarily halt a campaign without deleting it.
* Bulk Upload: Upload multiple facet rules at once.
* Bulk Download: Download existing facet rules for backup or review.