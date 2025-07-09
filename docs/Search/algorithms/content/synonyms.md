---
title: Synonyms
excerpt: >-
  Improve product discoverability by mapping similar, related, or alternate
  search terms using synonyms feature.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The Synonyms section in the Netcore Unbxd console helps ensure that shoppers find what they're looking for—even if they use different words, regional terms, misspellings, or abbreviations in their search. By defining synonyms, you connect related or equivalent terms so that shoppers receive relevant results for a variety of query styles.

This is especially helpful in reducing zero-result searches, improving product discoverability, and ensuring a consistent search experience across different shopper intents.

## When Are Synonyms Used?

Synonyms come into play in several everyday search scenarios:

1. **Terms with the Same Meaning**\
   Words like "ladies" and "women's" or "graph paper" and "grid paper" refer to the same thing and should return the same products.
2. **Geographically Different Terms**\
   Shoppers in different regions may use different words for the same product. For example, "slippers" in India are often referred to as "flip-flops" in the US. Mapping these terms ensures search results remain relevant regardless of location.
3. **Related Terms**\
   Even if two terms are not exact synonyms, they may be closely related in context. A search for "paper plates" could also show "plastic plates" as relevant alternatives.
4. **Hyponyms**\
   A more specific term (like "desktop PC") can be mapped to a broader category ("computers") to expand results meaningfully.
5. **Spelling Variants**\
   Differences in dialect or preference can lead to spelling variants like "color" vs "colour" or "adapter" vs "adaptor". These should be treated as equivalent.
6. **Common Misspellings**\
   Shoppers may frequently misspell brand names or product terms—e.g., "purel" instead of "Purell". Adding such synonyms ensures they still see the right products.
7. **Spacing Variations**\
   Words like "WiFi", "Wi-Fi", and "Wi Fi" are visually different but semantically the same. Handling such variations is key to delivering consistent results.
8. **Abbreviations**\
   Shoppers may search using abbreviations like "MK" for "Michael Kors" or "NYC" for "New York City". Mapping these helps return complete and relevant results.

By understanding these scenarios, you can set up synonyms that reflect how your customers actually search—making your on-site search smarter and more forgiving.

## What should synonyms not include?

1. **Empty record**: entry where there is no value entered (whitespace)
2. **Symbols**: entries where only symbols are typed as the value. The following characters are not accepted by our system : , ( comma) , + (plus), \{, } (curly braces), \* (Asterix),& (Ampersand) , \ (backslash)
3. **Alphanumeric**: entries with only alphanumeric values. It should have text characters.
4. **Stopwords**: entries that contain just words that add no value like of, for, the, or any such stopwords.
5. **Redundant Synonyms**: entries that already exist. Don’t add two similar inputs.
6. **Multi-term Synonyms**: Synonyms having more than 2 keywords should be avoided. 

# Types of Synonyms

1. **One-Way-Synonyms**\
   These are uni-directional. A search for the primary keyword returns results for its synonyms, but not vice versa. Example : If "ivory" is a one-way synonym for "white", then searching for “white running shoes” will return both white and ivory shoes. While searching for “ivory running shoes” will only return ivory shoes, not white.
2. **Two-Way-Synonyms**\
   These synonyms are bi-directional. When a shopper searches for any of the terms in the group, the search engine returns results for all related terms. Example: If "pants" and "trousers" are set as two-way synonyms, a search for either will return results for both.

Now that we know various use cases and types of synonyms let us understand how to configure these synonyms using the Unbxd console. 

# Add Synonyms

<Image align="center" border={true} caption="Add a Synonym" src="https://files.readme.io/fc002d24a7aff57d95027dec1bae74003cd3352e41ea534ed14d841474400326-AddSynonym.gif" width="80% " />

1. Navigate to **Content** > **Synonyms**.
2. Click **Add a Synonym** to configure your keywords along with the synonyms.
3. Provide keywords for Synonyms in the Type Search Keyword section.
4. Provide queries in **One-Way-Synonyms**and **Two-way-Synonyms**.
5. Click **Proceed** to save the configure Synonyms.

## Bulk Upload Synonyms

