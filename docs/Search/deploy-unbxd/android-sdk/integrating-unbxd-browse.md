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