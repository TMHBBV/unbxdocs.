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

<br />

## Analytics

This parameter allows you to enable or disable analytics tracking of the site search event.

> 👍 Tips
>
> This is an optional Parameter. By default, tracking is enabled.

```Text sample
val searchQuery = SearchQuery.Builder("Shirt").analytics(false).build() client.search(searchQuery, object : ICompletionHandler  
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

## Stats

This parameter provides information about all your catalog products with the highest and lowest field values.

```Text Sample
val searchQuery = SearchQuery.Builder("Shirt").showStatsForField("vPrice").build()  
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

<br />

## Variants

Products in the feed can be available in different sizes, colors, styles, materials, etc. For example, a dress can be available in different sizes, colors and/or styles.

* Variant 1:\
  Color – Blue,
  Size: Small,
  Style – Solid print
* Variant 2:\
  Color – Red,
  Size: Small,
  Style – Solid print
* Variant 3:\
  Color – Blue
  Size: Large
  Style – Polka-dot

The variants parameter enables or disables variants in the API response. It can take two values: “true” or “false”. The default value is “false”.

The variants parameter enables or disables variants in the API response. Variants have two values: True or False.

```Text Kotlin
val variant = Variant(true, 2)  
val searchQuery = SearchQuery.Builder("Shirt").variant(variant).build()  
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
Variant variant = new Variant(true, 20);
SearchQuery search query = new SearchQuery.Bu
ilder(shirt).variant(variant).build();
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
});
```

<br />

> 📘 NOTE
>
> Default value is “false”.

If you want to get multiple variants in the API response, you can use the ‘variantCount’ parameter. The variantCount parameter can have any numerical value (eg, 1,2,3, etc).

## Fields

The fields parameter is used to specify the set of fields to be returned as the response, otherwise, all the fields will be returned by default.

```Text Kotlin 
val searchQuery = SearchQuery.Builder("Shirt").fields(arrayOf("title","vPrice")).build()  
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
String fields[]= {"title","VPrice");
SearchQuery search query = new
SearchQuery.Builder(shirt).fields(fields).build();
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

Here in this example, only `Title` and `Price` of the product would be returned in the response, as opposed to all the fields.

## Facets

Facets are filters in the UI that allow visitors to narrow down result set based on product fields. It is usually known as Layered Navigation or Guided Navigation.Facets can be easily configured from the Manage -> Configure Search -> Configure Facet section of the Console.

Facets can be of three types:

* Multi-level: Facets on categories. For a given API response, multi-level facets would represent the top-most categories those products lie under.
* Text: Facets on text fields in the feed. For example, color, brand, etc.
* Range: Facets on numeric fields in the feed. For example, price, discount, etc.

### Multilevel

The MultiLevelFacet() parameter enables the Multi-level facet in the API in the search response.

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
IdFilter idFilter =new IdFilter("76678"
, "5001");
SearchQuery searchQuery = new
SearchQuery.Builder(shirt).facet(new
MultilevelFacet().build();
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
});
```

### Selected

This feature enables or disables the option to select multiple values within a facet or across facets for visitors.

