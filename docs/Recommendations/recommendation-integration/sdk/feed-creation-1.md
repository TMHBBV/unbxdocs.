---
title: Feed Creation
deprecated: false
hidden: false
metadata:
  robots: index
---
# Direct Feed Upload

Once you have your site key, you’re ready to upload your product catalog. A product catalog is a detailed list of products and their characteristics in a store.

This page walks you through the process of understanding what a schema and a catalog is, what and how you’ll need to upload both to seamlessly integrate them with our search solution.

1. Prepare Schema
2. Prepare Catalog
3. Upload Feed

TIP: Customers using Magento 2, Shopify, and Hybris can use our platform plugin to upload their feed and integrate Analytics.

## Prepare Schema

Your product catalog contains a list of all your products and their attributes. A schema defines the properties of the attributes in your product catalog.

For instance, when your catalog has fields like ‘title’, ‘size’, ‘price’, and ‘brand’, a schema file helps your search engine make sense of the information within such fields in the catalog. The schema establishes the properties of each attribute, determining the type of information the field will contain and display. A schema helps the search engine understand that ‘price’ is a numerical field and it should support range facets while ‘brand’ is a text field that should support text facets.

A schema is a key component of a product catalog that defines all fields used within your catalog. The type of operations supported on an attribute is directly driven by the schema defined for that attribute.

## Schema Format

The schema is part of a larger JSON feed file and is defined by the “schema” node. Each JSON object within the schema represents a field within your catalog.

Each field must contain the following four properties:

Fieldname (mandatory)\
datatype (mandatory)
multiValue (Mandatory)
isVariant (Optional)
id (Optional)
Autosuggest (Mandatory)

> 📘 NOTE
>
> While we recommend you upload both the schema and catalog as a unified JSON file, you can also upload the schema as a separate file.

fieldName\
The fieldName in the schema specifies the name of the attribute. Some examples of a fieldName are ‘productURL’, ‘sku’, ‘color’, ‘brand’ etc.

id\
The id in schema specifies a numerical identifier for an attribute in the catalog. Useful when product feeds may have the fieldID instead of the fieldName.

dataType\
A dataType defines the type of value a specific field can have.

The dataType attribute of a value (also known as a variable) is an attribute that tells what kind of data that value can have. Consider this analogy: A dataType is like a box that is designed to hold items only of specific characteristics.

We support the following nine dataTypes.

| **Data Type** | **Format**                                  | **Description**                                                                                                                 | **Searchable** |
| ------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| `text`        | String                                      | Used for fields that briefly describe a product such as title, occasion, color, brand, etc. Often used in search queries.       | yes            |
| `longText`    | String                                      | Used for fields that describe a product in detail such as description, seller\_name, etc. Not typically used in search queries. | yes            |
| `decimal`     | Decimal                                     | Used for fields that take decimal values such as price, discount, etc.                                                          | –              |
| `number`      | Numeric                                     | Used for fields that take numeric values such as quantity, orderCount, viewCount, etc.                                          | –              |
| `link`        | URL (string)                                | Used for fields that take URL strings as values such as productUrl, imageUrl, etc.                                              | –              |
| `date`        | ISO 8601 date format (YYYY-MM-DDTHH:MM:SSZ) | Used for fields that take date values such as createdAt, updatedAt, etc.                                                        | –              |
| `bool`        | true/false                                  | Used for fields that take boolean values such as availability, hasBanner, etc.                                                  | –              |
| `sku`         | String                                      | Used for fields that denote unique product information such as sku, uid (or pid), etc. Can be used in search queries.           | yes            |
| `path`        | String                                      | Used for hierarchical fields like categoryPath. Hierarchy values are separated by “>” (e.g., “Men>Shoes>Casual Shoes”).         | –              |
| `facet`       | String                                      | Used to filter products on Product Listing Pages. Not processed for spelling, stemming, or tokenization.                        | –              |
| `nsku`        | String                                      | Used for unique product info like skuid. Supports partial search. Can be used in search queries.                                | yes            |

> 📘 NOTE
>
> Data Types of fields that are made searchable display those products on the search results page. Data Types that are not searchable can be used for filtering, sorting, and faceting.

autoSuggest\
The autoSuggest attribute specifies if the value of the field will appear as a suggestion within the autosuggest widget.

multiValue\
A multiValue attribute determines if a field can take multiple values.  For example, when a shirt with one productID has two or more images (front/back) of the same shirt, then ‘image’ is a multiValue attribute.

To enable a field to accept multiple values, set multiValue to true. Else, false.For instance, in the screenshot below, a laptop may have multiple images for the same product (SKU) and this is called a multiValue attribute.Note: A multiValue attribute describes multiple attributes (different images etc) for a field of the same product/sku, while a variant describes different products with varying attributes (size/color/material) which can be grouped together. Both of these attributes help your shopper make an informed purchase decision.

isVariant\
Variants define different attribute values of the same product. For example, a dress can have different colors: red, green, blue. Such different values of the same attribute has the same productID and variantID. The laptop in the above example is also available in two different colors and hard disk capacities. This is called a variant attribute. Each laptop in the variants listed have different SKUs but are grouped together to help your shoppers view all the product options available.

