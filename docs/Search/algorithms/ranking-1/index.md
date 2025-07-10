---
title: Ranking
excerpt: Improve search ranking by better ordering of search results.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Learn how **User Behaviour (UB)** and **Popularity** signals are used to influence product ranking on the search and browse experiences. Both mechanisms rely on analytics data and are **enabled by default** for all sites integrated with analytics.

# Prerequisites

Before proceeding, ensure the following is done.

1. **Analytics Integration**
2. Site Access from Netcore Unbxd console.

There are two sections available for Ranking. Log in to Netcore Unbxd console and Navigate to **Algorithm** > **Ranking**

1. User Behavior
2. Popularity

# User Behaviour (UB)

**User Behaviour (UB)** is a feature in Netcore unbxd that captures how users interact with products for a given **search query**. These interactions include:

| **Event Type**        | **Description**                                                        |
| :-------------------- | :--------------------------------------------------------------------- |
| **Click Events**      | Triggered when a user clicks on a product in search or browse results. |
| **Add-to-Cart (Cut)** | Captures when a user adds a product to their shopping cart.            |
| **Order Events**      | Logged when a user completes a purchase for a product.                 |

This is calculated **at the query level**. For example, if multiple users search for **running shoes** and frequently click or order Product A, it will receive a higher UB score for that query.

## Configuration for User Behaviour and Popularity

* **Default**: UB is **enabled by default** for all clients with analytics integration.
* **Custom Configuration**: Clients can request custom UB formulas (e.g., adjusting weights for different interaction types) through the Analytics team.

> 📘 Note
>
> **UI Controls**: A button may be visible in the console but is currently a **placeholder**. Future updates may allow configuration through the console UI.

Below are the steps involved in User Behaviour Ranking:

1. **Event Tracking**: Streamed events (click, cut, order) are collected via the analytics integration.
2. **Query-Level Aggregation**: The system aggregates all interactions for a given query.
3. **Scoring**: Products are scored based on interaction types using a default formula (e.g., more weight to orders than clicks).
4. **Boosting**: These UB scores boost relevant products during future searches for the same query.

# Popularity

**Popularity** reflects how often products are ordered across **all queries and pages**. Unlike **user behaviour**, popularity is site-wide and not tied to a specific query.

Below are steps are involved in Popularity Ranking

1. **Site-Level Aggregation**: Orders are tracked across the entire catalog.
2. **Scoring**: Products with higher order volume are assigned higher popularity scores.
3. **Top-N Products**: The system identifies and ranks the **top 1000** products by default.

### Configuration

* **Default**: Popularity is also **enabled by default** for all clients with analytics integration.
* **Custom Configuration**: Clients can request:
  * A different number of top products (e.g., top 100 instead of 1000)
  * Custom weighting strategies (via Analytics team)