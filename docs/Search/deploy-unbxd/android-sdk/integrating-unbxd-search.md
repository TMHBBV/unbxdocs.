---
title: 'Integrating Unbxd Search '
deprecated: false
hidden: false
metadata:
  robots: index
---
Unbxd Site Search is an e-commerce search platform that enhances your on-site search to deliver fast, relevant, and tailored search results to visitors on your website/mobile application. Unbxd Site Search is platform-agnostic, which makes it incredibly versatile and easily implementable.

## Using Analytics Method

Search methods in the SDK are used to integrate UNBXD search in your Android App.

```Text Search Method Signature 
fun search(query: SearchQuery, completion: ICompletionHandler) {...} 
```

Let’s see how these arguments can be composed and passed in search () method invocation.

Different arguments that can be passed with the search method are:

* SearchQuery
* Format
* Start
* Rows
* Spellcheck
* Analytics
* stats
* Variants
* Field
* Facets
* Filtering
* Multiple Filters
* Sort

## Search Query

```Text Koltin
val searchQuery = SearchQuery.Builder("Shirt").facet(MultiLevelFacet()).build()  
client.search(searchQuery, object : ICompletionHandler  
                                       {
                                       override fun onSuccess(json: JSONObject, response: Response) 
                                       {
                                       //Handle success 
                                       }
                                       override fun onFailure(errorMessage: String, exception: Exception) 
                                       { 
                                       //Handle failure
                                       } 
                                       }
)
```
```java
SearchQuery search query = new
SearchQuery.Builder(shirt).build();
client.search(searchQuery, new
CompletionHandler() {
@Override
public void onSuccess(@NotNull
JSONObject json object, @NotNull Response
response) {
}
@Override
public void onFailure(@NotNull String s,
@NotNull Exception e) {
});
```

<br />

## Formats

The format parameter specifies the format of the response. Possible values are ‘JSON’ or ‘XML’.

> 👍 Tips
>
> This is an optional parameter. The default value is ‘JSON’.

```Text Kotlin
val searchQuery = SearchQuery.Builder("Shirt").facet(MultiLevelFacet()).build()  
client.search(searchQuery, object : ICompletionHandler  
                                       {
                                       override fun onSuccess(json: JSONObject, response: Response) 
                                       {
                                       //Handle success 
                                       }
                                       override fun onFailure(errorMessage: String, exception: Exception) 
                                       { 
                                       //Handle failure
                                       } 
                                       }
)
```
```Text Java
SearchQuery search query = new
SearchQuery.Builder(shirt).responseFormat(Resp
onseFormat.JSON).build();
client.search(searchQuery, new
CompletionHandler() {
@Override
public void onSuccess(@NotNull
JSONObject json object, @NotNull Response
response) {
}
@Override
public void onFailure(@NotNull String s,
@NotNull Exception e) {
}
});.         
```

## Start

The start parameter is used to offset the results by a specific number. It indicates an offset in the complete result set of the products. For instance, if there are 10 products in the search results page, and the offset is set at 5, then the results page will not list the first five products.

> 👍 Tips
>
> This is an optional parameter, and the default value is 0.

```Text Kotlin
val searchQuery = SearchQuery.Builder("Shirt").start(2).build() client.search(searchQuery, object : ICompletionHandler {  
override fun onSuccess(json: JSONObject, response: Response)  
                  {
                   //Handle success
                   override fun onFailure(errorMessage: String, exception: Exception)  
                  { //Handle failure
                  } 
                  }
)
```
```java
SearchQuery search query = new
SearchQuery.Builder(shirt).responseFormat(Resp
onseFormat.JSON).build();
client.search(searchQuery, new
CompletionHandler() {
@Override
public void onSuccess(@NotNull
JSONObject json object, @NotNull Response
response) {
}
@Override
public void onFailure(@NotNull String s,
@NotNull Exception e) {
}
});.         
```

## Rows

The rows parameter is used to paginate the results of a query. It indicates the number of products on a single page. It is an optional parameter, and the default value is 10; the maximum value is 100.

> 👍 Tips
>
> This is an optional parameter. The default value is 10, and the Permitted range is 1 - 100.

```Text Kotlin
val searchQuery = SearchQuery.Builder("Shirt").rows(20).build() client.search(searchQuery, object : ICompletionHandler {  
override fun onSuccess(json: JSONObject, response: Response)  
                                         {
                                          //Handle success 
                                         }
                                           override fun onFailure(errorMessage: String, exception: Exception) 
                                       { 
                                         //Handle failure
                                       } 
                                       }
)
```
```Text Java
SearchQuery search query = new
SearchQuery.Builder(shirt).rows(10).build();
client.search(searchQuery, new
ICompletionHandler() {
@Override
public void onSuccess(@NotNull
JSONObject jsonObject, @NotNull Response
response) {
}
@Override
public void onFailure(@NotNull String s,
@NotNull Exception e) {
}
});
```

<br />

## Spellcheck

The spellcheck feature provides spelling suggestions or spell-checks for misspelled search queries.

```Text Kotlin
val searchQuery = SearchQuery.Builder("Shirt").spellCheck(true).build() client.search(searchQuery, object : ICompletionHandler  
                                       {
                                       override fun onSuccess(json: JSONObject, response: Response) { //Handle success
                                       }
                                       override fun onFailure(errorMessage: String, exception: Exception) 
                                       { 
                                       //Handle failure
                                       } 
                                       }
)
```
```java
SearchQuery searchQuery = new Search query.B
uilder(shirt).spellCheck(true).build();
client.search(searchQuery, new
CompletionHandler() {
@Override
public void onSuccess(@NotNull
JSONObject jsonObject, @NotNull Response
response) {
}
@Override
public void onFailure(@NotNull String s,
@NotNull Exception e) {
}
});
```