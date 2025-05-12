---
title: Prepare Your Catalog
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Set up analytics for your product catalog and prepare the catalog feed for integration with **Unbxd**. The catalog feed is a structured file that contains all your products and their associated attributes, which will be used by the search engine to optimize product discovery on your website. Analytics tracking allows you to measure the performance of your products, search queries, and user interactions with the catalog.

## Product Catalog and Attributes

The product catalog holds all relevant information about your products. This data is critical for powering search results, filtering options, and personalized recommendations on your website. Every product in the catalog has associated attributes, which **Unbxd** uses to categorize and display the products in search results. Below are the key categories of attributes typically found in a catalog:

1. **Universal Attributes** : These are common attributes that are used across most businesses to describe their products:

| Attribute Name | Description                                                                                               |
| :------------- | :-------------------------------------------------------------------------------------------------------- |
| uniqueId       | A unique identifier for each product in the catalog, such as SKU or productID. This is a mandatory field. |
| title          | The name or title of the product.                                                                         |
| price          | The cost of the product.                                                                                  |
| description    | A detailed description of the product.                                                                    |
| category       | The category the product belongs to.                                                                      |
| imageUrl       | The URL pointing to the product image.                                                                    |
| productUrl     | The URL to the product's detail page                                                                      |
| currency       | The currency in which the product price is listed.                                                        |
| brand          | The brand name of the product.                                                                            |
| uniqueId       | The color of the product.                                                                                 |
| color          | The availability status of the product                                                                    |

These attributes help define the characteristics of the products in the catalog and are critical to search and discovery processes. In addition to the basic attributes, many catalogs will also include feature fields and custom fields.

2. **Product Catalog Fields** : The attributes in a product catalog can be classified into three main categories:

   <Accordion title="UniqueId" icon="fa-info-circle">
     The UniqueId is a unique identifier for each product in your catalog, commonly known as SKU or productID (PID). This identifier helps track products, sales, and inventory.\
     Note:
     The **UniqueId** does not have to be visible to shoppers but must be included for proper functionality in Unbxd. Specifying the UniqueId is mandatory for each product
   </Accordion>

   <Accordion title="Feature Fields" icon="fa-info-circle">
     Feature fields are critical attributes that are necessary for the basic functionality of Unbxd and should be included in the catalog. Here are some common feature fields:

     Field Name	multiValued	dataType	Description
     uniqueId (mandatory)	false	text	Unique identifier for a product. Cannot contain special characters except '-' and '\_'.
     variantId	false	text	Unique identifier for a variant (if applicable). Must be unique across the entire catalog.
     variants	true	text	Holds all the variants for a product (e.g., color, size, etc.).
     title	false	text	Title or name of the product.
     price	false	decimal (or double)	Price of the product.
     description	false	longText	Description of the product.
     category	true	text	Category the product belongs to.
     subCategory	true	text	Sub-category the product belongs to.
     categoryPath (mandatory)	true	path	The category hierarchy of a product (e.g., "Men>Shoes>Casual Shoes").
     categoryPathId	true	text	Category ID mappings for the hierarchy (e.g., "cat100
     imageUrl	true	link	URL to the product image.
     productUrl	false	link	URL to the Product Detail Page (PDP).
     currency	false	text	Currency of the product.
     brand	true	text	Brand of the product.
     color	true	text	Color of the product.
     availability	false	bool	Availability of the product (true/false).
     sku	false	sku	Unique identifier for an item.
     gender	false	text	Gender for the product.
     size	true	text	Size of the product.
     rating	false	decimal	Rating of the product.
     discount	false	decimal	Discount on the product.
     sellingPrice	false	decimal	Selling price of the product.

     Note: If your catalog contains a feature field with a different name, you can either map it to the corresponding feature field from the Unbxd Console or rename your existing field to match the feature field in the schema.
   </Accordion>

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Product Catalog Fields Name
      </th>

      <th>
        Description
      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        ***
      </td>

      <td>
        .
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>

      </td>

      <td>

      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

availability

These attributes help define the characteristics of the products in your catalog and are critical to search and discovery processes. In addition to these basic attributes, many catalogs will also include feature fields and custom fields.