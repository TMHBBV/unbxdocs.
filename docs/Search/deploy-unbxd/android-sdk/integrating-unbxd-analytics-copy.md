---
title: Integrating Unbxd Analytics II
deprecated: false
hidden: false
metadata:
  robots: index
---
## Tracking Recommendation Widget

If you are subscribed to Unbxd Recommendations, every time the shopper clicks on a Recommendation widget, the API below will be called.

<br />

userId.id: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.

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

<br />

userId.visitType: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.

<br />

requestId: The unbxd request id returned in the search/category page/recommendations API call response.

<br />

recommendationType : Specifies the type of recommendation widget. For different permissible values, refer the table below.