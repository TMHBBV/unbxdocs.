---
title: Dimension Mapping
excerpt: >-
  Learn how product attributes are used to filter, categorize, and refine search
  results
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

In **UNBXD**, **dimension mapping** refers to mapping various attributes or characteristics of a product to specific filters, facets, or categories that help users refine their search results or navigate product listings. **Dimensions** in UNBXD are typically product attributes such as:

* **Brand**
* **Price**
* **Size**
* **Color**
* **Category**
* **Material**
* **Ratings**
* **Discount**

UNBXD enables you to map these attributes (which serve as your dimensions) to search filters and facets, allowing users to refine their search and find products that match their preferences.

**For Example:**

* When you define the **brand** as a **dimension** in UNBXD, users can filter results by brands.
* Similarly, **price range** can be mapped to allow users to filter products by specific price bands.

### Map Product Attributes

The **mapping process** ensures that these attributes are correctly recognized and used for creating dynamic filters in your search or product listing pages. This enhances the search experience by enabling users to easily drill down into product categories.

1. Navigate to **Manage** > **Catalog** > **Dimension Mapping.**
2. Dimension Mapping is divided into two categories:

   * **Essential Fields**: These are the basic fields typically needed for product listings and search functionality. Refer to the given table to know the description of fields available for essential fields.

   | Field                    | Description                                                                              |
   | ------------------------ | ---------------------------------------------------------------------------------------- |
   | SKU (Stock Keeping Unit) | It is a unique identifier for each product or variant.                                   |
   | Title                    | It defines the product’s name or title.                                                  |
   | Image URL                | This is the link to the product image.                                                   |
   | Product URL              | It redirects to the direct link to the product's detail page.                            |
   | Rating                   | A decimal value for the product’s average rating.                                        |
   | Price                    | The standard price of the product or variant.                                            |
   | Selling Price            | This is the price at which the product is sold, often different from the original price. |
   | Availability             | This field indicates if the product is in stock or available.                            |
   | Category                 | This reflects the product's primary category.                                            |
   | Category Path            | The hierarchical path to the category (e.g., "Men > Apparel > T-Shirts").                |
   | Discount                 | The discount percentage or value applied to the product.                                 |
   | Badges                   | Any product badges, such as "New", "Bestseller", or "Sale".                              |
   | Swatch                   | The color swatch or image link for color variants.                                       |

   |

   * Vertical Field: These are additional fields specific to the **apparel** category. Refer to the given table for description of fields available in vertical field.

| Field       | Description                                                      |
| ----------- | ---------------------------------------------------------------- |
| Brand       | The brand of the product.                                        |
| Size        | The size of the product (e.g., Small, Medium, Large).            |
| Color       | The color of the product.                                        |
| Gender      | The target gender for the product (e.g., Men, Women, Unisex).    |
| Type        | The type or sub-category of the product (e.g., T-shirt, Jeans).  |
| Fit         | The fit style (e.g., Slim Fit, Regular Fit).                     |
| Neckline    | The type of neckline (e.g., V-neck, Round-neck).                 |
| Sleeve Type | The sleeve type (e.g., Short Sleeve, Long Sleeve).               |
| Fabric      | The fabric or material of the product (e.g., Cotton, Wool).      |
| Pattern     | The pattern of the product (e.g., Solid, Stripes, Plaid).        |
| Style       | The style of the back of the product (e.g., Backless, Zippered). |
| Waist Type  | The type of waist (e.g., High-rise, Low-rise).                   |

**Dimension Mapping** is critical for optimizing the e-commerce experience. They not only enhance product visibility and search accuracy but also help businesses deliver a high-quality, customer-friendly shopping environment that drives conversions and fosters long-term trust. By paying attention to these mappings, businesses can offer a seamless, engaging, and efficient product discovery process for their customers.

## Troubleshoot & FAQs

<Accordion title="What happens if I update my product feed—do I need to remap attributes?" icon="sparkles">
  No, once your dimension and product card mappings are set, you only need to ensure new feed fields follow the same naming and structure. If new fields are added, map them accordingly.
</Accordion>

<Accordion title="Some of the product filters missing in Search or Browse Preview" icon="sparkles">
  This could be because the required product attributes are not correctly mapped in \*\*Dimension Mapping \*\*or the attribute values are missing in your product feed.\
  Go to **Manage > Catalog > Dimension Mapping** and ensure the attributes are listed under **Essential Fields** or **Vertical Fields**.\
  Ensure your product feed includes valid data for those attributes you want to use as filters or facets.
</Accordion>

<Accordion title="I seeing a popup warning about missing dimension mapping attributes" icon="sparkles">
  Check the required attributes (like **Title**, **Image URL**, or **Selling Price**) are missing either in your feed or in your mapping configuration. Review your **Dimension Mapping** to ensure all required fields are mapped. Re-upload your product feed and confirm that the values for the essential attributes are present.
</Accordion>

<Accordion title="My attribute filters behaving unexpectedly" icon="sparkles">
  The field types might be incorrectly configured (e.g., a number stored as text). Fields intended for filtering may not be marked as **Facetable**.\
  Check that the field type matches its intended use (e.g., price should be numeric). Ensure the field is marked as **Facetable** in the backend.\
  If the issue persists, contact **Unbxd Support** for further assistance.
</Accordion>