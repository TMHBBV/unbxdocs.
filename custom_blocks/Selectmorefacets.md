---
name: Selectmorefacets
---
# Q. How can we allow our shoppers to select more than one facet?

A. In order to support selection of more than one values in facets the following changes should be made :

* Filter parameter changes : The **filter** parameter in the search API supports more than one value separated by an OR operator.  If the shopper selects more than one value in a facet then the payload for the filter parameter should be specified in the following manner : filter=:”” OR :”:”.
* Add Facet.multiselect parameter : Set **facet.multiselect=true** in the search request to ensure that the remaining values in the facet are retained along with the product count associated with them. By default, facet.multiselect is false, which leads to removal of remaining values from the facet once one value is selected.

The option to select multiple values in a facet is available only for ‘Range’ and ‘Text’ facets. Multi-level facets do not support selection of more than one value.