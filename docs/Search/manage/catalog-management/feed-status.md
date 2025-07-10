---
title: Feed Status
excerpt: Track if your catalog feed is in sync with Unbxd.
deprecated: false
hidden: true
metadata:
  robots: index
---
# Overview

The **Feed Status** section in the Netcore Unbxd Console allows you to **monitor the status of your catalog feed uploads** and verify whether your product data is successfully indexed. This ensures that your online store remains in sync with the latest catalog data submitted to Unbxd.

***

## Key Capabilities

* To track the **current indexing status** of the catalog feed.
* To verify details such as the **type of upload**, **number of products processed**, and **time taken** for indexing.
* To ensure the catalog feed has been properly received and processed by the Unbxd system.

***

# Navigate to Feed Status

<Image align="center" border={true} caption="Track the Status of your Catalog Feed" src="https://files.readme.io/c6b7d3b213edfe396254284cf660b49fd7944b345d587e7d1c5943f606628675-feedStatus.gif" width="80% " />

1. Log in to the Netcore Unbxd console.
2. Navigate to **Manage Catalog** > **Feed Status**. Refer to the given table to know the fields available here.

| Field              | Description                                                                                                |
| ------------------ | ---------------------------------------------------------------------------------------------------------- |
| **Feed File Name** | The name of the uploaded feed file. The `[REINDEX]` label indicates a full reindex of the product catalog. |
| **Status**         | Displays the current processing status of the feed. Possible values include:                               |

# Use Case

If you uploaded a catalog feed and want to confirm it was processed correctly:

1. Go to the **Feed Status** tab.
2. Check the row corresponding to your latest upload.
3. Confirm that:

   * **Status** = `INDEXED`
   * **Product Count** matches your expected number of products.
   * **Upload Type** shows `REINDEX` or `INCREMENTAL`, as applicable.

If the feed has failed, you may need to:

* Review the feed structure.
* Check for formatting errors or missing mandatory fields.
* Re-upload after correction.

***

> 👍 Best Practices
>
> * Regularly check the **Feed Status** after each catalog update to ensure consistency.
> * Use the **REINDEX** type when replacing the entire catalog.
> * Use **INCREMENTAL** uploads for faster updates to limited sets of products.
> * Monitor indexing time to detect any significant performance changes in feed processing.