---
title: Segments
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

## What is Segmentation?

Segmentation categorizes customers into groups based on:

* Shopping history
* Geographic location
* Device type
* Other behavioral or contextual attributes

This enables **targeted marketing** and **personalized merchandising** strategies.

## Role of Segmentation in eCommerce

Merchandisers use segmentation to show products relevant to a customer’s profile. Examples include:

* Showing **trending products** to new visitors
* Recommending products based on **past views** for returning users

## Unbxd’s Role in Segmentation

Unbxd provides a robust platform to:

* **Create and manage segments**
* **Configure default and custom attributes** (e.g., location, device, user type)
* Use **custom attributes** through API calls

## Types of Segments

Segments are defined based on:

**Location**: Analyze purchasing patterns across different regions. Recommend products with lower shipping costs based on shopper locations.

**Devices**: Identify purchasing trends across different devices. Track cross-device purchases and personalize each channel’s experience.

**Visit Type**: Differentiate between first-time and returning shoppers. Display trending products for new visitors and recently viewed or recommended products for returning shoppers.

**Custom Attributes**: They are included in the search API request to segment shoppers based on specific requirements.

# Create a Segment

To create a segment, follow these steps:

<Image align="center" border={true} caption="Create a Segment" src="https://files.readme.io/cfc114a48038d03ffd754dafd81c55590788a281f614e8fec639d61ec8cb051b-Segments.gif" width="80% " />

1. Navigate to **Merchandising** > **Segments** > **Add Segment**
2. Click on the **add new segment** and provide the name of your segment in the Add Segment Name box at the top.
3. Set up the attributes in the next block. You can set up a maximum of **6** attributes, which includes **one default** attribute and **five custom attributes.** Refer [here](https://unbxdocs.readme.io/docs/attributes#/) for the attribute details.
4. Select the "save segment" button.

The created segment will be visible on the Listing Page.

# Key Functionalities in the Segmentation Dashboard

The functionality below is present on the Segment listing page.

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
> The attributes can be rearranged in order of importance by drag-and-drop operations on the console. Learn more about Default attributes and Custom attributes [here](https://unbxdocs.readme.io/docs/attributes#/types-of-segment-attributes-in-unbxd).

4. **Bulk upload/download segment** : Easily upload or download segments in bulk for efficient management. You can upload a locally created JSON file with multiple segments to the console simultaneously. Similarly, you can download the list of created segments in bulk.
5. **Delete a Segment** : Custom attributes can be selectively deleted if not used in any active segment and  Unbxd default  attributes are permanent and cannot be removed from the system.

> 📘 Good to know
>
> **Active Segment**: If a segment is used by any active or upcoming campaigns in search or browse. It cannot be deleted unless the Segment expires or stopped.