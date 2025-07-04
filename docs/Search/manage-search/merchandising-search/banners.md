---
title: Banners
excerpt: Publish query and field-based Banners
deprecated: false
hidden: true
metadata:
  robots: index
---
# Overview

The Banners section allows you to effectively promote products, brands, special offers, or seasonal sales directly on your platform. With a single click, shoppers can be redirected to the desired landing page, ensuring a seamless user experience.

## Types of Banners

### Query-based Banner

These banners are directly tied to search queries. They appear on the search results page when the merchandised query matches the shopper query. They are ideal for promoting brands, offers, or events explicitly related to what the shopper is searching for.

**How It Works:**

1. You define a specific query in the Merchandising Workbench.
2. When a shopper enters that query, the corresponding banner is displayed at the top of the search results page.

**Use Case**:

* For the query “Woolen jacket”, a banner saying “Flat 20% Off on Winter Wear – Limited Time Offer!” with relevant visuals can be displayed.
* For the query “Gaming Laptops”, the visual for a banner saying “Buy a Gaming Laptop Today and Get Free Accessories!” can be shown.

### Field-based Banner

Field-based banners are contextually triggered based on the products retrieved in the search results. They are displayed when more than 80% of the retrieved products match specific criteria such as category, product type, or brand defined by you.

**How it works**:\
Field-based banners are perfect for dynamically adapting promotions to the dominant category or product type in the search results, ensuring highly relevant messaging.

1. Define field rule criteria (e.g., Product Type: Running Shoes or Category: Electronics).
2. If 80% or more of the search results satisfy the field rule, the corresponding banner is displayed.

**Use Case**:

* If a shopper searches for “Running Shoes”, and 80% of the results belong to “Nike” of the Brand Attribute, a banner saying “Shop Nike Shoes at 10% Off” can appear.
* If the shopper searches for “Cost-friendly smartphones”, and the majority of results are within the price range of “$ 500”, a banner saying “Exclusive Offers on cost-friendly mobiles!” can be displayed.

> 📘 Note
>
> * Use Query-based Banners when you want to control banners for specific, predefined searches.
> * Use Field-based Banners for dynamic, context-driven banners that respond to the product mix in the search results.

## Assets required

You can configure your banner in two ways:

1. Use a pre-designed image
2. Write HTML Code

### Use a pre-designed image

If you already have a designed banner image:

* Enter the Banner Image URL: Provide the link to your banner image hosted on a platform of your choice.
* Set the Destination URL: Add the link where shoppers will be redirected upon clicking the banner.

> 📘 Note:
>
> Ensure the banner image URL is publicly accessible to avoid display issues.

### Add HTML code

If you prefer to design your banner using HTML instead of an image, you can directly enter the HTML code along with all the necessary details.

Here's an example HTML code for a banner with the text "Exclusive Offers on cost-friendly mobiles!":

```html
<div style="width: 100%; background-color: #f8f9fa; padding: 20px; text-align: center; border: 1px solid #ccc;">
  <a href="https://example.com/cost-friendly-mobiles" style="text-decoration: none; color: inherit;">
    <img src="https://example.com/banner-image.jpg" alt="Exclusive Offers on cost-friendly mobiles!" style="max-width: 100%; height: auto; border-radius: 8px;">
    <h2 style="font-family: Arial, sans-serif; color: #333; margin-top: 10px;">Exclusive Offers on Cost-Friendly Mobiles!</h2>
    <p style="font-family: Arial, sans-serif; color: #555; font-size: 16px;">Click here to shop now and save big!</p>
  </a>
</div>
```

Code explanation:

1. **div** block: Contains the banner with styles for width, padding, and background color.
2. Anchor tag (**\<a>**): Makes the entire banner clickable, linking to the product or offer page.
3. Image (**\<img>**): Displays the banner image with a responsive design.
4. Heading (**\<h2>**): Highlights the banner's main message.
5. Paragraph (**\<p>**): Provides an additional call to action or descriptive text.

## Set up Query-based Banner

"Navigate to the Banners section"1) Login to Netcore Unbxd’s [self-serve console](\[https://console.unbxd.io/]\(https://console.unbxd.io/\)) ↗
2) From the **Site Key Picker**, click the site you want to apply a merchandising strategy.
3) After selecting the appropriate site key, navigate to **Merchandising**.
4) Hover over **Search** and click **Banners**.

```
```

