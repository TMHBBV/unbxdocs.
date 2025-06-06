---
title: Boost/Bury
deprecated: false
hidden: false
metadata:
  robots: index
---
Boosting within a page rule lets you promote (or demote) products for a particular page based on a specified condition. For example, a boost rule can be created for a category to boost products with field name “color” and value “red” to the top of the page results.

Boosting and burying can be done on 100 levels, allowing for soft boost and soft bury. Earlier, Unbxd used to support 3 levels of boosting (high, moderate, low) and just 1 level of demoting.

The mapping between old boost scoring to new scoring is mentioned below:

Boost of High in old scoring => Boost of level +40 in the new scoringBoost of Moderate in old scoring => Boost of level +20 in the new scoringBoost of Low in old scoring => Boost of level +10 in the new scoringDemote in old scoring => Bury of level -100 in the new scoring

The boost levels above determine the position of the products (from top to bottom respectively) on a specific page integrated using Unbxd Browse, for example, Category, Brand, etc.

Common Application of Boost/Bury

* Demoting ranking of products with low inventory.
* Promoting discounted products during clearance sale.
* Promoting private label brands in your e-commerce store.
* Existing use-case for boost is calling out slotting as a better alternative.

How to implement Boost?

To apply boost, select the attribute rule values. Attribute rule is created by selecting the field name which changes the comparator accordingly.

Field names can be either text fields or numeric ones. For example, fields like color, gender, fabric etc. are text value containing fields. Comparators are used for drawing comparisons with reference to a base value. The base value is the field name. When the field name is specified, accordingly an option from the drop-down menu of comparators is selected. If a text field is selected, the comparator can have following options:

contains: means the exact match of the field name character\
does not contain: means ‘should not match’ the field name exactly
equals: means a partial match of the field name characters
Not equals to: not a partial match of the field name
If a numeric field is selected, the comparator can have the following options:
equal to: the exact match of the number. Like boost products with an average rating of 4
in between: display products of the fields with the specified range of numbers. Like boost products with a rating from 2 to 4
more than: the products displayed should be of the greater value of the specified number
Less than: the products displayed should be of lesser value of the specified number
The ‘value’ field contains the numeric or text value of the field
The Search Results page will list products depending on the level you choose. By default, the value is 1, which means the product will only be slightly boosted (soft boost). If you scroll the bar to make the boost value ‘100’ (hard boost), then the product will display at the top of the results page. To implement boosting select the attribute rule and adjust the level to define their position.

> 📘 Note
>
> While boosting on multiple attributes simultaneously, we recommend you create multiple boost groups with varying boost or bury levels.

For instance, you created a boost rule for ‘Bowling Shoes’ with field name ‘color’ and value ‘black’ to promote them to the top of the search results.

In this illustration, black bowling shoes are set to be boosted (or set to be shown at the top) within the Search Results page. Only setting Boost rules will however result in the search results page showing only black bowling shoes, ahead of showing bowling shoes in other colors. This results in a lack of variety for your shoppers. Slotting, in such case, can be used to promote a certain number of bowling shoes at specific rows.The boost levels should be selected carefully. Applying extremely high levels of boost can distort the relevance of search results and push the ranking of most selling products down which is not ideal. With these data points you can boost any number of products by adjusting the attribute rule.

In previous versions, Unbxd used to support 3 levels of boosting (high, moderate, low) with just 1 level of bury. In the current version, you can boost or bury at 100 levels, allowing for soft boost and soft bury.

| Previous versions | Current version |
| :---------------- | :-------------- |
| High              | +40             |
| Moderate          | +20             |
| Low               | +10             |
| Demote            | -100            |

To boost/bury an existing campaign in a Query Rule:

1. In the Merchandise section, click START MERCHANDISING.
2. On the Boost tab, select field name from the dropdown list.
3. Select a comparator based on the field (equal to, not equal to, contains, does not contain).\
   Note: For the field “price”, comparator options are equal to, in between, more than, and less than.
4. Specify the value.
5. Move the slider to assign a boost level. The default value of the boost is Low.
6. To create multiple attribute rules for the boost group, click Add attribute rule.
7. To add multiple boost groups, click .

   Tips: As a best practice, always assign different boost level across different boost group in order to get the desired arrangement of the results.