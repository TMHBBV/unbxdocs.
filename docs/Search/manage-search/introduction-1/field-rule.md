---
title: Field Rule
deprecated: false
hidden: true
metadata:
  robots: index
---
Field rules are used to create facets and banners for a specific page. By default, facet under Site Rule is inherited to all the pages, however, you can override them by creating a field rule for that particular page.

Field rules allow you to show banners and facets when more than 80% of the products satisfy field rule criteria. While facets under Site Rules are displayed for all queries, Field Rules allow you to override the facets defined in site-rule based on product-type/category, etc.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/6929e510039c66d43ae2b84ac1a93306f788ecc6ea1f85b58ff857aad71f8c85-image.png" />

When a query has multiple Field Rules – where more than 80% of retrieved products can map to two different Field Rules – the creation date of Field Rules is considered. Older Field Rules will take precedence over newer Field Rules. While facets under Site Rules are displayed for all queries, Field Rules allow you to override them for queries for certain type/category.

For example, if a field rule is created for ‘Hybrid Cycles’ and when a shopper searches for ‘Cycles’, and 80% of the search results are ‘Hybrid Cycles’, then the ‘Hybrid Cycles’ field rule will be applied.

Field Rules created in Search and Browse are exclusive of each other and will not overlap.

> 📘 Note
>
> In case of conflicts in facet settings, field rules are given preference over site-rules.

## Create a Field Rule

To add a field rule follow the mentioned process :

1. Navigate to Merchandising → Browse → Field Rule.
2. To add fields, do the following:
   1. Click  .
   2. Select the fields you want to use. You can also search for the fields.\
      Note: You can select a maximum of five fields.
   3. Click Apply.\
      The selected fields appear in the Create Field Rule window.
3. Click  .The Create Field Rule window appears.
4. Select the field you want to use.
5. Select the respective field value.
6. Click Create Field Rule.The new field rule is added to the Field Rule tab.
7. Click the field rule you want to publish.
8. To set up banner using an image url, do the following:

a. Click Image url.

b. Enter the url of an existing banner image.

c. Enter the corresponding landing page url.

9. To set up a banner using HTML, click HTML, and then paste your banner HTML code.
10. Click the Facets tab. You can navigate to Manage → Configure Site to configure facets. For more information on configuring facets, see Configure Facets.
11. To reposition a facet, do the following:
    1. Hover on the faceting row you want to reposition. The reposition icon  appears.
    2. Click , and then drag the facet to a new position.
    3. If you want to show the facet on your site, in the Show column, select the respective facet checkbox.
    4. Click  to save the repositioning changes.

## Edit a Field Rule

To modify a facet, edit using the mentioned process :

1. Click the facet for which you want to edit the values.
2. Click .
3. Type the new facet length.
4. Select sort order for your facet. You can sort either by product count or alphabetically.
5. Click Save.
6. To go to the previous screen, click  PREV.
7. Click PUBLISH.

## Delete a Field Rule

To Delete a field rule follow the mentioned process :

1. Within the console, navigate to Merchandising > Browse > Field Rule.
2. Click Field Rule.
3. Click the delete icon for the required Rule.
4. You’ve successfully deleted the field rule.

> ❗️ CAUTION
>
> Deleting will permanently remove the Rule. You cannot recover a deleted field rule.