```Text Kotlin
//Selected facet with fieldId and valueId
val idFilter = IdFilter("76678", "5001")  
val searchQuery = SearchQuery.Builder("Shirt").facet(SelectedFacet(idFilter)).build()  
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
String idFilterſ]={"FA", "A0485"};
CategoryldFilter categoryFilter =new
CategoryIdFilter(ReferenceType.Typeld, idFilter);
SearchQuery search query = new
SearchQuery.Builder(shirt).facet(new
SelectedFacet(new FilterBase()).build();
client.search(searchQuery, new
CompletionHandler(){
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

Here in this example, only Title and Price of the product would be returned in the response, as opposed to all the fields.

<br />

## Filtering

You can refine fields using fieldId or fieldName.Three types of filters are supported:

* Text
* Range
* Multi-level
* Text

This filter is used to refine products based on fields with string values such as color, gender, brand, etc. It can be defined in the API call in two ways:

**Using Field IDs**

`idFilter` can be formed with two parameters:

* field: The ID of the field on which the text filter is applied.
* value: The ID of the value on which the results are filtered.

```Text Kotlin
val idFilter = IdFilter("76678", "5001")  
val searchQuery = SearchQuery.Builder("Shirt").filter(idFilter).build()  
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
FilterBase[] karray = new FilterBase[2];
karray[0] = new NameFilter("title", "KDD");
karray[1] = new NameFilter("availabilityText", "true");
MultipleIdFilter multipleIdFilter = new MultipleIdFilter(karray, FilterOperatorType.AND);
SearchQuery searchQuery = new SearchQuery.Builder("apple").multipleFilter(multipleIdFilter).build();
```

**Using Field Names**

Again, nameFilter can be formed with two parameters.

* type: The ID of the field on which the text filter is applied.
* value: The ID of the value on which the results are filtered.

```Text Kotlin
val nameFilter = NameFilter("vColor_uFilter","Black")  
val searchQuery = SearchQuery.Builder("Shirt").filter(nameFilter).build()  
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
FilterBase[] karray = new FilterBase[2]; karray[0] = new NameFilter("title", "KDD"); karray[1] = new NameFilter("availabilityText", "true"); MultipleIdFilter multipleIdFilter = new MultipleIdFilter(karray, FilterOperatorType.AND); SearchQuery searchQuery = new SearchQuery.Builder("apple").multipleFilter(multipleIdFilter).build();
```

<br />

#### Range

Used to refine products based on fields with datatypes, like:

* Date
* Number
* decimal

The API can be defined in two ways:

#### Using Field IDs

Filter Range of type ID is built using `IdFilterRange` class and it can be initialized with parameters below:

* `field`: The ID of the field on which the text filter is applied.
* `lower`: The ID of the lower limit of the range.
* `upper`: The ID of the upper limit of the range.

```Text Kotlin
val idFilterRange = IdFilterRange("76678","2034", "8906")  
val searchQuery = SearchQuery.Builder("Shirt").filter(idFilterRange).build()  
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
IdFilterRange idFilter=new
IdFilterRange("76678","2034", "8906");
SearchQuery searchQuery=new
SearchQuery.Builder(shirt).filter(idFilter).build();
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

* `field`: The ID of the field on which the text filter is applied.
* `lower`: The ID of the lower limit of the range.
* `upper`: The ID of the upper limit of the range.

```Text Kotlin
val nameFilterRange = NameFilterRange("vColor","red", "blue")  
val searchQuery = SearchQuery.Builder("Shirt").filter(nameFilterRange).build()  
let query = SearchQuery(key: "Shirt", filter: NameFilterRange(field: "vColor", lower: "red", upper: "blue"))  
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
IdFilterRange idFilter=new
IdFilterRange("76678","2034", "8906");
SearchQuery searchQuery=new
SearchQuery.Builder(shirt).filter(idFilter).build();
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

<br />

#### Multilevel

The multilevel filter is used to refine products based on categories.

The API call can be defined in two ways:

1. using Field IDs: “CategoryIdFilter” is used to filter the results using a category path comprised of category IDs.

```Text Kotlin

val categoryIdFilter = CategoryIdFilter(ReferenceType.TypeId, arrayOf("FA", "A0485"))  
val searchQuery = SearchQuery.Builder("Shirt").categoryFilter(categoryIdFilter).build()  
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
String idFilter[]={"FA", "A0485"};
CategoryIdFilter categoryFilter=new
CategoryIdFilter(ReferenceType.Typeld, idFilter);
SearchQuery searchQuery = new SearchQuery.Bu
ilder(shirt).categoryFilter(categoryFilter).build();
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

here in this example, only Title and Price of the product would be returned in the response, as opposed to all the fields.

