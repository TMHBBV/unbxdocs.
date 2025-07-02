---
title: Integrating Unbxd Browse
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The SDK lets you customize your page experience by leveraging various built-in features of Browse. You can also power any type of page, such as Category, Brand, or any other attribute.

Let’s see how the Browse Query can be composed and passed in browse() method invocation.

<br />

Using Browse Method\
Browse methods operate on Category fields query which is configured part of Browse Query.

Browse Methods has the following parts:

Browse Query\
Format
Start
Rows
Spellcheck
Analytics
Stats
Variants
Fields
Facets
Filtering
Multiple Filter
Sort
Browse Query
BrowseQuery consists of Category path or field details parameter Query with Category can be build as shown below:

`Using Field IDs`

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

<br />

`Using Field Names`

```
val categoryPath = CategoryNamePath(arrayOf("FA", "FA0484")) val browseQuery = BrowseQuery.Builder(categoryPath).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

`Using Page IDs`

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val browseQuery = BrowseQuery.Builder(categoryPath).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      { 
                                      Log.d("Client Response",json.toString())
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

`Using Page Names`

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val browseQuery = BrowseQuery.Builder(categoryPath).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

**Format**\
The format parameter specifies the format of the response. Possible values are:\* JSON \* XML.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val browseQuery = BrowseQuery.Builder(categoryPath). responseFormat(ResponseFormat.XML).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      { 
                                      Log.d("Client Response",json.toString())
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }                                     
)
```

> 📘 NOTE
>
> it is an optional parameter and the default value is ‘json’.

**Start**\
This parameter is used to offset the results by a specific number. It indicates offset in the complete result set of the products.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath).pageIndex(2).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

<br />

> 📘 NOTE: This is an optional parameter and the default value is 0.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath).rowsCount(20).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

> 📘 NOTE
>
> It is an optional parameter and the default value is 10, the maximum value is 100.

**Spellcheck**\
The spellcheck feature checks for misspelled search queries and recommends autocorrect suggestions.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath).spellCheck(true).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

**Analytics**\
The analytics parameter enables or disables tracking the query hit for analytics.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath).analytics(false).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

> 📘 NOTE
>
> By default, tracking is enabled.

**Stats**\
The stats parameter gives information about the products with highest and lowest field value.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath).showStatsForField("vPrice").build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

**Variants**\
This parameter enables or disables variants in the API response.It can take two values: TRUE or FALSE

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val variant = Variant(true, 2)  
val browseQuery = BrowseQuery.Builder(categoryPath).variant(variant).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

<br />

If you want to get more than one variants in the API response, you can use ‘variantCount’ parameter. It can have any numerical value (eg, 1,2,3, etc) or “.max” (to get all the variants).

**Fields**\
The fields parameter is used to specify the set of fields to be returned.When returning the results, only fields in the list will be included.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val variant = Variant(true, 2)  
val browseQuery = BrowseQuery.Builder(categoryPath).variant(variant).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

<br />

**Facets**\
Facets are the filters in the interface that allow shoppers to refine results based on product fields.

Facet option can have three values:

1. **Multilevel** :The facer multilevel parameter is used to enable multi-level facets in the API response.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val browseQuery = BrowseQuery.Builder(categoryPath). facet(MultiLevelFacet()).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client 
Response",json.toString())  
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

