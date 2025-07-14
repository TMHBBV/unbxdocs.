---
title: Commerce Search
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Unbxd Site Search is an e-commerce search platform that enhances your on-site search to deliver fast, relevant, and tailored search results to visitors on your website/mobile application. Unbxd Site Search is platform-agnostic, which makes it incredibly versatile and easily implementable.

For more information, see [here](https://unbxd.com/docs).

### Using Search Method

Search methods perform a search with key and a few other parameters. The search key is the mandatory argument and rest is applied for different criteria.

Query method signature:

```swift
init(key: String, rows: Int? = nil, start: Int? = nil, format: ResponseFormat = .JSON, spellCheck: Bool = false, analytics: Bool = true, statsField: String? = nil, variant: Variant? = nil, fields: Array? = nil, facet: Facet? = nil, filter: FilterAbstract? = nil, categoryFilter: CategoryFilterAbstract? = nil, multipleFilter: MultipleFilterAbstract? = nil, fieldsSortOrder: Array? = nil, personalization: Bool? = nil)
```

Search method signature:

```swift
func search(query: SearchQuery, completion: @escaping (_ response: Dictionary<String, Any>?, _ httpResponse: HTTPURLResponse?, _ error: Error?) -> Void) {  
    // Handle response or request
}
```

Keywords marked in bold are different arguments for the search method. ‘query’ of type ‘SearchQuery’ is mandatory argument and rest are optional which are used as needed. SearchQuery consists of searchKey parameter with a few other parameters. Let’s see how these arguments can be composed and passed in search() method invocation.

#### Search Query

SearchQuery consists of a searchKey parameter with other parameters. Invoking Search method with key:

```swift
let query = SearchQuery(key: "Shirt")
client.search(query: query, completion: { (response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Format

The format parameter specifies the format of the response. Possible values are ‘JSON’ or ‘XML’. It is an optional parameter and the default value is ‘JSON’.

```swift
let query = SearchQuery(key: "Shirt", format: .XML)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Start

The start parameter is used to offset the results by a specific number. It indicates offset in the complete result set of the products. It is an optional parameter and the default value is 0.

```swift
let query = SearchQuery(key: "Shirt", start: 2, format: .JSON)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Rows

The rows parameter is used to paginate the results of a query. It indicates the number of products on a single page. It is an optional parameter and the default value is 10, the maximum value is 100.

```swift
let query = SearchQuery(key: "Shirt", rows: 20)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Spellcheck

The spellcheck feature provides spelling suggestions or spell-checks for misspelled search queries.

```swift
let query = SearchQuery(key: "Shirt", spellCheck: true)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Analytics

The analytics parameter enables or disables tracking the query hit for analytics. By default, tracking is enabled.

```swift
let query = SearchQuery(key: "Shirt", analytics: false)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Stats

The stats parameter gives information about the products with the highest and lowest field value.

```swift
let query = SearchQuery(key: "Shirt", statsField: "price")
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Variants

Products in the feed can be available in different sizes, colors, styles, materials, etc. For example, a dress can be available in different sizes, colors and/or styles.

```
Variant 1: Color – Blue, Size: Small, Style – Solid print
Variant 2: Color – Red, Size: Small, Style – Solid print
Variant 3: Color – Blue, Size: Large, Style – Polka-dot
```

Variants parameter enables or disables variants in the API response. It can take two values: “true” or “false”. Default value is “false”.

Examples:

```json
{
    "feed": {
        "catalog": {
            "schema": [{
                "fieldName": "vColor",
                "id": "76678",
                "dataType": "text",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }, {
                "fieldName": "vSize",
                "dataType": "text",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }, {
                "fieldName": "vImages",
                "dataType": "link",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }, {
                "fieldName": "vPrice",
                "dataType": "decimal",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }]
        }
    }
}
```

Example: Search with variants:

Variants parameter enables or disables variants in the API response. It can take two values: “true” or “false”. Default value is “false”.

```swift
let query = SearchQuery(key: "Shirt", variant: Variant(has: true, count: 2))  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If you want to get more than one variants in the API response, you can use variantCount parameter. It can have any numerical value (for example, 1, 2, 3, etc) or “.max” (to get all the variants).

#### Fields

The fields parameter is used to specify the set of fields to be returned as the response, otherwise, all the fields will be returned in the response by default.

For more information, see [here](https://unbxd.com/docs) (Request Parameters section).

Example: Search:

The fields parameter is used to specify the set of fields to be returned. When returning the results, only fields in the list will be included.

```swift
let query = SearchQuery(key: "Shirt", fields: ["title","vPrice"])
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Facets

Facets are filters in the UI that allow visitors to narrow down result set based on product fields. It is usually known as Layered Navigation or Guided Navigation. Facets can be easily configured from the SDK.

Facets can be of three types:

* **Multi-level**: Facets on categories. For a given API response, multi-level facets would represent the top-most categories those products lie under.
* **Text**: Facets on text fields in the feed. For example, color, brand, etc.
* **Range**: Facets on numeric fields in the feed. For example, price, discount, etc.

Example: Search with multi-level Facets:

```swift
let query = SearchQuery(key: "Shirt", facet: .MultiLevel)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

Example: Search with multi-select Facets:

This feature enables or disables the option to select multiple values within a facet or across facets for visitors. For example, for a query “red dress”, facets of gender and size fields are displayed. If the value for facet.mult is selected is set as true and if a visitor selects Women in the Gender Facet, the search results will be refined according to the selection. However, all values in the gender facet will still be sent in the response as if the gender filter isn’t applied (and other filters are applied, if any).

```swift
let query = SearchQuery(key: "Shirt", facet: .MultiSelect)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

Example: Search with the selected facet with field ID and value ID:

```swift
let query = SearchQuery(key: "Shirt", facet: .Selected(IdFilter(field: "76678", value: "5001")))
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

Selected facet with field name and value name:

```swift
let query = SearchQuery(key: "Shirt", facet: .Selected(NameFilter(field: "Brand_uFilter", value: "Vince Camuto")))
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Filtering

A filter is used to restrict the products based on criteria passed. Three types of filters are supported:

* **Text**: It is used to filter products based on fields with string values such as color, gender, brand, etc. It can be defined in the API call in two ways:

  **Using Field Ids**:

  `IdFilter` can be formed with 2 parameters.

  ```swift
  field: The id of the field on which the text filter is applied.
  value: The id of the value on which the results are filtered.
  ```

  Example:

  ```swift
  let query = SearchQuery(key: "Shirt", filter: IdFilter(field: "76678", value: "5001"))
  client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
      //Handle response
  })
  ```

  **Using Field Names**:

  `NameFilter` can be formed with 2 parameters.

  ```swift
  type: The id of the field on which the text filter is applied.
  value: The id of the value on which the results are filtered.
  ```

  ```swift
  let query = SearchQuery(key: "Shirt", filter: NameFilter(field: "vColor_uFilter", value: "Black"))
  client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
      //Handle response
  })
  ```

* **Range**: It is used to filter products based on fields with data types – date, number or decimal. It can be defined in the API in two ways:

  **Using Field Names**:

  Filter Range of type id is built using `IdFilterRange` class and it can be initialized with below parameters.

  ```swift
  field: The id of the field on which the text filter is applied.
  lower: The id of the lower limit of the range.
  upper: The id of the upper limit of the range.
  ```

  Example:

  ```swift
  let query = SearchQuery(key: "Shirt", filter: IdFilterRange(field: "76678", lower: "2034", upper: "8906"))
  client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
      //Handle response
  })
  ```

  **Using Field Name**:

  Filter Range of type name is built using `NameFilterRange` class and it can be initialized with below parameters.

  ```swift
  field: The name of the field on which the text filter is applied.
  lower: The name of the lower limit of the range.
  upper: The name of the upper limit of the range.
  ```

  Example:

  ```swift
  let query = SearchQuery(key: "Shirt", filter: NameFilterRange(field: "vColor", lower: "red", upper: "blue"))
  client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
      //Handle response
  })
  ```

* **Multilevel**: It is used to filter products based on categories.

Each of the three filters can filter on field-name and field-id. Field-id/field-name is an optional parameter. If passed, it eliminates those products that do not match the criteria.

**NOTE**: If IDs are present in the feed, filtering should be done on IDs only.

The multilevel filter is used to filter products based on categories. It can be defined in the API call in two ways:

**Using Field Ids**:

`CategoryIdFilter` is used to filter the results using category path comprised of category IDs.

Example:

```swift
let categoryNameFilter = CategoryNameFilter()  
categoryNameFilter.categories.append("Fashion")  
categoryNameFilter.categories.append("Shirts")
let query = SearchQuery(key: "Shirt", categoryFilter: categoryNameFilter)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Search with Multiple Filters using Field ID/Field Name

