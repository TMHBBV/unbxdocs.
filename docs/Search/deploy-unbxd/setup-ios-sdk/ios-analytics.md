---
title: iOS Analytics
deprecated: false
hidden: false
metadata:
  robots: index
---
# Unbxd Analytics

The actions a shopper takes on your eCommerce store are known as Events. Tracking visitor analytics and behavior is essential to provide accurate and shopper-specific search and category page results while also demonstrating the value our solutions have on your business.

Unbxd Analytics tracks the following events:

* Visitor Logins
* Search Hit
* Category Page Hit
* Product Click
* Add to Cart
* Successful Orders
* Product Page View
* Cart Removal
* AutoSuggest
* Recommendation Widget Impression
* Search Impression
* Category Page Impression
* Dwell time (indicates time spent on a product page)

For more information about different events, see [here](https://unbxd.com/docs).

### Using UserID Method

SDK generates user id internally and using below method App can get UserId and visit type.

```swift
func userId() -> UserId
```

User ID instance would have:

```swift
let id: String  
let visitType: String
```

### Getting Request ID

RequestId should be passed to all the analytics APIs. It should be parsed from response header for key “Unbxd-Request-ID” from the request to Unbxd framework.

```swift
extension HTTPURLResponse  
{
    func unbxdRequestId() -> String?  
    {
        if let allHeaders = self.allHeaderFields as? [String: String] 
        {
            if let id = allHeaders["Unbxd-Request-Id"]  
            {
                return id  
            }
        }
        return nil  
    }
}
```

### Using Analytics Method

Analytics method signature:

```swift
func track(analyticsDetails: AnalyticsAbstract, completion: @escaping (_ response: Dictionary<String, Any>?, _ httpResponse: HTTPURLResponse?, _ error: Error?) -> Void) {  
    // Handle response or request
}
```

For iOS applications, `ViewController` (a type of class) acts as a page within the app. View controllers are identified by class names. Define String constants in each view controller and refer them in case of Analytics to track which page was viewed. For example, `LoginViewController` will have string constant say ‘Home Page’ so we post this string for page viewed event.

### Tracking Visitor Event

Whenever a new shopper visits the app, a visitor event is fired, containing information about whether a user is a first time visitor or a repeat visitor.

This information is extracted from a ‘visitor’ cookie which is created every time the visitor event is fired. The cookie maintains the information about “visitType” parameter (also used by other events). Its value can be either ‘first-time’ or ‘repeat’.

The SDK will assign a randomized unique identifier (UID) to every unique user, who installs your application and it would be used to identify the user as a first-time shopper or a repeat shopper. This distinct ID is saved to the storage device so that it will persist across sessions.

Whenever a new shopper installs, launches and performs some activity such as search, click, etc. on the application, a visitor event is fired from SDK, that contains information that shopper is a first-time shopper.

Each session of the shopper on the application has an inactivity timer and after the session is inactive for more than 30 minutes, the visitor event is fired again and reset the ‘visitType’ as repeat shopper.

The next time the shopper opens the application, if the last visitor event was fired more than 30 minutes ago, the visitor event is fired again with ‘visitType’ as “repeat” user. This means, that if the shopper is logged on to the application for more than 30 minutes, his/her visitType will be changed from ‘first-time’ to ‘repeat’ and will be “repeat” forever until he uninstalls and re-installs the application.

All of the above-mentioned tracking is done by the SDK itself and you as an application developer has to do nothing in order to track visitor event.

### Tracking Search Event

A search event is fired when a shopper types text within the search box and presses enter or clicks on the search button. This will take the shopper to the search results page.

Example:

```swift
let searchAnalytics = SearchAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, searchKey: "Shirt")
client.track(analyticsDetails: searchAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

Here in this example, “Shirt” is the string the shopper types in the search box and presses enter or clicks on the search button.

* **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first-time or a repeat shopper. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **query**: search query typed by a shopper in case products listing page shows the result of search event. “Shirt” in the above example.

### Tracking Category Page Event

Category Page event is fired when a shopper navigates through the categories on the online store and visits a category page.

Example:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["home"])
let categoryPageAnalytics = CategoryPageAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, categoryPages: categoryQuery, pageType: PageType.CategoryPath)
client.track(analyticsDetails: categoryPageAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier (UID) to every unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **withCategories**: The unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page. for instance, If you have integrated category pages using the API call: `https://search.unbxd.io/api-key/site-key/category?p=categoryName` then `categoryQuery` will be called as:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["categoryName"])
```

but if you have integrated category pages using the API call: `https://search.unbxd.io/api-key/site-key/category?p=category:categoryName` then `categoryQuery` will be called as:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["category:\(categoryName)"]) 
```

* **pageType**: Its an enum defined in SDK. it accepts the following values:
  * URL
  * CATEGORY\_PATH
  * TAXONOMY\_NODE
  * ATTRIBUTE
  * BOOLEAN
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.

### Tracking Product Click Event

Whenever a shopper clicks on a particular product in the search or category page results, a ‘click’ action is generated.

The following code needs to be called along with the appended data as described below:

Example:

```swift
let productClickAnalytics = ProductClickAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, pID: "2301609", query: "Socks", pageId: "Order", boxType: "RECOMMENDED_FOR_YOU")
client.track(analyticsDetails: productClickAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier – UID to every unique user, who installs your application and it would be used to identify the user as first-time or a repeat shopper. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **query**: search query typed by a shopper in case products listing page shows the result of search event.
* **pageId**: The unique identifier for the page passed in the category page API as parameter ‘p’ in case of products listing page shows the result of Category pages.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **boxType**: Recommendation widget clicked in case product is clicked from Recommendation Widget. Possible Values are:

| Widget Type          | Box Type                   |
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

### Tracking Add to Cart Event

Whenever a user adds a product to his cart, a ‘cart’ action is generated.

Example:

```swift
let addToCartAnalytics = ProductAddToCartAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, productID: "2301609", variantId: "231221", quantity: 2)
client.track(analyticsDetails: addToCartAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The Unbxd request id returned in the search/category page/recommendations API call response.
* **variantId**: The unique identifier of the variant being added.
* **quantity**: Quantity of the product added to the checkout bag.
* **productID**: SKU ID of the product.

### Tracking Order Event

An ‘order’ event will be fired after an order completes when the user comes back to the product page from the payment gateway. If a user buys multiple products in a single order, then multiple order events should be fired.

Example:

```swift
let orderAnalytics = ProductOrderAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, productID: "2301609", price: 20.5, quantity: 3)
client.track(analyticsDetails: orderAnalytics, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **variantId**: The unique identifier of the variant being added.
* **quantity**: Quantity of the product added to the checkout bag.
* **productID**: SKU ID of the product.

### Tracking Product Display Event

Product Display Page View is fired when a user visits a Product Display Page.

Example:

```swift
let productDisplayPageAnalytics = ProductDisplayPageViewAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, skuId: "2034")
client.track(analyticsDetails: productDisplayPageAnalytics, completion: {(response, httpResponse, err) -> Void in
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **SKUID**: SKU ID of the product.

### Cart Removal Event

Cart Removal event is fired when a product in the cart is removed.

Example:

```swift
let cartRemovalAnalytics = CartRemovalAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, skuId: "2034", variantId: "231221", quantity: 2)
client.track(analyticsDetails: cartRemovalAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **variantId**: The unique identifier of the variant being removed.
* **quantity**: Quantity of the product removed.
* **SKUID**: SKU ID of the product.

### Autosuggest Event

An autosuggest event is fired when a user types something, then clicks on any of the autosuggest results shown.

Example:

```swift
let autoSuggestAnalytics = AutoSuggestAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, skuId: "2034", query: "Red Socks", docType: "IN_FIELD", internalQuery: "red", fieldValue: "Red socks", fieldName: "infield1", sourceField: "color type", unbxdPrank: 6)
client.track(analyticsDetails: autoSuggestAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier (UID) to each unique user, who installs your application and it would be used to identify the user as a first-time or a repeat shopper. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **query**: Autosuggest suggestion returned by Unbxd.
* **docType**: It can be `IN_FIELD`, `POPULAR_PRODUCTS`, `TOP_SEARCH_QUERIES`, `KEYWORD_SUGGESTION`, `PROMOTED_SUGGESTIONS`.
* **internalQuery**: Query for which autosuggest results were generated.
* **fieldValue**: Set when autosuggest\_type is `IN_FIELD`. Set to the value of the “infield” in unbxd response. It is set to null otherwise.
* **fieldName**: Set when autosuggest\_type is `IN_FIELD`. Name of the autosuggest field in the search response. It is set to null otherwise.
* **sourceField**: Name of the fields present in the catalog on the combination of which in fields are generated. It is set when autosuggest\_type is not null.
* **skuId**: SKU id of the product. It is set non-null when autosuggest\_type is `POPULAR_PRODUCTS`.
* **unbxdPrank**: unbxdPrank is the position of selected suggestion the list of items/suggestions received in Autosuggest response.

`skuId`, `query`, `doctype`, `internalQuery`, etc are obtained from Autosuggest response data.

### Recommendation Widget Impression

If you are subscribed to Unbxd Recommendations, every time the Recommendation widget is rendered, the recommendation widget event would be fired.

Example:

```swift
let recommendationImpressionAnalytics = RecommendationWidgetAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, recommendationType: RecommendationType.ViewerAlsoViewed, productIds: ["1692741-1758","01692015-285","1692908-480"])
client.track(analyticsDetails: recommendationImpressionAnalytics, completion: {(response, httpResponse, err) -> Void in
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **recommendationType**: Specifies the type of recommendation widget. For different permissible values, refer the table below.

| Widget Type          | Box Type                   |
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

* **productIds**: The unique identifier of the products rendered.

### Search Impression

A search impression event is fired when a search results page loads for the first time, and whenever results changes on applying pagination, auto scroll, sort, and filters. For each of these actions, the unique IDs of the products visible on the search page should be sent as payload.

Example:

```swift
let searchImpressionAnalytics = SearchImpressionAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, query: "Shoes", productIds: ["1692741-1758","01692015-285","1692908-480"])
client.track(analyticsDetails: searchImpressionAnalytics, completion: {(response, httpResponse, err) -> Void in
})
```

* **action**: `search_impression`.
* **pids\_list**: List of product ids of products visible in the window when the event occurs.
* **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.

### Category Page Impression

A Category Page Impression event is fired when a category page results loads for the first time, and whenever the results change on applying pagination, auto scroll, sort, and filters. For each of these actions, the unique IDs of the products visible on the search page should be sent as payload.

Example:

```swift
let categoryPathQuery = CategoryNamePath.init(withCategories: ["men"])
let categoryPageImpression = CategoryPageImpressionAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, categoryPages: categoryPathQuery, pageType: PageType.Url, productIds: ["1692741-1758","01692015-285","1692908-480"])
client.track(analyticsDetails: categoryPageImpression, completion: {(response, httpResponse, err) -> Void in
    //Handle response
})
```

* **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor.
* **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
* **withCategories**: unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page. For instance, if you have integrated category pages using the API call: `https://search.unbxd.io/api-key/site-key/category?p=categoryName` then categoryQuery will be called as:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["categoryName"])
```

If you have integrated category pages using the API call: `https://search.unbxd.io/api-key/site-key/category?p=category:categoryName` then `categoryQuery` will be called as:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["category:\(categoryName)"])  
```

* **pageType**: It is an enum defined in SDK. It accepts the following values:
  * URL
  * CATEGORY\_PATH
  * TAXONOMY\_NODE
  * ATTRIBUTE
  * BOOLEAN
* **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
* **pids\_list**: List of product ids of products visible in the window when the event occurs.

### Dwell Time

A dwell time event is used to capture the amount of time spent on the product description page in milliseconds.

Example:

```swift
let dwellTimeAnalytics = DwellTimeAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, productID: "2301609", dwellTime: 60)
client.track(analyticsDetails: dwellTimeAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

### Tracking Facet Event

A facet event is fired when a filter is applied on Search results or Category pages.

Example:

```swift
let facetAnalytics = FacetAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, searchQuery: "Shirts", facetFields: NameFilter(field: "fit_fq", value: "Fitted"))
client.track(analyticsDetails: facetAnalytics, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

In this case, the value of the “action” parameter would be “facets”. Facets would have all the selected facets. In case of Category Page, send “page” info instead of “query”.