2. **Multiselect**: This feature enables or disables the option to select multiple values within a facet or across facets for shoppers.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val browseQuery = BrowseQuery.Builder(categoryPath). facet(MultiSelectFacet()).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      { 
                                      Log.d("Client Response",json.toString())
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

3. **Selected**

The selected facet parameter enables or disables the Selected Facets in the API response.Selected facet with field id and value id:

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val idFilter = IdFilter("76678", "5001")  
val browseQuery = BrowseQuery.Builder(categoryPath). facet(SelectedFacet(idFilter)).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

Selected facet with field name and value name:

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val nameFilter = NameFilter("Brand_uFilter", "Vince Camuto")  
val browseQuery = BrowseQuery.Builder(categoryPath).  
facet(SelectedFacet(nameFilter)).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

<br />

**Filtering**\
Filtering can be performed on fields using field Id or field Name.Three types of filters are supported:

1. Text

The text filter is used to filter products based on fields with string values such as color, gender, brand, etc. It can be defined in the API call in two ways:

* Using Field IDs: IdFilter can be formed with 2 parameters.field: The id of the field on which the text filter is applied. value: The id of the value on which the results are filtered.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val idFilter = IdFilter("76678", "5001")  
val browseQuery = BrowseQuery.Builder(categoryPath).filter(idFilter).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

* Using Field Names

  Again NameFilter can be formed with 2 parameters.

  **type**: The ID of the field on which the text filter is applied.

  **value**: The ID of the value on which the results are filtered

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val nameFilter = NameFilter("vColor_uFilter","Black")  
val browseQuery = BrowseQuery.Builder(categoryPath).filter(nameFilter).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

<br />

The range filter is used to filter products based on fields with datatypes – date, number or decimal. It can be defined in the API in two ways:

1. Using Field IDs

Filter Range of type id is built using IdFilterRange class and it can be initialized with below parameters.

field: The ID of the field on which the text filter is applied.

lower: The ID of the lower limit of the range.

upper: The ID of the upper limit of the range.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val idFilterRange = IdFilterRange("76678","2034", "8906")  
val browseQuery = BrowseQuery.Builder(categoryPath).filter(idFilterRange).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
override fun onFailure(errorMessage: String, exception: Exception)  
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

2. Using Field Names

Filter Range of type name is built using NameFilterRange class and it can be initialized with parameters:

field: The name of the field on which the text filter is applied.

lower: The name of the lower limit of the range.

upper: The name of the upper limit of the range.

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val nameFilterRange = NameFilterRange("vColor","red", "blue")  
val browseQuery = BrowseQuery.Builder(categoryPath). filter(nameFilterRange).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

**Multilevel**

The multilevel filter is used to filter products based on categories.The API call can be defined in two ways:

* Using Field IDs

“CategoryIdFilter” is used to filter the results using category path comprised of category IDs

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val categoryIdFilter = CategoryIdFilter(ReferenceType.TypeId, arrayOf("BC", "B0485"))  
val browseQuery = BrowseQuery.Builder(categoryPath). categoryFilter(categoryIdFilter).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

* Using Field Names\
  “CategoryNameFilter” is used to filter the results using category path comprised of category Names

```
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val categoryNameFilter = CategoryNameFilter(ReferenceType.TypeName, arrayOf("Fashion", "Shirts")) val browseQuery = BrowseQuery.Builder(categoryPath). categoryFilter(categoryNameFilter).build() client.browse(browseQuery, object : ICompletionHandler { override fun onSuccess(json: JSONObject, response: Response) { Log.d("Client Response",json.toString()) } override fun onFailure(errorMessage: String, exception: Exception) { Log.d("Client Response",errorMessage) } } ) val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val categoryNameFilter = CategoryNameFilter(ReferenceType.TypeName, arrayOf("Fashion", "Shirts")) val browseQuery = BrowseQuery.Builder(categoryPath). categoryFilter(categoryNameFilter).build() client.browse(browseQuery, object : ICompletionHandler { override fun onSuccess(json: JSONObject, response: Response) { Log.d("Client Response",json.toString()) } override fun onFailure(errorMessage: String, exception: Exception) { Log.d("Client Response",errorMessage) } } )
```

<br />

**Multiple Filters**\
There are two types of filter operations: AND, OR

1. And

* Using Field IDs

MultipleIdFilter takes 2 parameters, field Id and value id. Multiple filters can be added and ‘operatorType’ is set to ‘AND’.

```
var idFilters = ArrayList() idFilters.add(IdFilter("76678", "5001")) idFilters.add(IdFilter("76678", "5021"))  
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath). multipleFilter(MultipleIdFilter(idFilters, FilterOperatorType.AND)).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

* Using Field Names\
  MultipleNameFilter takes 2 parameters, field name and value name. Multiple filters can be added and ‘operatorType’ is set to ‘AND’.

```
var nameFilters = ArrayList() nameFilters.add(NameFilter("vColor_uFilter", "Black")) nameFilters.add(NameFilter("vColor_uFilter", "White"))  
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath). multipleFilter(MultipleIdFilter(nameFilters, FilterOperatorType.AND)).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      { 
                                      Log.d("Client Response",json.toString())
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception)                                       
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

<br />

**OR**

* Using Field IDs

MultipleIdFilter is takes 2 parameter, field Id and value id. Multiple filters can be added and ‘operatorType’ is set to ‘OR’.

```
var idFilters = ArrayList() idFilters.add(IdFilter("76678", "5001")) idFilters.add(IdFilter("76678", "5021"))  
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath). multipleFilter(MultipleIdFilter(idFilters, FilterOperatorType.OR)).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

* Using Field Names\
  MultipleNameFilter takes 2 parameters, field name and value name. Multiple filters can be added and ‘operatorType’ is set to ‘OR’.

```
var nameFilters = ArrayList() nameFilters.add(NameFilter("vColor_uFilter", "Black")) nameFilters.add(NameFilter("vColor_uFilter", "White"))  
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484"))  
val browseQuery = BrowseQuery.Builder(categoryPath). multipleFilter(MultipleIdFilter(nameFilters, FilterOperatorType.OR)).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

**Sort**\
The sort parameter is used to rank the products based on specified fields in the specified order.Sort can be done on a single field or multiple fields.

Single Field\
fieldName: The field on which the sort is applied.sortOrder: The order in which the sort is applied. This value can be “ASC” (forascending) or “DSC” (for descending)

```
var fieldsOrder = ArrayList() fieldsOrder.add(FieldSortOrder("vPrice", SortOrder.ASC))  
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val browseQuery = BrowseQuery.Builder(categoryPath). fieldsSortOrder(fieldsOrder).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      Log.d("Client Response",json.toString()) 
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception)                                       
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

**Multiple Fields**\
Here 2 or more FieldSortOrder instances are added.

```
var fieldsOrder = ArrayList() fieldsOrder.add(FieldSortOrder("vPrice", SortOrder.ASC)) fieldsOrder.add(FieldSortOrder("title", SortOrder.DSC))  
val categoryPath = CategoryIdPath(arrayOf("FA", "FA0484")) val browseQuery = BrowseQuery.Builder(categoryPath). fieldsSortOrder(fieldsOrder).build()  
client.browse(browseQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
Log.d("Client Response",json.toString())  
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```