With the Bulk Upload Synonyms feature, you can upload a list of synonyms. You can browse on your computer or use drag-and-drop. The supported upload format is .csv. It is advisable for first-time users to upload a list of synonyms already known to their previous search system so that they can handle all those instances in Unbxd search. 

Once uploaded, you can see the number of synonyms added. Using the Bulk Download Synonyms feature, you can also bulk download all the synonyms you have configured. A .csv file is downloaded.

# Delete a synonym:

1. Navigate to **Content** > **Synonyms**.
2. Search for the keyword and click the hamburger icon next to it. 
3. Click **Delete**, where you will receive a confirmation message for deletion. 
4. Click **Yes** if confirmed or No otherwise.

## Index Time Synonyms

The **Index Time Synonym** feature is designed to improve search recall by adding synonym keywords to the search index during the **full feed** or **re-indexing** process. These synonyms help to map multiple terms with the same meaning, ensuring that users can find relevant products, even if they use different words in their search queries.

### Prerequisites

Before using the Index Time Synonyms feature, ensure that the following prerequisites are met:

1. Configure your synonym relationships in the dashboard.
2. This feature is applied during the full feed or re-indexing process, meaning the system will only index synonyms when a feed is ingested or a re-indexing job is triggered.

### How it works

This feature is accessible only to Unbxd Admin users. Log in to Netcore Unbxd Dashboard and navigate to **Algorithm** > **Configs** > **Index Time Synonyms**.

Below is step by step workflow on Index Time Synonym:

<Table>
  <thead>
    <tr>
      <th>
        **Step**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Synonym Mapping Input**
      </td>

      <td>
        Merchandisers define synonym relationships through the dashboard.
        Example:

        * **Unidirectional Synonyms**: "pants → trousers, slacks, long briefs"
        * **Bidirectional Synonyms**: "pants ↔ trousers ↔ slacks ↔ long briefs"
        * These mappings are passed to the backend system for indexing.
      </td>
    </tr>

    <tr>
      <td>
        **Building the Inverted Synonym Trie**
      </td>

      <td>
        During feed ingestion, the system constructs an inverted synonym using the configured synonyms:

        * **Unidirectional Mapping**:"trousers → pants",  "slacks → pants",  "long briefs → pants"
        * **Bidirectional Mapping**: "trousers → pants, slacks, long briefs" "pants → trousers, slacks, long briefs", "slacks → pants, trousers, long briefs", "long briefs → pants, trousers, slacks"
      </td>
    </tr>

    <tr>
      <td>
        **SynonymTransformer Processing**
      </td>

      <td>
        In the Synonym Transformer processes the product catalog’s searchable fields (e.g., product titles, descriptions) and extracts text using a maximum window size of 3 words.\
        **Note**: Only single-token synonyms are indexed. Multi-word synonyms like "long briefs" are ignored.
      </td>
    </tr>

    <tr>
      <td>
        **Indexing into`syn_unx_tpm` and `syn_unx_auto`**
      </td>

      <td>
        Valid single-token synonyms are indexed into the following fields:

        * **syn\_unx\_tpm** for search queries
        * **syn\_unx\_auto** for autosuggest queries
        * Example: Product title "slacks" → synonym mapping "pants → slacks" → "pants" is indexed into `syn_unx_tpm`.\
          Multi-word synonyms like "long briefs" are not indexed.
      </td>
    </tr>
  </tbody>
</Table>

## FAQ & Troubleshoot

<Accordion title="When should I use Index Time Synonym?">
  Index Time Synonym is best used when you have a large number of synonyms to be indexed (e.g., 25+). It’s particularly useful during the onboarding process as feeds are indexed regularly.
</Accordion>

<Accordion title="Can I index multi-word synonyms?">
  No, the system only processes and indexes single-token synonyms (e.g., "pants" → "slacks"). Multi-word synonyms like "long briefs" are not indexed to avoid noise in the system.
</Accordion>

<Accordion title="What happens if I add synonyms after the feed is ingested?">
  If you add new synonyms after a feed has already been ingested, they will be indexed only during the next full feed or re-indexing cycle.
</Accordion>

<Accordion title="How often should I refresh the synonyms?">
  Synonyms are typically refreshed during full feeds or delta feeds, which are indexed regularly. Ensure the feed is ingested at appropriate intervals to keep the synonym mappings up-to-date.
</Accordion>