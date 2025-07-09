---
title: Concepts
excerpt: A curated list of keywords to match the category of the product searched.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The concepts are handy for improving the relevance for long-tail searches (high intent) where shoppers are aware of what they want to buy and type all the details of the product that they are looking for.

For example, a shopper searching for “Red polka dot half sleeve dresses” is clearly telling the search system that they are looking for the half sleeve (sleeve-type) “dresses” (product type) with polka dot ( pattern) in red color (attribute).  The challenge with some of these high-intent searches is that your eCommerce store may not have products matching the exact requirement of the shopper. For example, the store may carry full-sleeve polka dot dresses in red or half-sleeve polka dot dresses in blue and black, etc.

Defining concepts enables the search system to identify the important features from the search query (for example, “dress” in this query). The search restricts the result set to the products matching these important features while treating other query terms as optional. This allows your store to show products that are similar to the shopper’s search but do not fulfill all the requirements.

## What can be added as Concepts?

It is recommend adding all the product types from the catalog as concepts in order to achieve higher precision for searches where customers are searching using product types.

> 📘 NOTE
>
> Although concepts help in improving the precision of search they must be used judiciously. Adding too-many concepts can reduce the recall and may lead to zero results.

Depending upon your use-case you can include other catalog terms as Concepts.

If your shoppers are highly brand conscious and search for products using brand names then you can add all the brands in the catalog as **Concepts** to ensure that only products from the brands that are being searched are included in the result set.

| **Scenario**         | **Keyword**      | **Description**                                                                                          |
| -------------------- | ---------------- | -------------------------------------------------------------------------------------------------------- |
| **E-commerce Store** | Xbox Lego Batman | Shoppers are looking for Xbox-compatible games. PS4 games are irrelevant.                                |
| **Platform Concept** | Xbox, PS4        | Define Xbox and PS4 as concepts to ensure high precision in search results, showing only relevant games. |

> 📘 Note
>
> Our Named Entity Recognition (NER) algorithm offers an intelligent way of handling long tail searches.

# Add Concept

<Image align="center" border={true} caption="Add a Concept" src="https://files.readme.io/b57ca297fbad095144e16ea15c7fef2ba58dbee54c2196c957f6d8f89b9a7163-AddConcept.gif" width="80% " />

1. Navigate to **Content** > **Concepts**.
2. Click **Add a Concept** . Enter the keywords you want to add.
3. **Bulk Upload Concepts**: You can choose to upload a list of concept terms by either browsing on your computer or by using drag and drop. The supported upload format is .csv.

Unbxd’s AI will identify the concepts from your catalog and you could edit them as needed.

## What should concepts not include:

1. **Empty record**: entry where there is no value entered (whitespace)
2. **Symbols** : entries where only symbols are typed as the value. The following characters are not accepted by our system : `, ` ( comma) , `+`(plus), `{`, `}` (curly braces), `*` (Asterix),`&` (Ampersand) , `\` (backslash)
3. **Alphanumeric**: entries with only alphanumeric values. It should have text characters.
4. **Single term**: entries that do not have a long-tail query (more than two words).