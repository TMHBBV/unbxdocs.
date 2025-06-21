---
title: Javascript SDK
deprecated: false
hidden: false
metadata:
  robots: index
---
# Unbxd Search JS SDK Documentation

The Unbxd Search JS SDK enables integration of Unbxd search functionalities to optimize and customize search result layouts using JavaScript.

## Libraries

The following libraries are required for the Unbxd Search JS SDK:

| Library    | Version  |
|------------|----------|
| jQuery     | 1.11.3+  |
| Handlebars | 3.0.3+   |

If your website does not use these libraries, they can be bundled with the Unbxd Search JS file. Refer to the bundle build procedure for configuration details.

## Quickstart

This section guides you through integrating the Unbxd Search JS SDK to power a search results display page. The SDK uses Handlebars as its HTML templating engine.

### Step 1: Include Dependencies

Add the following CSS and JS files to the `<head>` section of your HTML page:

```html
<head>
    <link rel="stylesheet" href="http://demo-unbxd.unbxdapi.com/static/demo-unbxd/stylesheets/search.css" />
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/3.0.3/handlebars.min.js"></script>
    <script type="text/javascript" src="https://libraries.unbxdapi.com/unbxdSearch_v2.js"></script>
</head>
```

### Step 2: Instantiate setSearch

Initialize the `setSearch` method with the required configuration:

```javascript
<script type="text/javascript">
    new Unbxd.setSearch({
        siteName: "<your site key>",
        APIKey: "<your API key>",
        type: "search",
        inputSelector: "#search_input"
    });
</script>
```

## Authentication

Authenticate the Unbxd extension using your account keys (Site Key and API Key), which are issued upon signing up with Unbxd. Common scenarios include:

- One website with two environments (production and staging): 2 site keys, 1 API key.
- Multiple websites: A site key for each website and environment combination, with multiple API keys.

Obtain your keys from the Unbxd console (refer to the Help Documentation) and pass them as follows:

```javascript
new Unbxd.setSearch({
    siteName: "<your site key>",
    APIKey: "<your API key>"
});
```

### Configuration Details

- **siteName**:
  - **Data type**: String
  - **Required**: True
  - **Description**: Unique identifier for each customer/site.

- **APIKey**:
  - **Data type**: String
  - **Required**: True
  - **Description**: Unique API key assigned by Unbxd.

## Types of Pages to Render

The SDK supports rendering different page types:

- **Search**: Powers search results pages.
- **Browse**: Powers category listing pages.
- **Recommendations**: Powers personalized recommendations.

Specify the page type using the `type` parameter:

```javascript
new Unbxd.setSearch({
    siteName: "<your site key>",
    APIKey: "<your API key>",
    type: "search"
});
```

### Configuration Details

- **type**:
  - **Data type**: String
  - **Required**: True
  - **Default**: search
  - **Possible values**: `search`, `category`
  - **Description**: Indicates whether the page is for search or category.
  - **Dependencies**:
    - For `search`, provide `searchQueryParam`.
    - For `category`, provide `getCategoryID`.

## Configuring the Page

A search results or category landing page typically includes:

- Products list (grid or list view)
- Sort by widget
- Pagination widget (traditional, infinite scroll, or load more)
- Facets section
- Spell check/search results message
- Merchandising banners

### Search Input Box & Search Button Selector

Bind keyboard and mouse events to the search input and button:

```javascript
new Unbxd.setSearch({
    siteName: "<your site key>",
    APIKey: "<your API key>",
    type: "search",
    inputSelector: "#searchBox",
    searchButtonSelector: "#searchButton"
});
```

- **inputSelector**:
  - **Data type**: String
  - **Required**: False
  - **Default**: `#search_query`
  - **Description**: CSS selector for the search input box.

- **searchButtonSelector**:
  - **Data type**: String
  - **Required**: False
  - **Default**: `#search_button`
  - **Description**: CSS selector for the search button.

### Search Product Results Container