Multiple Filters: Multiple facets can be selected, which applies corresponding filters in a single call. There are two types of filter operations:

* AND
* OR

**Search with multiple filters using AND and field ID/field name**:

`MultipleIdFilter` takes two parameters, fieldType Id and fieldValue id.

`MultipleNameFilter` takes two parameters, fieldType name, and fieldValue name.

Multiple filters can be added and `operatorType` is set to ‘AND’.

```swift
// Using field ID
let multipleIdFilter = MultipleIdFilter.init()
multipleIdFilter.operatorType = .AND
multipleIdFilter.filters.append(IdFilter.init(withFieldType: "76678", fieldValue: "5001"))
multipleIdFilter.filters.append(IdFilter.init(withFieldType: "76678", fieldValue: "5021"))
client?.searchWithQuery(query: searchQuery, multipleFilter: multipleIdFilter, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response 
})
```

OR

```swift
// Using field name
let multipleNameFilter = MultipleNameFilter.init()
multipleNameFilter.operatorType = .AND
multipleNameFilter.filters.append(NameFilter.init(withFieldType: "vColor_uFilter", fieldValue: "Black"))
multipleNameFilter.filters.append(NameFilter.init(withFieldType: "vColor_uFilter", fieldValue: "White"))  
client?.searchWithQuery(query: searchQuery, multipleFilter: multipleNameFilter, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response 
})
```

