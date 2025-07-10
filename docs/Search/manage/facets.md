---
title: Facets
excerpt: Customize Facets based on query and fields
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Facets are an essential tool to strategically narrow down search results for shoppers searching for their intended products. For a single query, the Product Listing Page (PLP) might display an overwhelming number of products. By using product attributes as facets, you can effectively refine and narrow down the listing, enhancing the shopping experience.

## Advantages of using Facets

1. Increases product discoverability

   Imagine scrolling through hundreds of products, navigating page after page, only to feel exhausted and frustrated. This is the typical experience of users who cannot quickly find the products they are looking for. Faceted navigation addresses this issue in multiple ways:

   * Streamlines the search process.
   * Provides targeted filters to reduce unnecessary scrolling.

2. Fewer clicks to the desired product

   Faceted search minimizes the effort required to find specific products:

   * Helps users skip the tiresome task of endless scrolling or browsing through multiple pages.
   * Users can find the desired product in just a few clicks.
   * Provides an intuitive way for users to navigate back and forth between different product options with ease.

3. Higher conversion rate

   By simplifying the path to the desired product:

   * Users can reach their products of interest more quickly.
   * Reduces decision fatigue, enabling users to make purchase decisions faster.
   * Facilitates a smoother shopping journey, leading to higher likelihood of completing a purchase.

## Types of Facet merchandising available

### All queries

* Applied universally across all search queries and shopper segments on the site.
* Only one "All Queries" rule can exist per site.
* Influences the facets displayed for all shopper searches by default.
* Automatically generated when the site is initially set up.

Example for the "All Queries" Rule:\
For an ecommerce site selling a wide range of products, you can define an "All Queries" rule to include facets like:

* Price: Allows filtering by price range across all product categories.
* Brand: Displays a list of brands regardless of the search query.
* Customer Ratings: Enables filtering by user ratings for all searches.

These facets ensure shoppers always have the essential filtering options available, irrespective of their search query. For instance, a search for "laptops" or "sneakers" would still show facets like *Price*, *Brand*, and *Customer Ratings*.

## Field-based Facets

Field-based facets dynamically adapt to the search results. These facets appear on the search results page only when 80% or more of the products match the specific attribute-value conditions you’ve defined.

* Field-based facet rules apply universally to all search queries. Unlike query-driven rules, they are determined by the characteristics of the search results rather than the query itself.
* Query-specific facet rules take precedence over the "All Queries" rule, ensuring tailored results for specific searches.
* All campaigns run indefinitely. To prevent a facet rule from being applied, you must delete the rule.

Example:

Imagine you've created a campaign called “Sneakers” with a facet condition for the attribute "Type" set to the value "Sneakers." Within this campaign, you've defined the facet items to be activity type, material, and style.

Now, when a shopper enters any query, if 80% or more of the search results are products categorized as "Sneakers," the system will replace the default facets with the merchandised ones like activity type, material, and style. This new configuration will override the preexisting facets, including those defined under the All Queries rule, ensuring a more relevant and streamlined browsing experience for shoppers.

## How to edit and publish the All queries rule?

title="Locate the All queries rule">

