---
title: Feed Preparation and Upload
deprecated: false
hidden: false
metadata:
  robots: index
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
        Mandatory (Yes/ No)
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
        The multiValued attribute specifies whether a field can accept multiple values for a product.Set multiValued to true if the field can accept multiple values (e.g., a product that can have multiple colors or styles).

        <br />

        Set multiValued to false if the field can have only one value (e.g., product brand).
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

<br />

fieldName

Case-sensitive.

Should start with an alphabet or underscore.

Can only contain alphanumeric characters, hyphens (-), and underscores (\_).

Cannot contain special characters or spaces.

Cannot end with an underscore.

id\
The id attribute in the schema represents a numerical identifier for an attribute within the catalog. This is useful when product feeds contain field IDs instead of field names.