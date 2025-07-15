---
name: Multiplehierarchialfacets
---
# Q. Do we support multiple hierarchical facets on a single Search Results Page?

A. You can build a hierarchy in your facet values to enable multi-level navigation and filtering. This pattern is great for very long lists of values and to improve discoverability: your users will be able to browse up and down in the levels to refine their searches. Using multilevel faceting, we can view number of products present in each category and apply these filters directly to narrow down our search.

To enable, the dataType of these fields should be set as “path”. Hierarchical facets can be configured only on “path”  fields.

A sample request to check: `[https://search.unbxd.io/API](https://search.unbxd.io/API) Key/Site Key/search?&q=*&rows=40&start=0&version=V2&format=json&variants=true&filter=category_path:%22Apparel%22&filter=color:%22Black%22&facet.multiselect=tru`