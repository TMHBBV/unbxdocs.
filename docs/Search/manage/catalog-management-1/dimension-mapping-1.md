---
title: Dimension Mapping
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

In UNBXD, dimension mapping refers to mapping various attributes or characteristics of a product to specific filters, facets, or categories that help users refine their search results or navigate product listings. Dimensions in UNBXD are typically product attributes such as:

| Field Name | Description                                 |
| ---------- | ------------------------------------------- |
| Brand      | The brand name of the product.              |
| Price      | The selling price of the product.           |
| Size       | The size(s) available for the product.      |
| Color      | The color(s) available for the product.     |
| Category   | The product category or classification.     |
| Material   | The materials used in the product.          |
| Ratings    | The average customer rating of the product. |
| Discount   | The discount value or percentage applied.   |

Netcore Unbxd enables you to map these attributes (which serve as your dimensions) to search filters and facets, allowing users to refine their search and find products that match their preferences.

For Example: When you define the brand as a dimension in UNBXD, users can filter results by brands. Similarly, price range can be mapped to allow users to filter products by specific price bands.

**Map Product Attributes**

The mapping process ensures that these attributes are correctly recognized and used for creating dynamic filters in your search or product listing pages. This enhances the search experience by enabling users to easily drill down into product categories.

Navigate to **Manage** > **Catalog** > **Dimension Mapping**.

Dimension Mapping is divided into two categories:

1. **Essential Fields**: These are the basic fields typically needed for product listings and search functionality.

Description of fields available for Essential Fields

| Field                        | Description                                                               |
| ---------------------------- | ------------------------------------------------------------------------- |
| **SKU (Stock Keeping Unit)** | A unique identifier for each product or variant.                          |
| **Title**                    | The product’s name or title.                                              |
| **Image URL**                | The link to the product image.                                            |
| **Product URL**              | Direct link to the product’s detail page.                                 |
| **Rating**                   | A decimal value representing the product’s average rating.                |
| **Price**                    | The standard price of the product or variant.                             |
| **Selling Price**            | The price at which the product is sold, often discounted from original.   |
| **Availability**             | Indicates if the product is in stock or available.                        |
| **Category**                 | The product's primary category.                                           |
| **Category Path**            | The hierarchical path to the category (e.g., “Men > Apparel > T-Shirts”). |
| **Discount**                 | The discount percentage or value applied to the product.                  |
| **Badges**                   | Product badges like "New", "Bestseller", or "Sale".                       |
| **Swatch**                   | Color swatch or image link for color variants.                            |

2. **Vertical Field**: These are additional fields specific to the apparel category.

Description of fields available in Vertical field:

| Field           | Description                                                      |
| --------------- | ---------------------------------------------------------------- |
| **Brand**       | The brand of the product.                                        |
| **Size**        | The size of the product (e.g., Small, Medium, Large).            |
| **Color**       | The color of the product.                                        |
| **Gender**      | The target gender for the product (e.g., Men, Women, Unisex).    |
| **Type**        | The type or sub-category of the product (e.g., T-shirt, Jeans).  |
| **Fit**         | The fit style (e.g., Slim Fit, Regular Fit).                     |
| **Neckline**    | The type of neckline (e.g., V-neck, Round-neck).                 |
| **Sleeve Type** | The sleeve type (e.g., Short Sleeve, Long Sleeve).               |
| **Fabric**      | The fabric or material of the product (e.g., Cotton, Wool).      |
| **Pattern**     | The pattern of the product (e.g., Solid, Stripes, Plaid).        |
| **Style**       | The style of the back of the product (e.g., Backless, Zippered). |
| **Waist Type**  | The type of waist (e.g., High-rise, Low-rise).                   |

Dimension Mapping is critical for optimizing the e-commerce experience. They not only enhance product visibility and search accuracy but also help businesses deliver a high-quality, customer-friendly shopping environment that drives conversions and fosters long-term trust. By paying attention to these mappings, businesses can offer a seamless, engaging, and efficient product discovery process for their customers.

## Troubleshoot & FAQs

<Accordion title="What happens if I update my product feed—do I need to remap attributes?">
  No, once your dimension and product card mappings are set, you only need to ensure new feed fields follow the same naming and structure. If new fields are added, map them accordingly.
</Accordion>

<Accordion title="Some of the product filters missing in Search or Browse Preview">
  This could be because the required product attributes are not correctly mapped in Dimension Mapping or the attribute values are missing in your product feed.
  Navigate to Manage > Catalog > Dimension Mapping and ensure the attributes are listed under Essential Fields or Vertical Fields.
  Ensure your product feed includes valid data for those attributes you want to use as filters or facets.
</Accordion>

<Accordion title="I seeing a popup warning about missing dimension mapping attributes">
  Check the required attributes (like Title, Image URL, or Selling Price) are missing either in your feed or in your mapping configuration. Review your Dimension Mapping to ensure all required fields are mapped. Re-upload your product feed and confirm that the values for the essential attributes are present.
</Accordion>

<Accordion title="My attribute filters behaving unexpectedly">
  The field types might be incorrectly configured (e.g., a number stored as text). Fields intended for filtering may not be marked as Facetable.
  Check that the field type matches its intended use (e.g., price should be numeric). Ensure the field is marked as Facetable in the backend.
  If the issue persists, contact Unbxd Support for further assistance.
</Accordion>