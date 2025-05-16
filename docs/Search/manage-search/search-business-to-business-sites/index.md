---
title: Business-to-Business Sites
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Search plays a critical role in B2B e-commerce sites, with 92% of B2B purchases beginning with a search. However, B2B e-commerce sites face unique challenges such as managing large catalogs, complex pricing models, user group-based restrictions, and different variations of SKU searches. **Unbxd** empowers B2B stores to provide a seamless, consumer-grade search experience while handling the complexities specific to the B2B space.

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

**Use Case for Creating the Search Request**

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

The prices, discounts & taxes of products on B2B sites may change based on the user group of the buyer. We allow B2B sites to handle this complexity by adding the pricing, tax and discount information for each user group. When a user searches on the website, only the relevant prices, discounts & taxes applicable for the buyer are returned.

How to support different prices for different user groups ?\
Let’s take the same B2B office supplier discussed above. Now let’s assume that the retailer wants to set different prices of HP Inkjet printers (P3) for IT Companies (group1) and Backoffices (group2). The table below describes the scenario.

| ProductID | Title                | UserGroup | Price |
| --------- | -------------------- | --------- | ----- |
| P1        | Lenovo laptop        | group1    | $670  |
| P2        | Xerox Copier machine | group2    | $950  |
| P3        | HP Inkjet printer    | group1    | $650  |
| P3        | HP Inkjet printer    | group2    | $600  |

In our previous example, Product P3 was accessible to both user groups. in this scenario, business has more complicated requirements where if this product is being viewed by a buyer from IT Companies (group1) then price of the product should be shown as $650 and if the product is being viewed by a buyer from Backoffices (group2) then price of the product should be shown as $600.

Unbxd Feed Example:

```
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
			"price":600
		}
	]
}]
```

**Use Case for Creating the Search Request for**

1. When a buyer from IT companies (group1) logs in to the B2B site and searches for “Printer”. The following search API will be triggered :

```
https://search.unbxd.io/{APIKEY}/{SITEKEY}/search?q="Printer"&variants.condition=user_group:"group1"
```

This API request will return P3 the variant document for group1 which has the price as 650.

2. When a buyer from Backoffices (group2) logs in to the B2B site and searches for “printer”. The following search API will be triggered :
   ```
   https://search.unbxd.io/{APIKEY}/{SITEKEY}/search?q="printer"&variants.condition=user_group:"group2"
   ```

This API request will return the product P3 and P2. For the product P3, only the variant document with price of $600 would be returned.

### 5. Multi-Seller and Multi-User Group Scenario

We have two sellers: **Seller 1** and\*\* Seller 2\*\*. Seller 1 may choose to classify small scale IT companies and enterprise IT companies in different user groups to sell them products at different prices. But Seller 2 may classify both the small scale IT companies and enterprise IT companies in the same group. So, a shopper may be assigned to usergroup\_1 by Seller 1 and usergroup\_3 by Seller 2.

<br />

| **Seller**  | **Small Scale IT Companies (User Group 1)** | **Enterprise IT Companies (User Group 2)** | **Comments**                                                                                                        |
| ----------- | ------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| **Seller1** | usergroup\_1                                | usergroup\_2                               | Seller 1 classifies small scale and enterprise IT companies in different user groups (usergroup\_1 & usergroup\_2). |
| **Seller2** | usergroup\_3                                | usergroup\_3                               | Seller 2 considers both small scale and enterprise IT companies in a single user group (usergroup\_3).              |

**Unbxd Feed Structure Sample Example**:

```
[{
	"uniqueId" :"124",
	"title":"Lenevo laptop 9th generation",
	"variants":[{

		"usergroup":"usergroup_1",
		"seller_id" : "seller_1",
		"price" :100$
	},{
		"usergroup":"usergroup_2",
		"seller_id":"seller_1",
		"price":150$
	},{
		"usergroup":"usergroup_3",
		"seller_id":"seller_2",
		"price":120$
	}]
},
{
	"uniqueId" :"4572",
	"title":"Xerox Copier Machine multipurpose",
	"variants":[{

		"usergroup":"usergroup_3",
		"seller_id" : "seller_2",
		"price" :500$
	}]
},
{
	"uniqueId" :"34634",
	"title":"HP Laptops with Intel CPU inside",
	"variants":[{

		"usergroup":"usergroup_3",
		"seller_id" : "seller_2",
		"price" :120$
	}]
},
{
	"uniqueId" :"92457",
	"title":"HP Inkjet Printer ",
	"variants":[{

		"usergroup":"usergroup_1",
		"seller_id" : "seller_1",
		"price" :300$
	},{
		"usergroup":"usergroup_2",
		"seller_id":"seller_1",
		"price":350$
	}]
}]
```

**Use Case for Creating the Search Request for**

When Shopper 1 is looking for Laptops, first fetch the seller and user group relationship, which in this case is – Seller 1 and Usergroup 1 ; Seller 2 and Usergroup 3. The API request to Unbxd will then look like below:

```Text API format
https://search.unbxd.io/{APIKEY}/{SITEKEY}/search?q="laptops"&variants.condition=(seller_id:"seller_1" AND usergroup:"usergroup_1" ) OR (seller_id:"seller_2" AND usergroup:"usergroup_A" )
```

In this case, the user sees Lenovo Laptop (124) & HP Laptop (34634). Since Lenovo laptop (124) is sold through Seller 1 and Seller 2, this product will show both pricing options for the user ($100, $120).