---
title: Unbxd Recommendations
deprecated: false
hidden: false
metadata:
  robots: index
---
Unbxd Recommendations offers a wide range of widgets for every page. Recommendations API returns product details for options like MoreLikeThis, RecentlyViewed, etc.

The Unbxd SDK supports the following types of widgets:

Recommended For You\
Recently Viewed
More Like This
Viewed also Viewed
Bought also Bought
Cart Recommendations
Top Sellers
Top Sellers – Category page
Top Sellers – Product page
Top Sellers – Brand
Complete the look.
Recommendations for you
The Recommended For You method returns recommendations based on the shopper’s interaction history on the online store or app.

```
val userId = client.userId()  
val recommendedForYour = RecommendedForYourRecommendation.Builder(userId.id).region("US").currency(" USD").build()  
client.recommend(recommendedForYour, object : ICompletionHandler  
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

**Recently Viewed**

The Recently Viewed method recommends products that were recently viewed by a shopper.

```
val recentlyViewedRecommendation = RecentlyViewedRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build()  
client.recommend(recentlyViewedRecommendation, object : ICompletionHandler  
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

**More like these**\
The “More Like These” method is built to recommend products similar to the one being viewed on the Product Detail Page (PDP).

```
val moreLikeThisRecommendation = MoreLikeThisRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build()  
client.recommend(moreLikeThisRecommendation, object : ICompletionHandler  
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