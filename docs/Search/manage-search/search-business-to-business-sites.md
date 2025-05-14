---
title: 'Search: Business-to-Business Sites'
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Search plays a critical role in B2B e-commerce sites, with 92% of B2B purchases beginning with a search, according to Forrester. However, B2B e-commerce sites face unique challenges such as managing large catalogs, complex pricing models, user group-based restrictions, and different variations of SKU searches. **Unbxd** empowers B2B stores to provide a seamless, consumer-grade search experience while handling the complexities specific to the B2B space.

### Challenges Faced by B2B Sites:

* Large catalogs with over 100,000 products.
* Pricing based on user groups.
* Product visibility restrictions based on user groups.
* Different variations of **Stock Keeping Unit** search.
* Large numbers of facets customized across categories.

Unbxd offers features specifically designed for B2B sites to address these challenges. These include SKU search, faceted search, catalog visibility based on user groups, and multi-seller, multi-user group pricing.

## B2B Search Features

Unbxd offers advanced search capabilities for B2B e-commerce, including SKU optimization, faceted filtering, user group-based catalog visibility, and dynamic pricing to streamline the shopping experience for businesses.

### 1. SKU Search

In B2B e-commerce, repeat purchases are common, and many users search using SKU IDs. Unbxd optimizes SKU searches by handling SKU attributes differently from text attributes. We have designed two data types, sku and nsku, to improve SKU search performance.

**SKU Data Type**\
The SKU data type supports searches based on partial SKU matches (e.g., users can search by the first few characters of the SKU ID). It also supports Camel case and Alphanumeric searches.

**Example**:

| SKU IDs       | Query Description                                   | Match Type                 |
| ------------- | --------------------------------------------------- | -------------------------- |
| CM532-REQS/RE | Exact SKU with special characters                   | Matches with SKU ID        |
| CM532 REQS RE | Exact SKU without special characters                | Matches with SKU ID        |
| CM532-REQS RE | Exact SKU with a special character omitted          | Matches with SKU ID        |
| CM53          | Partial SKU search with trailing characters removed | Matches with SKU ID        |
| REQS/RE       | Partial SKU search with leading characters removed  | Does not match with SKU ID |

```json
{
  "dataType": "sku",
  "multiValue": "false",
  "autoSuggest": "false",
  "fieldName": "manufacture_part_id"
}

```

**NSKU Data Type**\
The nsku data type allows for more flexible substring matches within SKU IDs, supporting prefix, suffix, and partial matches, including special characters.

| NSKU ID        | Query Description                                   | Match Type          |
| :------------- | :-------------------------------------------------- | :------------------ |
| MOTR-900044/34 | Exact SKU with special characters                   | Matches with SKU ID |
| MOTR 900044 34 | Exact SKU without special characters                | Matches with SKU ID |
| MOTR-900044 34 | Exact SKU with a special character omitted          | Matches with SKU ID |
| MOTR-90        | Partial SKU search with trailing characters removed | Matches with SKU ID |
| 900044/34      | Partial SKU search with leading characters removed  | Matches with SKU ID |

```Text JSON
{
  "dataType": "nsku",
  "multiValue": "false",
  "autoSuggest": "false",
  "fieldName": "part_id"
}
```

### 2. Faceted Search

B2B shoppers know exactly what they are looking for and need an efficient way to filter products. Unbxd supports faceted search that allows users to quickly narrow down results. B2B sites can control facet visibility and ordering using Field Rules. B2B sites can define thousands of facets globally and customize facet experiences for category pages. Hierarchical facets enable users to drill down through multi-level product classifications.

### 3. Catalog Visibility Based on User Groups

In a B2B business that sells office supplies, customers are grouped into different user categories based on the products they commonly purchase. For this example, there are two main customer groups:

1. IT Companies
2. Backoffices

IT Companies typically purchases products such as Laptops, Monitors, and Printers. The B2B retailer has provided access to products within the Laptop and Printers categories for this group. Therefore, Group 1 has access to the Lenovo Laptop (P1) and the HP Inkjet Printer (P3).

Backoffices usually purchases products like Printers, Paper Supplies, Scanners, and Xerox Machines. For this group, the retailer has granted access to products from the Printers and Copier Devices categories. As a result, Backoffices can access the Xerox Machine (P2) and the HP Inkjet Printer (P3).

The table below summarizes the product access for each group:

Group 1 (IT Companies):

Lenovo Laptop (P1)

HP Inkjet Printer (P3)

Group 2 (Backoffices):

Xerox Machine (P2)

HP Inkjet Printer (P3)

```Text JSON
[{
  "uniqueId": "P1",
  "title": "Lenovo laptop",
  "description": "Lenovo laptops 9th generation CPU.",
  "variants": [
    {
      "user_group": "group1",
      "price": 670
    }
  ]
},
{
  "uniqueId": "P2",
  "title": "Xerox Copier Machine",
  "description": "Xerox Machine with double side printing.",
  "variants": [
    {
      "user_group": "group2",
      "price": 950
    }
  ]
}]
```

Search Request Examples:

* Group 1 ([IT companies](https://search.unbxd.io/\{APIKEY}/\{SITEKEY}/search?q="Laptop"\&variants.condition=user_group:"group1))
* Group 2 ([Backoffices](https://search.unbxd.io/\{APIKEY}/\{SITEKEY}/search?q="printer"\&variants.condition=user_group:"group2))

### 4. Pricing Based on User Groups

B2B sites often have different pricing, discounts, and taxes based on user groups. Unbxd supports this by indexing product prices, discounts, and taxes for each user group.Example of Different Pricing for User Groups:

| ProductID | Title                | UserGroup | Price |
| --------- | -------------------- | --------- | ----- |
| P1        | Lenovo laptop        | group1    | $670  |
| P2        | Xerox Copier machine | group2    | $950  |
| P3        | HP Inkjet printer    | group1    | $650  |
| P3        | HP Inkjet printer    | group2    | $600  |

Search Request Examples:

* Group 1 (IT companies): [https://search.unbxd.io/\{APIKEY}/\{SITEKEY}/search?q="Printer"\&variants.condition=user\_group:"group1](https://search.unbxd.io/\{APIKEY}/\{SITEKEY}/search?q="Printer"\&variants.condition=user_group:"group1)"
* Group 2 (Backoffices): [https://search.unbxd.io/\{APIKEY}/\{SITEKEY}/search?q="printer"\&variants.condition=user\_group:"group2](https://search.unbxd.io/\{APIKEY}/\{SITEKEY}/search?q="printer"\&variants.condition=user_group:"group2)

### 5. Multi-Seller and Multi-User Group Scenario

Unbxd supports complex scenarios where multiple sellers serve multiple user groups with varying prices and availability. This functionality is useful for B2B marketplaces with multiple sellers. For Example:

| ProductID | Seller   | UserGroup 1 Pricing | UserGroup 2 Pricing | UserGroup 3 Pricing |
| --------- | -------- | ------------------- | ------------------- | ------------------- |
| 124       | Seller 1 | $100                | $150                | NA                  |
| 124       | Seller 2 | NA                  | NA                  | $120                |

Search Request Example:\
For a shopper looking for Laptops from multiple sellers:

```Text Plaintext
https://search.unbxd.io/{APIKEY}/{SITEKEY}/search?q="laptops"&variants.condition=(seller_id:"seller_1" AND usergroup:"usergroup_1") OR (seller_id:"seller_2" AND usergroup:"usergroup_3")
```

This will return both pricing options for the Lenovo Laptop.