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

<Image align="center" border={true} caption="Navigate to Attribute Enrichment" src="https://files.readme.io/c11597b6b36f4e095708b2465e4febeff07caaa75a1f38abbf5c85bebbc80637-Attri_enrich_gif.gif" width="80% " />

## Dashboard Keywords and Their Functionality

**Attribute Enrichment** improves the discoverability of your products by ensuring that your product catalog has the necessary and complete attributes. There are three metrics of the **Attribute Enrichment**

| **Metric**             | **Description**                                                                                                    |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Total Dimensions**   | The total number of attributes being tracked for enrichment in your product catalog.                               |
| **Missing Dimensions** | The number of attributes that are currently missing or incomplete in the catalog and need to be enriched.          |
| **Mapped Dimensions**  | The attributes that have been successfully mapped to the system, meaning they are linked and ready for enrichment. |

This below section on the dashboard, helps you monitor the overall progress of your attribute enrichment process and provides clarity on which attributes are ready, which ones are missing, and how many are already mapped for enrichment.

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        **Section**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Search**
      </td>

      <td>
        Allows you to search for specific attributes or products in the catalog. It helps quickly locate dimensions or attributes that need enrichment.
      </td>
    </tr>

    <tr>
      <td>
        **Rerun**
      </td>

      <td>
        Triggers the enrichment process again for attributes. This button is useful for refreshing or recalculating attribute data when necessary.
      </td>
    </tr>

    <tr>
      <td>
        **Filter**
      </td>

      <td>
        Opens the Filter Options, where you can apply filters based on the below:

        * **By State**
          **Mapped**: Attributes that have been successfully linked to the system.
          **Unmapped**: Attributes that are not yet linked or integrated.
          **Enriching**: Attributes currently being enriched.
          **Review**: Attributes that are pending review or validation.
          **Enriched**: Fully enriched attributes.
        * **By Category**: Filter attributes by specific product categories to focus on attributes that are relevant to particular types of products.
        * **By Type**: Filter attributes by their data type, such as
          **Metrics**: Numerical or measurable attributes
          **Info**: Descriptive attributes
      </td>
    </tr>

    <tr>
      <td>
        **[Enrich Attributes]()**
      </td>

      <td>
        Initiates the enrichment process for selected attributes. By clicking this, you can automatically enrich missing or incomplete attributes using AI-driven enhancements.
      </td>
    </tr>

    <tr>
      <td>
        **Dimensions**
      </td>

      <td>
        It refer to standard attributes taken from **Google taxonomy** that should be present in your product catalog to enhance search performance.
      </td>
    </tr>

    <tr>
      <td>
        **Completeness**
      </td>

      <td>
        Indicates the progress or percentage of completion for the enrichment process of the catalog.\
        refers to the percentage of products that have attribute values, calculated within the relevant categories.
      </td>
    </tr>

    <tr>
      <td>
        **Missing In Products**
      </td>

      <td>
        This field indicates the number of products that are currently missing values for a particular attribute within the relevant categories.
      </td>
    </tr>

    <tr>
      <td>
        **Status**
      </td>

      <td>
        The Status reflects the current stage of enrichment for an attribute.

        * **Mapped**: The attribute is linked to the system and ready for enrichment.
        * **Unmapped**: The attribute is not yet linked or integrated into the system.
        * **Enriching**: The attribute is currently being enriched with data.
        * **In Review**: The enriched attribute is pending approval or verification.
        * **Complete**: The attribute enrichment process is finished.
      </td>
    </tr>

    <tr>
      <td>
        **Catalog Attributes**
      </td>

      <td>
        It refers to the catalog fields that have been mapped to other dimensions, such as **Google attributes**. This mapping shows the actual linkage between your **product catalog** and the **Google taxonomy**, ensuring that your product data is properly categorized and ready for search optimization.
      </td>
    </tr>
  </tbody>
</Table>

> 👍 Good to know:
>
> **Google Taxonomy** is a structured classification system used by Google to categorize products in various categories for search and shopping purposes. It is a standardized list of product categories that help organize products and ensure they appear in relevant search results across Google services, such as Google Search, Google Shopping, and Google Ads.

## Add New Enrichment

1. On the Attribute Enrichment Dashboard, scroll on the Attribute listing page to click on **Enrich**.
2. Select the [Strategies](https://unbxdocs.readme.io/docs/attribute-enrichment#/product-enrichment-strategies) that suit your requirement and click on **Next**.
3. Map your attributes and click **Preview** or **Run on entire catalog**.

Leverage Attribute Enrichment to boost your e-commerce platform’s search experience and overall conversion metrics.

> 📘 Note
>
> For a personalized walkthrough, consider booking a demo or requesting a search experience audit through your Netcore Unbxd account.