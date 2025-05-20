---
title: Phrases
excerpt: >-
  Define multi-word phrases to control and improve search result relevance based
  on shopper intent
deprecated: false
hidden: false
metadata:
  robots: index
---
# What are Phrases?

Phrases are standard multi-word search terms that shoppers use when looking for specific types of products (e.g., "paintbrush," "shoe polish," "running shoes"). The Phrases feature allows you to define these multi-word terms and guide the search engine to understand the shopper's true intent behind them, leading to more relevant search results.

## Why are Phrases Important?

Without specific guidance, a search engine might treat each word in a multi-word query equally. For example:

A search for a **paint brush** could return a mix of any product related to 'paint' (like cans of paint) and any product related to 'brush' (like hair brushes), alongside actual paint brushes. This happens if the engine isn't well-trained or lacks sufficient data to understand the combined meaning.

This can lead to a confusing and inaccurate search experience. The Phrases feature solves this by letting you specify which part of the phrase is most crucial for determining relevance.

### How Phrases Work: Controlling Relevance

When you add a phrase, you instruct the search system on how to prioritize results based on the shopper's multi-word query. You have three options to define this relevance:

| **Option**                  | **Description**                                                                                                             |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **Include the left-term**   | Displays results matching the full phrase **AND** results strongly related to the leftmost significant word of the phrase.  |
| **Include the right-term**  | Displays results matching the full phrase **AND** results strongly related to the rightmost significant word of the phrase. |
| **Include the full phrase** | Displays only results that closely match the exact full phrase entered.                                                     |

For phrases with three or more words (e.g., "Hand sanitizer dispenser"), the "left-term" and "right-term" options refer to the most significant defining word on the respective side ('Hand' or 'Dispenser' in the example), guiding the focus along with the full phrase match.

## Use Case

| **Example Phrase**           | **Shopper Intent**                                                        | **Key Term**                     | **Configuration**               | **Result**                                                                                                                      |
| ---------------------------- | ------------------------------------------------------------------------- | -------------------------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Shoe Polish**              | Looking for polish for shoes, not shoes themselves.                       | 'Polish' (the rightmost term)    | Select "Include the right-term" | Prioritizes results for 'polish' products and exact 'shoe polish' matches, minimizing irrelevant 'shoe' results.                |
| **Paint Brush**              | Looking for brushes specifically for painting.                            | 'Brush' (the rightmost term)     | Select "Include the right-term" | Focuses on 'brush' products suitable for painting and exact 'paintbrush' matches, reducing noise from general 'paint' products. |
| **Hand Sanitizer Dispenser** | Looking for dispensers for hand sanitizer, not just the sanitizer liquid. | 'Dispenser' (the rightmost term) | Select "Include the right-term" | Prioritizes 'dispenser' results and exact 'hand sanitizer dispenser' matches.                                                   |

## Add a Phrase

To add Phrase (or a single synonym):

1. Navigate to **Algorithms** > **Content** > **Phrase**. Click **Add a Phrase** to configure your keywords along with the synonyms.

In the Terms or Phrase field, enter the multi-word phrase (e.g., "coffee table").

2. Click **Proceed** to **save** configure phrase.
3. Select the desired relevance option: Include the left-term, Include the right-term, or Include the full phrase based on the shopper's likely intent

### Bulk Upload Phrase

You can upload a list of phrases using the Bulk Upload Phrase feature. You can browse on your computer or use drag-and-drop. The supported upload format is .csv. You may need to check specific formatting requirements for including the left/right/full term designation in the CSV. Once uploaded, you can see the number of phrases added. Using the Bulk Download Phrase feature, you can also bulk download all the phrases you have configured. A .csv file is downloaded.

### What Phrases Should NOT Include

To ensure phrases function correctly and maintain data quality, avoid entries that are:

1. Empty or Blank: Phrases cannot be empty or consist only of whitespace.
2. Symbol-Only: Phrases composed entirely of symbols are not permitted.
3. Containing Forbidden Characters: Avoid using the following characters within any part of the phrase: `,` (comma), `+` (plus), `{` (curly braces), `}` (curly braces), `*` (asterisk), `&` (ampersand), `\` (backslash).
4. Purely Alphanumeric/Codes: Phrases must contain meaningful words. Entries consisting only of numbers or alphanumeric codes without descriptive text (e.g., `12345`, `ABC789`) are not valid phrases.
5. Stopword-Only: Phrases made entirely of common, non-specific words (e.g., "the of", "for a") lack meaning and are invalid.
6. Single Words: This feature is for multi-word terms. Do not add single words (e.g., "shoes"). A phrase must contain at least two words to be effective here.