Configure the container for search results and the product card template:

```javascript
searchResultContainer: "#searchResultContainer",
searchResultSetTemp: [
    'grid: {{#products}}',
    '<div class="unbxd_product_tile">',
    '<a href="{{productUrl}}" class="unbxd-product-image" title="{{title}}" unbxdparam_sku="{{uniqueId}}" unbxdparam_prank="{{unbxdprank}}">',
    '<img alt="{{title}}" src="{{imageUrl}}">',
    '<div class="prod_price">Price: ${{price_min}} - ${{price_max}}</div>',
    '<div class="prod_title">{{title}}</div>',
    '</a></div>',
    '{{/products}}'
].join('')
```

- **searchResultContainer**:
  - **Data type**: String
  - **Required**: True
  - **Description**: CSS selector for the product results wrapper.
  - **Sample**: `#unbxd_product_results_container`

- **searchResultSetTemp**:
  - **Data type**: Array/Function
  - **Required**: True
  - **Description**: Handlebars template for product cards or a function for dynamic binding.

### Sort Options

Configure the sort by feature:

```javascript
sortContainerSelector: "#sortContainer",
sortContainerType: "select",
sortOptions: [
    { name: "Relevancy" },
    { name: "Price: High to Low", field: "price_max", order: "desc" },
    { name: "Price: Low to High", field: "price_min", order: "asc" }
]
```

- **sortContainerSelector**:
  - **Data type**: String
  - **Required**: False
  - **Description**: CSS selector for the sort section.
  - **Sample**: `#sort_section`

- **sortOptions**:
  - **Data type**: Array
  - **Required**: False
  - **Sample**:
    ```json
    [
        { name: "Relevancy" },
        { name: "Price: H-L", field: "price", order: "desc" },
        { name: "Price: L-H", field: "price", order: "asc" }
    ]
    ```

- **sortContainerType**:
  - **Data type**: String
  - **Required**: True (if sort is applicable)
  - **Default**: `select`
  - **Accepted values**: `click`, `select`

### Pagination

Configure pagination behavior:

#### Traditional Pagination

```javascript
isPagination: true,
paginationContainerSelector: "#paginationContainer",
paginationTemp: [
    '{{#if hasPrev}}',
    '<span class="unbxd_prev" unbxdaction="prev">Previous</span>',
    '{{/if}}',
    '{{#pages}}',
    '{{#if current}}',
    '<span class="unbxd_page highlight">{{page}}</span>',
    '{{else}}',
    '<span class="unbxd_page" unbxdaction="{{page}}">{{page}}</span>',
    '{{/if}}',
    '{{/pages}}',
    '{{#if hasNext}}',
    '<span class="unbxd_next" unbxdaction="next">Next</span>',
    '{{/if}}'
].join('')
```

- **isPagination**:
  - **Data type**: Boolean
  - **Required**: False
  - **Default**: False
  - **Description**: Enable traditional pagination.

- **paginationContainerSelector**:
  - **Data type**: String
  - **Required**: True (if `isPagination` is true)
  - **Sample**: `#pagination_section`

- **paginationTemp**:
  - **Data type**: String
  - **Required**: False
  - **Description**: Handlebars template for pagination.

#### Infinite Scroll

```javascript
isAutoScroll: true,
heightDiffToTriggerNextPage: 250
```

- **isAutoScroll**:
  - **Data type**: Boolean
  - **Required**: False
  - **Default**: False
  - **Description**: Enable infinite scroll.

- **heightDiffToTriggerNextPage**:
  - **Data type**: Number
  - **Required**: True (if `isAutoScroll` is true)
  - **Default**: 100
  - **Sample**: 250

#### Load More Button

```javascript
isClickNScroll: true,
clickNScrollElementSelector: "#load_more_results"
```

- **isClickNScroll**:
  - **Data type**: Boolean
  - **Required**: False
  - **Default**: False
  - **Description**: Enable load more button.

