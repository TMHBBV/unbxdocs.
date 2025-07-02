---
title: Integrating Unbxd Analytics II
deprecated: false
hidden: false
metadata:
  robots: index
---
## Tracking Recommendation Widget

If you are subscribed to Unbxd Recommendations, every time the shopper clicks on a Recommendation widget, the API below will be called.

```
val userId = client.userId()  
val recommendationWidgetAnalytics = RecommendationWidgetAnalytics(userId.id,  
userId.visitType, requestId, RecommendationType.RecommendedForYou, arrayOf("1692741, 01692015, 1692908"))  
client.track(recommendationWidgetAnalytics, object : ICompletionHandler  
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

<br />

productIds : List of product ids of products visible in the window when the event occurs. For example “arrayOf(“1692741”, “01692015”, “1692908”))” in above code.

\*userId.id: \*The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the device storage so that it will persist across sessions.

userId .visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

requestId:\* The unbxd request id returned in the search/category page/recommendations API call response.

query:For example “shirt” in the above code.

## Category Page Impression

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