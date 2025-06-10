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