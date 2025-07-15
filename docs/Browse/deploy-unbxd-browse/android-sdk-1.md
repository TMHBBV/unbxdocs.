---
title: Android SDK
deprecated: false
hidden: false
metadata:
  robots: index
---
# Android SDK

Unbxd SDK implements support for making network calls to Unbxd platform and lets you easily configure and integrate Unbxd Site Search in your eCommerce application.

The following features are currently supported with Unbxd SDK:

* **Search**: Allows you to interact with the Unbxd platform and implement all search related functionality
* **Autosuggest**: Allows to autocomplete search queries and showcase relevant products
* **Browse**: Allows you to interact with the Unbxd platform and implement all category related functionality
* **Analytics**: Allows integration of site event, session-related analytics
* **Recommendations**: Allows you to integrate product recommendations with the help of recorded events

## System Requirements

Before you can integrate our SDK, you need to:

### STEP 1

Set up your Site Search Dashboard

### STEP 2

Get your API key, Site key

### STEP 3

Upload your Product Feed

You need to have:

* Kotlin 1.2.71 or above
* Okhttp3 3.8.1 or above

Our SDK is `.aar` programmed using Kotlin. This can be integrated with the Android application programmed with either Kotlin and Java.

## Install SDK

Android SDK is hosted in a private Maven repository and is integrated as a Gradle dependency.

The first step to install the Android SDK is to update the Android app’s `build.gradle` file to add a dependency on the mobile app, then do a Gradle sync.

To add dependency go to file `build.gradle` and go to dependencies section and add the code as shown below:

```groovy
repositories {
    maven {
        url 'http://3.95.143.246:8081/artifactory/libs-release-local/'
        credentials {
            username ""
            password ""
        }
    }
}

dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    implementation 'com.squareup.okhttp3:okhttp:3.8.1'
    implementation (group: 'com.unbxd.sdk', name:'unbxdsdk', version: '1.0.1', ext:'aar')
    implementation project(path: ':unbxdsdk')
}
```

Credentials would be provided by Unbxd.

Unbxd employees can view the credentials here and the procedures here.

After changes to `build.gradle` are done, do a Gradle sync.

***

## Initialize SDK

To initialize SDK, import Unbxd framework:

```kotlin
import com.unbxd.sdk.Client
```

Unbxd is initialised with API key and Site key:

```kotlin
val client = Client(<API_KEY>, <SITE_KEY>, applicationContext)
```

> **NOTE:** We advise you to use your API Key in encrypted form on your frontend and never share it with anyone.

***

## Integrating Unbxd Search

Unbxd Site Search is an e-commerce search platform that enhances your on-site search to deliver fast, relevant, and tailored search results to visitors on your website/mobile application.

Unbxd Site Search is platform-agnostic, which makes it incredibly versatile and easily implementable.

### Using Analytics Method

Search methods in SDK are used to integrate UNBXD search in your Android App.

**Search method signature:**

```kotlin
fun search(query: SearchQuery, completion: ICompletionHandler) { ... }
```

Let’s see how these arguments can be composed and passed in `search()` method invocation.

Different arguments that can be passed with the search method are:

* SearchQuery
* Format
* Start
* Rows
* Spellcheck
* Analytics
* Stats
* Variants
* Field
* Facets
* Filtering
* Multiple Filters
* Sort

### Search Query

`SearchQuery` attaches the query which is searched on a website with search function as shown in the code below. Here `"Shirt"` is the search query.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Formats

The `format` parameter specifies the format of the response. Possible values are `JSON` or `XML`.

> Tips: This is an optional parameter. The default value is `JSON`.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").responseFormat(ResponseFormat.XML).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Start

The `start` parameter is used to offset the results by a specific number. It indicates offset in the complete result set of the products.

> Tips: This is an optional parameter and the default value is `0`.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").start(2).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Rows

The `rows` parameter is used to paginate the results of a query. It indicates the number of products on a single page.

> Tips: This is an optional parameter. The default value is `10`, maximum value is `100`.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").rows(20).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Spellcheck

The spellcheck feature provides spelling suggestions or spell-checks for misspelled search queries.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").spellCheck(true).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Analytics

This parameter allows you to enable or disable analytics tracking the site search event.

> Tips: This is an optional Parameter. By default, tracking is enabled.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").analytics(false).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Stats

This parameter provides information about all the products within your catalog that have the highest and lowest field values.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").showStatsForField("vPrice").build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Variants

Products in the feed can be available in different sizes, colors, styles, materials, etc. For example, a dress can be available in different sizes, colors and/or styles.