**Search with multiple filters using OR and field ID/field name**:

`MultipleIdFilter` takes two parameters, fieldType Id and fieldValue id.

`MultipleNameFilter` takes two parameters, fieldType name, and fieldValue name.

Multiple filters can be added and `operatorType` is set to ‘OR’.

```swift
// Using field ID
let multipleIdFilter = MultipleIdFilter()  
multipleIdFilter.operatorType = .OR  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5001"))  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5021"))  
let query = SearchQuery(key: "Shirt", multipleFilter: multipleIdFilter)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})    
```

OR

```swift
// Using field name
let multipleNameFilter = MultipleNameFilter()  
multipleNameFilter.operatorType = .OR  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "Black"))  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "White"))  
let query = SearchQuery(key: "Shirt", multipleFilter: multipleIdFilter)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Sorting

The sort parameter is used to rank the products based on specified fields in the specified order. You can sort on a single field or in multiple fields.

**Search with sorting on the single field/multiple fields**:

* **fieldName**: The field on which the sort is applied.
* **sortOrder**: The order in which the sort is applied. This value can be “ASC” (for ascending) or “DSC” (for descending).

```swift
// single field
var fieldsWithOrder = Array()  
fieldsWithOrder.append(FieldSortOrder(field: "price", order: .ASC))  
let query = SearchQuery(key: "Shirt", fieldsSortOrder: fieldsWithOrder)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// multiple fields hence 2 or more FieldSortOrder instances are added
var fieldsWithOrder = Array()  
fieldsWithOrder.append(FieldSortOrder(field: "price", order: .ASC))  
fieldsWithOrder.append(FieldSortOrder(field: "title", order: .DSC))  
let query = SearchQuery(key: "Shirt", fieldsSortOrder: fieldsWithOrder)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Spellcheck

The spellcheck feature provides spelling suggestions or spell-checks for misspelled search queries. In such cases, the context-aware algorithm of Unbxd understands your visitor’s intent and sends a “Did You Mean” response along with search result set for the query, if any.

```swift
let query = SearchQuery(key: "Shirt", spellCheck: true)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

<br />

```swift
// Using Field Name
let nameRange = NameFilterRange(field: "vColor", lower: "red", upper: "blue")  
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypeKeywordSuggestions(resultsCount: 4), filter: nameRange)  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

