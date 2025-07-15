---
title: Prepare Your Schema
deprecated: false
hidden: false
metadata:
  robots: index
---
A schema establishes the properties of each attribute within a product catalog and determines the various functions and operations that can be supported for each attribute. For example, a numeric dataType will allow less than, greater than, and range facets, whereas a text dataType will support operations such as contains and support text facets.

***

# Schema Formats

The schema is part of a larger JSON feed file and is defined by the “schema” node. Each JSON object within the schema represents a field within your catalog.

Each field must contain the following properties:

* fieldName (Mandatory)
* dataType (Mandatory)
* multiValued (Mandatory)
* autoSuggest (Mandatory)
* isVariant (Optional)
* id (Optional)

> 📘 Important Recommendation
>
> While we recommend you upload both the schema and catalog as a unified JSON file, you can also upload the schema as a separate file.

## fieldName

The fieldName specifies the name of the attribute such as title, color, and brand. Field names are case-sensitive; should start with an alphabet or underscore; can only contain alphanumeric characters, hyphens and underscores; cannot contain special characters, spaces, or end with an underscore.

## id

The id in schema specifies a numerical identifier for an attribute in the catalog. Useful when product feeds may have the fieldID instead of the fieldName.

## dataType

A dataType defines the type of value a specific field can have. We support the following dataTypes.

| dataType | Format                                      | Description                                                                                                                                                                               | Searchable |
| :------- | :------------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------- |
| text     | String                                      | Used for text fields such as title, color, brand, style, etc.                                                                                                                             | yes        |
| longText | String                                      | Used for large text fields such as description and summary. Not every catalog will contain fields required to be marked as longText.                                                      | Yes        |
| decimal  | Decimal                                     | Used for fields that take decimal values such as price, discount, etc.                                                                                                                    | No         |
| number   | Numeric                                     | Used for fields that take numeric values such as quantity, orderCount, viewCount, etc.                                                                                                    | No         |
| link     | URL (string)                                | Used for fields that take URL strings as values, such as productUrl, imageUrl, etc.                                                                                                       | No         |
| date     | ISO 8601 date format (YYYY-MM-DDTHH:MM:SSZ) | Used for fields that take date values such as createdAt, updatedAt, etc.                                                                                                                  | No         |
| bool     | true/false                                  | Used for fields that take boolean values such as availability, hasBanner, etc.                                                                                                            | No         |
| sku      | String                                      | Used for fields uniquely identifying a product, such as SKU, product number, part number, etc.                                                                                            | No         |
| path     | String                                      | Used for hierarchical fields. E.g., categoryPath. Different values within a hierarchy are separated using “>”. Eg, “Men>Shoes>Casual Shoes”                                               | No         |
| facet    | String                                      | An internally reserved schema type used by Unbxd when processing for spelling, stemming, or tokenization is not required and should not be used by customers unless directed by Unbxd.    | No         |
| nsku     | String                                      | This data type is mainly used for B2B catalogs and supports any substring match, including prefix and suffix matches, special character handling, camel case, and alpha-numeric searches. | No         |

> 📘 Note
>
> Data Types of fields that are made searchable display those products on the search results page. Data Types that are not searchable can be used for filtering, sorting, and faceting.

## multiValued

A multiValued attribute determines if a field can have multiple values for a product. For example, a Nike shoe can be considered sporty and casual in which case you could send multiple values for a style field: “style”:\[“casual”,”sport”]. However, a field such as brand would be single-valued: “brand”:”Nike”. To enable a field to accept multiple values, set multiValued to true, otherwise to false.

## isVariant

Only required for catalogs with variants, if an attribute is a variant field instead of a parent product field, set it to true, else set it to false.

***

## Sample Schema

```
{
"feed": {
        "catalog": {
            "schema": [{
                "fieldName": "vColor",
                "id": "76678",
                "dataType": "text",
                "multiValued":true,
                "autoSuggest":false,
                "isVariant":true
            }, {
                "fieldName": "vSize",
                "dataType": "text",
                "multiValued":true,
                "autoSuggest":false,
                "isVariant":true
            }, {
                "fieldName": "vImages",
                "dataType": "link",
                "multiValued":true,
                "autoSuggest":false,
                "isVariant":true
            },
{
                "fieldName": "vPrice",
                "dataType": "decimal",
                "multiValued":true,
                "autoSuggest":false,
                "isVariant":true
            }]
        }
    }
}
```

***

## Schema Upload Process

You can upload a schema using APIs with the exception of instances where any post-processing is performed by Unbxd on your schema which requires an SFTP upload.

Every schema upload appends to an existing schema, if any. You can update the characteristics

In case the schema has fields that are already found within an existing schema, the property values of the existing fields are updated. Similarly, when the new schema has new fields that are not found within an existing schema, the existing schema appends and adds the new fields. It is currently not possible to delete existing fields through the schema API.

***

# API Parameters

The API parameters along with sample request and response are defined below:

\<Tabs>
&#x20; \<Tab title="API Endpoint">
&#x20;  Method : POST
End Point :  \{feed end point}/\{siteKey}/upload/schema
Description : This API will perform an upload/update of the schema file.
&#x20; \</Tab>

&#x20; \<Tab title="Parameters">
\*\*siteKey\*\*: A unique identifier provided when your Unbxd account is created. This key can also be retrieved from your Unbxd Console. This is a required field.

secretKey: A unique identifier provided when your Unbxd account is created. The secretKey is used to authorize your upload request. This is a private key and will not be exposed to the public. This is a required field.

file: The name of the schema, as a JSON file.

feed end point : The feed end point depends upon the region selected at the time of site creation.

US region: http\://feed.unbxd.io/

ANZ region : http\://feed-anz.unbxd.io/

UK region : http\://feed-uk.unbxd.io/

SG region : http\://feed-apac.unbxd.io/
&#x20; \</Tab>

&#x20; \<Tab title="Error Codes">
&#x20;   We use conventional HTTP response codes to indicate success or failure of an API request.
201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
&#x20; \</Tab>

&#x20; \<Tab title="Sample Request">
&#x20; curl -X POST https\://\{Feed end point}/api/\{siteKey}/upload/schema&#x20;
-H 'Authorization:\{secretKey}'&#x20;
-F file=\{file}
&#x20; \</Tab>
\</Tabs>

***

# Best Practices

To ensure your schema is uploaded and integrated seamlessly, here are some practices we recommend:

* Schema is required for all fields (except for internal fields created by Unbxd)
* Schemas not adequately defined will be rejected.
* Ensure your schema file is in JSON format.
* Field names are case-sensitive.
* Field names should start with alphabets or underscore. It can be alphanumeric, can have hyphens and underscores. It cannot contain special characters, spaces in between words, or end with an underscore.
* Do not send fields that have null values.