* Variant 1: Color – Blue, Size: Small, Style – Solid print
* Variant 2: Color – Red, Size: Small, Style – Solid print
* Variant 3: Color – Blue, Size: Large, Style – Polka-dot

The variants parameter enables or disables variants in the API response. It can take two values: `true` or `false`. Default value is `false`.

```kotlin
val variant = Variant(true, 2)
val searchQuery = SearchQuery.Builder("Shirt").variant(variant).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

> 📘 NOTE:
>
> Default value is `false`. If you want to get multiple variants in the API response, you can use the `variantCount` parameter. The `variantCount` parameter can have any numerical value (e.g., 1, 2, 3, etc).

### Fields

The `fields` parameter is used to specify the set of fields to be returned as the response, otherwise, all the fields will be returned in the response by default.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").fields(arrayOf("title","vPrice")).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

In this example, only Title and Price of the product would be returned in the response, as opposed to all the fields.

### Facets

Facets are filters in the UI that allow visitors to narrow down result set based on product fields. It is usually known as Layered Navigation or Guided Navigation.

Facets can be easily configured from the Manage -> Configure Search -> Configure Facet section of the Console.

Facets can be of three types:

* **Multi-level**: Facets on categories.
* **Text**: Facets on text fields in the feed. For example, color, brand, etc.
* **Range**: Facets on numeric fields in the feed. For example, price, discount, etc.

#### Multilevel

`MultiLevelFacet()` parameter is used to enable Multi-level facet in the API in search response.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").facet(MultiLevelFacet()).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Multiselect

This feature enables or disables the option to select multiple values within a facet or across facets for visitors.

```kotlin
val searchQuery = SearchQuery.Builder("Shirt").facet(MultiSelectFacet()).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Selected

This feature enables or disables the option to select multiple values within a facet or across facets for visitors.

**Selected facet with fieldId and valueId:**

```kotlin
val idFilter = IdFilter("76678", "5001")
val searchQuery = SearchQuery.Builder("Shirt").facet(SelectedFacet(idFilter)).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

**Selected facet with field name and value name:**

```kotlin
let query = SearchQuery(key: "Shirt", facet: .Selected(NameFilter(field: "Brand_uFilter", value: "Vince Camuto")))
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Filtering

You can refine fields using `fieldId` or `fieldName`. Three types of filters are supported:

* **Text**
* **Range**
* **Multi-level**

#### Text

This filter is used to refine products based on fields with string values such as color, gender, brand, etc.

**Using Field IDs:**

```kotlin
val idFilter = IdFilter("76678", "5001")
val searchQuery = SearchQuery.Builder("Shirt").filter(idFilter).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

**Using Field Names:**

```kotlin
val nameFilter = NameFilter("vColor_uFilter","Black")
val searchQuery = SearchQuery.Builder("Shirt").filter(nameFilter).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Range

Used to refine products based on fields with datatypes, like:

* Date
* Number
* Decimal

The API can be defined in two ways:

**Using Field IDs:**

```kotlin
val idFilterRange = IdFilterRange("76678","2034", "8906")
val searchQuery = SearchQuery.Builder("Shirt").filter(idFilterRange).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

**Using Field Names:**

```kotlin
val nameFilterRange = NameFilterRange("vColor","red", "blue")
val searchQuery = SearchQuery.Builder("Shirt").filter(nameFilterRange).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Multi-level

The multilevel filter is used to refine products based on categories. The API call can be defined in two ways:

**Using Field IDs:**

```kotlin
val categoryIdFilter = CategoryIdFilter(ReferenceType.TypeId, arrayOf("FA", "A0485"))
val searchQuery = SearchQuery.Builder("Shirt").categoryFilter(categoryIdFilter).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

**Using Field Names:**

```kotlin
val categoryNameFilter = CategoryNameFilter(ReferenceType.TypeName, arrayOf("Fashion", "Shirts"))
val searchQuery = SearchQuery.Builder("Shirt").categoryFilter(categoryNameFilter).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Multiple Filters

There are two types of filter operations:

* **AND**
* **OR**

##### AND

**Using Field IDs:**

`MultipleIdFilter` takes 2 parameters: `fieldId`, `valueId`. Multiple filters can be added and `operatorType` is set to `AND`.

