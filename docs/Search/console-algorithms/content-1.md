---
title: Content
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The **Content** section under **Console Algorithms** is designed to improve the relevance and intelligence of search results by leveraging your catalog's semantic understanding. It allows merchandisers and product managers to configure how the system interprets and expands search queries using natural language enhancements like synonyms, stemming, concepts, and more.

This page plays a critical role in ensuring that customers find what they are looking for—even when they don’t use exact product keywords.

***

## Synonyms

The **Synonyms** tab helps map search terms to equivalent or related words, ensuring that alternate terms, variations, and common expressions still return the right products.

### Unbxd AI Recommended Synonyms

* Displays automatically suggested synonyms based on your product catalog.
* Up to 500 synonyms can be identified by Unbxd AI.
* Click **Know More** to explore the logic and benefits of these recommendations.

***

# Synonym Configuration Table

| Column               | Description                                                                                                                                                                     |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Search Keyword**   | The keyword entered by a user in a search query. This is the anchor term to which synonyms are mapped.                                                                          |
| **One Way Synonyms** | Related terms that expand search coverage when a user searches for the main keyword. These synonyms apply in one direction only—from search keyword to synonym, not vice versa. |
| **Two Way Synonyms** | Bi-directional terms that are treated interchangeably. Searching any of the mapped terms will yield results for all others.                                                     |

You can view, edit, or delete existing synonyms using the controls beside each row.

***

### Functionalities

| Control           | Functionality                                                                |
| ----------------- | ---------------------------------------------------------------------------- |
| **Search**        | Allows filtering the synonym list by keyword. Useful for large catalogs.     |
| **More Options**  | Access bulk upload/download options for synonym rules.                       |
| **Save Changes**  | Click to apply any modifications to the synonym mappings.                    |
| **Add a Synonym** | Opens a dialog to manually add a new synonym rule—either one-way or two-way. |

***

### Why It Matters

* Boosts search relevance and recall without changing core product data.
* Helps handle customer typos, regional language variations, and branding differences.
* Enhances conversion by reducing "no results" pages and improving discovery.

***

## Phrases

The **Phrases** section allows you to configure multi-word search terms to help the system better interpret product-specific queries. These phrases are especially useful for understanding product types that consist of multiple words (e.g., "mini dress", "indoor pots").

This setup enhances search accuracy and ensures that users are presented with the most relevant results, even when their queries involve complex or compound expressions.

* Automatically detects and suggests **multi-word product phrases** from your catalog.
* These recommendations help streamline the process of identifying combinations of terms that should be treated as a single search unit.
* You can modify, accept, or delete these AI-generated suggestions.
* A “Know More” link is provided to understand how phrase recognition works.

***

### Phrases Configuration

| Column                  | Description                                                                                                                                                                    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Phrases**             | Displays the multi-word term you want the system to recognize (e.g., “mini dress”).                                                                                            |
| **Include Right Term**  | Allows you to select meaningful tokens from the phrase that should influence search results. These may be variations, partial matches, or condensed forms (e.g., "minidress"). |
| **Include Full Phrase** | Select this to treat the entire phrase as a single searchable unit. Ideal when breaking the phrase into individual words might reduce relevance.                               |

Each row allows for custom selection of the tokenization behavior depending on your product and query patterns.

***

### Functionalities

| Control          | Description                                                                                 |
| ---------------- | ------------------------------------------------------------------------------------------- |
| **Search**       | Search existing phrases quickly. Useful when managing a large phrase list.                  |
| **More Options** | Offers bulk upload/download capabilities for managing phrases.                              |
| **Save Changes** | Apply any updates made to phrase configurations.                                            |
| **Add a Phrase** | Manually add a new phrase to the system with token settings for Right Term and Full Phrase. |

***

### Why Use Phrase Mapping

* Prevents misinterpretation of product names or types during search.
* Helps clarify product categories, such as distinguishing “mini dress” from unrelated uses of “mini” or “dress”.
* Enhances control over how catalog data contributes to the relevance model.

***

## Stemming

Stemming truncates the query to its root form to sound semantically correct and deliver relevant results while having the same contextual meaning. Ex. It cuts down the query ‘painting brush’ to ‘paint  brush’ form. You can add the stemmed versions of individual words to override the Unbxd stemming algorithm.

