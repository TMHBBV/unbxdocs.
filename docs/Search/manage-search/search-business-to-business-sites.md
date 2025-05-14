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

Let’s take a B2B business which sells office supplies.  The business may group all the  IT companies into the same user group (say  group1) who commonly purchas products such as Laptops, Monitors, Printers etc. The Backoffices customers may be  grouped into a different user group (say group2) who commonly purchase products like Printers, Paper Supply, Scanner, Xerox Machine.

For this example let’s assume that there are three products: Lenovo laptop (P1),Xerox machine (P2) and HP Inkjet printer (P3). The B2B retailer has allowed IT companies (group1) access to products from categories Laptop & Printers (i.e. P1 & P3 are accessible to group1). Similarly, the B2B retailer has allowed Backoffices (group2) access to products from categories Printers & Copier devices (i.e. group2 has access to P2 and P3). The table below summarises this scenario.

| **Product ID** | **Title**            | **User Group Authorized** | **Price** |
| -------------- | -------------------- | ------------------------- | --------- |
| P1             | Lenovo Laptop        | group1                    | $670      |
| P2             | Xerox Copier Machine | group2                    | $950      |
| P3             | HP Inkjet Printer    | group1, group2            | $650      |

<br />

```Text JSON
[{
	"uniqueId": "P1",
	"title": "Lenovo laptop",
	"description": "Lenovo laptops 9th generation CPU. Compatible with wireless printer.",
	"variants":[
		{
			"user_group" :"group1",
			"price":670
		}

	]
},

{
	"uniqueId": "P2",
	"title": "Xerox Copier Machine",
	"description": "Xerox Machine with double side printing. USB connection with laptop to transfer scanned documents.",
	"variants":[
		{
			"user_group" :"group2",
			"price":950
		}

	]
},

{
	"uniqueId": "P3",
	"title": "HP Ink Printer",
	"description": "HP Inkjet printer for fine printing.",
	"variants":[
		{
			"user_group" :"group1",
			"price":650
		},
		{
			"user_group" :"group2",
			"price":650
		}
	]
}]
```

**Creating the Search Request**

1. **When a buyer from IT companies (group1) logs in to the B2B site and searches for “Laptop”, the following search API will be triggered**

```
https://search.unbxd.io/{APIKEY}/{SITEKEY}/search?q="Laptop"&variants.condition=user_group:"group1"
```

**Description**: This API request will return only product P1. The product P2 has the term “laptop” in description so it matches the search term. Since the buyers from group1 do not have access to P2 it will be hidden from the search result for this user.

2. **When a buyer from Backoffices (group2) logs in to the B2B site and searches for “printer”. The following search API will be triggered**

```
https://search.unbxd.io/{APIKEY}/{SITEKEY}/search?q="printer"&variants.condition=user_group:"group2"
```

**Description**: Although, the products P1 & P3 have the term printer in title or description. The search request will only return the product P2 because the buyer only has access to P2.

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