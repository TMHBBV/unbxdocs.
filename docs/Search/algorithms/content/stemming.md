---
title: Stemming
excerpt: >-
  Manage and override automatic word-stemming rules to improve search result
  accuracy and relevance. 
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Stemming is a search engine process that reduces different forms of a word down to its common root or base form (the 'stem'). This helps the search understand that word variations often share the same core meaning. The main goal is to connect shoppers with relevant products even if they use a slightly different word form than what's listed in your product data.

For Example, through stemming, the search engine can understand that searches for "running shoes," "run fast," or "ran a mile" are all related to the root word "run." This allows it to return relevant run-related products for all these queries. By default, the system (Unbxd) applies its own stemming logic automatically (like potentially stemming 'painting' to 'paint').

## Why Overriding Default Stemming is Important?

While automatic stemming is often helpful, the default algorithm can sometimes reduce a word incorrectly, changing its intended meaning within your specific catalog and leading to irrelevant search results. Manually overriding the default stemming for specific words is crucial for maintaining search accuracy in such cases.

**Problem Example 1**: The system might automatically stem "dressing" (like salad dressing or wound dressing) to "dress" (the clothing item). Showing 'dresses' when a shopper searches for "dressing" is incorrect.

**Problem Example 2**: The system might stem "leggings" (the clothing item) to "leg". Showing general 'leg'-related items for a 'leggings' search is irrelevant.

**Solution (Override)**: You can fix this by adding a stemming rule that maps the word to itself. This tells the system not to reduce the word, preserving its original meaning.

For 'dressing': Set **Keyword** = dressing, **Stemmed Word** = dressing

For 'leggings': Set **Keyword** = \*\*leggings, **Stemmed Word** = leggings.

By overriding incorrect default stemming, you ensure shoppers find products directly related to their search terms, improving their experience and conversion rates.

## Add Stemming (Single Override)

You can add individual stemming rules directly through the user interface:

1. Navigate to **Algorithm** **Content** > **Stemming** in your Netcore Unbxd panel.
2. Click the **Add Stemmed Word** button.
3. In the Keyword field, enter the original word whose stemming you want to control (e.g., dressing). In the Stemmed Word field, enter the desired root form.

> 📘 Important
>
> To prevent the word from being stemmed, enter the original word itself here (e.g., dressing).

4. Save the new stemming rule. It will now override the default behavior for that specific keyword.

You can typically edit existing rules directly from the list view on this page.

## Bulk Upload Stemming Rules

If you have multiple stemming overrides to define, you can add them efficiently using the bulk upload feature:

1. Navigate to **Content** > **Stemming**.
2. Select **Bulk Upload Stemmed Words**.
3. Prepare your stemming rules in a .csv (Comma Separated Values) file format.

| Column 1                                             | Column 2                                                                                                  |
| :--------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| Keyword (the original word) Example: **Shoe Polish** | Stemmed Word (The desired stem, or the original word itself to prevent stemming) Example: **Shoe Polish** |

Each row represents one stemming rule.

4. Upload the .csv file using the browse or drag-and-drop functionality provided.

The system will process the file and add the specified stemming overrides.

### What Stemming Overrides Should Not Include?

To ensure your stemming rules function correctly and maintain data quality, avoid creating entries with the following issues:

1. **Empty Entries**: Both 'Keyword' and 'Stemmed Word' fields must contain values (cannot be blank or just whitespace).
2. **Missing Stemmed Word**: Every 'Keyword' must have a corresponding 'Stemmed Word' defined in your override entry.
3. **Symbol-Only Entries**: Entries consisting only of symbols (e.g., `*&^%`) are not valid in either the **Keyword** or **Stemmed Word** field.
4. **Forbidden Characters**: Do not use these specific characters within your keywords or stemmed words: `,` (comma), `+` (plus), `{`, `}` (curly braces), `*` (asterisk), `&` (ampersand), `\` (backslash).
5. **Purely Alphanumeric/Codes**: Overrides for entries that are only numbers or non-descriptive codes without meaningful text (e.g., `12345`, `X4T5`) are generally not applicable or useful for stemming.
6. **Stopwords**: Defining custom stemming for common stopwords (like `the`, `a`, `is`, `of`, `for`) is typically unnecessary and not recommended as it usually doesn't significantly impact search relevance.