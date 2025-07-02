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

**Viewed also viewed**\
As the name suggests, this method recommends products viewed by other shoppers.

```
val viewedAlsoViewedRecommendation = ViewedAlsoViewedRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build() client.recommend(viewedAlsoViewedRecommendation, object : ICompletionHandler { override fun onSuccess(json: JSONObject, response: Response) { Log.d("Client Response",json.toString()) } override fun onFailure(errorMessage: String, exception: Exception) { Log.d("Client Response",errorMessage) } } ) val viewedAlsoViewedRecommendation = ViewedAlsoViewedRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build() client.recommend(viewedAlsoViewedRecommendation, object : ICompletionHandler { override fun onSuccess(json: JSONObject, response: Response) { Log.d("Client Response",json.toString()) } override fun onFailure(errorMessage: String, exception: Exception) { Log.d("Client Response",errorMessage) } } )
```

**Bought also bought**\
Similar to the “Viewed also Viewed” method, the Bought also Bought method recommends products bought by other shoppers.

```
val boughtAlsoBoughtRecommendation = BoughtAlsoBoughtRecommendation.Builder(userId.id, "2312314").region("US").currency("USD").build()  
client.recommend(boughtAlsoBoughtRecommendation, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      { Log.d("Client Response",json.toString())
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

**Cart Recommendations**\
This method recommends complementary products on the “Cart page” for those present in the shopper’s cart.

```
val cartRecommendation =  
CartRecommendation.Builder(userId.id).region("US").currency("USD").build()  
client.recommend(cartRecommendation, object : ICompletionHandler  
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

**Top Sellers – Home page**\
This method recommends top selling products bought from the homepage.

```
val homePageTopSellersRecommendation = HomePageTopSellersRecommendation.Builder(userId.id).region("US"). currency("USD").build()  
client.recommend(homePageTopSellersRecommendation, object : ICompletionHandler  
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

**Top Sellers – Category page**\
This method recommends top selling products from a specific category.

```
val categoryTopSellersRecommendation = CategoryTopSellersRecommendation.Builder(userId.id, ).region("US").currency("USD").build()  
client.recommend(categoryTopSellersRecommendation, object : ICompletionHandler  
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

**Top Sellers – Brand**\
This method recommends top selling products from a specific brand.

```
val brandTopSellersRecommendation = BrandTopSellersRecommendation.Builder(userId.id, "Nike").region("US").currency("USD").build()  
client.recommend(brandTopSellersRecommendation, object : ICompletionHandler  
                                      {
                                      override fun onSuccess(json: JSONObject, response: Response) 
                                      { Log.d("Client Response",json.toString())
                                      }
                                      override fun onFailure(errorMessage: String, exception: Exception) 
                                      { Log.d("Client Response",errorMessage)
                                      } 
                                      }
)
```

**Complete the look**

The Complete the Look method showcases curated products on a PDP that are usually associated with the original product.

```
val completeTheLookRecommendation = CompleteTheLookRecommendation.Builder(userId.id, "23121").region("US").currency("USD").build()  
client.recommend(completeTheLookRecommendation, object : ICompletionHandler  
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