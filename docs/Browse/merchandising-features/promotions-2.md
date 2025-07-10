---
title: Promotions
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The Promotions feature in the Netcore Unbxd Self Serve Console allows retailers to strategically control product placement on Search Results Pages (SRPs). By leveraging this tool, businesses can prioritize or hide products, pin or slot items in specific positions, and organize listings to align with marketing goals. Promotions enhance user experience and drive sales by ensuring that relevant and high-priority products get the visibility they deserve.

## Prerequisites

Before setting up promotions, ensure the following are in place:

1. Complete Product Catalog is uploaded and updated.
2. Ensure product attributes are accurate and comprehensive to create effective promotion rules.
3. You have the required access to the Netcore Unbxd Self Serve Console with merchandising privileges.

# Promotion Strategy

Utilize Netcore Unbxd following Promotional strategies to target merchandising tactics to prioritize, organize, and test product visibility to maximize engagement and sales.

| **Strategy**          | **Description**                                                                         | **Example**                                                                             |
| --------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Boost Products**    | Raise priority for specific products to appear higher in search results.                | Outdoor gear store boosts “insulated water bottles” for “camping essentials” searches.  |
| **Bury Products**     | Hide irrelevant or unwanted products from specific searches.                            | Beauty store hides products with animal ingredients when users search “vegan.”          |
| **Pin Products**      | Fix products to specific positions in search results.                                   | Fashion retailer pins “winter coats” at the top for “outerwear” searches.               |
| **Slot Products**     | Assign multiple products to fixed ranks in search results for strategic placement.      | Electronics store slots “noise-canceling headphones” in top positions for “headphones.” |
| **Sort Listing Page** | Organize products by attributes like price or alphabetical order.                       | Furniture store sorts products A-Z by brand for easier navigation.                      |
| **A/B Testing**       | Experiment with different merchandising strategies to find what drives best engagement. | Test promoting new arrivals vs. best-sellers for the same query.                        |
| **Landing Pages**     | Create custom pages for themes or promotions to showcase relevant products together.    | “Back to School” page featuring backpacks and stationery                                |

## Types of Promotion Rules

1. **Global Rule**\
   Applies universally to all queries and segments. Only one per site. Automatically created when the site is set up. It supports Boost/Bury or Filter strategies.
2. **Query-Specific Rules**\
   Tailored to specific search queries or customer segments. Supports Boost/Bury, Sort, Pin, Slot, and Filter strategies. **Query-specific rules override Global Rules**.

Example: Global Rule boosts “Summer Dresses” everywhere, but a query-specific rule for “Winter Sale” hides them.

### How to Use Promotions

<Image align="center" border={true} caption="Navigate to Promotions" src="https://files.readme.io/e0f7922894abc3c2d6e6741fccfbe52186f479339a0f25cdf11b9ec39fa58dd3-promotions.gif" width="80% " />

Log in to the Netcore Unbxd Console. Select the site you want to put the strategy and navigate to **Merchandising** > **Search** > **Promotions**.

You can perform following actions from the Promotions overview page. You can perform the below actions:

| **Action**          | **Description**                                                                         |
| ------------------- | --------------------------------------------------------------------------------------- |
| **Create**          | Design and set up a new promotion campaign or offer from scratch.                       |
| **Edit**            | Modify the details or parameters of an existing promotion to optimize performance.      |
| **Publish**         | Activate the promotion, making it live and visible to customers.                        |
| **Preview**         | Review how the promotion will appear to users before going live.                        |
| **Duplicate**       | Copy an existing promotion to quickly create a similar campaign with slight variations. |
| **Stop**            | Pause or terminate an ongoing promotion to prevent further customer exposure.           |
| **Bulk Upload**     | Upload multiple promotions or promotional assets at once to streamline campaign setup.  |
| **Export to email** | Share promotion details or reports via email for collaboration or review.               |
| **Import Rule**     | Bring in predefined promotion rules or criteria from external sources for consistency.  |

> 📘 Note
>
> Avoid using overlapping active campaigns for the same query and segment to prevent conflicts.

### View and Manage Campaigns

1. **View All Campaigns**\
   Navigate to **Merchandising** > **Search** > **Promotions** to view all launched campaigns. Campaigns are grouped by query and show details like date range, applied segment, current status, type (Merchandised Page or Landing Page), and campaign performance data.