<br />

For instance, the search engine can stem “dressing” as “dress”. This would lead to incorrect results, this behaviour can be overridden by adding “dressing” and its acceptable form “dressing” to stemming dictionary.

To add/edit stemmed words:

Navigate to Content > Stemming.\
Click the ‘hamburger’ icon > Bulk Upload Stemmed Words. You can upload a list of stemmed words by either browsing on your computer or by using drag and drop. The supported upload format is .csv.
Once added, you would see the list of keywords and their stemmed forms. If you feel the stemmed word defined by Unbxd is not as per your requirement, you can edit it under ‘Stemmed Words’. Specify the entire word under both ‘Keywords’ and ‘Stemmed Words’ if the reduced form doesn’t mean the same. Like, Painting can be reduced to Paint but Leggings cannot reduce to Legs.
What should stemming not include:

Empty record: entry where there is no value entered (whitespace) &#x20;
Stemword empty record: entries without a stem word for the root word.
Symbols: entries where only symbols are typed as the value. The following characters are not accepted by our system : ‘ , ‘ ( comma) , ‘+’ (plus), ‘\{‘, ‘}’ (curly braces), ‘\*’ (Asterix),’&’ (Ampersand) , ‘\’ (backslash)&#x20;
Alphanumeric: entries with only alphanumeric values. It should have text characters.
Stopwords: entries that contain just words that add no value like of, for, the, or any such stopwords.
Single term: entries that do not have a stemmed term for the root word.

***

## Concepts

The concepts are handy for improving the relevance for long-tail searches (high intent) where shoppers are aware of what they want to buy and type all the details of the product that they are looking for.

For example, a shopper searching for “Red polka dot half sleeve dresses” is clearly telling the search system that they are looking for the half sleeve (sleeve-type) “dresses” (product type) with polka dot ( pattern) in red color (attribute).  The challenge with some of these high intent searches is that your eCommerce store may not have products matching the exact requirement of the shopper. For example, the store may carry full sleeve polka dot dresses in red color or half sleeve polka dot dresses in blue and black color, etc.

<br />

&#x20;

<br />

Defining concepts enables the search system to identify the important features from the search query (for example “dress” in this query). The search restricts the result set to the products matching these important features while treating other query terms as optional. This allows your store to show products that are similar to the shopper’s search but do not fulfill all the requirements.

What can be added as Concepts?

We recommend adding all the product types from the catalog as concepts in order to achieve higher precision for searches where customers are searching using product types.

NOTE: Although concepts help in improving the precision of search they must be used judiciously. Adding too-many concepts can reduce the recall and may lead to zero results.

Depending upon your use-case you can include other catalog terms as Concepts. For example, if your shoppers are highly brand conscious and search for products using brand names then you can add all the brands in the catalog as Concepts to ensure that only products from the brands that are being searched are included in the result set. Let’s take another example from an e-commerce store that sells computer games (for example, Xbox games, ps4 games, etc.). For these stores, when a customer is searching for “Xbox lego batman” they are only interested in games that are compatible with “Xbox”. Showing a PS4 game is of no use to the shopper. In such scenarios, you can define Xbox, PS4 platforms as concepts because shoppers are looking for high precision when searching using these terms.

NOTE: Our Named Entity Recognition (NER) algorithm offers an intelligent way of handling long tail searches.

To add concepts:

Navigate to Content > Concepts.\
Click the ‘hamburger’ icon > Bulk Upload Concepts. You can upload a list of concept terms by either browsing on your computer or by using drag and drop. The supported upload format is .csv.
Unbxd’s AI will identify the concepts from your catalog and you could edit them as needed.
What should concepts not include:

Empty record: entry where there is no value entered (whitespace) &#x20;
Symbols: entries where only symbols are typed as the value. The following characters are not accepted by our system : ‘ , ‘ ( comma) , ‘+’ (plus), ‘\{‘, ‘}’ (curly braces), ‘\*’ (Asterix),’&’ (Ampersand) , ‘\’ (backslash)&#x20;
Alphanumeric: entries with only alphanumeric values. It should have text characters.
Single term: entries that do not have a long-tail query (more than two words).
Stopwords