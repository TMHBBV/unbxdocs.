---
title: Vector Search
excerpt: It understands what you really mean, your intent
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Vector Search is a smart AI-enabled feature in Unbxd that helps shoppers find the right products  easily. Instead of just looking for exact words in a search (like traditional search engines do), Vector Search understands what the shopper means.

So even if the search doesn’t use the exact same words as the product listings, it can still show the most relevant results. Vector Search doesn’t just look at the words you typed. It tries to understand what you really mean — your intent. So instead of just matching words, it matches meaning.

**For example**, if you have a search query like “**shoes for hiking in the mountains**”, Vector Search can also show:

* “trail running shoes”
* “outdoor hiking boots”
* “mountain trekking footwear”
* "all-terrain sneakers”

These are all semantically related, even if they don’t contain the exact same words. This is especially helpful for longer, more detailed searches, like when someone types a full sentence or a specific need.

## Prerequisites

1. You should have a valid UNBXD account with appropriate permissions to access the Self-Serve Console.
2. Vector Search must be enabled on your UNBXD panel. Refer here to enable Vector Search in your account.

### Impact of Vector Search

Vector Search helps users find what they mean, not just what they say. It improves the accuracy, depth, and usefulness of search results, especially for longer or more natural language queries.

1. **Understands intent:**\
   Helps the search engine interpret the meaning behind what users type, not just the words.
2. **Fewer dead ends**:\
   Reduces the chances of “no results found” pages by showing related products.
3. **Better relevance**:\
   Surfaces products that truly match what the user is looking for, even if the keywords don’t match exactly.
4. **Boosts conversions**:\
   When users find what they need faster, they’re more likely to buy — improving sales and user satisfaction.

# Enable Vector Search

<Image align="center" border={true} caption="Set up Vector Search" src="https://files.readme.io/7dd1c4df49e1189d0ceaad21606778586c49da003adc14633343f6385c44435a-VectorSearch.gif" width="80% " />

1. Log in to the Netcore Unbxd console page.
2. Navigate to **Algorithm** > **Intent** > **Vector Search**.
3. Click Contact support link to auto create support ticket for enabling this feature on your panel. Once approved, the toggle button is enabled for your panel.

## Set your Vector Search strategy.

There are two options available to do so: Hybrid search & Fallback search.

* **Hybrid search** : You have to set up the minimum number of words to activate Hybrid search.
* **Fallback search**: If the number of products shown in the search results is less than or equal to the number you’ve set, Vector Search will automatically turn on to show more relevant results.

<Image align="center" border={true} caption="Strategy Selection" src="https://files.readme.io/6bd79970e10c034884dc2b06e727475e0812c5baae8189593ba1c4308b6a8c4f-image.png" width="80% " />

<br />

# Strategies Selection of Vector Search

Vector Search helps improve search results by understanding the meaning behind what users type. Unbxd uses two smart strategies to make the most of this: Hybrid search and Fallback search.

1. **Hybrid Search**

Hybrid Search combines traditional keyword-based search with vector search. This way, users get results that match the exact words and products that are related in meaning.\
It ensures users don’t miss out on relevant products just because the words are different.

For example: If a user searches for “smartphone”, traditional search will show 15 results with the word “smartphone” in it. With Hybrid Search, vector search adds results like:

* “mobile phone"
* “cell phone”
* “smart device”
* "gadget"

**Final result count: 40 relevant products.**\
*This ensures that the search results are complete and useful for shoppers.*

2. **Fallback Search**

Fallback Search kicks in when keyword search returns few or no results. Instead of showing an empty page, Unbxd automatically switches to vector search to show related items. It saves the user from dead ends and keeps the experience smooth.

For example: If a user searches for “running shoes”, keyword search returns 10 products. If you've set the fallback limit to 10 then vector search gets activated automatically. With Fallback Search, Vector search adds more results like:

* “jogging shoes”
* “sports shoes”
* “trail running shoes”
* “athletic shoes”

**Final result count: 30 products**\
*This ensures Vector Search makes up for what keyword search missed.*

# Troubleshooting & FAQs

<Accordion title="Do I need to enable Vector Search manually?">
  Yes, To enable:
  Go to Unbxd Console > Algorithm > Intent > Vector Search.
  Click Contact Support to auto-create a ticket. Once approved, the toggle button becomes active
</Accordion>

<Accordion title="How do I activate Hybrid Search?">
  You must set the minimum number of words required in the search query to trigger Hybrid Search (ideal for long-tail or descriptive queries).
</Accordion>

<Accordion title="What happens if the query is too short for Hybrid Search?">
  If the query doesn’t meet the minimum word count you've set, Vector Search won’t activate under Hybrid mode, and traditional search will be used instead.
</Accordion>