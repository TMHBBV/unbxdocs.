---
title: Browse
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The SDK lets you customize your page experience by leveraging various built-in features of Browse. You can also power any type of page, such as Category, Brand, or any other attribute.

## Using Browse Method

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

##