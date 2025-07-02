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