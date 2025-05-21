---
title: Prepare Your Catalog
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Set up analytics for your product catalog and prepare the catalog feed for integration with **Unbxd**. The catalog feed is a structured file that contains all your products and their associated attributes. The search engine will use it to optimize product discovery on your website. Analytics tracking allows you to measure the performance of your products, search queries, and user interactions with the catalog.

## Product Catalog and Attributes

The product catalog holds all relevant information about your products. This data is critical for powering search results, filtering options, and personalized recommendations on your website. Every product in the catalog has associated attributes, which **Unbxd** uses to categorize and display the products in search results. Below are the key categories of attributes typically found in a catalog:

### **Catalog Attributes**

These are common attributes that are used across most businesses to describe their products:

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
| availability   | Indicates if the product is available (true/false).                                                       |

These attributes help define the characteristics of the products in the catalog and are critical to search and discovery processes. In addition to the basic attributes, many catalogs will also include feature fields and custom fields.

### Catalog Fields

This refers to a specific attribute or piece of information associated with a product in the catalog. Fields represent the individual characteristics of a product that help define, categorize, and search for it within the system. Each field holds a specific type of data, such as text, numbers, or links, and is used to describe and organize products. Catalog attributes can be classified into the following categories:

1. **UniqueId**: A unique identifier (SKU, productID) for each product. It helps track sales and manage inventory. The uniqueId might not be visible to customers.
2. **Feature** **Fields**\
   Feature fields are essential for basic functionality and are expected to be included in the catalog. Some of these fields are mandatory.

| Field Name         | Description                                                                   | Multi-Valued | Data Type |
| ------------------ | :---------------------------------------------------------------------------- | ------------ | --------- |
| **uniqueId**       | Unique identifier for the product. (No special characters except `-` and `_`) | false        | text      |
| **variantId**      | Unique identifier for a variant (if applicable)                               | false        | text      |
| **variants**       | Field for holding variants of a product                                       | true         | text      |
| **title**          | Name or title of the product                                                  | false        | text      |
| **price**          | Price of the product                                                          | false        | decimal   |
| **description**    | Product description                                                           | false        | longText  |
| **category**       | Product's main category                                                       | true         | text      |
| **subCategory**    | Product's sub-category                                                        | true         | text      |
| **categoryPath**   | Hierarchical category path (e.g., "Men>Shoes>Casual Shoes")                   | true         | path      |
| **categoryPathId** | Category ID mapping for catalogs with IDs                                     | true         | text      |
| **imageUrl**       | URL to the product image                                                      | true         | link      |
| **productUrl**     | URL to the Product Detail Page (PDP)                                          | false        | link      |
| **currency**       | Currency of the product                                                       | false        | text      |
| **brand**          | Brand of the product                                                          | true         | text      |
| **color**          | Color of the product                                                          | true         | text      |
| **availability**   | Availability status (true/false)                                              | false        | bool      |
| **sku**            | SKU (unique identifier for an item)                                           | false        | sku       |
| **gender**         | Gender (if applicable)                                                        | false        | text      |
| **size**           | Size of the product                                                           | true         | text      |
| **rating**         | Product rating                                                                | false        | decimal   |
| **discount**       | Product discount                                                              | false        | decimal   |
| **sellingPrice**   | Selling price of the product                                                  | false        | decimal   |

3. **Custom fields** : This refer to attributes that are not part of the feature fields but are specific to your catalog. These fields should be included in the schema for product discovery by the search engine.
4. **Searchable Fields**: Attributes that improve search results. Searchable fields are indexed and used for queries when shoppers search for products. Only the attributes you mark as searchable will be used to display results. To modify searchable fields, navigate to **Manage** > **Configure Search** > **Relevancy Ranking** in the Unbxd Console.

> 📘 Note
>
> Changes to searchable fields will be applied after the next feed indexing.

### Variants

Variants are different versions of the same product that share the same SKU or productID but differ in certain attributes (e.g., color, size). These variants are treated as separate products on the search results page. Example Variants:\
**Illustration 1**: An HDMI cable with 5 variants: color, size, gauge, quantity, and output.

**Illustration 2:** A product ‘Mango Badam’ with 1 variant: size.

**Illustration 3**: A skirt with 2 variants: color and size, with other attributes like price, description, and fabric/material remaining the same.

## Best Practices for Catalog Preparation

To ensure your catalog is uploaded and integrated seamlessly, follow these best practices:

1. Ensure every product has a unique uniqueId.
2. Define all attributes in the schema (including custom fields).
3. Ensure the catalog file is in JSON format.
4. Field names are case-sensitive.
5. Field names should follow these rules:
   * Start with an alphabet or an underscore.
   * Can include alphanumeric characters, hyphens, and underscores.
   * Cannot contain special characters, spaces, or end with an underscore.
   * Do not send fields that have null values.

## Map catalog fields to an entity

During mapping a catalog field to an entity, it is recommended that you map the fields from the catalog that contains the information related to the entity. Let’s say a retailer has a title, description, and brand attribute in their catalog. The title and description attribute may contain the brand names of the product for most of the products in the catalog. However, they also contain other details about the products such as size, color, etc. Hence, in order to get the best results for different algorithm, it is recommended to map only the brand attribute to the entity called BRAND because it would only contain the information about product brands and it won’t have details about other product properties.

If catalog does not have an independent attribute for an entity, leave the field mapping against the entity as blank.\
In such cases, it won’t influence the search results based on the detection. However, if there is an entity that is extremely important and used frequently by your shopper during searches you can go ahead and map the attribute which is closest to the entity.

### Assign Weights

The weight-ages assigned to entity/fields mapped against an entity allows us to understand how important these entities/fields are for your shoppers. These weight-ages are used while re-ranking the search results and increasing the product count in search results.  TYPE (i.e. product type) , BRAND, COLOR are some of the entities which are found to be important for a shopper Fashion domain.

> 📘 Note
>
> Entities without field mapping and weightage won’t be available for re-ranking results and increasing result count.

As quoted above, imagine people searching for ‘blue sofa’, get ‘blue shirt’ in their results?\
It would be a terrible experience for shoppers indeed. This might happen when you rank the attributes wrong or do not rank them at all. In such a case, the search engine randomly selects products for display. Therefore,

Assign proper weights to the mapped fields:

| **Weight** | **Description**                                              |
| ---------- | ------------------------------------------------------------ |
| **High**   | The first priority of attribute while searching for results. |
| **Medium** | Good to have, but not the most critical attribute.           |
| **Low**    | Not particularly needed, less important in results.          |

So, if we assign HIGH weightage to **product\_type** while searching for **blue sofa**, we would get results for **blue sofa** and **not blue shirt**.

With relevant mapping and assigning weights, you provide:

1. **Re-ranking of products**: We are indirectly boosting products that you would want your customers to see above others. For example, Encouraging your **brand name**.

If Amazon wants to promote solimo, whenever a shopper searches for roasted brown almonds, solimo almonds would show the top results.

2. **Improved recall**: With algoritms offered by Netcore Unbxd, you get the option to abstain your site from providing zero results. So, whenever a shopper types a long tail search query that has no exact match, sites return zero results or 1-2 results. For example with one of the algorithms, **Named Entity Recognition(NER)**, you could provide more products in the result set by providing a number. This means if the result set contains less than  number of products then let NER increase the number of results. For example, If a shopper searches for Bain brown boots. The result set contains 3 products. So, NER matches the query with the HIGH weightage attribute which in this case was color and product type and provides more results on the same. More brown shoes or boots. Learn more about the different algorithms offered here.