```kotlin
var idFilters = ArrayList<IdFilter>()
idFilters.add(IdFilter("76678", "5001"))
idFilters.add(IdFilter("76678", "5021"))
val searchQuery = SearchQuery.Builder("Shirt").multipleFilter(MultipleIdFilter(idFilters, FilterOperatorType.AND)).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

**Using Field Names:**

`MultipleNameFilter` takes 2 parameters: `fieldName`, `valueName`. Multiple filters can be added and `operatorType` is set to `AND`.

```kotlin
var nameFilters = ArrayList<NameFilter>()
nameFilters.add(NameFilter("vColor_uFilter", "Black"))
nameFilters.add(NameFilter("vColor_uFilter", "White"))
val searchQuery = SearchQuery.Builder("Shirt").multipleFilter(MultipleIdFilter(nameFilters, FilterOperatorType.AND)).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

##### OR

**Using Field IDs:**

```kotlin
var idFilters = ArrayList<IdFilter>()
idFilters.add(IdFilter("76678", "5001"))
idFilters.add(IdFilter("76678", "5021"))
val searchQuery = SearchQuery.Builder("Shirt").multipleFilter(MultipleIdFilter(idFilters, FilterOperatorType.OR)).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

**Using Field Names:**

```kotlin
var nameFilters = ArrayList<NameFilter>()
nameFilters.add(NameFilter("vColor_uFilter", "Black"))
nameFilters.add(NameFilter("vColor_uFilter", "White"))
val searchQuery = SearchQuery.Builder("Shirt").multipleFilter(MultipleIdFilter(nameFilters, FilterOperatorType.OR)).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Sort

The `sort` parameter is used to rank the products based on specified fields in the specified order. Sort can be done on a single field or multiple fields.

#### Single Field

* `fieldName`: The field on which the sort is applied.
* `sortOrder`: The order in which the sort is applied. This value can be `ASC` (for ascending) or `DSC` (for descending).

