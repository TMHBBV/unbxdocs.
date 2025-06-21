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

Variants can be enabled or disabled in AutoSuggest query responses.

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

#### Doctype: InField

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

#### Doctype: Top Queries

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

### Filters in Autosuggest

Filters, when used in AutoSuggest, help restrict products based on criteria passed.

#### Text Filter: Using Field IDs

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

#### Text Filter: Using Field Names

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

### Integrating Unbxd Analytics (Advanced)

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
* Dwell Time
* Facet Clicks

#### Get User ID and Visit Type

```kotlin
val userId = client.userId()
val id = userId.id           // Unique User Identifier
val visitType = userId.visitType  // "first-time" or "repeat"
```

#### Get Request ID from Response

```kotlin
fun Response.unbxdRequestId(): String? {
    val headers = this.headers()
    return headers["Unbxd-Request-Id"] ?: headers["x-request-id"]
}
```

***

#### Example: Tracking Visitor Event

```kotlin
val visitorAnalytics = VisitorAnalytics(userId.id, userId.visitType, requestId)
client.track(visitorAnalytics, object : ICompletionHandler {
    override fun onSuccess(json: JSONObject, response: Response) {
        Log.d("Analytics", json.toString())
    }
    override fun onFailure(errorMessage: String, exception: Exception) {
        Log.e("Analytics", errorMessage)
    }
})
```

> Note: The SDK automatically tracks visitor events when a user opens the app.

***

#### Example: Tracking Search Event

```kotlin
val searchAnalytics = SearchAnalytics(userId.id, userId.visitType, requestId, "Shirt")
client.track(searchAnalytics, object : ICompletionHandler { ... })
```

***

#### Example: Tracking Category Page Event

```kotlin
val categoryPath = CategoryIdPath(arrayOf("cat3380002"))
val categoryPageAnalytics = CategoryPageAnalytics(userId.id, userId.visitType, requestId, categoryPath, PageType.Boolean)
client.track(categoryPageAnalytics, object : ICompletionHandler { ... })
```

***

#### Example: Product Click Event

```kotlin
val clickAnalytics = ProductClickAnalytics(userId.id, userId.visitType, requestId, "2301609", "Socks", RecommendationType.RecommendedForYou.boxType)
client.track(clickAnalytics, object : ICompletionHandler { ... })
```

***

#### Example: Add to Cart Event

```kotlin
val addToCart = ProductAddToCartAnalytics(userId.id, userId.visitType, requestId, "2301609", "231221", 2)
client.track(addToCart, object : ICompletionHandler { ... })
```

***

#### Example: Order Event

```kotlin
val order = ProductOrderAnalytics(userId.id, userId.visitType, requestId, "2301609", 20.5, 2)
client.track(order, object : ICompletionHandler { ... })
```

***

#### Example: PDP View Event

```kotlin
val pdp = ProductDisplayPageViewAnalytics(userId.id, userId.visitType, requestId, "2034")
client.track(pdp, object : ICompletionHandler { ... })
```

***

#### Example: Cart Removal

```kotlin
val remove = CartRemovalAnalytics(userId.id, userId.visitType, requestId, "2034", "231221", 2)
client.track(remove, object : ICompletionHandler { ... })
```

***

#### Example: Autosuggest Click

```kotlin
val suggest = AutoSuggestAnalytics(userId.id, userId.visitType, requestId, "2034", "Red Socks", DocType.INFIELD.jsonKey, "red", "Red socks", "infield1", "color type", 6)
client.track(suggest, object : ICompletionHandler { ... })
```

***

#### Example: Recommendation Widget Click

```kotlin
val widgetClick = RecommendationWidgetAnalytics(userId.id, userId.visitType, requestId, RecommendationType.RecommendedForYou, arrayOf("1692741", "01692015", "1692908"))
client.track(widgetClick, object : ICompletionHandler { ... })
```

***

#### Example: Search Impression

```kotlin
val impression = SearchImpressionAnalytics(userId.id, userId.visitType, requestId, "Shoes", arrayOf("1692741", "01692015", "1692908"))
client.track(impression, object : ICompletionHandler { ... })
```

***

#### Example: Category Page Impression

```kotlin
val catPath = CategoryNamePath(arrayOf("home", "furniture", "entrywayfurniture"))
val catImpression = CategoryPageImpressionAnalytics(userId.id, userId.visitType, requestId, catPath, PageType.Url, arrayOf("1692741", "01692015", "1692908"))
client.track(catImpression, object : ICompletionHandler { ... })
```

***

#### Example: Dwell Time

```kotlin
val dwell = DwellTimeAnalytics(userId.id, userId.visitType, requestId, "2301609", 60.0)
client.track(dwell, object : ICompletionHandler { ... })
```

***

#### Example: Facet Click

```kotlin
val facet = FacetAnalytics(userId.id, userId.visitType, requestId, "Shirts", NameFilter("fit_fq", "Fitted"))
client.track(facet, object : ICompletionHandler { ... })
```

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