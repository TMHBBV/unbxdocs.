---
title: 'Integrating Unbxd Autosuggest '
deprecated: false
hidden: false
metadata:
  robots: index
---
The Autosuggest feature provides query suggestions, which help your visitors search faster on your site. Unbxd supports autocomplete of search queries and showcases products relevant to the query as users type.

Unbxd Autosuggest comprises different types of suggestions that are known as doctypes. A standard Unbxd Autosuggest is segmented into five doctypes:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Features
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        In-fields
      </td>

      <td>
        The In-fields doctype suggests groups of relevant products along with their associated field values to which the query may belong.
        These field values can be categories, brands, occasions, etc. For example, a visitor types 'Sh', the In-field doctype will have the following suggestions.
        Shirts:

        * In Men(based on gender)
        * In Nike(based on brand)
        * In Blue(based on occasion)
      </td>
    </tr>

    <tr>
      <td>
        Top Queries
      </td>

      <td>
        This doctype displays the frequently searched queries in your e-commerce store, populated with the help of Unbxd Analytics, which tracks your store.
      </td>
    </tr>

    <tr>
      <td>
        Popular Products
      </td>

      <td>
        This doctype displays popular products with thumbnail images. Like Top Queries doctype, Unbxd Analytics needs to be integrated into your e-commerce store to render Popular products.
      </td>
    </tr>

    <tr>
      <td>
        Promoted Suggestions
      </td>

      <td>
        These are documents that a customer can configure directly from the merchandising console.\
        For example, if a customer configures  'jogging shoes' and 'running shoes' as promoted suggestions, and a shopper searches for 'sh', the intended results are returned.
      </td>
    </tr>
  </tbody>
</Table>

#### Using Autosuggest Query

Arguments used to for Autosuggest query are as follows:

* AutosuggestQuery
* Variants
* DocType
* Filters

Let's discuss each of these in details.

## Autosuggest Query

AutoSuggest can be initialized with 'Key' for suggestions. This is a mandatory parameter. 'Shir' in below example, the sample query types by the user.

```
val autosuggestQuery = AutosuggestQuery.Builder("Shir").build()  
client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

## Variant

Variants can be enabled or disabled in AutoSuggest query responses. Variant status can be srt to true/false as below.

```
val autosuggestQuery = AutosuggestQuery.Builder("Shir").variant(Variant(true, 2)).build()  
client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

#### Example: search with variants

Variants parameter enables or disables variants in the API response. It can take two values: “true” or “false”. Default value is “false”.

```
let query = SearchQuery(key: "Shirt", variant: Variant(has: true, count: 2))  
client.search(query: query, completion: {(response:Any?, error:Error?) -> Void in  
  //Handle response
 })
```

If you want to get more than one variant in the API response, you can use the variantCount parameter. It can have any numerical value (for example,1,2,3, etc) or “.max” (to get all the variants).

## Doctype

Autosuggest comprises different types of suggestions known as doctypes, as discussed above.

A standard Unbxd Autosuggest is segmented into five doctypes:

* InField
* Keyword Suggestions
* Top Queries
* Promoted Suggestions
* Popular Products

Let’s discuss how to integrate each of these DocTypes, in your autosuggest response.

### InField

The inField doctype with result count can be configured as shown below:

```
val docType = DocTypeInField.Builder().resultCount(3).build()  
val autosuggestQuery = AutosuggestQuery.Builder("Shir").inField(docType).build()  
client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

> 📘 NOTE
>
> If resultCount is not set, default value two will be considered as results count for inField doctype.

### Keyword Suggestions

Key Suggestions doctype with result count can be configured as shown below:

```
val docType = DocTypeKeywordSuggestions.Builder().resultCount(4).build()  
val autosuggestQuery = AutosuggestQuery.Builder("Shir").keywordSuggestions(docType).build() client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

> 📘 NOTE
>
> If resultCount is not set, default value 2 will be considered as results count for Keyword Suggestions doctype.

### Top Queries

Top Queries doctype with result count can be configured as below:

```
val docType = DocTypeTopQueries.Builder().resultCount(3).build() val autosuggestQuery =  
AutosuggestQuery.Builder("Shir").topQueries(docType).build()  
client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

> 📘 NOTE
>
> If resultCount is not set, default value 2 will be considered as results count for Top Queries doctype.

### Promoted Suggestions

Promoted Suggestions are product recommendations that a merchandiser can configure from the console.

This allows you to manually insert keyword suggestions in autosuggest, which may not be part of the default relevance results.Promoted Suggestions doctype with result count can be configured as below:

```
val docType = DocTypePromotedSuggestions.Builder().resultCount(5).build() val autosuggestQuery = AutosuggestQuery.Builder("Shir").promotedSuggestions(docType).build()  
client.autosuggest(autosuggestQuery, object : ICompletionHandler  
                                      { 
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      {
                                      //Handle success }
override fun onFailure(errorMessage: String, exception: Exception)  
                                      { 
                                      //Handle failure
                                      } 
                                      }
)
```

> 👍 NOTE
>
> If resultCount is not set, default value 2 will be considered as results count for Top Queries doctype.

### Popular Products

The Product Products doctype displays products most searched for in your eCommerce store with thumbnail images.

Popular Products doctype with fields and result count can be configured as below:

```
val docType = DocTypePopularProducts.Builder().resultCount(3).fields(arrayOf("vColor", "price")).build()  
val autosuggestQuery = AutosuggestQuery.Builder("Shir").popularProducts(docType).build()  
client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

> 👍 NOTE
>
> If resultCount is not set, default value 3 will be considered as results count for Promoted Suggestions doctype.

## Filters

Filters, when used in AutoSuggest, helps to restrict products based on criteria passed.

Two types of filters are supported:

* Text
* Range

### Text

The text filter is used to filter products based on fields with string values such as color, gender, brand, etc. It can be defined in the API call in two ways:

#### Using Fields IDs

IdFilter can be formed with two parameters.

* field: The id of the field on which the text filter is applied.
* value: The id of the value on which results are filters.

```
val idFilter = IdFilter("76678", "5001")  
val autosuggestQuery = AutosuggestQuery.Builder("Shir").filter(idFilter).build() client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

#### Using Field Names

Again, NameFilter can be formed with two parameters:

* field: The ID of the field on which the text filter is applied.
* value: The ID of the value on which the results are filtered.

```
val nameFilter = NameFilter("vColor", "Black")  
val autosuggestQuery = AutosuggestQuery.Builder("Shir").filter(nameFilter).build() client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

### Range

The range filter is used to refine products based on fields with datatypes:

* date
* number
* decimal

You can define the API in two ways:

#### Using Fields IDs

Filter Range of type id is built using FilterIdRange class and it can be initialized with below parameters.

* field: The ID of the field on which the text filter is applied.
* lower: The ID of the lower limit if the range.
* upper: The ID of the upper limit of the range.

```
val idFilterRange = IdFilterRange("76678","2034", "8906") val autosuggestQuery = AutosuggestQuery.Builder("Shir").filter(idFilterRange).build()  
client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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

### Using Field Names

Filter Range of type name is built using the FilterNameRange class, and it can be initialized with the following parameters.

* field: The name of the field on which the text filter is applied.
* lower: The name of the lower limit of the range.
* upper: The name of the upper limit of the range.

```
val nameFilterRange = NameFilterRange("vColor","red", "blue") val autosuggestQuery = AutosuggestQuery.Builder("Shir").filter(nameFilterRange).build()  
client.autosuggest(autosuggestQuery, object : ICompletionHandler  
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