- **clickNScrollElementSelector**:
  - **Data type**: String
  - **Required**: True (if `isClickNScroll` is true)
  - **Sample**: `#load_more_results`

### Facets

Configure the facets section:

```javascript
facetContainerSelector: "#facetContainer",
facetCheckboxSelector: "#facetContainer .facet_value input[type=checkbox]",
facetMultiSelect: true,
facetTemp: [
    '{{#facets}}',
    '<div id="{{facet_name}}">',
    '<h3>{{name}}</h3>',
    '<div class="facet_values">',
    '{{#selected}}',
    '<div class="facet_value">',
    '<input type="checkbox" id="{{../facet_name}}-{{value}}" checked unbxdParam_facetName="{{../facet_name}}" unbxdParam_facetValue="{{value}}">',
    '<label for="{{../facet_name}}-{{value}}">{{value}} ({{count}})</label>',
    '</div>',
    '{{/selected}}',
    '{{#unselected}}',
    '<div class="facet_value">',
    '<input type="checkbox" id="{{../facet_name}}-{{value}}" unbxdParam_facetName="{{../facet_name}}" unbxdParam_facetValue="{{value}}">',
    '<label for="{{../facet_name}}-{{value}}">{{value}} ({{count}})</label>',
    '</div>',
    '{{/unselected}}',
    '</div></div>',
    '{{/facets}}'
].join('')
```

- **facetContainerSelector**:
  - **Data type**: String
  - **Required**: True
  - **Sample**: `#facets_container`

- **facetCheckboxSelector**:
  - **Data type**: String
  - **Required**: True
  - **Sample**: `#facets_container .facet_value input[type=checkbox]`

- **facetMultiSelect**:
  - **Data type**: Boolean
  - **Required**: True
  - **Default**: True
  - **Description**: Allow multiple facet selections.

- **facetTemp**:
  - **Data type**: String
  - **Required**: False
  - **Description**: Handlebars template for facets.

### Selected Facets

```javascript
selectedFacetContainerSelector: "#selectedFacetContainer",
selectedFacetTemp: [
    '<ol class="unbxd_selected_facets">',
    '{{#filters}}',
    '<li>{{value}} <a href="#" class="unbxd-remove-item" unbxdParam_facetName="{{fsysname}}" unbxdParam_facetValue="{{value}}">x</a></li>',
    '{{/filters}}',
    '</ol>'
].join('')
```

- **selectedFacetContainerSelector**:
  - **Data type**: String
  - **Required**: True
  - **Sample**: `#selected_filters_section`

- **selectedFacetTemp**:
  - **Data type**: String
  - **Required**: False
  - **Description**: Handlebars template for selected facets.

### Spellcheck

Configure the spellcheck section:

```javascript
spellCheck: "#spellCheck",
spellCheckTemp: '<h3>Did you mean: {{suggestion}}</h3>'
```

- **spellCheck**:
  - **Data type**: String
  - **Required**: False
  - **Sample**: `#did_you_mean`

- **spellCheckTemp**:
  - **Data type**: String
  - **Required**: True
  - **Default**: `<h3>Did you mean: {{suggestion}}</h3>`

### Search Query Display

```javascript
searchQueryDisplay: "#searchQueryDisplay",
searchQueryDisplayTemp: '<h3>Search results for {{query}} – {{numberOfProducts}}</h3>'
```

- **searchQueryDisplay**:
  - **Data type**: String
  - **Required**: True
  - **Sample**: `#search_result_display`

- **searchQueryDisplayTemp**:
  - **Data type**: String
  - **Required**: True
  - **Default**: `<h3>Search results for {{query}} – {{numberOfProducts}}</h3>`

## Callback Functions

### onFacetLoad

```javascript
onFacetLoad: function(obj) {
    if (this.facetScrollTop) {
        jQuery("html, body").animate({
            scrollTop: 0
        }, 300);
        this.facetScrollTop = false;
    }
}
```