"Setting up the campaign"1) On the Banners overview page, navigate to New banner and then click Query-based banner.
2) You'll go to the Add banners interface.
3) Enter the Query for which you want to set up banners for—this is the search term you expect your shopper to use.
   1. To apply the same rule to additional queries, click + Apply same rule to more queries, add queries separated by commas, and press Enter.
4) Enter a Campaign Name for internal reference.
5) Select a Segment from the list to target specific shopper groups or click + Create New Segment to make a custom/new one.
6) Set the Duration for the campaign, including the Time Zone, Start and End dates, and times.
   1. For an open-ended campaign, enable Run Perpetually. This option allows you to run any campaign until it is manually stopped.
7) Optionally, add a Description for future reference.
8) When finished, click Next to proceed.

"Configuring the banner"\
Put in the HTML code of the pre-designed image based on your preference.

"Saving or publishing the banner"\
After applying the rule, you can do one of the following.

## Banners overview page

Apart from adding new banner rules via the overview page, you can,

1. View a comprehensive list of all campaigns
2. Configure field settings
3. Edit existing campaigns
4. Publish draft campaigns to the live site
5. View summary of campaign rules
6. Duplicate existing campaigns
7. Apply the same rule to additional queries
8. Create new campaigns for the same query
9. Stop active campaigns
10. Preview how the site will look with the banner
11. Bulk upload banners for efficiency
12. Import banners from one site to another
13. Bulk download existing banner rules

\<Accordion title="How to view a comprehensive list of all the campaigns I launched?">\
To view a comprehensive list of all your banner campaigns, select the site key, click **Merchandising**, navigate to **Search**, and then **Banners**.

\<Accordion title="How to edit an existing campaign or publish a draft campaign?">1) Locate the campaign you wish to modify.
2) Click the **Edit** icon to open the campaign.
3) Review and make necessary changes.
4) Click **Publish Rule** to make the campaign live.
   \</Accordion>

\<Accordion title="How to view a summary of the rules I added to my campaign?">\
To view the summary of a specific banner, locate the campaign in the list and click the **Eye** icon at the far-right end of the row.
\</Accordion>

\<Accordion title="How to apply the same rule to additional queries?">\
💡 **Note**: This applies only to Query-based Banners. Field rules are applicable across all queries.

\<Accordion title="Why create different banners for the same query?">\
Creating different banners for the same query enables you to:

```
```

```
```

```
```

\<Accordion title="How to duplicate existing campaigns?">1) Locate the campaign to duplicate.
2) Click the **More Options** icon and select **Duplicate Rule**.
3) Edit the duplicated banner as needed, ensuring no overlapping date ranges.
4) Save the campaign as a **Draft** or publish it live by clicking **Publish Rule**.
   \</Accordion>

\<Accordion title="How to create new campaigns for the same query?">1) Locate the campaign to modify.
2) Click the **More Options** icon and select **Add Another Campaign**.
3) Configure the banner settings as needed.
4) Save as a **Draft** or publish it live by clicking **Publish Rule**.
   \</Accordion>

\<Accordion title="How to stop active campaigns?">\
💡 **Note**: For Field Rule banners, you must delete the campaign.

```
```

\<Accordion title="How to preview the site with the campaign rules applied?">1) Locate the campaign to preview.
2) Click the **More Options** icon and select **Search Preview**.
3) Review the banner and its details on the preview site.
   \</Accordion>

\<Accordion title="How to bulk upload banners?">1) Navigate to the **More Options** button and select **Bulk Upload Banners**.
2) Upload the CSV file (download the sample file for reference).
3) If overriding existing rules, check the corresponding option.
4) Imported banners will appear on the Overview page.
   \</Accordion>

\<Accordion title="How to import banners from one site to another?">1) Navigate to the **More Options** button and select **Import Rule**.
2) Choose the **Source Site**.
3) Select the query and campaigns to import.
4) Click **Import** to complete the process.
   💡 **Note**: Imported campaigns with conflicts will override existing rules.
   \</Accordion>

\<Accordion title="How to export existing banner campaigns?">1) Navigate to the **More Options** button and select **Bulk Download Banners**.
2) A CSV file containing campaign data will be downloaded.
   \</Accordion>

\<Accordion title="How to delete an existing banner campaign?">\
💡 **Note**: Deleting a campaign is the only way to stop Field Rule banners from displaying.

```
```