## Unbxd Browse

The SDK lets you customize your page experience by leveraging various built-in features of Browse. You can also power any type of page, such as Category, Brand, or any other attribute.

### Using Browse Method

Browse methods operate on Category fields query which is configured part of Browse Query.

Query method signature:

```swift
init(categoryQuery: CategoryAbstract, rows: Int? = nil, start: Int? = nil, format: ResponseFormat = .JSON, spellCheck: Bool = false, analytics: Bool = false, statsField: String? = nil, variant: Variant? = nil, fields: Array? = nil, facet: Facet = .None, filter: FilterAbstract? = nil, categoryFilter: CategoryFilterAbstract? = nil, multipleFilter: MultipleFilterAbstract? = nil, fieldsSortOrder: Array? = nil)
```

Browse method signature:

```swift
func browse(query: BrowseQuery, completion: @escaping (_ response: Any?, _ error: Error?) -> Void)
```

#### Browse with Page Name/Page ID

`BrowseQuery` consists of Category path or field details parameter and few other optional parameters.

It is mandatory to pass either page name or page ID. If both are passed together, page name would be ignored and results would be shown as per page ID. The value passed under page ID (or page name) is displayed in the Unbxd Console and analytics reports as-it-is.

```swift
// With Page name
let categoryQuery = CategoryIdPath(withCategories: ["Fashion","Shoes","Sneakers","Athletic shoes"])  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// With Page ID                        
let categoryQuery = CategoryIdPath(withCategories: ["FA","FA0484"])  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// With Field ID    
let categoryQuery = CategoryIdPath(withCategories: ["FA","FA0484"])  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// With Field name
let categoryQuery = CategoryNameFields(field: "vColor", value: "Black")  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Example: Browse with Variants

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, variant: Variant(has: true, count: 2))
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If you want to get more than one variants in the API response, you can use the `Count` parameter. It can have any numerical value (for example, 1, 2, 3, etc) or “.max” (to get all the variants).

#### Fields

The fields parameter is used to specify the set of fields to be returned as the response, otherwise, all the fields will be returned in the response by default.

**Browse with selected fields**:

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, fields: ["title","vPrice"])
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Facets

Facets are the filters in the UI that allow visitors to narrow down result set based on product fields. It is usually known as Layered Navigation or Guided Navigation. Facets can be easily configured from the **Manage -> Configure Browse -> Configure Facet** section of the Console.

Facets can be of three types:

* **Multi-level**: Facets on categories. For a given API response, multi-level facets would represent the top-most categories those products lie under.
* **Text**: Facets on text fields in the feed. For example, color, brand, etc.
* **Range**: Facets on numeric fields in the feed. For example, price, discount, etc.

**Browse with multi-level facets**:

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, facet: .MultiLevel)
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with multi-select facets**:

This feature enables or disables the option to select multiple values within a facet or across facets for visitors.

For example, for a query “red dress”, facets of gender and size fields are displayed. If the value for `facet.multiselect` is set as true and if a visitor selects Women in the Gender facet, the Browse results will be refined according to the selection. However, all values in the gender facet will still be sent in the response as if the gender filter isn’t applied (and other filters are applied, if any).

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, facet: .MultiSelect)
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with the selected facet with field ID and value ID**:

```swift
// With Field ID, Value ID
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, facet: .Selected(IdFilter(field: "76678", value: "5001")))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// With Field Name, Value Name
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, facet: .Selected(NameFilter(field: "Brand_uFilter", value: "Vince Camuto")))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Filtering

A filter is used to restrict the products based on criteria passed. Three types of filters are supported:

* **Text**: It is used to filter products based on fields with string values such as color, gender, brand, etc.
* **Range**: It is used to filter products based on fields with data types – date, number or decimal.
* **Multilevel**: It is used to filter products based on categories.

Each of the three filters can filter on field-name and field-id. Field-id/field-name is an optional parameter. If passed, it eliminates those products that do not match the criteria.

**NOTE**: If IDs are present in the feed, filtering should be done on IDs only.

**Browse with text filter using field ID/field name**:

“filter-id” is used to filter the results using field-id. Using Field IDs, ‘IdFilter’ can be formed with two parameters:

