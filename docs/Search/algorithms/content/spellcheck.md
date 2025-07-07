---
title: Spellcheck
excerpt: Identifies misspelled words/phrases in Search queries.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Spellcheck checks the misspelled queries to avoid zero results. By enabling spellcheck, your site displays results even if they type the wrong spelling of their intended query. It .

**Spellcheck works based on the following factors**:

1. **Levenshtein Distance**: It calculates the difference between two strings by checking up to 2 character changes to suggest similar terms.
2. **Search Results**: It uses the rest of the user's query to generate relevant search results.
3. **Catalog-Based Suggestions**: Recommendations are limited to the terms available in the catalog.

## To enable/disable spellcheck:

Navigate to **Algorithm** > **Content** > **Spellcheck**. Enable or Disable based on the queries.\
Once done, spellcheck is set.

<Image align="center" border={true} caption="Enable Spellcheck" src="https://files.readme.io/a03edbb1fc7a9c5c2e2d66440f6ee83a15200ac548c9359f05c000656b162295-image.png" />

## Spellcheck Override

Rule-based control that allows merchandisers to override automatic spell correction behavior for specific queries or terms

<Image align="center" border={true} caption="Set up Spellcheck Override" src="https://files.readme.io/0dc559e9a04678f4813d04795d23ee7494aeca2182e646cfc02cea26f30c23fd-image-20250609-100811.png" width="80% " />

Once enabled, click on **Add Keywords** to override specific keywords to stop suggesting similar queries. Below is use case scenarios accepted for Spellcheck override.

<Table>
  <thead>
    <tr>
      <th>
        **Use Case**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Single-Word (Token) Handling**
      </td>

      <td>
        The system applies to single-word (one-token) terms only. Multi-word phrases are not processed by this setup.
        For example: "kursi" is valid, while "long briefs" is not processed.
      </td>
    </tr>

    <tr>
      <td>
        **Camel Casing**
      </td>

      <td>
        Camel casing is automatically handled during **query parsing**. Camel-cased words are treated as single terms for search.
      </td>
    </tr>

    <tr>
      <td>
        **Special Character Handling**
      </td>

      <td>
        Special characters like apostrophes, hyphens, etc., are handled automatically during **query parsing**, ensuring they do not interfere with the search process.
      </td>
    </tr>
  </tbody>
</Table>

Below functionality is available on the dashboard of Spellcheck

| **Operation**     | **Description**                                                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Search**        | Allows users to search for specific data entries or products within the system. This feature enables efficient navigation through large datasets.             |
| **Bulk Upload**   | Allows users to upload multiple files or data entries at once. This is used to efficiently update or add a large amount of data to the system.                |
| **Bulk Download** | Allows users to download multiple files or data entries at once. This operation is typically used for exporting large sets of data for analysis or reporting. |