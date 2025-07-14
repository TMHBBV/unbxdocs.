---
title: Add New Promotion
deprecated: false
hidden: false
metadata:
  robots: index
---
Query-specific merchandising rules allow you to customize promotions for specific queries or segments, offering a more targeted approach to shopper engagement.

## Navigate to the Promotions section

1. Login to Netcore Unbxd’s [self-serve console](https://console.unbxd.io/) ↗
2. From the **Site Key Picker**, click the site you want to apply a merchandising strategy.
3. After selecting the appropriate site key, navigate to **Merchandising**.
4. Hover over **Search** and click **Promotions**.

## Create new Promotion

Set Rule Conditions

| Parameters               | Description                                                                 |
| ------------------------ | --------------------------------------------------------------------------- |
| **Query**                | Define the search query (e.g: winter boots) that will trigger the redirect. |
| **Campaign Name**        | Assign a name to the promotion rule                                         |
| **Segment**              | Specify the user segment this promotion applies to.                         |
| **Campaign Duration**    | Set the time period during which the promotion will be active.              |
| **Campaign Description** | Provide a brief description of the promotion’s purpose.                     |

* On the Promotions overview page, click **New Promotion**.

* You will be redirected to the **Add Rule interface**.

* Enter the **Query** for which you want to set up merchandising rules, this is the search term you expect your shopper to use.

  As you update the query name, the instant preview will display products relevant to the query and show the total number of applicable products.

* Enter a Campaign Name for internal reference.

* Select a \*\*Segment \*\*from the list to target specific shopper groups or click + Create New Segment to make a custom/new one.

* Set the Duration for the campaign, including the Time Zone, Start and End dates, and times.

  For an open-ended campaign, enable Run Perpetually. This option allows you to run any campaign until it is manually stopped.

* Optionally, add a Description for future reference.

* When finished, click Next to proceed.

### Create Landing Pages (Optional)

Landing Pages are dedicated custom results pages built for specific queries. Merchandiser-driven landing pages offer full control, letting you access your entire catalog, override algorithms, and curate the search results using merchandising strategies.

* To create landing pages, toggle the option to green. Once enabled, the preview section will display all the products in your catalog.

If you prefer to add customizations on top of the search results produced by Netcore Unbxd AI and don't want to access your complete catalog, you can proceed without enabling the Landing Page option (keep it in its default disabled state).

### AI-Suggested Queries

AI-Suggested Queries recommend relevant search terms and category-based recommendations based on past search patterns, user behavior, popular searches, and semantic understanding.

This helps users refine their queries, discover products efficiently, and reduce zero-result searches.

**Example**

If you enter `White Dresses` as a query, the algorithm will surface related terms like:

white dress, white shoes, white bag, white sneakers, and so on.

Click the "`+`" icon next to each query you want to include, then click **Apply Changes**. The same rules will now apply to all the selected queries.

### Associate Collections (Optional)

You can use Collections to associate a curated product set with the landing page by selecting one or multiple Collections from the drop-down menu. You can create new ones by clicking + Create New Collection.

* After associating Collections with the landing page, the preview will update to display only the products included in the selected Collections

### Set up A/B test (Optional)

You can enable the A/B test option to compare two strategies you’ve curated or pit your merchandising strategy against Netcore Unbxd's default result set.

1. Traffic split: Choose how to divide traffic between variations, with options like 50-50, 60-40, or 70-30. Ensure the total equals 100%.
2. Select a KPI: Determine the key metric to decide the winning strategy. Use the Winner is decided by drop-down to choose from Click Rate, Average Order Value, Revenue Per Visit, Conversion Rate, or Cart Rate.
3. Set test duration: Specify the test duration, which should be shorter than the overall campaign timeline.
4. Fallback strategy: Select a preferred fallback variation from the Preferred option in case there is no winner drop-down. This will ensure the campaign continues seamlessly even if no winner is determined during the test period.
5. Once done, click Apply.
6. You can now proceed with configuring the merchandising strategy.
   * If testing Variation A against Variation B, you’ll need to customize the result set for each variant.
   * If testing Variation A against Netcore Unbxd’s default result set, you’ll only need to set the strategy for Variation A.

### Design your merchandising strategy

With Query-specific rules, you can create rules using one or a combination of these options:

* [Boost/Bury](/user-guides/merchandising/promotions/boost): Increase or decrease product visibility.
* [Sort](/user-guides/merchandising/promotions/sort): Arrange products based on specific criteria.
* [Pin](/user-guides/merchandising/promotions/pin): Fix key products at any exact position from 1 to 50.
* [Slot](/user-guides/merchandising/promotions/slot): Assign multiple products to predefined positions in a single go.
* [Filter](/user-guides/merchandising/promotions/filter): Exclude or include products from a superset.