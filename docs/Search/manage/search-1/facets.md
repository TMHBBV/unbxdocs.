---
title: Facets
excerpt: Customize Facets based on query and fields
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Facets are essential for narrowing down search results and helping shoppers find products more efficiently. On a Product Listing Page (PLP), a single query may return hundreds of products. By using product attributes as facets, users can filter and refine listings, enhancing their shopping experience.

***

## Advantages of Using Facets

### 1. Increases Product Discoverability

* Streamlines the product search process.
* Offers targeted filters to reduce unnecessary scrolling.

### 2. Fewer Clicks to the Desired Product

* Helps users avoid navigating through multiple pages.
* Allows quick access to specific product options.
* Simplifies navigation across different product variations.

### 3. Higher Conversion Rate

* Accelerates time-to-product discovery.
* Reduces decision fatigue and helps in faster purchase decisions.
* Creates a smoother shopping journey, leading to increased conversions.

***

## Types of Facet Merchandising

### 1. All Queries

* Applied globally to all search queries and shopper segments.
* Only one "All Queries" rule can exist per site.
* Acts as the default facet configuration.
* Automatically created during site setup.

**Example:**

On an eCommerce site, an "All Queries" rule might include:

* **Price**: Filter by price range.
* **Brand**: Show all available brands.
* **Customer Ratings**: Filter by product ratings.

These facets appear regardless of query—for example, for both "laptops" and "sneakers."

***

### 2. Field-Based Facets

* Applied dynamically based on the characteristics of search results.
* Activated only when **80% or more** of products in results match the defined condition.
* Field-based rules apply universally across queries but are based on product attributes rather than query intent.
* Query-specific facet rules override the "All Queries" rule.
* All campaigns are persistent until manually deleted.

**Example:**

If a “Sneakers” campaign is configured to trigger when 80%+ of results match the attribute "Type = Sneakers", then custom facets like **Activity Type**, **Material**, and **Style** will override the default facets for that session.

***

## Managing All Queries Rule

<Image align="center" border={true} caption="Configure Global Facets" src="https://files.readme.io/627c6a49e30de7e530a4a24a86938e58c296dda20576eb16f324bafd525ab17d-ManageSearch.gif" width="80% " />

### How to Locate and Edit

1. Log in to the [Netcore Unbxd Self-Serve Console](https://console.unbxd.io/).
2. Use the Site Key Picker to select your site.
3. Navigate to **Merchandising > Search > Facets**.
4. The "All Queries" rule appears first by default (in draft mode).

### How to Edit the Rule

1. Click the **Edit** icon in the top-right corner.
2. In the **Add/Configure Facets** section, click the **Edit** icon to open the list of facetable fields.
3. Use toggle switches to enable/disable specific fields.
4. Configure properties for each field:

   * **Display Name**: Facet label shown to users.
   * **Facet Length**: Max number of values shown.
   * **Sort Order**: Choose between Product Count, A–Z, etc.
5. Click **OK**, then **Apply Changes**.
6. Click **Publish Rule** to go live.

***

## Creating a Field-Based Facet Rule

### Step 1: Set Up the Campaign

1. On the **Facets Overview** page, click **New Facets**.
2. Choose an attribute from the dropdown (must be configured in Field Settings).
3. Define the value condition (e.g., *Type = Sneakers*).
4. Click **Next**.

### Step 2: Configure Facets

1. Click **+ Add Facets** to open the list of available fields.
2. Use toggles to show/hide each field.
3. Configure the following:

   * **Display Name**
   * **Facet Length**
   * **Sort Order**
4. Click **OK**, then **Apply Changes**.

### Step 3: Save or Publish

* **Save**: Keep the campaign as a draft.
* **Publish**: Make the facet rule live immediately.

***

## Facets Overview Page – What You Can Do

1. View all existing campaigns.
2. Configure field settings.
3. Edit or update existing campaigns.
4. Publish draft campaigns.
5. Stop active campaigns.
6. Bulk upload facet rules.
7. Bulk download existing facet rules.

***

## View All Campaigns

To view all your facet campaigns:

1. Select your site key.
2. Go to **Merchandising > Search > Facets**.

You will see a comprehensive list of all active, draft, and stopped facet campaigns.

***

## Bulk Upload Facet Rules

You can upload facet rules in bulk using a CSV file.

1. Navigate to **Facets Overview > More Options > Bulk Upload**.
2. Upload a correctly formatted CSV with your facet configurations.
3. Review and confirm the import.