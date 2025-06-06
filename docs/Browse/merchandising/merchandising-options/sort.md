---
title: Sort
deprecated: false
hidden: false
metadata:
  robots: index
---
Sorting allows you to rearrange the search results based on certain fields in a particular order. Search results can be sorted in either numerical (ascending/descending) or alphabetical order (A-Z or Z-A) depending on the field value. By default, products are sorted by relevance to match your shopper’s intent. When a campaign has multiple sort rules, the first sort rule will have precedence over subsequent sort rules.

> 📘 Note
>
> You cannot create sort rules when boost/slot/sort rules exist.

## Common Applications of Sorting

* You can apply sorting price attribute to rank products based on their sale price while creating a rule for ‘Cheap shoes’.
* You can use the sorting rule to sort product based on user ratings to ensure highest rated products come first

## How to implement sorting?

To apply sorting rules, select the field name based on which you would want to sort the products and display it on the search results page. The products for the selected field name can be sorted either in descending or in ascending order.

If you have created a sort group with the following attribute rules:

* price (ascending)
* color (A-Z), and
* brand (A-Z)

The search result will be in this order:

* Products sorted on price (ascending)
* Products with same price sorted on color (A-Z)
* Products with same price and color, sorted on brand (A-Z)

> 📘 Note
>
> You cannot create sort groups when a boost/slot/pin rules exist.

To create a sort group:

1. In the Merchandise section, click START MERCHANDISING.
2. Click the Sort tab.
3. Select the field name from the dropdown list.
4. Select sort order (ascending and descending or ascending A-Z and descending Z-A).
5. To add multiple attribute rules for the sort group, click Add attribute rule.

You have successfully created a sort group.