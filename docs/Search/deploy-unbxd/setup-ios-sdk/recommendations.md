---
title: Recommendations
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Unbxd Recommendations is a set of tailored widgets that showcase personalized product suggestions to visitors on different pages of your online e-commerce store. The widgets are easy to configure and provide a smart way of exposing your inventory to visitors. These widgets are powered by the Unbxd analytics engine, which constantly tracks and records visitor events on your store, such as clicks, cart additions, orders, etc. The captured event information is used to build profiles that help our search engine fetch relevant products for each widget.

The Unbxd SDK supports the following types of widgets:

* Recommended For You
* Recently Viewed
* More Like This
* Viewed also Viewed
* Bought also Bought
* Cart Recommendations
* Top Sellers
* Homepage Top Sellers
* Category Top Sellers
* PDP Top Sellers
* Brand Top Sellers
* Complete the Look

Recommendations method signature:

```swift
func recommend(recommendationQuery: RecommendationQuery, completion: @escaping (_ response: Any?, _ error: Error?) -> Void) {  
    // Handle response or request
}
```

### Examples

**RECOMMENDED FOR YOU**: The Recommended For You method returns recommendations based on the visitor’s interaction history on the online store or app.

Sample:

```swift
let forYouQuery = RecommendedForYourRecomendations(uid: uid, region: "USA", currency: "USD", format: .JSON)  
client.recommend(recommendationQuery: forYouQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**RECENTLY VIEWED**:

The Recently Viewed method recommends products that were recently viewed by a visitor.

Sample:

```swift
let recentlyViewedQuery = RecentlyViewedRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: recentlyViewedQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**MORE LIKE THESE**:

The More Like This method is built to recommend products similar to the one being viewed on the PDP (Product Detail Page).

Sample:

```swift
let moreLikeThisQuery = MoreLikeThisRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: moreLikeThisQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**VIEWED ALSO VIEWED**:

As the name suggests, this method recommends products viewed by other visitors.

Sample:

```swift
let alsoViewedQuery = ViewedAlsoViewedRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: alsoViewedQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**BOUGHT ALSO BOUGHT**:

Similar to the Viewed also Viewed method, the Bought also Bought method recommends products bought by other visitors.

Sample:

```swift
let alsoBoughtdQuery = BoughtAlsoBoughtRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: alsoBoughtdQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**CART RECOMMENDATIONS**: This method recommends complementary products on the “Cart page” for those present in the visitor’s cart.

Sample:

```swift
let cartRecommendationQuery = CartRecomendations(uid: uid, region: "USA")
client.recommend(recommendationQuery: cartRecommendationQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**HOMEPAGE TOP SELLERS**:

This method recommends top selling products bought from the homepage.

Sample:

```swift
let homePageTopSellerQuery = HomePageTopSellersRecomendations(uid: uid, region: "USA")  
client.recommend(recommendationQuery: homePageTopSellerQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**CATEGORY TOP SELLERS**:

This method recommends top selling products from a specific category.

Sample:

```swift
let categoryTopSellerQuery = CategoryTopSellersRecomendations(uid: uid, region: "USA", categoryName: "")  
client.recommend(recommendationQuery: categoryTopSellerQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**TOP SELLERS**:

This method recommends top selling products from a specific product.

Sample:

```swift
let pdpTopSellerQuery = PDPTopSellersRecomendations(uid: uid, region: "USA")  
client.recommend(recommendationQuery: pdpTopSellerQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**BRAND TOP SELLERS**:

This method recommends top selling products from a specific brand.

Sample:

```swift
let brandTopSellerQuery = BrandTopSellersRecomendations(uid: uid, region: "USA", brandName: "Nike")  
client.recommend(recommendationQuery: brandTopSellerQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**COMPLETE THE LOOK**:

The Complete the Look method showcases curated products on a Product Display Page (PDP) that are usually associated with the original product.

Sample:

```swift
let completeTheLookQuery = CompleteTheLookRecomendations(uid: uid, productID: "2312314", region: "USA")  
client.recommend(recommendationQuery: completeTheLookQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

## Sample iOS App

Please find the link to sample iOS App:

* **Fashion vertical**: [https://github.com/unbxd/FashionApp](https://github.com/unbxd/FashionApp)
* **Home Decor App**: [https://github.com/unbxd/HomeDecorApp](https://github.com/unbxd/HomeDecorApp)