2. **Search Campaign**\
   To find a campaign/query using Filters use the search bar to find campaigns by entering the associated query or apply filters based on status, page type, date range, created by, segment, or collection to narrow your search.
3. **Summary of the rules added to campaign**\
   Click the **Eye icon** next to the campaign to view a summary of the rules applied.

### Edit and Modify Campaigns

1. **Edit an existing campaign**\
   Locate the campaign and click the **Edit icon** to make necessary changes. After editing, click Publish rule to make the campaign live.
2. **Applying the same rule to additional queries**\
   Click the **More options** icon, select **+** Apply same rule to more queries, and add the additional queries. The rules from the original query will apply to the new queries.
3. **Create new campaigns for the same query**\
   Duplicate an existing campaign or create a new one for the same query. Creating a new campaign requires configuring rules from scratch, while duplicating carries over existing rules.
4. **Duplicate existing campaigns**\
   Click the More options icon, select Duplicate Rule, and a copy of the campaign will be created. You can then edit the new campaign and save it as a draft or publish it.
5. **Stop active campaigns**\
   Locate the campaign, click the More Options icon, and select Stop promotions to stop it from being live.

### Campaign Preview and Testing

1. **Preview the site with the campaign rules applied**\
   Click the More options icon and select Search preview to view the campaign results on a preview site.
2. **Customize the quick preview**\
   Access **Performance Metrics** and **Insights** by clicking the More Options button to toggle between Site Performance and Query Performance, and choose between List View or Grid View to display products.

### Bulk Actions

1. **Bulk upload Promotion rules**\
   Use the Bulk Upload Promotions option under More Options to upload promotion rules via a JSONL file. The file can be uploaded by dragging or browsing, and you can choose to override existing rules.
2. **Import campaigns from one site to another**\
   Use the Import Rule option under More Options to import campaigns from one site to another. You can select the source site, review campaigns, and click Import.
3. **Export existing campaigns**\
   Click **Export** to Email under More Options to receive a JSON file with your campaign data via email.

### Campaign Performance and Analytics

1. **Access campaign performance data**\
   On the Promotion overview page, find the overall campaign performance. For product-specific performance, use Quick Preview to view Site Performance and Query Performance metrics.
2. **View product-specific performance**\
   In the Quick Preview page, enable Site Performance and Query Performance to view key metrics for individual products and how they performed for specific queries.

### Delete Campaigns

1. **Delete an existing campaign**\
   Locate the campaign, click the More options icon, and select Delete Rule to remove it.

## Create New Promotion

<Image align="center" border={true} caption="Add New Promotion" src="https://files.readme.io/951685b28a6d6f5697c390b0a7938da46800c897491491e0f271d9c2a1d4c0af-Merchandising_Promotions.gif" width="80% " />

Query-specific merchandising rules allow you to customize promotions for specific queries or segments, offering a more targeted approach to shopper engagement. Navigate to **Merchandising** > **Search** > **Promotions** > **Add promotions**. Following parameters is mandatory to fill.

<Table>
  <thead>
    <tr>
      <th>
        **Parameter**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Query**
      </td>

      <td>
        Define the search query (e.g., winter boots) that will trigger the redirect.
      </td>
    </tr>

    <tr>
      <td>
        **Campaign Name**
      </td>

      <td>
        Assign a name to the promotion rule.
      </td>
    </tr>

    <tr>
      <td>
        **Segment**
      </td>

      <td>
        Specify the user segment this promotion applies to or click + Create New Segment to make a custom/new one.
      </td>
    </tr>

    <tr>
      <td>
        **Campaign Duration**
      </td>

      <td>
        Set the time period during which the promotion will be active.
        For an open-ended campaign, enable **Run Perpetually**. This option allows you to run any campaign until it is manually stopped.
      </td>
    </tr>

    <tr>
      <td>
        **Campaign Description**
      </td>

      <td>
        Provide a brief description of the promotion’s purpose.
      </td>
    </tr>
  </tbody>
</Table>

> 📘 Note
>
> As you update the **Query** name, the instant preview will display products relevant to the query and show the total number of applicable products.

Once the details are in place, click **Next** to add an extensive optional options to strategically control product placement on Search Results Pages.