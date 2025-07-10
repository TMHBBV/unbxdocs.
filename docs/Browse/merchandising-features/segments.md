---
title: Segments
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

**Segments** in UNBXD Browse allow merchandisers to group shoppers based on specific attributes such as **device**, **user type**, **location**, or even **custom-defined attributes** like membership IDs or store IDs.

These segments are essential for delivering **targeted, personalized product experiences and campaigns**, helping improve engagement and conversions.

# Segments Dashboard

The main Segments dashboard provides a table listing all existing shopper segments. Each row includes:

| Column                   | Description                                                                                 |
| ------------------------ | ------------------------------------------------------------------------------------------- |
| **Segment Details**      | Name of the segment, creation timestamp, and creator's email ID.                            |
| **Associated Campaigns** | Number of campaigns using this segment, categorized into “Search” and “Browse”.             |
| **Attributes**           | The criteria used to define the segment (e.g., location, user type, device, custom fields). |

Each segment can be **edited** or **deleted**.

***

# Add Segment

To add a new shopper segment, follow these steps:

1. Enter Segment Name. Provide a unique and descriptive name for the segment.
2. Set Shopper Attributes (up to 6). refer to the table to know the Default Attributes (provided by Unbxd).

| Attribute     | Description                                                   |
| ------------- | ------------------------------------------------------------- |
| **Location**  | Target users from a specific city, state, country, or region. |
| **User Type** | Choose between `New` and `Existing` visitors.                 |
| **Device**    | Choose between `Desktop`, `Tablet`, or `Mobile`.              |

Refer to the given table to know the Custom Attributes. These allow advanced segmentation based on internal identifiers or business rules.

| Field                | Description                                                                  |
| -------------------- | ---------------------------------------------------------------------------- |
| **Custom Attribute** | Select from available fields like `storeID`, `member-id`, `segment_id`, etc. |
| **Value**            | Enter the specific value to match (e.g., `Titanium`, `1001`, etc.).          |

> 📘 Note
>
> You can define custom attributes via **Attribute Configuration** (explained below).

Once all attributes are configured, click **Save Segment**.

***

# Attribute Configuration

This allows you to manage and organize which attributes are available for defining segments. The available types are:

| Attribute Type       | Example                              |
| -------------------- | ------------------------------------ |
| **Custom attribute** | `storeID`, `member-id`, `segment_id` |
| **Unbxd default**    | `User type`, `Location`, `Device`    |

You can:

* **Reorder** attributes using drag-and-drop.
* **Delete** unused attributes.
* **Add new custom attributes** dynamically.

Click **Save Configuration** to apply changes.