- **Data type**: Function
- **Required**: Optional
- **Description**: Invoked after facets are rendered.

### onIntialResultLoad

```javascript
onIntialResultLoad: function(obj) {
    var pids_list = [];
    for (var i = 0; i < obj['response']['products'].length; i++) {
        var prd = obj['response']['products'][i];
        var sku = prd['uniqueId'];
        pids_list.push(sku.replace(/\./g, ""));
    }
    var impressionObj = { query: obj['searchMetaData']['queryParams']['q'], pids_list: pids_list };
    Unbxd.track(impressionObj, 'search_impression');
}
```

- **Data type**: Function
- **Required**: Optional
- **Description**: Invoked on initial page binding.

### onPageLoad

```javascript
onPageLoad: function(obj) {
    var pids_list = [];
    for (var i = 0; i < obj['response']['products'].length; i++) {
        var prd = obj['response']['products'][i];
        var sku = prd['uniqueId'];
        pids_list.push(sku.replace(/\./g, ""));
    }
    var impressionObj = { query: obj['searchMetaData']['queryParams']['q'], pids_list: pids_list };
    Unbxd.track(impressionObj, 'search_impression');
}
```

- **Data type**: Function
- **Required**: Optional
- **Description**: Invoked on page content refresh.

## Helper Functions

### unbxdIf

```handlebars
{{#unbxdIf ../facet_name "v_PriceRange_uFilter"}}Price{{else}}{{../facet_name}}{{/unbxdIf}}
```

- **Purpose**: Renders a block if two arguments are equal.

### prepareFacetValue

```handlebars
{{#prepareFacetValue value}}{{/prepareFacetValue}}
```

- **Purpose**: Returns three non-breaking spaces if the value is empty, otherwise returns the value.

## Available Configurations

| Config Name                     | Data Type | Description                                                                 | Sample Values                                                                 |
|---------------------------------|-----------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| siteName                        | String    | Unique identifier for each customer/site                                    | demo-com809841570123270                                                       |
| APIKey                          | String    | Unique API key assigned by Unbxd                                            | 7689867nbh868u4j3b4u998                                                      |
| inputSelector                   | String    | CSS selector for the search input box                                       | #search_mini_form input                                                       |
| searchButtonSelector            | String    | CSS selector for the search submit button                                   | #search_mini_form button.searchicon                                           |
| type                            | String    | Indicates search or category page                                           | search, category                                                              |
| searchQueryParam                | String    | Search query parameter name                                                 | q                                                                             |
| spellCheck                      | String    | CSS selector for the "Did you mean" section                                 | #did_you_mean                                                                 |
| spellCheckTemp                  | String    | HTML template for the spellcheck section                                    | `<span>Did you mean <span class="bold">{{suggestion}}</span> ?</span>`        |
| searchQueryDisplay              | String    | CSS selector for the search results message section                         | #search_result_display                                                        |
| searchResultContainer           | String    | CSS selector for the product results container                              | #results-container                                                            |
| isAutoScroll                    | Boolean   | Enable autoscroll behavior                                                  | true                                                                          |
| heightDiffToTriggerNextPage     | Number    | Pixels from bottom to trigger next page                                      | 250                                                                           |
| isClickNScroll                  | Boolean   | Enable load more behavior                                                   | true                                                                          |
| clickNScrollElementSelector     | String    | CSS selector for the load more button                                       | #load-more-results                                                            |
| isPagination                    | Boolean   | Enable traditional pagination                                               | true                                                                          |
| paginationContainerSelector     | String    | CSS selector for the pagination section                                     | .page-nav-section                                                             |
| facetMultiSelect                | Boolean   | Allow multiple facet selections                                             | true                                                                          |
| facetContainerSelector          | String    | CSS selector for the facets section                                         | #facets_container                                                             |
| facetCheckBoxSelector           | String    | CSS selector for facet checkboxes                                           | #facets_container .facet_value input[type=checkbox]                           |
| selectedFacetContainerSelector  | String    | CSS selector for the selected facets section                                | #applied-filter-section                                                       |
| clearSelectedFacetsSelector     | String    | CSS selector for the clear all facets link                                  | #clear-all-filters                                                            |
| removeSelectedFacetSelector     | String    | CSS selector for individual facet reset links                              | .unbxd-remove-item                                                            |
| sortContainerSelector           | String    | CSS selector for the sort section                                           | #sort-section                                                                 |
| sortOptions                     | Array     | List of sort options                                                        | `[{name: "Popularity"}, {name: "Low to High Price", field: "price_min", order: "asc"}]` |
| sortContainerType               | String    | Type of sort container (click or select)                                    | click, select                                                                 |
| pageSize                        | Number    | Number of products per page                                                 | 24                                                                            |
| pageSizeContainerSelector       | String    | CSS selector for the page size section                                      | #results-pagesize                                                             |
| pageSizeOptions                 | Array     | List of page size options                                                   | `[{name: "48 item", value: "48"}, {name: "72 items", value: "72"}]`           |
| pageSizeContainerType           | String    | Type of page size container (click or select)                               | click, select                                                                 |
| viewTypeContainerSelector       | String    | CSS selector for the page view section                                      | #results-pageview                                                             |
| viewTypes                       | Array     | List of view types                                                          | `["list", "grid"]`                                                            |
| variants                        | Boolean   | Enable variants display                                                     | true                                                                          |
| variantsCount                   | Number    | Number of variants to show                                                  | 3                                                                             |
| isSwatches                      | Boolean   | Enable swatches display                                                     | true                                                                          |
| swatchesSelector                | String    | CSS selector for swatches                                                   | .swatch-box                                                                   |
| mappedFields                    | Object    | Field names for product attributes                                          | `{ "imageUrl": "imageUrl", "title": "title" }`                                |