```kotlin
var fieldsOrder = ArrayList<FieldSortOrder>()
fieldsOrder.add(FieldSortOrder("vPrice", SortOrder.ASC))
val searchQuery = SearchQuery.Builder("Shirt").fieldsSortOrder(fieldsOrder).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Multiple Fields

When two or more `FieldSortOrder` instances are added:

```kotlin
var fieldsOrder = ArrayList<FieldSortOrder>()
fieldsOrder.add(FieldSortOrder("vPrice", SortOrder.ASC))
fieldsOrder.add(FieldSortOrder("title", SortOrder.DSC))
val searchQuery = SearchQuery.Builder("Shirt").fieldsSortOrder(fieldsOrder).build()
client.search(searchQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Integrating Unbxd Autosuggest

The Autosuggest feature provides query suggestions, which helps your visitors to search faster in your site. Unbxd supports autocompletion of search queries and showcasing products relevant to query as they type.

Unbxd Autosuggest comprises of different types of suggestions that are known as doctypes. A standard Unbxd Autosuggest is segmented into five doctypes:

* **In-fields**: Suggest groups of relevant products along with associated field values
* **Keyword Suggestions**: Intelligent suggestions generated by Unbxd
* **Top Queries**: Frequently searched queries
* **Popular Products**: Popular products with thumbnail images
* **Promoted Suggestions**: Configured directly from merchandising console

### Using Autosuggest Query

Arguments used for Autosuggest query are as follows:

* AutosuggestQuery
* Variants
* DocType
* Filters

#### Autosuggest Query

`AutoSuggest` can be initialized with `key` for suggestions. This is a mandatory parameter.

```kotlin
val autosuggestQuery = AutosuggestQuery.Builder("Shir").build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Variant

Example: Search with variants

Variants parameter enables or disables variants in the API response. It can take two values: “true” or “false”. Default value is “false”.

```kotlin
val autosuggestQuery = AutosuggestQuery.Builder("Shir").variant(Variant(true, 2)).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

If you want to get more than one variants in the API response, you can use variantCount parameter. It can have any numerical value (for example,1,2,3,etc) or “.max” (to get all the variants).

#### Doctype: InField

Autosuggest comprises of different types of suggestions that are known as doctypes as discussed above. A standard Unbxd Autosuggest is segmented into five doctypes:

* InField
* Keyword Suggestions
* Top Queries
* Promoted Suggestions
* Popular Products

Let’s discuss how to integrate each of these DocTypes, in your autosuggest response.

### InField

The inField doctype with result count can be configured as shown below:

```kotlin
val docType = DocTypeInField.Builder().resultCount(3).build()
val autosuggestQuery = AutosuggestQuery.Builder("Shir").inField(docType).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

> 📘 NOTE
>
> If resultCount is not set, default value 2 will be considered as results count for inField doctype.

### Keyword Suggestions

Keyword Suggestions doctype with result count can be configured as shown below:

#### Doctype: Keyword Suggestions

```kotlin
val docType = DocTypeKeywordSuggestions.Builder().resultCount(4).build()
val autosuggestQuery = AutosuggestQuery.Builder("Shir").keywordSuggestions(docType).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

> 📘 NOTE
>
> If resultCount is not set, default value 2 will be considered as results count for Keyword Suggestions doctype.

#### Top Queries

Top Queries doctype with result count can be configured as below:

```kotlin
val docType = DocTypeTopQueries.Builder().resultCount(3).build()
val autosuggestQuery = AutosuggestQuery.Builder("Shir").topQueries(docType).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Doctype: Promoted Suggestions

Promoted Suggestions are product recommendations that a merchandiser can configure from the console.

This gives you the flexibility to manually insert keyword suggestions in autosuggest which may not be part of the default relevance results.Promoted Suggestions doctype with result count can be configured as below:

```kotlin
val docType = DocTypePromotedSuggestions.Builder().resultCount(5).build()
val autosuggestQuery = AutosuggestQuery.Builder("Shir").promotedSuggestions(docType).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Doctype: Popular Products

The Popular Products doctype displays products most searched for in your eCommerce store with thumbnail images.

Popular Products doctype with fields and result count can be configured as below:

```kotlin
val docType = DocTypePopularProducts.Builder().resultCount(3).fields(arrayOf("vColor", "price")).build()
val autosuggestQuery = AutosuggestQuery.Builder("Shir").popularProducts(docType).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

> 📘 NOTE
>
> If resultCount is not set, default value 3 will be considered as results count for Promoted Suggestions doctype.

### Filters in Autosuggest

Filters, when used in AutoSuggest, helps to restrict products based on criteria passed. Two types of filters are supported

* Text
* Range
* Text

The text filter is used to filter products based on fields with string values such as color, gender, brand, etc. It can be defined in the API call in two ways:

#### Text Filter: Using Field IDs

IdFilter can be formed with 2 parameters.field: The id of the field on which the text filter is applied. value: The id of the value on which the results are filtered.

```kotlin
val idFilter = IdFilter("76678", "5001")
val autosuggestQuery = AutosuggestQuery.Builder("Shir").filter(idFilter).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Text Filter: Using Field Names Again NameFilter can be formed with 2 parameters.

* field: The ID of the field on which the text filter is applied.
* value: The ID of the value on which the results are filtered.

```kotlin
val nameFilter = NameFilter("vColor", "Black")
val autosuggestQuery = AutosuggestQuery.Builder("Shir").filter(nameFilter).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

#### Range Filter: Using Field IDs

The range filter is used to refine products based on fields with datatypes:

* date
* number
* decimal

You can define the API in two ways:

`Using Field IDs`

```kotlin
val idFilterRange = IdFilterRange("76678", "2034", "8906")
val autosuggestQuery = AutosuggestQuery.Builder("Shir").filter(idFilterRange).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

Using Field Names

Filter Range of type name is built using FilterNameRange class and it can be initialized with below parameters.

* field: The name of the field on which the text filter is applied.
* lower: The name of the lower limit of the range.
* upper: The name of the upper limit of the range.

#### Range Filter: Using Field Names

```kotlin
val nameFilterRange = NameFilterRange("vColor", "red", "blue")
val autosuggestQuery = AutosuggestQuery.Builder("Shir").filter(nameFilterRange).build()
client.autosuggest(autosuggestQuery, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        //Handle success
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        //Handle failure
    }
})
```

### Integrating Unbxd Analytics

Unbxd Analytics tracks a wide range of shopper interactions called **events**, which are essential for optimizing product discovery and generating accurate reports.

#### Supported Events:

* Visitor
* Search Hit
* Category Page Hit
* Product Click
* Add to Cart
* Order
* Product Page View
* Cart Removal
* AutoSuggest
* Recommendation Widget Impression
* Search Impression
* Category Page Impression
* Dwell time (time spent on a product page)

#### Get User ID and Visit Type

SDK generates user ID internally and using below method in Client, App can get UserId and Visit type.

```kotlin
fun userId(): UserId  
User Id instance would have,  
val id: String  
val visitType: String
```

#### Get Request ID from Response

```kotlin
fun Response.unbxdRequestId(): String?  
                                      {
                                      val allHeaders = this.headers()
var requestId = allHeaders.get("Unbxd-Request-Id") if (!requestId.isNullOrEmpty())  
                                      {
                                      return requestId 
                                      }
                                      requestId = allHeaders.get("x-request-id") if (!requestId.isNullOrEmpty()) 
                                      {
                                      return requestId 
                                      }
                                      return null
                                      }<br>
```

### Tracking Visitor Event

Whenever a new user visits the app, a visitor event is fired, containing information about whether a user is a first time visitor or a repeat visitor.

This information is extracted from a ‘visitor’ cookie which is set every time the visitor event is fired. The cookie maintains the information about “visitType” parameter (also used by other events). Its value can be either ‘first-time’ or ‘repeat’.

The SDK will generate a randomized unique identifier (UUID)- UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to a storage device so that it will persist across sessions.

Whenever a new user installs, launches and do some activity such as search, click, etc.. on the application, a visitor event is fired from SDK, that contains information that shopper is a ‘first-time’ user.

Each session of the shopper on the application has an expiry time of 30 minutes and after it expires, the visitor event is fired again and reset the ‘visitType’ as “repeat” user. Next time the shopper opens the application, if the last visitor event was fired more than 30 minutes ago, the visitor event is fired again with ‘visitType’ as “repeat” user. This means, that if the shopper is logged on to the application for more than 30 minutes, his/her visitType will be changed from ‘first-time’ to ‘repeat’ and will be “repeat” forever until he uninstalls and re-installs the application.

```
val userId = client.userId()  
val visitorAnalytics = VisitorAnalytics(userId.id, userId.visitType, requestId)  
client.track(visitorAnalytics, object : ICompletionHandler  
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
> All of the above-mentioned tracking is done by the SDK itself and you as an application developer has to do nothing in order to track visitor event. You can retrieve the UID and visit type using the userId method.

### Tracking Search Event

A search event is fired when a shopper types something in the search box and presses enter or clicks on the search button. This will take the user to the search results page.

```
val userId = client.userId()  
val searchAnalytics = SearchAnalytics(userId.id, userId.visitType, requestId,  
"Shirt")
client.track(searchAnalytics, object : ICompletionHandler  
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

here in this example, “Shirt” is the string shopper types in the search box and presses enter or clicks the search button.

userId.visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.\
userId.id:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
requestId: The unbxd request id returned in the search/category page/recommendations api call response.

### Tracking Category Page Event

Category Page event is fired when a user navigates through the categories on the online store and visits a category page.

```
val categoryPath = CategoryIdPath(arrayOf("cat3380002"))  
val categoryPageAnalytics = CategoryPageAnalytics(userId.id, userId.visitType,  
requestId, categoryPath, PageType.Boolean)  
client.track(categoryPageAnalytics, object : ICompletionHandler  
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

Here,userId.id: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

requestId: The unbxd request id returned in the search/category page/recommendations API call response.

\*categoryPath: \*:unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page. for instance, If you have integrated category pages using the API call: `[https://search.unbxd.io/api-key/site-key/category?p=categoryName](https://search.unbxd.io/api-key/site-key/category?p=categoryName` then categoryQuery will be called as

```
let categoryQuery = CategoryNamePath(withCategories:["categoryName"])
```

but if you have integrated category pages using the API call: [https://search.unbxd.io/api-key/site-key/category?p=category:categoryName](https://search.unbxd.io/api-key/site-key/category?p=category:categoryName)

then categoryQuery will be called as

```
let categoryQuery = CategoryNamePath(withCategories: ["category:\(categoryName)"]) 
```

PageType: Its an enum defined in SDK. it accepts the following values:

* URL
* CATEGORY\_PATH
* TAXONOMY\_NODE
* ATTRIBUTE
* BOOLEAN
* Tracking Product Click Event

Whenever a user clicks on a particular product in the search or category page results, a ‘click’ action is generated.

The following code needs to be called along with the appended data as described below:

```
val userId = client.userId()  
val productClickAnalytics = ProductClickAnalytics(userId.id, userId.visitType, requestId, "2301609", "Socks", RecommendationType.RecommendedForYou.boxType)  
client.track(productClickAnalytics, object : ICompletionHandler  
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

userId.id: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

requestId: The unbxd request id returned in the search/category page/recommendations api call response.

pageId(in example-2301609): Sends the unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page.

query( in example-Socks): Sends search query in case of search in the products listing page

boxType: Recommendation widget clicked in case product is clicked from Recommendation Widget. Possible Values are:

| **Widget Type**      | **Box Type**               |
| -------------------- | -------------------------- |
| Recommended For You  | RECOMMENDED\_FOR\_YOU      |
| Recently Viewed      | RECENTLY\_\_VIEWED         |
| More Like These      | MORE\_LIKE\_\_THESE        |
| Viewed also Viewed   | ALSO\_\_VIEWED             |
| Bought also Bought   | ALSO\_\_BOUGHT             |
| Cart Recommendations | CART\_\_RECOMMEND          |
| HomePage Top Sellers | TOP\_\_SELLERS             |
| Category Top Sellers | CATEGORY\_\_TOP\_\_SELLERS |
| PDP Top Sellers      | PDP\_\_TOP\_\_SELLERS      |
| Brand Top Sellers    | BRAND\_\_TOP\_\_SELLERS    |

### Tracking Add to Cart Clicks

An Add to Cart click event is fired every time shopper adds an item to cart.

```
val userId = client.userId()  
val addToCartAnalytics = ProductAddToCartAnalytics(userId.id, userId.visitType, requestId, "2301609", "231221", 2)  
client.track(addToCartAnalytics, object : ICompletionHandler  
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

userId.id:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

\*requestId \*: The unbxd request id returned in the search/category page/recommendations API call response.

PID: SKU id of the product. For example “2301609” in the above code.

variantId: Id of the variant being added. For example “231221” in the above code.

quantity: Quantity of the product added to the checkout bag. For example “2” in the above code.

### Tracking Order Event

A product order event is fired upon order completion after the shopper returns to a product page from the payment gateway.

```
val userId = client.userId()  
val orderAnalytics = ProductOrderAnalytics(userId.id, userId.visitType, requestId, "2301609", 20.5, 2)  
client.track(orderAnalytics, object : ICompletionHandler  
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

userId.id:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

requestId: The unbxd request id returned in the search/category page/recommendations API call response.

\*pid: \*SKU id of the product. For example “2301609” in the above code.

Price: Order Payment of the product paid by the customer. For example “20.5” in the above code.

qty: Quantity of the product bought. For example “2” in the above code.

### Tracking Product Display Page Views

A product display page view event is fired every time a shopper visits a Product Display Page (PDP).

```
val userId = client.userId()  
val productDisplayAnalytics = ProductDisplayPageViewAnalytics(userId.id, userId.visitType, requestId, "2034")  
client.track(productDisplayAnalytics, object : ICompletionHandler  
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

userId.id:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType:This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

requestId:The unbxd request id returned in the search/category page/recommendations api call response.

pid:SKU id of the product. For example “2034” in the above code.

### Tracking Cart Removals

A cart removal event is fired when a shopper removes an item from the cart.

```
val userId = client.userId()  
val cartRemovalAnalytics = CartRemovalAnalytics(userId.id, userId.visitType, requestId, "2034", "231221", 2)  
client.track(cartRemovalAnalytics, object : ICompletionHandler  
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

userId.id:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType:This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

requestId:The unbxd request id returned in the search/category page/recommendations api call response.

pid:SKU id of the product. For Example “2034” in the above code.

variantId:Id of the variant being removed. For example “231221” in the above code.

qty:Quantity of the product removed. For example “2” in the above code.

### Tracking Autosuggest

An autosuggest event is fired when a shopper searches for a product and clicks on a product within the autosuggest widget/panel.

```
val userId = client.userId()  
val autoSuggestAnalytics = AutoSuggestAnalytics(userId.id, userId.visitType, requestId, "2034", "Red Socks", DocType.INFIELD.jsonKey, "red", "Red socks", "infield1", "color type", 6)  
client.track(autoSuggestAnalytics, object : ICompletionHandler  
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

userId.id:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

\*requestId: \*The unbxd request id returned in the search/category page/recommendations api call response.

pid:SKU id of the product.It is set non-null when autosuggest\_type is POPULAR\_PRODUCTS. For example “2034” in the above code.

query: Autosuggest suggestion returned by Unbxd.

\*docType : \*It can be IN\_FIELD, POPULAR\_PRODUCTS TOP\_SEARCH\_QUERIES, KEYWORD\_SUGGESTION, PROMOTED\_SUGGESTIONS.

\*internalQuery : \*Query for which autosuggest results were generated. For example “red” in the above code.

fieldValue : Set when autosuggest\_type is IN\_FIELD. Set to the value of the “infield” in unbxd response. It is set to null otherwise. For example “Red socks” in the above code.

fieldName : Set when autosuggest\_type is IN\_FIELD. Name of the autosuggest field in the search response. It is set to null otherwise. For Example “infield1” in the above code.

* sourceField:\* Name of the fields present in the catalog on the combination of which in fields are generated. It is set when autosuggest\_type is not null. For example “color type” in the above code.

* unbxdPrank:\* unbxdPrank is the position of selected suggestion the list of items/suggestions received in Autosuggest response. For example “6” in the above code.

skuId, query, doctype, internalQuery, etc are obtained from Autosuggest response data.

### Tracking Recommendation Widget

If you are subscribed to Unbxd Recommendations, every time the shopper clicks on a Recommendation widget, the API below will be called.

```
val userId = client.userId()  
val recommendationWidgetAnalytics = RecommendationWidgetAnalytics(userId.id,  
userId.visitType, requestId, RecommendationType.RecommendedForYou, arrayOf("1692741, 01692015, 1692908"))  
client.track(recommendationWidgetAnalytics, object : ICompletionHandler  
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

userId.id: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

requestId: The unbxd request id returned in the search/category page/recommendations API call response.

recommendationType : Specifies the type of recommendation widget. For different permissible values, refer the table below.

| **Widget Type**      | **Box Type**               |
| -------------------- | -------------------------- |
| Recommended For You  | RECOMMENDED\_FOR\_YOU      |
| Recently Viewed      | RECENTLY\_\_VIEWED         |
| More Like These      | MORE\_LIKE\_\_THESE        |
| Viewed also Viewed   | ALSO\_\_VIEWED             |
| Bought also Bought   | ALSO\_\_BOUGHT             |
| Cart Recommendations | CART\_\_RECOMMEND          |
| HomePage Top Sellers | TOP\_\_SELLERS             |
| Category Top Sellers | CATEGORY\_\_TOP\_\_SELLERS |
| PDP Top Sellers      | PDP\_\_TOP\_\_SELLERS      |
| Brand Top Sellers    | BRAND\_\_TOP\_\_SELLERS    |

*productIds:* List of product IDs rendered.

### Search Result Impression

A search impression event is fired when a search results page loads for the first time, and whenever results changes on applying pagination, auto scroll, sort, and filters. For each of these actions, the uniqueIds’ of the products visible on the search page will be sent as payload.

```
val userId = client.userId()  
val searchImpressionAnalytics = SearchImpressionAnalytics(userId.id, userId.visitType, requestId, "Shoes", arrayOf("1692741", "01692015", "1692908"))  
client.track(searchImpressionAnalytics, object : ICompletionHandler  
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

productIds : List of product ids of products visible in the window when the event occurs. For example “arrayOf(“1692741”, “01692015”, “1692908”))” in above code.

\*userId.id: \*The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the device storage so that it will persist across sessions.

userId .visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

* requestId:\* The unbxd request id returned in the search/category page/recommendations API call response.

query:For example “shirt” in the above code.

### Category Page Impression

Similar to a search page impression event, a category page impression event is fired when a category page results loads for the first time, and every time the results changes on applying pagination, auto scroll, sort, and filters. For each of these actions, the uniqueIds’ of the products visible on the search page will be sent as payload.

```
val categoryPath = CategoryNamePath(arrayOf("home", "furniture", "entrywayfurniture"))  
val categoryPageImpressionAnalytics = CategoryPageImpressionAnalytics(userId.id, userId.visitType, requestId,  
categoryPath, PageType.Url, arrayOf("1692741", "01692015", "1692908"))  
client.track(visitorAnalytics, object : ICompletionHandler  
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

userId.id:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

userId.visitType:This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

categoryPath: unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page. for instance, If you have integrated category pages using the API call: [https://search.unbxd.io/api-key/site-key/category?p=categoryNamethen](https://search.unbxd.io/api-key/site-key/category?p=categoryNamethen) categoryQuery will be called as

```
let categoryQuery = CategoryNamePath(withCategories:  
["categoryName"])
```

<br />

but if you have integrated category pages using the API call: [https://search.unbxd.io/api-key/site-key/category?p=category:categoryName](https://search.unbxd.io/api-key/site-key/category?p=category:categoryName)

then categoryQuery will be called as

```
let categoryQuery = CategoryNamePath(withCategories: ["category:\(categoryName)"])  
```

<br />

* pageType: \* It is an enum defined in SDK. it accepts the following values

URL\
CATEGORY\_PATH
TAXONOMY\_NODE
ATTRIBUTE
BOOLEAN
requestId: The unbxd request id returned in the search/category page/recommendations API call response.

productIds : List of product ids of products visible in the window when the event occurs. For example “arrayOf(“1692741”, “01692015”, “1692908”))” in above code.

### Dwell Time

A dwell time event is used to capture the amount of time a shopper spends on the product description page.

```
val userId = client.userId()  
val dwellTimeAnalytics = DwellTimeAnalytics(userId.id, userId.visitType, requestId,  
"2301609", 60.0)
client.track(dwellTimeAnalytics, object : ICompletionHandler  
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

### Facets

A facet event is fired when a filter is applied on Search or Category pages.

```
val userId = client.userId()  
val facetAnalytics = FacetAnalytics(userId.id, userId.visitType, requestId, "Shirts", NameFilter("fit_fq", "Fitted"))  
client.track(facetAnalytics, object : ICompletionHandler  
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

## Integrating Unbxd Browse

The SDK lets you customize your page experience by leveraging various built-in features of Browse. You can also power any type of page, such as Category, Brand, or any other attribute.

Let’s see how the Browse Query can be composed and passed in browse() method invocation.

### Using Browse Method

Browse methods operate on Category fields query which is configured part of Browse Query.

Browse Methods has the following parts:

* Browse Query
* Format
* Start
* Rows
* Spellcheck
* Analytics
* Stats
* Variants
* Fields
* Facets
* Filtering
* Multiple Filter
* Sort
* Browse Query

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

### Format

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
> It is an optional parameter and the default value is ‘json’.

### Start

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

> 📘 NOTE
>
> This is an optional parameter and the default value is 0.

### Rows

This parameter is used to paginate the results of a query. It indicates the number of products on a single page.

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

> 📘 NOTE:
>
> It is an optional parameter and the default value is 10, the maximum value is 100.

### Spellcheck

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

### Analytics

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

<br />

> 📘 NOTE
>
> By default, tracking is enabled.

Stats\
The stats parameter gives information about the products with highest and lowest field value.

### Integrating Unbxd Recommendations

Unbxd Recommendations offers a wide range of widgets tailored for different pages. The Recommendations API returns product suggestions such as More Like This, Recently Viewed, and others.

#### Supported Recommendation Widgets:

* Recommended For You
* Recently Viewed
* More Like This
* Viewed also Viewed
* Bought also Bought
* Cart Recommendations
* Top Sellers (Home, Category, Product, Brand)
* Complete the Look

#### Recommended For You

```kotlin
val userId = client.userId()
val recommendedForYou = RecommendedForYourRecommendation.Builder(userId.id).region("US").currency("USD").build()
client.recommend(recommendedForYou, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Recently Viewed

```kotlin
val recentlyViewedRecommendation = RecentlyViewedRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build()
client.recommend(recentlyViewedRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### More Like This

```kotlin
val moreLikeThisRecommendation = MoreLikeThisRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build()
client.recommend(moreLikeThisRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Viewed also Viewed

```kotlin
val viewedAlsoViewedRecommendation = ViewedAlsoViewedRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build()
client.recommend(viewedAlsoViewedRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Bought also Bought

```kotlin
val boughtAlsoBoughtRecommendation = BoughtAlsoBoughtRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build()
client.recommend(boughtAlsoBoughtRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Cart Recommendations

```kotlin
val cartRecommendation = CartRecommendation.Builder(userId.id).region("US").currency("USD").build()
client.recommend(cartRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Top Sellers – Home Page

```kotlin
val homePageTopSellersRecommendation = HomePageTopSellersRecommendation.Builder(userId.id).region("US").currency("USD").build()
client.recommend(homePageTopSellersRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Top Sellers – Category Page

```kotlin
val categoryTopSellersRecommendation = CategoryTopSellersRecommendation.Builder(userId.id).region("US").currency("USD").build()
client.recommend(categoryTopSellersRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Top Sellers – Product Page

```kotlin
val pdpTopSellersRecommendation = PDPTopSellersRecommendation.Builder(userId.id, "23121").region("US").currency("USD").build()
client.recommend(pdpTopSellersRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Top Sellers – Brand

```kotlin
val brandTopSellersRecommendation = BrandTopSellersRecommendation.Builder(userId.id, "Nike").region("US").currency("USD").build()
client.recommend(brandTopSellersRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

#### Complete the Look

```kotlin
val completeTheLookRecommendation = CompleteTheLookRecommendation.Builder(userId.id, "23121").region("US").currency("USD").build()
client.recommend(completeTheLookRecommendation, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Client Response", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.d("Client Response", errorMessage)
    }
})
```

# Sample iOS App

For sample app, click the link below: [Android Home Decor](https://github.com/unbxd/AndroidHomeDecor-/%22).