---
title: 'Integrate Unbxd Analytics '
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The actions a visitor takes on your e-commerce store are known as Events. Tracking visitor analytics and behavior is essential in order to provide accurate and visitor-specific search and category page results, and also help showcase how your business benefits from Unbxd through the reporting.

Unbxd Analytics tracks different events:

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

SDK generates user ID internally and using below method in Client, App can get UserId and Visit type.

```
fun userId(): UserId  
User Id instance would have,  
val id: String  
val visitType: String
```

```Text Getting Request Id 
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

<br />

Using Analytics Method Using Analytics methods app can publish event details and the merchandiser would be able to track those events in the portal. Below are the events, analytics method support

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

## Tracking Visitor Event

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

> 👍 NOTE
>
> All of the above-mentioned tracking is done by the SDK itself and you as an application developer has to do nothing in order to track visitor event. You can retrieve the UID and visit type using the userId method.

## Tracking Search Event

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

<br />

In this example, “Shirt” is the string the shopper types in the search box and presses enter or clicks the search button.

* `userId.visitType`: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* `userId.id`:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* `requestId`: The unbxd request id returned in the search/category page/recommendations api call response.

## Tracking Category Page Event

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

Here, `userId.id`: The SDK will generate a randomized unique identifier – UID to each unique user who installs your application, and it will be used to identify the user as a first-time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

`userId.visitType`: SDK extracts this information from a ‘visitor’ cookie setup. Its value can be either ‘first-time’ or ‘repeat’.

`requestId`: The unbxd request id returned in the search/category page/recommendations API call response.

`categoryPath`: unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page. For instance, if you have integrated category pages using the API call: [https://search.unbxd.io/api-key/site-key/category?p=categoryName](https://search.unbxd.io/api-key/site-key/category?p=categoryName) then categoryQuery will be called as

```
let categoryQuery = CategoryNamePath(withCategories:["categoryName"])
```

<br />

But if you have integrated category pages using the API call: "[https://search.unbxd.io/api-key/site-key/category?p=categoryName](https://search.unbxd.io/api-key/site-key/category?p=categoryName)" Then categoryQuery will be called as

```
let categoryQuery = CategoryNamePath(withCategories: ["category:\(categoryName)"]) 
```

PageType: It's an enum defined in the SDK. It accepts the following values:

* URL
* CATEGORY\_PATH
* TAXONOMY\_NODE
* ATTRIBUTE
* BOOLEAN

## Tracking Product Click Event

A ' click ' action is generated whenever a user clicks on a particular product in the search or category page results.

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

* `userId.id`: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* `userId.visitType`: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* `requestId`: The unbxd request ID returned in the search/category page/recommendations api call response.
* `pageId(in example-2301609)`: Sends the unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page.
* `query( in example-Socks`): Sends search query in case of search in the products listing page.
* `boxType`: Recommendation widget clicked in case product is clicked from Recommendation Widget.

Possible Values are

| Widget Type          | Box type                   |
| :------------------- | :------------------------- |
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

## Tracking Add to Cart Clicks

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

* `userId.id`:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* `userId.visitType`: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* `requestId`: The unbxd request ID returned in the search/category page/recommendations API call response.
* `PID`: SKU id of the product. For example, “2301609” in the above code.
* `variantId`: Id of the variant being added. For example, “231221” in the above code.
* `quantity`: Quantity of the product added to the checkout bag. For example, “2” in the above code.

## Tracking Order Event

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

* **userId.id**:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **userId.visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **pid**: SKU id of the product. For example “2301609” in the above code.
* **Price**: Order Payment of the product paid by the customer. For example “20.5” in the above code.
* **qty**: Quantity of the product bought. For example “2” in the above code.

## Tracking Product Display Page Views

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

* **userId.id**:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **userId.visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations api call response.
* **pid**: SKU id of the product. For example “2034” in the above code.

## Tracking Cart Removals

A cart removal event is fired when a shopper removes an item from the cart.

```
val userId = client.userId() &#x20;
val cartRemovalAnalytics = CartRemovalAnalytics(userId.id, userId.visitType, requestId, "2034", "231221", 2) &#x20;
client.track(cartRemovalAnalytics, object : ICompletionHandler &#x20;
&#x20;                                     \{  &#x20;
&#x20;                                     override fun onSuccess(json: JSONObject, response: Response)&#x20;
&#x20;                                     \{
&#x20;                                     Log.d("Client Response",json.toString())&#x20;
&#x20;                                     }
&#x20;                                     override fun onFailure(errorMessage: String, exception: Exception)&#x20;
&#x20;                                     \{&#x20;
&#x20;                                     Log.d("Client Response",errorMessage)
&#x20;                                     }&#x20;
&#x20;                                     }
)
userId.id:The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
```

<br />

* **userId.visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations api call response.
* **pid**: SKU id of the product. For Example “2034” in the above code.
* **variantId**: Id of the variant being removed. For example “231221” in the above code.
* **qty**: Quantity of the product removed. For example “2” in the above code.

## Tracking Autosuggest

An autosuggest event is fired when a shopper searches for a product and clicks on a product within the autosuggest widget/panel.

```
val userId = client.userId()  
val autoSuggestAnalytics = AutoSuggestAnalytics(userId.id, userId.visitType, requestId, "2034", "Red Socks", DocType.INFIELD.jsonKey, "red", "Red socks", "infield1", "color type", 6)  
client.track(autoSuggestAnalytics, object : ICompletionHandler  
                                      \{   
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      \{
                                      Log.d("Client Response",json.toString())                       
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      \{ 
                                      Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

<br />

* **userId.id**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **userId.visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations api call response.
* **pid**: SKU id of the product.It is set non-null when autosuggest\_type is POPULAR\_PRODUCTS. For example “2034” in the above code.
* **query**: Autosuggest suggestion returned by Unbxd.
* **docType** : It can be IN\_FIELD, POPULAR\_PRODUCTS TOP\_SEARCH\_QUERIES, KEYWORD\_SUGGESTION, PROMOTED\_SUGGESTIONS.
* **internalQuery** : Query for which autosuggest results were generated. For example “red” in the above code.
* **fieldValue** : Set when autosuggest\_type is IN\_FIELD. Set to the value of the “infield” in unbxd response. It is set to null otherwise. For example “Red socks” in the above code.
* **fieldName** : Set when autosuggest\_type is IN\_FIELD. Name of the autosuggest field in the search response. It is set to null otherwise. For Example “infield1” in the above code.
* **sourceField**: Name of the fields present in the catalog on the combination of which in fields are generated. It is set when autosuggest\_type is not null. For example “color type” in the above code.
* **unbxdPrank**: unbxdPrank is the position of selected suggestion the list of items/suggestions received in Autosuggest response. For example “6” in the above code.

skuId, query, doctype, internalQuery, etc are obtained from Autosuggest response data.