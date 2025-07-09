---
title: Segments
deprecated: false
hidden: false
metadata:
  robots: index
---
# Segmentation in eCommerce

## What is Segmentation?

Segmentation categorizes customers into groups based on:

* Shopping history
* Geographic location
* Device type
* Other behavioral or contextual attributes

This enables **targeted marketing** and **personalized merchandising** strategies.

***

## Role of Segmentation in eCommerce

Merchandisers use segmentation to show products relevant to a customer’s profile. Examples include:

* Showing **trending products** to new visitors
* Recommending products based on **past views** for returning users

***

## Unbxd’s Role in Segmentation

Unbxd provides a robust platform to:

* **Create and manage segments**
* **Configure default and custom attributes** (e.g., location, device, user type)
* Use **custom attributes** through API calls

***

## Types of Segments

Segments can be defined using the following attributes:

* **Location**:\
  Analyze regional buying patterns. Recommend products with lower shipping costs based on location.

* **Devices**:\
  Understand behavior across devices. Personalize experience for mobile, tablet, or desktop users.

* **Visit Type**:\
  Differentiate between first-time and returning visitors to optimize product recommendations.

* **Custom Attributes**:\
  These are passed in the API request and allow segmentation based on business-specific rules.

***

# Setting Up Netcore Segments

Navigate to **Merchandising > Segmentation** in the Unbxd Self-Serve Console.

***

## Key Functionalities in the Segmentation Dashboard

1. **Search**

   * Use the search icon to find segments by attributes like location, device, and visit type.

2. **Filter**

   * Use filters to refine segment visibility based on:

     | Option             | Description                                      |
     | ------------------ | ------------------------------------------------ |
     | Created Date       | Time period during which the segment was created |
     | Creator Email      | User who created the segment                     |
     | Segment Attributes | Filters by location, device, and visit type      |

3. **Custom Attributes**

   * Click the **settings icon** to “Add New Custom Attribute”.
   * Notes:

     * You can add **up to 5 custom attributes**.
     * Use **drag-and-drop** to reorder them based on importance.
     * Learn more: \[Attributes Documentation Link Placeholder]

4. **Bulk Upload/Download Segments**

   * **Upload**: Use a JSON file to import multiple segments.
   * **Download**: Export all existing segments for offline review or backup.

5. **Delete a Segment**

   * **Custom attributes** can be deleted **only if** not in use by an active segment.
   * **Default attributes** are **permanent** and **cannot be deleted**.
   * An **active segment** is one used by an ongoing or scheduled campaign in Search or Browse.

6. **Add New Segment**

   ### Steps to Create a Segment:

   * Go to **Merchandising > Segments > Add Segment**

   * Enter a name in the **Add Segment Name** field.

   * Choose and configure up to **6 attributes total**:

     * **Default Attributes**:

       * *Location*: Add multiple locations.
       * *Visit Type*: Choose between `New`, `Returning`, or both.
       * *Devices*: Select multiple device types.
     * **Custom Attributes**:

       * Add up to **3 custom attributes**.
       * Each custom attribute supports **one value per segment**.
       * Must be included in the API request using exact naming.

   * Click **Save Segment** to finish.

   * Your new segment will now be visible on the **Segments Listing Page**.