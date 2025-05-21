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