If, isVariant=true, then the product will have variants. If there are no variants, set isVariant is set to false.

## Sample Schema

```
{
"feed": {
        "catalog": {
            "schema": [{
                "fieldName": "vColor",
                "id": "76678",
                "dataType": "text",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }, {
                "fieldName": "vSize",
                "dataType": "text",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }, {
                "fieldName": "vImages",
                "dataType": "link",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            },
{
                "fieldName": "vPrice",
                "dataType": "decimal",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }]
        }
    }
}
```

<br />

Schema Upload Process\
You can upload a schema using APIs with the exception of instances where any post-processing is performed by Unbxd on your schema which requires an SFTP upload.

Every schema upload appends to an existing schema, if any. You can update the characteristics

In case the schema has fields that are already found within an existing schema, the property values of the existing fields are updated. Similarly, when the new schema has new fields that are not found within an existing schema, the existing schema appends and adds the new fields. It is currently not possible to delete existing fields through the schema API.

API Parameters\
The API parameters along with sample request and response are defined below:

```Text API Endpoint
Method : POST

 

End Point :  {feed end point}/{siteKey}/upload/schema

 

Description : This API will perform an upload/update of the schema file.
```
```Text Parameter
Method : POST

 

End Point :  {feed end point}/{siteKey}/upload/schema

 

Description : This API will perform an upload/update of the schema file.

siteKey: A unique identifier provided when your Unbxd account is created. This key can also be retrieved from your Unbxd Console. This is a required field.

 

secretKey: A unique identifier provided when your Unbxd account is created. The secretKey is used to authorize your upload request. This is a private key and will not be exposed to the public. This is a required field.

 

file: The name of the schema, as a JSON file.

 

feed end point : The feed end point depends upon the region selected at the time of site creation.

 

US region: http://feed.unbxd.io/

 

ANZ region : http://feed-anz.unbxd.io/

 

UK region : http://feed-uk.unbxd.io/

 

SG region : http://feed-apac.unbxd.io/


```
```Text Error Codes
Method : POST

 

End Point :  {feed end point}/{siteKey}/upload/schema

 

Description : This API will perform an upload/update of the schema file.

We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
```
```
Method : POST

 

End Point :  {feed end point}/{siteKey}/upload/schema

 

Description : This API will perform an upload/update of the schema file.

curl -X POST https://{Feed end point}/api/{siteKey}/upload/schema 
-H 'Authorization:{secretKey}' 
-F file={file}
```

### Best Practices

To ensure your schema is uploaded and integrated seamlessly, here are some practices we recommend:

Start by defining a schema for your custom fields. Unbxd Feature fields have a fixed predefined schema that cannot be modified.\
Schemas not adequately defined will be rejected.
Ensure your schema file is in JSON format.
Field names are case-sensitive.
Field names should start with alphabets or underscore. It can be alphanumeric, can have hyphens and underscores. It cannot contain special characters, spaces in between words, or end with an underscore.
Do not send fields that have null values.

## Prepare Catalog

In this section, we define what a catalog and its attributes are, how you can send your updated catalog file to us and some practices we recommend you follow while preparing your catalog for upload. Once you’ve uploaded your catalog, it becomes the feed that powers our search solution on your eCommerce site. A catalog powers the content in an eCommerce site and contains attributes that describe properties of the product in more detail.

The catalog file contains a list of all your products and its attributes. The information associated with products is managed by search engines using attributes or fields. The attributes contain information about properties of the product.

Some generic attributes considered universal across businesses are:

uniqueID (required)\
title
price
description
category
imageURL
productURL
currency
brand
color
price
availability
Broadly, the typical feed will contain many other attributes, which will have display, searchable, merchandisable, and unique attributes.

Fields\
The product attributes store information related to a particular product. The attributes in a catalog can be classified into following categories :

UniqueId\
Feature Fields
Custom Fields

UniqueID

UniqueId is a unique identifier that is associated with every product in the catalog and it is used to uniquely identify a product. Also known as a Stock Keeping Unit (SKU) or a productID (pid), the unique identifier helps the search engine keep a track of sales of a particular product and maintain your store’s inventory. The UniqueId attributes may not be visible to the shoppers and can remain completely hidden.

NOTE: Specifying 'UniqueId' for a product is mandatory.

Feature fields\
Feature fields are a list of predefined Unbxd fields with a fixed schema that doesn’t need to be defined in the feed file, and are automatically marked searchable.These fields are necessary for Autosuggest and Recommendations to work properly.

In most cases, you do not have to define the schema for these fields, however, when the feature field does not match with the corresponding field within your product feed, you can define the schema by the dataType of that field. In another example, if the “size” field in your catalog has data type “decimal” instead of text, the schema for the “size” field has to be defined in the product feed. Similarly, if the “gender” field in your catalog is “multivalue=true” instead of false, the schema for the “gender” field would need to be defined before the product attribute data in the Product Feed.