## Multiple Filters

There are two types of filter operations:

* AND
* OR

#### AND: Using Field IDs

MultipleIdFilter takes two parameters:

* fieldId
* valueId

```Text Kotlin
// Multiple Filters can be added and 'operatorType' is set to 'AND'
var idFilters = ArrayList() idFilters.add(IdFilter("76678", "5001")) idFilters.add(IdFilter("76678", "5021"))  
val searchQuery = SearchQuery.Builder("Shirt").multipleFilter(MultipleIdFilter(idFilters, FilterOperatorType.AND)).build()  
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
SearchQuery searchQuery = new
SearchQuery.Builder(shirt).multipleFilter(new
MultipleldFilter(new NameFilter[]{new
NameFilter("vColor_uFilter", "Black")},
FilterOperatorType.AND).build();
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

#### OR: Using Field IDs

MultipleIdFilter takes two parameters:

* fieldId
* valueId

```Text Kotlin
//Multiple filters can be added and 'operatorType' is set to 'OR'
var idFilters = ArrayList() idFilters.add(IdFilter("76678", "5001")) idFilters.add(IdFilter("76678", "5021"))  
val searchQuery = SearchQuery.Builder("Shirt").multipleFilter(MultipleIdFilter(idFilters, FilterOperatorType.OR)).build()  
client.search(searchQuery, object : ICompletionHandler  
                                      { override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      //Handle success
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { 
                                      //Handle failure
                                      } 
                                      }
)<br><br>
```
```Text Java
SearchQuery search query = new
SearchQuery.Builder(shirt).multipleFilter(new
MultipleldFilter(new IdFilter[]{new IdFilter("76678",
"5001")}, FilterOperatorType.OR)).build();
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
});
```

<br />

#### Using Field Names

MultipleNameFilter takes two parameters:

* field name
* value name

Multiple filters can be added, and ‘operatorType’ is set to ‘OR’.

```Text Kotlin
var nameFilters = ArrayList() nameFilters.add(NameFilter("vColor_uFilter", "Black")) nameFilters.add(NameFilter("vColor_uFilter", "White"))  
val searchQuery = SearchQuery.Builder("Shirt").multipleFilter(MultipleIdFilter(nameFilters, FilterOperatorType.OR)).build()  
client.search(searchQuery, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: 
JSONObject, response: Response)  
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
FilterBase[] karray = new FilterBase[2]; karray[0] = new NameFilter("title", "KDD"); karray[1] = new NameFilter("availabilityText", "true"); MultipleIdFilter multipleIdFilter = new MultipleIdFilter(karray, FilterOperatorType.OR); SearchQuery searchQuery = new SearchQuery.Builder("apple").multipleFilter(multipleIdFilter).build();
```

## Sort

The sort parameter ranks the products based on specified fields in the specified order.

Sort can be done on a single field or multiple fields.

#### Single Field

* fieldName: The field on which the sort is applied.
* sortOrder: The order in which the sort is applied.

```Text Kotlin
//This value can be 'ASC'(for ascending) or 'DSC'(for descending)
var fieldsOrder = ArrayList() fieldsOrder.add(FieldSortOrder("vPrice", SortOrder.ASC))  
val searchQuery = SearchQuery.Builder("Shirt").fieldsSortOrder(fieldsOrder).build() client.search(searchQuery, object : ICompletionHandler  
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
//ASC (for ascending )
FieldSortOrder[] fieldSortOrder = new
FieldSortOrder[]{new FieldSortOrder("VPrice",
Sortorder.ASC)};
Search query search query = new SearchQuery.Bu
ilder(shirt).fieldsSortOrder(fieldSortOrder).build();
client.search(searchQuery, new
CompletionHandler() {
@Override
public void onSuccess(@NotNull
JSONObject json Object, @NotNull Response
response) {
}
@Override
public void onFailure(@NotNull String s,

@NotNull Exception e) {
}
});
```