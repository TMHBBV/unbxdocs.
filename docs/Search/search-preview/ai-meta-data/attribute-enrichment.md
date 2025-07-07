---
title: Attribute Enrichment
excerpt: >-
  Leverages AI to automatically fill in missing or incomplete product
  attributes, enhancing search visibility and improving product discoverability.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The **Attribute Enrichment** in the console aims to enhance catalog completeness for optimal search performance. This dashboard facilitates the identification of missing or incomplete attributes in product catalogs, providing detailed metrics and allowing merchandisers to prioritize enrichment efforts. It presents various attributes, their status, and their impact on search performance.

## Why is this Useful?

Merchandisers often struggle with incomplete or inconsistent product data, such as missing attributes for key categories like **material** for a **T-shirt** or **screen size** for a **Smartwatch**. These gaps can lead to:

* **Poor Search Relevance**: Customers might not find products if key attributes are missing.
* **Reduced Discoverability**: Filters and facets relying on these attributes won't function effectively.
* **Inconsistent Product Information**: Leading to a fragmented customer experience.

**AI Suggested Redirects** leverages advanced [strategies](https://unbxdocs.readme.io/docs/attribute-enrichment#/product-enrichment-strategies) to intelligently suggest redirects based on past search patterns, filling in these gaps and improving product visibility. This ensures a smoother and more relevant shopping experience for your customers.

### Product Enrichment Strategies

The Netcore Unbxd console offers four core enrichment strategies to help you optimize and enhance your product catalog.

1. **Large Language Models (LLMs)**

This strategy harnesses the power of **Large Language Models (LLMs)** to intelligently generate new, missing product fields based on existing information in your catalog. It's ideal for creating descriptive content or structured data points that are not readily available.

For Example: For a **"Smartwatch"** missing the "battery life" attribute, the LLM analyzes the product description, such as "Up to 48 hours of usage on a single charge," and automatically adds the missing "battery life" data.

2. **Google Translator Enrichment**

This strategy enables the translation of existing product fields from one language (typically English) into a specified target language. It helps expand your e-commerce presence into new markets and provides localized search experiences by generating multilingual product data.

For Example: **Original Product Data:**

```Text Original Product Data
{  
  "id": "PROD123",  
  "product_type": "Smartwatch"  
}  

```
```Text Enriched Product Data (after translation)
{  
  "id": "PROD123",  
  "product_type": "Smartwatch",  
  "enr_unx_ar_translate_product_type": "ساعة ذكية"  
} 
```

3. **Transliterate Enrichment**

The Transliterate Enrichment strategy converts text from one script to another while preserving phonetic pronunciation. This is especially useful for search queries where users might type foreign words using English characters. It differs from translation by changing the script, not the meaning.

For Example : 1. **English to Hindi Transliteration**

```Text Original Product Data
{  
  "id": "GROCERY456",  
  "product_name": "Basmati Rice"  
}  
```
```Text Enriched Product Data (after Transliterate processing):
{  
  "id": "GROCERY456",  
  "product_name": "Basmati Rice",  
  "enr_unx_hi_translit_product_name": "bāsmatī rā'is"  
}  
```

For Example: 2. **Latin Script - Similar to Translation**

```Text Original Product Data
{  
  "id": "PROD123",  
  "product_type": "Smartwatch"  
}  
```
````Text Enriched Product Data (after Transliterate processing):
{  
  "id": "PROD123",  
  "product_type": "Smartwatch",  
  "enr_unx_es_translit_product_type": "Reloj inteligente"  
}  
```  | 

This format simplifies the explanation and example for users, making it easy to understand the functionality of the **Transliterate Enrichment** strategy.
````

4. **SEO Keyword Enrichment**:

The SEO Keyword Enrichment strategy uses Large Language Models (LLM) to generate relevant SEO keywords for your products based on existing product data. These keywords help improve your product's visibility in organic search results, driving more traffic to your e-commerce site.

For Example: **Configuration from fields: product\_title, description, category**

```Text Original Product Data
{  
  "id": "PROD789",  
  "product_title": "Organic Cotton Baby Bodysuit",  
  "description": "Soft and breathable 100% organic cotton bodysuit for infants aged 0-6 months. Features snap closures for easy diaper changes and a cute animal print. Perfect for sensitive skin.",  
  "category": "Baby Clothing"  
} 
```
````Text Enriched Product Data (after SEO Keyword processing):
{  
  "id": "PROD789",  
  "product_title": "Organic Cotton Baby Bodysuit",  
  "description": "Soft and breathable 100% organic cotton bodysuit for infants aged 0-6 months. Features snap closures for easy diaper changes and a cute animal print. Perfect for sensitive skin.",  
  "category": "Baby Clothing",  
  "seo_keywords": [  
    "organic baby clothes",  
    "cotton bodysuit infant",  
    "newborn organic cotton",  
    "baby clothes 0-6 months",  
    "snap closure bodysuit",  
    "sensitive skin baby clothes",  
    "animal print baby outfit"  
  ]  
}  
```  |

This format breaks down how the SEO Keyword Enrichment strategy works, providing a simple explanation and an example of how it generates SEO keywords from product data.

````

## How to Get Started

Log in to Netcore Unbxd Dashboard and navigate to **Manage** > **Catalog** > **Attribute Enrichment**

<Image align="center" border={true} caption="Navigate to Attribute Enrichment" src="https://files.readme.io/4dac8cf8173b238cc8e531f14d089772e618331133cb30e58c3e82a7177229d9-Attribute_Enrichment.gif" width="80% " />

1. Initial Setup: Map product attributes to Google Category taxonomy (e.g., Product Title, Category, Brand) using the "Target Field" column.
2. Track Completeness: Ensure the "Completeness" column accurately reflects the percentage of attributes populated for each product category.
3. Define Metrics: Set up calculation formulas for the "Missing" and "Search Impact" columns based on product data and search analytics.
4. Monitor Progress: Use the "Status" and "Mapping" columns to monitor the enrichment process and track the lifecycle of each attribute.
5. Prioritize Action: Use the "Actions" column to trigger appropriate actions (enrich, publish, review) based on the status of each attribute.

## Dashboard Keywords and Their Functionality

Below are the functionality present on the Netcore Unbxd Console.

| **Section**             | **Description**                                                                                                                                                                                                                                                                                                        | **Details from Image**                                                                             |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| **Dimensions**          | Dimensions refer to standard attributes taken from [Google taxonomy]() that should be present in your product catalog to enhance search performance. These dimensions are essential for improving how your products are discovered and ranked in search results, making them an integral part of attribute enrichment. | **33** total dimensions.                                                                           |
| **Mapped Dimensions**   | Shows the attributes that have been successfully mapped and are ready for enrichment.                                                                                                                                                                                                                                  | **19** mapped dimensions.                                                                          |
| **Missing Dimensions**  | Tracks the attributes that are missing or incomplete in your catalog and need to be enriched.                                                                                                                                                                                                                          | **14** missing dimensions.                                                                         |
| **Completeness**        | Indicates the progress or percentage of completion for the enrichment process of the catalog.                                                                                                                                                                                                                          | Visual progress circle shows the overall state of enrichment (partially filled).                   |
| **Missing In Products** | Displays the number of products missing certain attributes, indicating which products need to be enriched.                                                                                                                                                                                                             | **302** products missing specific attributes.                                                      |
| **Status**              | Shows the current status of attributes: **Mapped**, **In Review**, **Unmapped**, or **Enriched**.                                                                                                                                                                                                                      | Attributes are in various states: **Mapped**, **In Review**, **Unmapped**.                         |
| **Catalog Attributes**  | Provides a detailed view of each catalog attribute’s enrichment process, including its status and necessary actions to complete enrichment.                                                                                                                                                                            | Includes catalog attributes like **adwords\_grouping**, **dress\_occasion**, and **dress\_style**. |

> 👍 Good to know:
>
> **Google Taxonomy** is a structured classification system used by Google to categorize products in various categories for search and shopping purposes. It is a standardized list of product categories that help organize products and ensure they appear in relevant search results across Google services, such as Google Search, Google Shopping, and Google Ads.

## Add New Enrichment

1. On the Attribute Enrichment Dashboard, scroll on the Attribute listing page to click on **Enrich**.

<Image align="center" border={true} caption="Add New Attribute Enrichment" src="https://files.readme.io/a2e8d0948e14068c9a7c1b09e2714aa5f4e3f83f0274c3ee8d26e3dcada5b438-setup_attribute_enrich.gif" width="80% " />

2. Select the [Strategies](https://unbxdocs.readme.io/docs/attribute-enrichment#/product-enrichment-strategies) that suit your requirement and click on **Next**.
3. Map your attributes and click **Preview** or **Run on entire catalog**.

Leverage Attribute Enrichment to boost your e-commerce platform’s search experience and overall conversion metrics.

> 📘 Note
>
> For a personalized walkthrough, consider booking a demo or requesting a search experience audit through your Netcore Unbxd account.