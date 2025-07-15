---
title: Prepare Your Catalog
deprecated: false
hidden: false
metadata:
  robots: index
---
In this section, we define the product catalog and its attributes and different ways of sending your catalog to the Unbxd system. The catalog file contains a list of all your products and its attributes. The information associated with products is managed by search engines using attributes or fields.

Some generic attributes considered universal across businesses are:

* uniqueID (required)
* title
* price
* description
* category
* imageURL
* productURL
* currency
* brand
* color
* price
* availability

Broadly, the typical feed will contain many other attributes, which will have display, searchable, merchandisable, and unique attributes.

***

# Fields

The product attributes store information related to a particular product. The attributes in a catalog can be classified into following categories :

* UniqueId
* Feature Fields
* Custom Fields

## UniqueID

UniqueId is a unique identifier that is associated with every product in the catalog and it is used to uniquely identify a product. Also known as a Stock Keeping Unit (SKU) or a productID (pid), the unique identifier helps the search engine keep a track of sales of a particular product and maintain your store’s inventory. The UniqueId attributes may not be visible to the shoppers and can remain completely hidden.

> 📘 NOTE
>
> Specifying 'UniqueId' for a product is mandatory.

## Feature fields

Feature fields are a list of Unbxd fields that are necessary for majority of basic functionality to work and are expected to be included in your catalog.

| fieldname                      | multiValued | dataType           | Description                                                                                                                                                                                                                                                              |
| :----------------------------- | :---------- | :----------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| uniqueId (mandatory field)     | false       | text               | Unique identifier of a product. It cannot have special character except ‘-’ and ‘\_’                                                                                                                                                                                     |
| variantId                      | false       | text               | Unique identifier of a variant (if present). It cannot have special character except ‘-’ and ‘\_’. It needs to be unique across entire product catalog.                                                                                                                  |
| variants                       | true        | text               | Field holding all the variants for a product.                                                                                                                                                                                                                            |
| title                          | false       | text               | Title or name of a project.                                                                                                                                                                                                                                              |
| price                          | false       | decimal(or double) | Price of a product.                                                                                                                                                                                                                                                      |
| description                    | false       | longText           | Description of a product.                                                                                                                                                                                                                                                |
| category                       | true        | text               | Name of the category a product belongs to.                                                                                                                                                                                                                               |
| subCategory                    | true        | text               | Name of the sub-category a product belongs to.                                                                                                                                                                                                                           |
| categoryPath (mandatory field) | true        | path               | The category hierarchy of a product separated by  “>” such as “Men>Shoes>Casual Shoes” If categoryPathId below is included, categoryPath is not required as it will be generated automatically by the system                                                             |
| categoryPathId                 | true        | text               | For catalogs that have category ids available, categoryPathId represents the mapping between category names and category ids. IDs and Names need to be separated using “\|”. For example, “cat100\|Home>cat101\|Luggage & Travel Accessories>cat102\|Travel Accessories” |
| imageUrl                       | false       | link               | URL of a product image.                                                                                                                                                                                                                                                  |
| productUrl                     | false       | link               | URL of the Product Detail Page (PDP) of a product.                                                                                                                                                                                                                       |
| currency                       | false       | text               | Currency of a product.                                                                                                                                                                                                                                                   |
| brand                          | false       | text               | Brand of a product.                                                                                                                                                                                                                                                      |
| color                          | rue         | text               | Color of a product.                                                                                                                                                                                                                                                      |
| availability                   | false       | bool               | Product availability in “true”/“false” format.                                                                                                                                                                                                                           |
| sku                            | false       | sku                | Unique identifier for an item.                                                                                                                                                                                                                                           |
| gender                         | false       | text               | Gender for a product.                                                                                                                                                                                                                                                    |
| size                           | true        | text               | Size of a product.                                                                                                                                                                                                                                                       |
| rating                         | false       | decimal            | Rating of a product.                                                                                                                                                                                                                                                     |
| discount                       | false       | decimal            | Discount on a product.                                                                                                                                                                                                                                                   |
| sellingPrice                   | false       | decimal            | Selling price of a product.                                                                                                                                                                                                                                              |

&#x9;	&#x9;

> 📘 NOTE
>
> If your catalog contains a feature field with a different name, you can either map it to the corresponding feature field from the Unbxd Console or rename your existing field to a feature field in the schema.

***

## Custom fields

Attributes that are not part of our list of Feature Fields but part of your product catalog are known as Custom Fields. These attributes and their properties are included in your schema.

Like Feature fields, our search engines use these attributes to power product discovery on your web page.

***

# Variants

Variants are products that share the same SKU or productID (PID) but have at least one or more fields, like color, size, patterns that are different from the other fields of the same PID. These products will be displayed as a distinct product in the search results page.

Once your catalog has updated information related to variants, you can add variants to your existing feed. In each of the illustrations below, variants are configured to appear differently.

Illustration 1 : The HDMI cable has 5 variants – color, size, gauge, quantity, and output.

<Image align="center" className="border" border={true} width="50% " src="https://files.readme.io/ac96c364512753c5f0d83eca68ae1bd38553578a1f5b8a49bcbced781d07f09b-illustration_1.png" />

Illustration 2: In the illustration below, the product ‘Mango Badam’ has 1 variant – size. The PLP chooses to display the product as two separate entities here.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/e5b8cb45687cdf406764b1779e82c9d27666e7e54fcec544565372e7fae85ad0-illustration_2.png" />

Illustration 3: In this illustration, the skirt has two variants – color and size. The other fields like title, description, fabric/material, price are the same.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/ecbf3c0ec82ca26f1ac9a30c0c36647fa3c23a4c321ba522f72e50127c1971e7-Variant_3.png" />

***

## Best Practices

To ensure your feed is uploaded and integrated seamlessly, here are some practices we recommend:

* Ensure every product has the associated uniqueId.
* Ensure all attributes are defined in the schema.
* Ensure your catalog file is in JSON format.
* Field names are case-sensitive.
* Field names should start with an alphabet or underscore. They can be alphanumeric, have hyphens, or underscores. They cannot contain special characters, spaces between words, or end with an underscore.
* Do not send fields that have null values.