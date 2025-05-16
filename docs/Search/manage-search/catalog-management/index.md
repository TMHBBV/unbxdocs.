---
title: 'Catalog Management '
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Catalog management allows you to configure and monitor your product catalog from the console. You can track the status of recent catalog uploads, adjust field mappings to enhance the understanding of your catalog by algorithms, and make changes to certain schema items directly from the console.

## Field Mapping

Field mapping helps define the relationship between product fields in your catalog and Unbxd's feature field attributes. Fields are defined in your catalog schema file and linked to the respective values in the product feed file. **For example**, A product like “Mobile phone” might have fields like brand, price, color, manufacturing date, etc.

### Why Do We Need to Map Fields?

Mapping is necessary when field names in your catalog do not match the predefined feature fields in Unbxd's system. If there’s a mismatch, the field attribute becomes unsearchable. **For example**, if you have a field named ‘amount3’ in your catalog to represent price, and Unbxd expects a field called ‘Price’, you can use field mapping to map ‘Price’ to ‘amount3’. This ensures that, going forward, when you mention ‘Price’ in campaigns, the system will know to map it to ‘amount3’ in your catalog.

## Feature Fields vs. Custom Fields

**Feature Fields** are predefined fields in Unbxd with a fixed schema, not requiring definition in the feed file. These fields are crucial for functionality such as Autosuggest and Recommendations. **Example**: If your catalog has a field named ‘amount’ to indicate price, you can map it to the feature field ‘price’ without needing to redefine the schema.

Feature fields are automatically handled unless there is a data mismatch. If the feature field and the catalog field are not aligned (e.g., a data type mismatch), you must define the schema in the product feed. **Example**: If the “size” field in your catalog is of data type “decimal” instead of text, you must specify this in your schema. Similarly, for multi-value fields like “gender”, the schema must reflect the correct setting.

> 📘 Note
>
> Feature fields can be used without explicitly defining them in the schema. If you have a similar field, you can either map it to the corresponding feature field or rename it to match a feature field in the schema.

Only fields present in the user catalog will be visible by default. All fields in the user catalog should also be present in the schema upload. If a feature field is found in the user catalog, it must match the corresponding feature field's data type in the schema (e.g., "category" must be defined as "string").

> 📘 Important
>
> Fields of data type “path” are handled differently. Fields like “catinfo” and its variations such as “catinfo1,” “catinfo2,” will appear in the console.

**Custom fields** are product attributes that are not part of Unbxd’s predefined feature fields but are present in your catalog. These attributes and their properties are included in the schema. Like feature fields, custom fields power product discovery through Unbxd’s search engine and can influence the product recommendations on your web page.