1. Login to Netcore Unbxd’s [<u>self-serve console</u>](https://console.unbxd.io/) ↗
2. From the Site Key Picker, click the site you want to apply a merchandising strategy.
3. After selecting the appropriate site key, navigate to Merchandising.
4. Hover over Search and click Facets.
5. On the Facets Overview page, the All queries rule is listed as the first item by default and is initially set to draft mode.

title="Edit the All queries rule">

1. Click the Edit icon in the top-right corner of the rule. *The targeted query cannot be changed.*
2. Under the Add/Configure Facets section, click the Edit icon. A window displaying all available facetable fields will appear.
3. In the Status section, use the toggle switch to show or not to show any specific fields.
4. Adjust the properties of each field as needed by clicking the edit icon of the respective field.
   * Display Name: Specify the name to be shown as the facet's title.
   * Facet Length: Set the maximum number of values to display for the facet field.
   * Sort Order: Determine the order in which the facet field values will appear.
5. After making the desired changes, click Ok and then Apply Changes.
6. Once satisfied with the configuration, click Publish Rule to make the changes live.

## How to create a field-based facet rule?

title="Configure the fields">
&#x20;   You can merchandise facets for up to 5 fields of your choice. To configure the fields:

&#x20;   1\. Go to the Facets Overview page and click the More Options button.
&#x20;   2\. Select Field Settings from the drop-down.
&#x20;   3\. Search for the attributes you want to merchandise and choose up to 5 fields.
&#x20;   4\. Once selected, click Apply.

&#x20;   You’re now ready to set up your facet campaign based on fields.
&#x20;&#x20;

&#x20; title="Set up the campaign">
&#x20;   1\. On the Facets Overview page, click New Facets.
&#x20;   2\. You’ll be directed to the Add Facets interface.
&#x20;   3\. From the drop-down menu, select the attribute you want to base the condition on. The options will match the attributes configured in Field Settings.
&#x20;      1\. If no options appear, navigate to Field Settings and configure the fields.
&#x20;   4\. After selecting the attribute, specify the value you want to use as the condition.
&#x20;   5\. Once finalized, click Next.


&#x20; \<Step title="Configure the facets">
&#x20;   1\. Click + Add Facets. A window displaying all available facetable fields will appear.
&#x20;   2\. In the Status section, use the toggle switch to show or not to show any specific fields.
&#x20;   3\. Adjust the properties of each field as needed by clicking the edit icon of the respective field.
&#x20;      1\. Display Name: Specify the name to be shown as the facet's title.
&#x20;      2\. Facet Length: Set the maximum number of values to display for the facet field.
&#x20;      3\. Sort Order: Determine the order in which the facet field values will appear.
&#x20;   4\. After making the desired changes, click Ok and then Apply Changes.
&#x20;    &#x20;
&#x20;title="Save or publish the facets rule">
&#x20;   After configuring the attributes to display, you can do one of the following.

&#x20;   1\. Click the Save button to retain the Campaign as a draft.
&#x20;   2\. Click the Publish rule button to push it live.
&#x20;

## What can you do with the Facets overview page?

1. View a comprehensive list of all campaigns
2. Configure field settings
3. Edit existing campaigns
4. Publish draft campaigns to the live site
5. Stop active campaigns
6. Bulk upload facets
7. Bulk download existing Facet rules

&#x20;title="How to view a comprehensive list of all the campaigns I launched?">
&#x20;   To view a comprehensive list of all your facet campaigns, select the site key, click \*\*Merchandising\*\*, navigate to \*\*Search\*\*, and then \*\*Facets\*\*.

&#x20;   \#### Key information on the campaign list

&#x20;   Campaigns are organized by query, with multiple campaigns for the same query grouped in a single row.

&#x20;   For each campaign, the following details are displayed:

&#x20;   \* \*\*Date Range\*\*: Always set to perpetual.
&#x20;   \* \*\*Segment\*\*: Always applied to all users.
&#x20;   \* \*\*Status\*\*: Indicates whether the campaign is \*Active\* or in \*Draft\*.

&#x20;   \#### Finding the campaign/query using Filters and the search bar

&#x20;   1\. Log in to \*\*Netcore Unbxd’s self-serve console\*\*.
&#x20;   2\. In the \*\*Site Key Picker\*\*, select the site where you want to apply the merchandising strategy.
&#x20;   3\. Once the site is selected, go to the \*\*Merchandising\*\* section.
&#x20;   4\. Hover over \*\*Search\*\* and click \*\*Facets\*\*.
&#x20;   5\. You’ll be directed to the \*\*Facets overview page\*\*, where you can view a list of all campaigns—draft or live.
&#x20;   6\. Use the search bar to find the campaign you want by entering the associated query.
&#x20;   7\. You can also apply filters to narrow your search and quickly locate the facet rule. You can filter campaigns based on the following criteria:
&#x20;      \* \*\*Status\*\* – Active, Draft
&#x20;      \* \*\*Created By\*\* – The user who created the campaign
&#x20;   8\. After selecting your desired filters, click \*\*Apply Filters\*\*.

&#x20;   The listing page will now display only the campaigns that match the filters you have applied.
&#x20;  title="How to edit an existing campaign or publish a draft campaign?">
&#x20;   If you have created a facet rule and saved it as a draft or want to make changes to a live campaign, follow these steps to publish it on the live site:

&#x20;   1\. Locate the campaign you wish to modify.
&#x20;   2\. Click the \*\*Edit\*\* icon to open the campaign.
&#x20;   3\. Review the Facet details and make necessary edits.
&#x20;   4\. After verifying all the changes, click \*\*Publish rule\*\* to make the campaign live.
&#x20; title="How to delete an existing facet rule?">
&#x20;   💡\*\*Note\*\*: Deleting the campaign is the only way to stop a facet rule from getting applied.

&#x20;   1\. Locate the campaign you wish to delete.
&#x20;   2\. Navigate to the \*\*More options\*\* icon at the far-right end of the row.
&#x20;   3\. Click \*\*Delete\*\* and confirm \*\*Delete\*\*.
&#x20; \</Accordion>

&#x20; \<Accordion title="How to Bulk upload Facet rules?">
&#x20;   You can bulk upload Facet rules as a CSV file. To do this:

&#x20;   1\. Navigate to the \*\*More Options\*\* button at the top and select \*\*Bulk upload facets\*\*.
&#x20;   2\. Upload the file by either dragging and dropping it or clicking \*\*Upload File\*\*. You can download a sample CSV file for reference purposes.
&#x20;   3\. If you want to override existing rules, check the corresponding option.
&#x20;   4\. Once the upload is complete, the imported Facet rules will appear on the Overview page.
&#x20; title="How to export existing facet rules?">
&#x20;   You can download all your existing facet rules as a CSV file.

&#x20;   1\. Click the \*\*More Options\*\* button at the top and select \*\*Bulk download facets\*\*.
&#x20;   2\. Once initiated, a CSV containing all your campaign data will get downloaded to your local system.
&#x20;&#x20;