Any changes you make to the schema of a feature field will be overwritten by the predefined default schema of that field.

| **Field Name**               | **Multi Value** | **Data Type**       | **Description**                                                                                                               |
| ---------------------------- | --------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `uniqueId` *(mandatory)*     | false           | text                | Unique identifier of a product. Cannot have special characters except ‘-’ and ‘\_’.                                           |
| `variantId`                  | false           | text                | Unique identifier of a variant (if present). Must be unique across entire catalog. No special characters except ‘-’ and ‘\_’. |
| `variants`                   | true            | text                | Holds all the variants for a product.                                                                                         |
| `title`                      | false           | text                | Title or name of the product.                                                                                                 |
| `price`                      | false           | decimal (or double) | Price of the product.                                                                                                         |
| `description`                | false           | longText            | Description of the product.                                                                                                   |
| `category`                   | true            | text                | Name of the category the product belongs to.                                                                                  |
| `subCategory`                | true            | text                | Name of the sub-category the product belongs to.                                                                              |
| `categoryPath` *(mandatory)* | true            | path                | Category hierarchy. Values separated using “>” (e.g., “Men>Shoes>Casual Shoes”).                                              |
| `categoryPathId`             | true            | text                | Category hierarchy with names and IDs. Format: \`ID                                                                           |
| `imageUrl`                   | false           | link                | URL of the product image.                                                                                                     |
| `productUrl`                 | false           | link                | URL of the Product Detail Page (PDP).                                                                                         |
| `currency`                   | false           | text                | Currency of the product.                                                                                                      |
| `brand`                      | false           | text                | Brand of the product.                                                                                                         |
| `color`                      | true            | text                | Color(s) of the product.                                                                                                      |
| `availability`               | false           | bool                | Availability of the product (`true`/`false`).                                                                                 |
| `sku`                        | false           | sku                 | Unique identifier for the item.                                                                                               |
| `gender`                     | false           | text                | Gender associated with the product.                                                                                           |
| `size`                       | true            | text                | Size(s) of the product.                                                                                                       |
| `rating`                     | false           | decimal             | Product rating.                                                                                                               |
| `discount`                   | false           | decimal             | Discount on the product.                                                                                                      |
| `sellingPrice`               | false           | decimal             | Selling price of the product.                                                                                                 |

<br />

> 📘 NOTE
>
> Feature Fields can be used without explicitly defining them in the schema. If you have a similar field, you can either map it to the corresponding feature field from the Console or  rename your existing field to a feature field in the schema.

Custom fields\
Attributes that are not part of our list of Feature Fields but part of your product catalog are known as Custom Fields. These attributes and their properties are included in your schema.

Like Feature fields, our search engines use these attributes to power product discovery on your web page.

Searchable fields\
Searchable attributes are attributes that optimize your search results. Whilst there could be 100s of attributes that define a product, we index only the attributes you mark as searchable.

In other words, searchable attributes are those attributes which are used to search when shoppers type in a query. Products displayed will have attributes that are relevant to the search query.

The list of searchable attributes can be modified from the Console. The settings to modify searchable fields is available under  Manage > Configure Search > Relevancy Ranking. The changes made in searchable fields from the console are only available after the next successful feed indexing. In the “Relevancy Ranking” section, only those attributes are available whose dataType qualifies for searchable criteria.

Variants\
Variants are products that share the same SKU or productID (PID) but have at least one or more fields, like color, size, patterns that are different from the other fields of the same PID. These products will be displayed as a distinct product in the search results page.

Once your catalog has updated information related to variants, you can add variants to your existing feed. In each of the illustrations below, variants are configured to appear differently.

## Best Practices

To ensure your feed is uploaded and integrated seamlessly, here are some practices we recommend:

Ensure every product has the associated uniqueId.\
Ensure all attributes are defined in the schema.
Ensure your catalog file is in JSON format.
Field names are case-sensitive.
Field names should start with alphabets or underscore. It can be alphanumeric, can have hyphens and underscores. It cannot contain special characters, spaces in between words, or end with an underscore.
Do not send fields that have null values.
Upload Feed
Once you’ve identified the attributes you need to upload, you can choose how you want to send your feed. You can upload your catalog using APIs, via a Secure File Transfer Protocol, or using a Platform extension. A product catalog may have multiple feed files, however to power your eCommerce search, we need your unified product feed file in JSON format.

Caution: Acquaint yourself with the attributes within your schema and catalog file before you proceed. If you upload a schema or a catalog file with invalid attributes, you will get an error.

We support three methods of feed upload:

1. [Rest APIs](): Use our custom REST APIs to upload your feed directly.
2. Secure File Transfer Protocol: Upload your feed through an SFTP. Feed files uploaded on SFTP servers are transformed and uploaded to Unbxd servers. SFTP upload supports feed files in CSV, JSON and XML formats.
3. Platform Extensions: Our platform extensions can be used to upload feed seamlessly. Integrate our Magento 2 , Shopify or SAP Hybris plugin to automate catalog transfer from these platforms.