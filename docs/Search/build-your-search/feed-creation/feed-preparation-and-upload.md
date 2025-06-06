---
title: Prepare Schema
excerpt: >-
  Guide to preparing and uploading product catalog feeds and schemas for
  seamless integration with Unbxd
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: set-up-analytics
      title: Prepare Your Catalog
      type: basic
---
# Overview

To integrate your product catalog into Unbxd, it is crucial to prepare and upload the catalog schema. This schema defines the attributes and properties of each field within the product catalog, ensuring that Unbxd understands how to process and display data. It also determines which operations can be performed on each attribute, such as search, sorting, and filtering. This section will guide you through the feed preparation process and the schema upload procedure.

## Schema Structure

The schema is a part of a larger JSON feed file, defined by the **schema** node. Each field within the product catalog is represented by a JSON object within the schema.

### Schema Field Properties

Each field in the schema must contain the following four mandatory properties:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field Property
      </th>

      <th>
        Description
      </th>

      <th>
        Mandatory/ Optional
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        fieldName
      </td>

      <td>
        The fieldName represents the name of an attribute within your catalo, such as title, color, brand, etc. Ensure to follow the below thumbnail:

        * Field names are case-sensitive.
        * Field names must start with an alphabet or underscore.
        * Field names can only contain alphanumeric characters, hyphens (**-**), and underscores (**\_**).
        * Field names cannot contain special characters or spaces.
        * Field names cannot end with an underscore.
      </td>

      <td>
        Mandatory
      </td>
    </tr>

    <tr>
      <td>
        dataType
      </td>

      <td>
        The dataType defines the type of value an attribute can have. The supported dataType values include:

        * **text**: *String* – Used for text fields (e.g., title, color, brand, style). Searchable: Yes
        * **longText**: *String* – Used for large text fields (e.g., description, summary). Searchable: Yes
        * **decimal**: *Decimal* – Used for decimal values (e.g., price, discount). Searchable: No
        * **number**: *Numeric* – Used for numeric values (e.g., quantity, orderCount, viewCount). Searchable: No
        * **link**: *URL* – Used for URL values (e.g., productUrl, imageUrl). Searchable: No
        * **date**: *Date* – Used for date values (e.g., createdAt, updatedAt). Searchable: No
        * **bool**: *Boolean* – Used for boolean values (e.g., availability, hasBanner). Searchable: No
        * **sku**: *String* – Used for product identifiers (e.g., sku, part number). Searchable: Yes
        * **path**: *String* – Used for hierarchical fields (e.g., categoryPath). Searchable: No
        * **facet**: *String* – Reserved for internal use by Unbxd for tokenization processing. Searchable: No
        * **nsku**: *String* – Used for B2B catalogs supporting substring matches. Searchable: Yes\
          ***Searchable=Yes means the field is part of the searchable index,
          Searchable= No means the field is part of the searchable index.***
      </td>

      <td>
        Mandatory
      </td>
    </tr>

    <tr>
      <td>
        multiValued
      </td>

      <td>
        The multiValued attribute specifies whether a field can accept multiple values for a product.

        * multiValued = **true** if the field can accept multiple values. For example - a product that can have multiple colors or styles like "Casual" or "Sport"
        * multiValued = **false** if the field can have only one value. For example product brand like "Nike"
      </td>

      <td>
        Mandatory
      </td>
    </tr>

    <tr>
      <td>
        autoSuggest
      </td>

      <td>
        This specifies whether the attribute should have an auto-suggestion feature. This feature helps in providing suggestions as the user types, typically for text-based attributes (e.g., brand, title).
      </td>

      <td>
        Mandatory
      </td>
    </tr>

    <tr>
      <td>
        isVariant
      </td>

      <td>
        The isVariant attribute indicates whether the field is a variant attribute, which is used only for catalogs with variants.

        * isVariant = true for variant attributes (e.g., size, color).
        * isVariant = false for parent product attributes (e.g., title, brand).
      </td>

      <td>
        Optional
      </td>
    </tr>

    <tr>
      <td>
        id
      </td>

      <td>
        This attribute in the schema represents a numerical identifier for an attribute within the catalog. This is useful when product feeds contain **field ID**s instead of **fieldNames**.
      </td>

      <td>
        Optional
      </td>
    </tr>
  </tbody>
</Table>

### Sample Schema

```json json
{
"feed": {
        "catalog": {
            "schema": [{
                "fieldName": "code",
                "dataType": "text",
                "multiValued": "false",
                "autoSuggest": "false",
                "isVariant": "false"
            }, {
                "fieldName": "title",
                "dataType": "text",
                "multiValued": "false",
                "autoSuggest": "false",
                "isVariant": "false"
            }, {
                "fieldName": "imageUrl",
                "dataType": "link",
                "multiValued": "true",
                "autoSuggest": "false",
                "isVariant": "false"
            }, {
                "fieldName": "brand",
                "dataType": "link",
                "multiValued": "true",
                "autoSuggest": "false",
                "isVariant": "false"
            }, {
                "fieldName": "brand",
                "dataType": "link",
                "multiValued": "true",
                "autoSuggest": "false",
                "isVariant": "false"
            }, { 
                "fieldName": "vPrice",
                "dataType": "decimal",
                "multiValued": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }]
        }
 }
}
```

### Schema Upload Process

You can upload a schema using the following methods:

1. APIs: Upload via the schema API (for most use cases).
2. SFTP: Required if post-processing is done by Unbxd on the schema.

### Behavior of Schema Upload

1. Each schema upload appends to the existing schema (if any).
2. If a field already exists, the property values will be updated.
3. New fields are added to the schema.
4. It is not possible to delete existing fields via the API.

### API Parameters

```Text API End Point
Method : POST
 
End Point :  {feed end point}/api/{siteKey}/upload/schema

Description : This API will perform an upload/update of the schema file.
```
```Text Parameter
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
We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
```
```Text Sample Request
curl -X POST https://{Feed end point}/api/{siteKey}/upload/schema 
-H 'Authorization:{secretKey}' 
-F file={file}
```

## Best Practices for Schema Upload

1. Schema is required for all fields (except internal fields created by Unbxd).
2. Ensure your schema file is in JSON format.
3. Field names are case-sensitive.
4. Field names should:
   * Start with an alphabet or underscore.
   * Be alphanumeric, can include hyphens and underscores.
   * Cannot contain special characters, spaces, or end with an underscore.
   * Do not send fields with null values.

s