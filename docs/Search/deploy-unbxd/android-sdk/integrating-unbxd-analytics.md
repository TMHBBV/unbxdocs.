---
title: 'Integrating Unbxd Analytics '
deprecated: false
hidden: false
metadata:
  robots: index
---
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