* **Field**: The id/name of the field on which the text filter is applied.
* **Value**: The id/name of the value on which the results are filtered.

```swift
// Using field ID
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, filter: IdFilter(field: "76678", value: "5001"))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// Using field name
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, filter: NameFilter(field: "vColor_uFilter", value: "Black"))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with Range filter using field ID/field name**:

Range filter is built using `FilterIdRange` class and it can be initialized with parameters below.

* **field**: The id/name of the field on which the text filter is applied.
* **lower**: The id of the lower limit of the range.
* **upper**: The id of the upper limit of the range.

```swift
// Using field ID
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, filter: IdFilter(field: "76678", value: "5001"))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// Using field name
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, filter: NameFilter(field: "vColor_uFilter", value: "Black"))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with Multi-level filter using field ID/field name**:

`CategoryIdFilter` is used to filter the results using a category path comprised of category IDs.

`CategoryNameFilter` is used to filter the results using a category path comprised of category Names.

```swift
// Using field ID
let categoryIdFilter = CategoryIdFilter()  
categoryIdFilter.categories.append("FA")  
categoryIdFilter.categories.append("A0485")  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, categoryFilter: categoryIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// Using field name
let categoryNameFilter = CategoryNameFilter()  
categoryNameFilter.categories.append("Fashion")  
categoryNameFilter.categories.append("Shirts")  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, categoryFilter: categoryNameFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
}) 
```

**Browse with Multiple filters using field ID/field name**:

Multiple Filters: Multiple facets can be selected which applies corresponding filters in a single call. There are two types of filter operations:

* AND
* OR

**Browse with multiple filters using AND and field ID/field name**:

`MultipleIdFilter` takes two parameters, field Id and Value id.

`MultipleNameFilter` takes two parameters, field name and Value name.

Multiple filters can be added and `operatorType` is set to ‘AND’.

```swift
// Using field ID
let multipleIdFilter = MultipleIdFilter()  
multipleIdFilter.operatorType = .AND  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5001"))  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5021"))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, multipleFilter: multipleIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})    
```

OR

```swift
// Using field name
let multipleNameFilter = MultipleNameFilter()  
multipleNameFilter.operatorType = .AND  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "Black"))  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "White"))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, multipleFilter: multipleIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with multiple filters using OR and field ID/field name**:

`MultipleIdFilter` takes two parameters, field Id and Value id.

`MultipleNameFilter` takes two parameters, field name and Value name.

Multiple filters can be added and `operatorType` is set to ‘OR’.

```swift
// Using field ID
let multipleIdFilter = MultipleIdFilter()  
multipleIdFilter.operatorType = .OR  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5001"))  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5021"))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, multipleFilter: multipleIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})    
```

OR

```swift
// Using field name
let multipleNameFilter = MultipleNameFilter()  
multipleNameFilter.operatorType = .OR  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "Black"))  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "White"))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, multipleFilter: multipleIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Sorting

The sort parameter is used to rank the products based on specified fields in the specified order. You can sort on a single field or in multiple fields.

