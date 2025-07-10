---
title: Intent
excerpt: >-
  Improve search results by displaying products that match your shopper’s
  intent.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The Intent Algorithm for the Unbxd Console is designed to understand and interpret a user's search query in a more human-like way. It helps improve search results by identifying the user's intent behind the query, rather than simply matching keywords.

## Key Features:

1. **Understanding User Intent**: The algorithm looks beyond the specific words in the search query and analyzes the overall context to determine what the user is likely looking for. It recognizes synonyms, related concepts, and potential variations in how products or content are searched.
2. **Personalized Search Experience**: It tailors the search results based on what it understands the user intends to find. This personalization could be based on previous searches, user behavior, or the most common search patterns for similar queries.
3. **Ranking and Relevance**: The intent algorithm not only identifies the user's query intent but also ranks results in a way that prioritizes relevance. This means showing the most likely products or content that align with the detected intent, even if the exact terms don't match the query.

### Usecase:

| **Aspect**                                       | **Description**                                                                                              |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Query**                                        | "Running shoes for men"                                                                                      |
| **Recognized Intent**                            | "Products for men's athletic footwear"                                                                       |
| **Context**                                      | "Running shoes"                                                                                              |
| **Category**                                     | "Men's shoes"                                                                                                |
| **Benefit 1: Improved Search Accuracy**          | Reduces irrelevant results by understanding intent, offering suggestions that better match the user's needs. |
| **Benefit 2: Natural Language Processing (NLP)** | Interprets variations in search terms to create a more intuitive and accurate search experience.             |

Currently Netcore Unbxd offers below Intent search

1. Measurement Search
2. Vector Search

Lets dive into details of both the search algorithms.