## Platform Integration

For platform-specific integration details, refer to the Unbxd Help Documentation.

---

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Unbxd Search Page</title>
    <link rel="stylesheet" href="http://demo-unbxd.unbxdapi.com/static/demo-unbxd/stylesheets/search.css" />
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/3.0.3/handlebars.min.js"></script>
    <script type="text/javascript" src="https://libraries.unbxdapi.com/unbxdSearch_v2.js"></script>
    <style>
        .search-container { margin: 20px; }
        .search-input { padding: 10px; width: 300px; }
        .search-button { padding: 10px; }
        .search-results { display: flex; justify-content: flex-start; gap: 20px; flex-wrap: wrap; }
        .unbxd_product_tile { width: 200px; margin: 10px; border: 1px solid #ddd; padding: 10px; }
        .facets-container { width: 200px; margin-right: 20px; }
        .pagination-container { margin: 20px; 0; }
        .sort-container { margin: flex; 10px; 0 }
        .selected-facets { margin: 10px; 0; }
        .spell-check { display: inline-block; color: #e44c; }
    </style>
</head>
<body>
    <div class="search-container">
        <input type="text" id="searchBox" class="search-input" placeholder="Search products..." />
        <button id="searchButton" class="search-button">Search</button>
    </div>
    <div id="spellCheckContainer" class="spell-check"></div>
    <div id="searchQueryDisplay"></div>
    <div id="selectedFacetContainer" class="selected-facets"></div>
    <div class="main-content">
        <div id="facetContainer" class="facets-container"></div>
        <div class="results-section">
            <div id="sortContainer" class="sort-container"></div>
            <div id="searchResultContainer" class="search-results"></div>
            <div id="paginationContainer" class="pagination-container"></div>
        </div>
    </div>

    <script type="text/javascript">
        new Unbxd.setSearch({
            siteName: "<your site key>",
            APIKey: "<your API key>",
            type: "search",
            inputSelector: "#searchBox",
            searchButtonSelector: "#searchButton",
            searchQueryParam: "q",
            searchResultContainerSelector: "#searchResultContainer",
            searchResultSetTemp: [
                'grid: {{#products}}',
                '<div class="unbxd_product_tile">',
                '<a href="{{productUrl}}" class="unbxd-product-image" title="{{title}}" unbxdparam_sku="{{uniqueId}}" unbxdparam_prank="{{unbxdprank}}">',
                '<img alt="{{title}}" src="{{imageUrl}}">',
                '<div class="prod_price">Price: ${{price_min}} - ${{price_max}}</div>',
                '<div class="prod_title">{{title}}</div>',
                '</a></div>',
                '{{/products}}'
            ].join(''),
            facetContainerSelector: "#facetContainer",
            facetCheckboxSelector: "#facetContainer .facet_value input[type=checkbox]",
            facetMultiSelect: true,
            facetTemp: [
                '{{#facets}}',
                '<div id="{{facet_name}}">',
                '<h3>{{name}}</h3>',
                '<div class="facet_values">',
                '{{#selected}}',
                '<div class="facet_value">',
                '<input type="checkbox" id="{{../facet_name}}-{{value}}" checked unbxdParam_facetName="{{../facet_name}}" unbxdParam_facetValue="{{value}}">',
                '<label for="{{../facet_name}}-{{value}}">{{value}} ({{value}})</label>',
                '</div>',
                '{{/selected}}',
                '{{#unselected}}',
                '<div class="facet_value">',
                '{{<input type="checkbox" id="{{../facet_name}}-{{value}}" unbxdParam_facetName="{{../facet_name}}" unbxdParam_facetValue="{{value}}">}}',
                '{{<label for="{{../facet_name}}-{{value}}">{{value}} ({{value}})</label>',
                '</div>',
                '{{/unselected}}',
                '</div></div>',
                '{{/facets}}'
            ].join(''),
            selectedFacetContainerSelector: "#selectedFacetContainer",
            selectedFacetTemp: [
                '<ol class="unbxd_filters">',
                '{{#filters}}',
                '<li>{{value}} <a href="#" class="unbxd-remove-item" unbxdParam_facetName="{{fsysname}}" unbxdParam_facetValue="{{value}}">x</a></li>',
                '{{/filters}}',
                '</ol>'
            ].join(''),
            clearSelectedFacetsSelector: "#clear_all_filters",
            removeSelectedFacetSelector: ".unbxd-remove-item",
            spellCheck: "#spellCheck",
            spellCheckTemp: '<h3>Did you mean: {{suggestion}}</h3>',
            searchQueryDisplay: '#searchQueryDisplay',
            searchQueryDisplayTemp: '<h3>Search results for {{query}} – {{numberOfProducts}}</h3>',
            sortContainerSelector: "#sortContainer",
            sortContainerType: "select",
            sortOptions: [
                { name: "Relevancy" },
                { name: "Price: High to Low", field: "price_max", order: "desc" },
                { name: "Price: Low to High", field: "price_min", order: "asc" }
            ],
            isPagination: true,
            paginationContainerSelector: "#paginationContainer",
            paginationTemp: [
                '{{#if hasPrev}}',
                '<span class="unbxd_prev" unbxdaction="prev">Previous</span>',
                '{{/if}}',
                '{{#pages}}',
                '{{#if current}}',
                '<span class="unbxd_page highlight">{{page}}</span>',
                '{{else}}',
                '<span class="unbxd_page" unbxdaction="{{page}}">{{page}}</span>',
                '{{/if}}',
                '{{/pages}}',
                '{{#if hasNext}}',
                '<span class="unbxd_next" unbxdaction="next">Next</span>',
                '{{/if}}'
            ].join(''),
            pageSize: 24,
            pageSizeContainerSelector: "#pageSizeContainer",
            pageSizeOptions: [
                { name: "12 items", value: "12" },
                { name: "24 items", value: "24" },
                { name: "48 items", value: "48" }
            ],
            pageSizeContainerType: "select"
        });
    </script>
</body>
</html>
```
