---
title: 'Named Entity Recognition (NER) '
excerpt: >-
  Help in understanding the intent of the user by adding semantic knowledge with
  a query.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Named Entity Recognition (NER) models, also referred to as entity extraction models are machine learning models that tokenize each search query to map it to the desired attributes and return the most relevant products with the highest precision. It goes beyond simple text-pattern matching techniques.

NER identifies pre-defined attributes (called entity) from a search query to decode the shopper’s intent. For example for a search query “**red polka dot dress for women**”, the NER model will detect the following entities:

**COLOR** : “red”\
**PATTERN** : “polka dot”
**PRODUCT TYPE** : “dress”
**GENDER** : “Women”

## Strategies in NER

NER is calculated based on two strategies:

1. Re-rank search results using detected entities
2. Increase the product count in the search result

**Let’s look at both strategies in detail.**

### Re-rank search results using detected entities​

Once the NER model identifies the entities, it uses the field mappings (done as part of the NER configuration) to identify the products whose attributes match with the detected search term against the entity. The products identified using the approach are promoted in the search ranking based on the weights assigned to the entity/attribute.

NER based reranking helps in improving search relevance in following ways :

* It gives merchandisers the ability to promote the ranking of products based on their understanding of shoppers’ preference towards various entities/ product properties.

**For example**, if a merchandiser has observed that the shoppers are more interested in TYPE, BRAND, COLOR, GENDER and are flexible with PATTERN, SLEEVETYPE then they can adjust the ranking weight-ages based on these properties.

* It understands the shoppers’ intent by understanding what they are looking for and promotes the products matching the shoppers’ specifications to the top. The model will promote the products matching these specifications. In the process, the NER based re-ranking reduces the impact of including unstructured fields (such as product description or marketing description) in the searchable fields list.

**For example**, if the search query is “red polka dot dress for women” then NER identifies that the shopper is looking for product TYPE: “dress” in COLOR: “red” with PATTERN: “polka dot” for GENDER: “Women”.

### Increase the product count in search result​

On occasions where the number of products matching the shopper’s search specifications is extremely low (including scenarios with zero results), NER strategies are needed. This is common for long-tail searches where the query length is higher. Our NER model offers a strategy to diversify the product selections in such cases by reformulating the search query.

**How does NER help in increasing product count?**

NER allows the search engine to relax the constraints of a search query in order to increase the search results for a search query. Selectively increasing the search results allows your search engine to showcase related products and increases the chances of conversions.  For example: In query like **blue check casual shirt for men**

Without NER query reformulation, the number of products in search result = 2 (Only 2 products match in the catalog)\
With NER query reformulation the new query becomes: “Blue casual shirt for men” AND Boost (checks)”.
The PATTERN (i.e. “checks”) is made an option term resulting in an increase in the results from 2 products to 50 products.
*A boost is applied on the products where PATTERN is “checks” in order to ensure that the 2 products matching exact shopper specifications appear at the top.*

## How to configure NER?

The NER model can be applied to your website as below:

1. Enable the toggle switch against “Apply NER model to your site”
2. Go to **Manage Map & Weightage** and perform the following actions:
   * **Map Entities identified by the model to the fields in your catalog**: The entities identified by our model are listed in the table. Map the fields in your product catalog which contain the information related to these entities. Our model requires these catalog mapping in order to influence the search results.
   * **Assign weightage**: Once an attribute is mapped against an entity, it would be available for assigning weights.
3. Click on **Save** to close the pop-up and save the settings.
4. Configure strategies as explain above.

> 📘 Note
>
> At-least one entity must be mapped to a catalog field and assigned a weightage to enable NER.

### Configure strategy for increased result count

Two steps are needed in order to configure the strategy for increasing the result count.

1. Enable the strategy by clicking on the checkbox against **Increase the product count in search result**.
2. Select the threshold above which the NER based query reformulation must be disabled. By default, the threshold is set as 10 which means if a query returns more than 10 products in the search result (with high precision) then the query reformulation will not be applied. Only if the number of products in the search result is less than the selected threshold, the NER based query reformulation will take place. In order to decide the threshold, you need to consider the following factors :
   1. The number of products displayed on the search results page. If the search results page displays 50 product on a single page then you may choose to increase the limit to 20 or 25.
   2. The number of queries that would be impacted by NER. A lower threshold would mean that query reformulation would happen for lesser number of queries. In order to decide the threshold, you can look create a table that contains the number of queries and their conversion rates across different ranges.

| **Products in Search Result** | **Search Hits** | **Conversion Rate** |
| ----------------------------- | --------------- | ------------------- |
| 0-5                           | 10,000          | 1.5%                |
| 0-10                          | 25,000          | 2%                  |
| 0-20                          | 100,000         | 2.1%                |
| 0-25                          | 125,000         | 2.5%                |
| 0-50                          | 500,000         | 5%                  |