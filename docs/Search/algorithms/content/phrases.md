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

Phrases are common multi-word search terms that shoppers use when looking for specific types of products (e.g., "paintbrush," "shoe polish," "running shoes"). The Phrases feature allows you to define these multi-word terms and guide the search engine to understand the shopper's true intent behind them, leading to more relevant search results.

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

### Examples of Phrase Configuration

\<Tabs>
&#x20; \<Tab title="Example 1">
Phrase: Shoe Polish
Shopper Intent: Looking for polish for shoes, not shoes themselves.
Key Term: 'Polish' (the rightmost term).
Configuration: Select "Include the right-term".

Result: When a shopper searches for "Shoe Polish", the engine prioritizes results for 'polish' products and exact 'shoe polish' matches, minimizing irrelevant 'shoe' results.
&#x20;   Add a Phrase

To add Phrase (or a single synonym):

1.Navigate to Content > Phrase.

2.Click Add a Phrase to configure your keywords along with the synonyms.

In the Terms or Phrase field, enter the multi-word phrase (e.g., "coffee table").
Click Proceed to save the configure phrase.

Select the desired relevance option: Include the left-term, Include the right-term, or Include the full phrase based on the shopper's likely intent
&#x20;  &#x20;
What Phrases Should NOT Include

To ensure phrases function correctly and maintain data quality, avoid entries that are:

1\. Empty or Blank: Phrases cannot be empty or consist only of whitespace.

2\. Symbol-Only: Phrases composed entirely of symbols are not permitted.
&#x20;  &#x20;
3\. Containing Forbidden Characters: Avoid using the following characters within any part of the phrase: , (comma), + (plus), \{ (curly braces), } (curly braces), \* (asterisk), & (ampersand), \ (backslash).

4\. Purely Alphanumeric/Codes: Phrases must contain meaningful words. Entries consisting only of numbers or alphanumeric codes without descriptive text (e.g., "12345", "ABC789") are not valid phrases.
&#x20;  &#x20;
5\. Stopword-Only: Phrases made entirely of common, non-specific words (e.g., "the of", "for a") lack meaning and are invalid.
&#x20;  &#x20;
6\. Single Words: This feature is for multi-word terms. Do not add single words (e.g., "shoes"). A phrase must contain at least two words to be effective here.
&#x20; \</Tab>

&#x20; \<Tab title="Second Tab">
&#x20;   Here's content that's only inside the second Tab.
&#x20; \</Tab>

&#x20; \<Tab title="Third Tab">
&#x20;   Here's content that's only inside the third Tab.
&#x20; \</Tab>
\</Tabs>