For more information, see [here](https://unbxd.com/docs) (Request Parameters section).

**Browse with sorting on the single field/multiple fields**:

* **field**: The field on which the sort is applied.
* **Order**: The order in which the sort is applied. This value can be “ASC” (for ascending) or “DSC” (for descending).

```swift
// single field
var fieldsWithOrder = Array()  
fieldsWithOrder.append(FieldSortOrder(field: "price", order: .ASC))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, fieldsSortOrder: fieldsWithOrder)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// multiple fields hence 2 or more FieldSortOrder instances are added
var fieldsWithOrder = Array()  
fieldsWithOrder.append(FieldSortOrder(field: "price", order: .ASC))  
fieldsWithOrder.append(FieldSortOrder(field: "title", order: .DSC))
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, fieldsSortOrder: fieldsWithOrder)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Spellcheck

The spellcheck feature provides spelling suggestions or spell-check for misspelled Browse queries. In such cases, the context-aware algorithm of Unbxd understands your visitor’s intent and sends a “Did You Mean” response along with Browse result set for the query, if any.

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, spellCheck: true)
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

## Unbxd Recommendations

Unbxd Recommendations is a set of tailored widgets that showcase personalized product suggestions to visitors on different pages of your online e-commerce store. The widgets are easy to configure and provides a smart way of exposing your inventory to the visitors. These widgets are powered by the Unbxd analytics engine that constantly tracks and records visitor events on your store such as clicks, cart additions, orders, etc. The captured event information is used to build profiles that help our search engine to fetch relevant products for each widget.

The Unbxd SDK supports the following types of widgets:

* Recommended For You
* Recently Viewed
* More Like This
* Viewed also Viewed
* Bought also Bought
* Cart Recommendations
* Top Sellers
* Homepage Top Sellers
* Category Top Sellers
* PDP Top Sellers
* Brand Top Sellers
* Complete the Look

Recommendations method signature:

```swift
func recommend(recommendationQuery: RecommendationQuery, completion: @escaping (_ response: Any?, _ error: Error?) -> Void) {  
    // Handle response or request
}
```

### Examples

**RECOMMENDED FOR YOU**: The Recommended For You method returns recommendations based on the visitor’s interaction history on the online store or app.

Sample:

```swift
let forYouQuery = RecommendedForYourRecomendations(uid: uid, region: "USA", currency: "USD", format: .JSON)  
client.recommend(recommendationQuery: forYouQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**RECENTLY VIEWED**:

The Recently Viewed method recommends products that were recently viewed by a visitor.

Sample:

```swift
let recentlyViewedQuery = RecentlyViewedRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: recentlyViewedQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**MORE LIKE THESE**:

The More Like This method is built to recommend products similar to the one being viewed on the PDP (Product Detail Page).

Sample:

```swift
let moreLikeThisQuery = MoreLikeThisRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: moreLikeThisQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**VIEWED ALSO VIEWED**:

As the name suggests, this method recommends products viewed by other visitors.

Sample:

```swift
let alsoViewedQuery = ViewedAlsoViewedRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: alsoViewedQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**BOUGHT ALSO BOUGHT**:

Similar to the Viewed also Viewed method, the Bought also Bought method recommends products bought by other visitors.

Sample:

```swift
let alsoBoughtdQuery = BoughtAlsoBoughtRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: alsoBoughtdQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**CART RECOMMENDATIONS**: This method recommends complementary products on the “Cart page” for those present in the visitor’s cart.

Sample:

```swift
let cartRecommendationQuery = CartRecomendations(uid: uid, region: "USA")
client.recommend(recommendationQuery: cartRecommendationQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**HOMEPAGE TOP SELLERS**:

This method recommends top selling products bought from the homepage.

Sample:

```swift
let homePageTopSellerQuery = HomePageTopSellersRecomendations(uid: uid, region: "USA")  
client.recommend(recommendationQuery: homePageTopSellerQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**CATEGORY TOP SELLERS**:

This method recommends top selling products from a specific category.

Sample:

```swift
let categoryTopSellerQuery = CategoryTopSellersRecomendations(uid: uid, region: "USA", categoryName: "")  
client.recommend(recommendationQuery: categoryTopSellerQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**TOP SELLERS**:

This method recommends top selling products from a specific product.

Sample:

```swift
let pdpTopSellerQuery = PDPTopSellersRecomendations(uid: uid, region: "USA")  
client.recommend(recommendationQuery: pdpTopSellerQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**BRAND TOP SELLERS**:

This method recommends top selling products from a specific brand.

Sample:

```swift
let brandTopSellerQuery = BrandTopSellersRecomendations(uid: uid, region: "USA", brandName: "Nike")  
client.recommend(recommendationQuery: brandTopSellerQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**COMPLETE THE LOOK**:

The Complete the Look method showcases curated products on a Product Display Page (PDP) that are usually associated with the original product.

Sample:

```swift
let completeTheLookQuery = CompleteTheLookRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: completeTheLookQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

## Sample iOS App

Please find the link to sample iOS App:

* **Fashion vertical**: [https://github.com/unbxd/FashionApp](https://github.com/unbxd/FashionApp)
* **Home Decor App**: [https://github.com/unbxd/HomeDecorApp](https://github.com/unbxd/HomeDecorApp)