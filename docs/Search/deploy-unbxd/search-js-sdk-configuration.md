---
title: Search JS SDK Configuration
deprecated: false
hidden: false
metadata:
  robots: index
---
This document outlines the available configuration options for the UNBXD Search JS SDK. Refer to the [GitHub Link](#) for implementation examples.

***

# Examples/Recipes

* [Basic (default template) : ES5](#)
* [Basic (default template) : ES6](#)
* [Custom product card](#)
* [Pagination: infinite scroll](#)
* [Pagination: fixed size](#)
* [Pagination: Load More](#)
* [Range slider as checkboxes](#)
* [Customised](#)
* [IE10 Support](#)

***

# Search Template Config

The search template options are configured under the `products` object.

| **OPTIONS**        | **DATATYPE** | **DESCRIPTION**                                                            |
| ------------------ | ------------ | -------------------------------------------------------------------------- |
| `gridCount`        | Number       | Number of columns in grid view                                             |
| `defaultFilters`   | Object       | Default filters applied to all API requests                                |
| `template`         | Function     | Function with parameters: `product`, `idx` for rendering each product card |
| `productItemClass` | String       | Class name for the product card                                            |
| `productType`      | String       | One of `SEARCH`, `BROWSE`, or `CATEGORY`                                   |
| `attributesMap`    | Object       | Field mappings for the current product card                                |
| `el`               | Element      | Element to place the search template                                       |

***

# Loader Config

| **OPTIONS** | **DATATYPE** | **DESCRIPTION**              |
| ----------- | ------------ | ---------------------------- |
| `template`  | Function     | Template function for loader |
| `el`        | Element      | Element to place the loader  |

***

# No Results Config

| **OPTIONS** | **DATATYPE** | **DESCRIPTION**                          |
| ----------- | ------------ | ---------------------------------------- |
| `template`  | Function     | Template function for no-results section |
| `el`        | Element      | Element to place the no-results message  |

***

# Facet Config

| **OPTIONS**               | **DATATYPE** | **DESCRIPTION**                                   |
| ------------------------- | ------------ | ------------------------------------------------- |
| `facetsEl`                | Element      | Element to place facet elements                   |
| `facetTemplate`           | Function     | Template with args `facetInfo`, `facets`          |
| `facetItemTemplate`       | Function     | Template to render individual facet filters       |
| `facetMultiSelect`        | Boolean      | Enable multiple facet selection                   |
| `facetClass`              | String       | CSS class name for facet item                     |
| `facetAction`             | String       | Interaction type: `click` or `change`             |
| `selectedFacetClass`      | String       | CSS class for selected facet                      |
| `selectedFacetsEl`        | Element      | Element to place selected facets                  |
| `selectedFacetTemplate`   | Function     | Template to customize selected facet view         |
| `rangeFacetEl`            | Element      | Placeholder to render range facet                 |
| `rangeTemplate`           | Function     | Template function for customizing range filters   |
| `rangeWidgetConfig`       | Function     | Config for range sliders (minLabel, maxLabel)     |
| `multiLevelFacetSelector` | String       | Class name for multilevel facet items             |
| `multiLevelFacetEl`       | Element      | Placeholder to render multilevel facet            |
| `facetDepth`              | Number       | Number of category filter levels                  |
| `clearFacetsSelector`     | String       | CSS class for "Clear All" button                  |
| `removeFacetsSelector`    | String       | CSS class to remove individual facet filters      |
| `onFacetLoad`             | Function     | Callback after a facet is selected                |
| `applyMultipleFilters`    | Boolean      | Apply multiple facet filters at once              |
| `isCollapsible`           | Boolean      | Enable accordion-style facets                     |
| `defaultOpen`             | String       | Facets to open by default: `ALL`, `FIRST`, `NONE` |
| `isSearchable`            | Boolean      | Enable search within facets                       |

***

# Pagination Config

| **OPTIONS**  | **DATATYPE** | **DESCRIPTION**                                                    |
| ------------ | ------------ | ------------------------------------------------------------------ |
| `el`         | Element      | Placeholder for pagination element                                 |
| `type`       | String       | One of: `FIXED_PAGINATION`, `INFINITE_SCROLL`, or `CLICK_N_SCROLL` |
| `onPaginate` | Function     | Callback after pagination action                                   |
| `action`     | String       | Pagination trigger: `click` or `change`                            |
| `template`   | Function     | Custom template for pagination layout                              |

***

# Spellcheck Config

| **OPTIONS** | **DATATYPE** | **DESCRIPTION**                             |
| ----------- | ------------ | ------------------------------------------- |
| `enabled`   | Boolean      | Enable spellcheck feature                   |
| `el`        | Element      | Element to place spellcheck suggestions     |
| `template`  | Function     | Function to customize spellcheck appearance |

***

# Sort Config

| **OPTIONS**         | **DATATYPE** | **DESCRIPTION**                                             |
| ------------------- | ------------ | ----------------------------------------------------------- |
| `el`                | Element      | Placeholder for the sort section                            |
| `options`           | Array        | Array of sort options                                       |
| `sortClass`         | String       | CSS class name for sort option items                        |
| `selectedSortClass` | String       | CSS class for the selected sort item                        |
| `template`          | Function     | Template to customize sort layout (receives options object) |

***

# PageSize Config

| **OPTIONS**             | **DATATYPE** | **DESCRIPTION**                                |
| ----------------------- | ------------ | ---------------------------------------------- |
| `pageSize`              | Number       | Number of results per page                     |
| `options`               | Array        | Array of available page size options           |
| `pageSizeClass`         | String       | CSS class for page size element                |
| `selectedPageSizeClass` | String       | CSS class for selected page size               |
| `action`                | String       | `click` or `change` based on UI interaction    |
| `template`              | Function     | Template for customizing the page size section |
| `el`                    | Element      | Element to place the page size controls        |

***

# Breadcrumb Config

| **OPTIONS**     | **DATATYPE** | **DESCRIPTION**                           |
| --------------- | ------------ | ----------------------------------------- |
| `enabled`       | Boolean      | Enable breadcrumbs                        |
| `el`            | Element      | Placeholder for breadcrumb trail          |
| `selectorClass` | String       | CSS class for individual breadcrumb items |
| `template`      | Function     | Custom template for breadcrumb layout     |

***

# Product Views

| **OPTIONS**             | **DATATYPE** | **DESCRIPTION**                                    |
| ----------------------- | ------------ | -------------------------------------------------- |
| `el`                    | Element      | Element to place view toggle                       |
| `action`                | String       | Event to trigger view change (`click` or `change`) |
| `viewTypeClass`         | String       | Class for the view type icons                      |
| `selectedViewTypeClass` | String       | Class for selected view type                       |
| `viewTypes`             | String       | View types available: `LIST`, `GRID`               |

***

# Variants Config

| **OPTIONS**  | **DATATYPE** | **DESCRIPTION**                                   |
| ------------ | ------------ | ------------------------------------------------- |
| `enabled`    | Boolean      | Enable variant support                            |
| `count`      | Number       | Number of variants per product                    |
| `groupBy`    | String       | Field to group variants (must exist in catalogue) |
| `attributes` | Array        | List of required variant fields                   |
| `mapping`    | Object       | Mapping between product and variant fields        |