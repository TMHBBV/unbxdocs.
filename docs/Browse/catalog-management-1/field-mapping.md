---
title: Field Mapping
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The fields for a product are defined in the schema file with their respective values defined in the feed file. For example, a product “Mobile phone” can have fields like brand, price, color, manufacturing date, etc.

Why do we need to map fields?

You need to map fields because you might have defined the field name differently in your catalog than what exists as Unbxd’s feature field attribute. In such cases, the particular field attribute then becomes unsearchable because of the mismatch.

Suppose, you have called your field ‘amount1’, ‘amount2’, ‘amount3’ in your catalog and you know that ‘amount3’ represents Price. You can use Field mapping to map ‘Price’ to ‘amount3’ so that going forward you can just mention ‘Price’ in any of your campaign and we’ll know to map it to ‘amount3’ field in your catalog.

What are Feature fields and Custom Fields?

Feature Fields are pre-defined Unbxd fields while Custom fields are the fields define by you.

Let’s read about them in detail.

# Feature Fields

Feature fields are a list of predefined Unbxd fields with a fixed schema that doesn’t need to be defined in the feed file. These fields are necessary for Autosuggest and Recommendations to work properly.

In most cases, you do not have to define the schema for these fields, however, when the feature field does not match with the corresponding field within your product feed, you can define the schema by the dataType of that field.

For example, if you have the field ‘amount’ that indicates the price of the product, you can map the field ‘amount’ to ‘price’ and not have to redefine the schema.

In another example, if the “size” field in your catalog has data type “decimal” instead of text, the schema for the “size” field has to be defined in the product feed. Similarly, if the “gender” field in your catalog is “multivalue=true” instead of false, the schema for the “gender” field would need to be defined before the product attribute data in the Product Feed.

> 📘 Note
>
> Feature Fields can be used without explicitly defining them in the schema. If you have a similar field, you can either map it to the corresponding feature field from the Console or  rename your existing field to a feature field in the schema.

# Custom Fields

Attributes that are not a part of our list of Feature Fields but part of your product catalog are known as Custom Fields. These attributes and their properties are included in your schema.

Like Feature fields, our search engines use these attributes to power product discovery on your web page.