---
title: 'Merchandising : Segments'
excerpt: >-
  It allow you to group and target shoppers based on attributes, enabling
  personalized experiences and marketing strategies
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Segmentation categorizes customers into groups based on shopping history, geographic location, device type, and other attributes. This enables targeted marketing and merchandising strategies.

In eCommerce, a merchandiser uses segmentation to display products more relevant to a customer’s specific segment. For example, showing trending products to new visitors or recommending items based on past views for returning customers.

**Netcore Unbxd** provides a platform to create and manage these segments. It allows configuring attributes (like location, device, and user type) and custom attributes.

## Types of Segments

Segments are defined based on:

**Location**: Analyze purchasing patterns across different regions. Recommend products with lower shipping costs based on shopper locations.

**Devices**: Identify purchasing trends across different devices. Track cross-device purchases and personalize each channel’s experience.

**Visit Type**: Differentiate between first-time and returning shoppers. Display trending products for new visitors and recently viewed or recommended products for returning shoppers.

**Custom Attributes**: They are included in the search API request to segment shoppers based on specific requirements.

## Create a Segment

To create a segment, follow these steps:

<Image align="center" border={true} caption="Create a Segment" src="https://files.readme.io/cfc114a48038d03ffd754dafd81c55590788a281f614e8fec639d61ec8cb051b-Segments.gif" width="80% " />

1. Navigate to **Merchandising** > **Segments** > **Add Segment**
2. Click on the **add new segment** and provide the name of your segment in the Add Segment Name box at the top.
3. Set up the attributes in the next block. You can set up a maximum of **6** attributes, which includes **one default** attribute and **five custom attributes.** Refer [here](https://unbxdocs.readme.io/update/docs/attributes#/) for the attribute details.
4. Select the "save segment" button.

The created segment will be visible on the Listing Page.

## Segment Listing Page

The below functionality is present on the Segment listing page.

1. **Search** : Use the search option (search icon) to find and manage existing segments based on attributes such as location, device, and visit type.
2. **Filter** : Use the filter option (filter icon) to view the table below to know about the options available in Filters.

| **Option**               | **Description**                                    |
| ------------------------ | -------------------------------------------------- |
| **Created date**         | Period in which the segment was created            |
| **Creator email**        | Who has created the segment                        |
| **Segment's attributes** | Group shoppers by location, device, and visit type |

3. **Custom Attributes**: Click on the (setting button image) and select **add new custom attribute** to create an attribute. These attributes will be used to create segments.

> 📘 Note
>
> The attributes can be rearranged in order of importance by drag-and-drop operations on the console. Learn more about Default attributes and Custom attributes [here]().

4. **Bulk upload/download segment** : Easily upload or download segments in bulk for efficient management. You can upload a locally created JSON file with multiple segments to the console simultaneously. Similarly, you can download the list of created segments in bulk.
5. **Delete a Segment** : Custom attributes can be selectively deleted if not used in any active segment and  Unbxd default  attributes are permanent and cannot be removed from the system.

> 📘 Good to know
>
> **Active Segment**: If a segment is used by any active or upcoming campaigns in search or browse. It cannot be deleted unless the Segment expires or stopped.

<Image align="center" border={true} caption="Delete a Segment" src="https://files.readme.io/8dd8b2e22a0376a2dd8c9a338b65f4660d4d53e5f5098501ac6e07a50f0b2700-image.png" width="80% " />