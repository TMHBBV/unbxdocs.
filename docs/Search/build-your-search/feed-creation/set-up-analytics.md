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
| availability   | Indicates if the product is available (true/false).                                                       |

These attributes help define the characteristics of the products in the catalog and are critical to search and discovery processes. In addition to the basic attributes, many catalogs will also include feature fields and custom fields.

2. **Product Catalog Fields** : This refers to a specific attribute or piece of information associated with a product in the catalog. Fields represent the individual characteristics of a product that help define, categorize, and search for it within the system. Each field holds a specific type of data, such as text, numbers, or links, and is used to describe and organize products. For Example:

| Field Name      | Description                                                  |
| :-------------- | :----------------------------------------------------------- |
| **uniqueId**    | unique identifier for the product (e.g., SKU or product ID). |
| **title**       | The product name or title.                                   |
| **price**       | The cost of the product.                                     |
| **description** | A detailed description of the product.                       |
| **category**    | The category under which the product is classified.          |
| **imageUrl**    | A link to the product’s image.                               |

Fields can be divided into categories like:

* **Feature Fields**: Core attributes that are necessary for basic functionalities like search, filtering, and sorting.
* **Custom Fields**: Additional attributes specific to a particular business or product but not required for basic functionalities.