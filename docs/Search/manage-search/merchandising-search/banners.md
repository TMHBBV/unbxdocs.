---
title: Banners
excerpt: Publish query and field-based Banners
deprecated: false
hidden: false
metadata:
  robots: index
---
.

# Overview

The **Banners** section allows you to effectively promote products, brands, special offers, or seasonal sales directly on your platform. With a single click, shoppers can be redirected to the desired landing page, ensuring a seamless user experience.

***

## Types of Banners

### Query-based Banner

Query-based banners are tied directly to specific **search queries**. They appear on the search results page when the **merchandised query matches the shopper's query**. Ideal for promoting brands, offers, or events explicitly related to what the shopper is searching for.

**How It Works:**

1. Define a specific query in the **Merchandising Workbench**.
2. When a shopper enters that query, the banner is displayed at the top of the search results page.

**Use Cases:**

* For the query **“Woolen jacket”**, display a banner:\
  *“Flat 20% Off on Winter Wear – Limited Time Offer!”*
* For the query **“Gaming Laptops”**, display a banner:\
  *“Buy a Gaming Laptop Today and Get Free Accessories!”*

***

### Field-based Banner

These banners are **contextually triggered** based on the products in the search results. Displayed when **more than 80%** of the results match specified **field rule criteria** (e.g., category, product type, brand).

**How It Works:**

1. Define field rule criteria, e.g., `Product Type: Running Shoes` or `Brand: Nike`.
2. If 80%+ of search results match this rule, the banner appears.

**Use Cases:**

* If a shopper searches **“Running Shoes”** and 80% belong to the **Nike** brand, show:\
  *“Shop Nike Shoes at 10% Off”*
* For **“Cost-friendly smartphones”** where most results are under `$500`, show:\
  *“Exclusive Offers on Cost-Friendly Mobiles!”*

> 📘 **Tip**:
>
> * Use **Query-based Banners** for predefined search control.
> * Use **Field-based Banners** for dynamic, product-driven promotions.

***

## Banner Asset Setup

You can configure your banner in two ways:

1. **Use a Pre-Designed Image**
2. **Write Custom HTML Code**

### 1) Pre-Designed Image

* **Banner Image URL**: Link to your hosted image.
* **Destination URL**: The URL to redirect users upon click.

> 📘 **Note**: Ensure the image URL is **publicly accessible**.

### 2. HTML Code

You can create custom banners with HTML. Here’s an example:

```html
<div style="width: 100%; background-color: #f8f9fa; padding: 20px; text-align: center; border: 1px solid #ccc;">
  <a href="https://example.com/cost-friendly-mobiles" style="text-decoration: none; color: inherit;">
    <img src="https://example.com/banner-image.jpg" alt="Exclusive Offers on cost-friendly mobiles!" style="max-width: 100%; height: auto; border-radius: 8px;">
    <h2 style="font-family: Arial, sans-serif; color: #333; margin-top: 10px;">Exclusive Offers on Cost-Friendly Mobiles!</h2>
    <p style="font-family: Arial, sans-serif; color: #555; font-size: 16px;">Click here to shop now and save big!</p>
  </a>
</div>
```

**Code Breakdown:**

* `<div>`: Banner container with styling
* `<a>`: Entire banner is clickable
* `<img>`: Displays banner image
* `<h2>` and `<p>`: Banner message and CTA

***

## Setting Up a Query-Based Banner

### Step-by-Step:

1. Log in to [Netcore Unbxd Console](https://console.unbxd.io/).
2. Select your **Site Key**.
3. Go to **Merchandising > Search > Banners**.

### Create a Campaign:

1. Click **New Banner > Query-Based Banner**.
2. Enter the **Query** (shopper's search term).
3. Click **+ Apply same rule to more queries** to add more.
4. Add a **Campaign Name** for internal tracking.
5. Choose a **Segment** or **Create New Segment**.
6. Set **Duration** (Start/End time, Time Zone).

   * Optionally enable **Run Perpetually**.
7. Add an optional **Description**.
8. Click **Next**.

### Configure Banner:

* Add either the **HTML Code** or the **Pre-designed Image URL + Destination URL**.

### Save or Publish:

* Click **Save Draft** or **Publish Rule**.

***

## Banners Overview Page: Actions You Can Take

You can manage campaigns through the **Overview Page**:

1. View all campaigns
2. Configure field settings
3. Edit or delete campaigns
4. Publish draft campaigns
5. View campaign rule summaries
6. Duplicate campaigns
7. Add multiple queries to one rule
8. Launch new campaigns for the same query
9. Stop active campaigns
10. Preview live site with banner
11. Bulk upload banners via CSV
12. Import/export banners across sites

***

## Accordion Help Topics

<details>
  <summary><strong>How to view a list of all campaigns?</strong></summary>
  Select the **Site Key**, go to **Merchandising > Search > Banners** to view all campaigns.
</details>

<details>
  <summary><strong>How to edit or publish a draft campaign?</strong></summary>

  1. Locate the campaign.
  2. Click **Edit**, make changes.
  3. Click **Publish Rule** to go live.
</details>

<details>
  <summary><strong>How to view rule summary?</strong></summary>
  Click the **Eye Icon** on the right side of the campaign row to view details.
</details>

<details>
  <summary><strong>How to apply same rule to more queries?</strong></summary>
  💡 **Note**: This applies **only** to Query-based Banners.
</details>

<details>
  <summary><strong>Why create multiple banners for the same query?</strong></summary>
  To test different creatives or messaging for performance comparison.
</details>

<details>
  <summary><strong>How to duplicate a campaign?</strong></summary>

  1. Click **More Options > Duplicate Rule**.
  2. Edit as needed (avoid overlapping dates).
  3. Save or publish.
</details>

<details>
  <summary><strong>How to create new campaigns for the same query?</strong></summary>

  1. Click **More Options > Add Another Campaign**.
  2. Configure as needed.
  3. Save as Draft or Publish.
</details>

<details>
  <summary><strong>How to stop active campaigns?</strong></summary>
  💡 **Note**: For Field-based banners, you must delete the campaign.
</details>

<details>
  <summary><strong>How to preview banners live on site?</strong></summary>
  Click **More Options > Search Preview** to view the banner on the site.
</details>

<details>
  <summary><strong>How to bulk upload banners?</strong></summary>

  1. Go to **More Options > Bulk Upload Banners**.
  2. Upload CSV (use sample template).
  3. Select **override** option if needed.
</details>

<details>
  <summary><strong>How to import banners from another site?</strong></summary>

  1. Go to **More Options > Import Rule**.
  2. Choose **Source Site** and select campaigns.
  3. Click **Import**.\
     💡 Conflicting rules will be overridden.
</details>

<details>
  <summary><strong>How to export banner campaigns?</strong></summary>
  Click **More Options > Bulk Download Banners** to export campaigns as a CSV.
</details>

<details>
  <summary><strong>How to delete a banner campaign?</strong></summary>
  💡 Deleting is the only way to stop Field Rule banners from showing.
</details>