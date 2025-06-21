---
title: iOS SDK
deprecated: false
hidden: false
metadata:
  robots: index
---
The Unbxd SDK implements support for making network calls to the Unbxd platform and lets you easily configure and integrate Unbxd Site Search in your eCommerce application.

# Features

The following features are currently supported with Unbxd SDK.

| Features              | Description                                                                                                                                                                                                                                               |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Analytics             | Allows you to track various visitor events on the eCommerce store such as product clicks, add to cart, orders, etc.                                                                                                                                       |
| Unbxd Commerce Search | Allows you to interact with the Unbxd platform and implement all search related functionality with ease.                                                                                                                                                  |
| Autosuggest           | For autocompletion of search queries and showcasing products relevant to query as you type.                                                                                                                                                               |
| Browse                | Allows you to interact with the Unbxd platform and implement all category related functionality with ease. You can customize the experience on various pages – Category, Brand, or any other attribute by leveraging various built-in features of Browse. |
| Recommendations       | Allows you to integrate the Unbxd recommendations widgets that showcase personalized product suggestions to visitors on every page of your eCommerce store.                                                                                               |

# Unbxd SDK for iOS

The Unbxd SDK implements support for making network calls to the Unbxd platform and lets you easily configure and integrate Unbxd Site Search in your eCommerce application.

## Features

The following features are currently supported with Unbxd SDK.

| Features                | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| Analytics               | Allows you to track various visitor events on the eCommerce store such as product clicks, add to cart, orders, etc. |
| Unbxd Commerce Search   | Allows you to interact with the Unbxd platform and implement all search related functionality with ease. |
| Autosuggest             | For autocompletion of search queries and showcasing products relevant to query as you type. |
| Browse                  | Allows you to interact with the Unbxd platform and implement all category related functionality with ease. You can customize the experience on various pages – Category, Brand, or any other attribute by leveraging various built-in features of Browse. |
| Recommendations         | Allows you to integrate the Unbxd recommendations widgets that showcase personalized product suggestions to visitors on every page of your eCommerce store. |

## Prerequisites

Before you get started with the integration, you need to:

- **Get your Site Key**: Set up your Unbxd account and obtain an API key, Site key. These keys are generated at the time of account creation and can be accessed within Console at **Manage > Configure Site > Keys**.
- **Upload your Product catalog**: A product catalog contains product-specific information for products in your inventory, like, title, price, category, color, description, availability, etc. Unbxd product discovery algorithms rely on the products and their fields within your feed data. You need to upload your catalog as a single JSON file.

For more information on product feed, see [here](https://unbxd.com/docs).

## Dependencies

- **Alamofire** 5.1.3 or above – Alamofire is a Swift-based HTTP networking library for iOS and Mac OS X.
- **CocoaLumberjack** 3.4.1 or above – Logging framework.

## Supported Platforms

Unbxd SDK is a dynamic framework programmed using Swift 4. This can be integrated with iOS applications with version 9.0 and above. The Framework is compatible with both Swift and Objective-C.

## Installation

Cocoapods is an application level dependency manager for Cocoa projects. It provides a standard format for managing external libraries. You can install it with the command below:

```bash
$ gem install cocoa pods
```

To integrate UnbxdSDK into your Xcode project using Cocoapods, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'  
source 'https://github.com/unbxd/iOS-SDK-Pod.git'  
platform :ios, '10.0'

target 'demo-unbxd' do  
  use_frameworks!
  pod 'Unbxd'
end 
```

Run the command below:

```bash
$ pod install
```

## Initialization

To begin, you will need to initialize the client. Import UnbxdSDK framework as below:

```swift
import Unbxd 
```

UnbxdSDK is initialized with an API key and Site key.

```swift
let client = Client(siteKey: "<SITE-KEY>", apiKey: "<API-KEY>", logsConfig: LogsConfig)
```

**LogsConfig** – Used to configure log level and provide folder path where log file to be saved. Example:

```swift
let logsFolderPath = "\(NSHomeDirectory())/Documents"  
LogsConfig(logLevel: .verbose, folderPath: logsFolderPath) 
```

All the SDK methods are invoked on a shared instance of `UbClient`.

**IMPORTANT**: We advise you to use your API Key in encrypted form on your frontend and never share it with anyone.

## Unbxd Analytics

The actions a shopper takes on your eCommerce store are known as Events. Tracking visitor analytics and behavior is essential to provide accurate and shopper-specific search and category page results while also demonstrating the value our solutions have on your business.

Unbxd Analytics tracks the following events:

- Visitor Logins
- Search Hit
- Category Page Hit
- Product Click
- Add to Cart
- Successful Orders
- Product Page View
- Cart Removal
- AutoSuggest
- Recommendation Widget Impression
- Search Impression
- Category Page Impression
- Dwell time (indicates time spent on a product page)

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

- **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first-time or a repeat shopper. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
- **query**: search query typed by a shopper in case products listing page shows the result of search event. “Shirt” in the above example.

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

- **UID**: The SDK will generate a randomized unique identifier (UID) to every unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **withCategories**: The unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page. for instance, If you have integrated category pages using the API call: `https://search.unbxd.io/api-key/site-key/category?p=categoryName` then `categoryQuery` will be called as:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["categoryName"])
```

but if you have integrated category pages using the API call: `https://search.unbxd.io/api-key/site-key/category?p=category:categoryName` then `categoryQuery` will be called as:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["category:\(categoryName)"]) 
```

- **pageType**: Its an enum defined in SDK. it accepts the following values:
  - URL
  - CATEGORY_PATH
  - TAXONOMY_NODE
  - ATTRIBUTE
  - BOOLEAN
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.

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

- **UID**: The SDK will generate a randomized unique identifier – UID to every unique user, who installs your application and it would be used to identify the user as first-time or a repeat shopper. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **query**: search query typed by a shopper in case products listing page shows the result of search event.
- **pageId**: The unique identifier for the page passed in the category page API as parameter ‘p’ in case of products listing page shows the result of Category pages.
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
- **boxType**: Recommendation widget clicked in case product is clicked from Recommendation Widget. Possible Values are:

| Widget Type              | Box Type                   |
|--------------------------|----------------------------|
| Recommended For You      | RECOMMENDED_FOR_YOU        |
| Recently Viewed          | RECENTLY__VIEWED           |
| More Like These          | MORE_LIKE__THESE           |
| Viewed also Viewed       | ALSO__VIEWED               |
| Bought also Bought       | ALSO__BOUGHT               |
| Cart Recommendations     | CART__RECOMMEND            |
| HomePage Top Sellers     | TOP__SELLERS               |
| Category Top Sellers     | CATEGORY__TOP__SELLERS     |
| PDP Top Sellers          | PDP__TOP__SELLERS          |
| Brand Top Sellers        | BRAND__TOP__SELLERS        |

### Tracking Add to Cart Event

Whenever a user adds a product to his cart, a ‘cart’ action is generated.

Example:

```swift
let addToCartAnalytics = ProductAddToCartAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, productID: "2301609", variantId: "231221", quantity: 2)
client.track(analyticsDetails: addToCartAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

- **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **requestId**: The Unbxd request id returned in the search/category page/recommendations API call response.
- **variantId**: The unique identifier of the variant being added.
- **quantity**: Quantity of the product added to the checkout bag.
- **productID**: SKU ID of the product.

### Tracking Order Event

An ‘order’ event will be fired after an order completes when the user comes back to the product page from the payment gateway. If a user buys multiple products in a single order, then multiple order events should be fired.

Example:

```swift
let orderAnalytics = ProductOrderAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, productID: "2301609", price: 20.5, quantity: 3)
client.track(analyticsDetails: orderAnalytics, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

- **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
- **variantId**: The unique identifier of the variant being added.
- **quantity**: Quantity of the product added to the checkout bag.
- **productID**: SKU ID of the product.

### Tracking Product Display Event

Product Display Page View is fired when a user visits a Product Display Page.

Example:

```swift
let productDisplayPageAnalytics = ProductDisplayPageViewAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, skuId: "2034")
client.track(analyticsDetails: productDisplayPageAnalytics, completion: {(response, httpResponse, err) -> Void in
    //Handle response
})
```

- **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
- **SKUID**: SKU ID of the product.

### Cart Removal Event

Cart Removal event is fired when a product in the cart is removed.

Example:

```swift
let cartRemovalAnalytics = CartRemovalAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, skuId: "2034", variantId: "231221", quantity: 2)
client.track(analyticsDetails: cartRemovalAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

- **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
- **variantId**: The unique identifier of the variant being removed.
- **quantity**: Quantity of the product removed.
- **SKUID**: SKU ID of the product.

### Autosuggest Event

An autosuggest event is fired when a user types something, then clicks on any of the autosuggest results shown.

Example:

```swift
let autoSuggestAnalytics = AutoSuggestAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, skuId: "2034", query: "Red Socks", docType: "IN_FIELD", internalQuery: "red", fieldValue: "Red socks", fieldName: "infield1", sourceField: "color type", unbxdPrank: 6)
client.track(analyticsDetails: autoSuggestAnalytics, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

- **UID**: The SDK will generate a randomized unique identifier (UID) to each unique user, who installs your application and it would be used to identify the user as a first-time or a repeat shopper. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
- **query**: Autosuggest suggestion returned by Unbxd.
- **docType**: It can be `IN_FIELD`, `POPULAR_PRODUCTS`, `TOP_SEARCH_QUERIES`, `KEYWORD_SUGGESTION`, `PROMOTED_SUGGESTIONS`.
- **internalQuery**: Query for which autosuggest results were generated.
- **fieldValue**: Set when autosuggest_type is `IN_FIELD`. Set to the value of the “infield” in unbxd response. It is set to null otherwise.
- **fieldName**: Set when autosuggest_type is `IN_FIELD`. Name of the autosuggest field in the search response. It is set to null otherwise.
- **sourceField**: Name of the fields present in the catalog on the combination of which in fields are generated. It is set when autosuggest_type is not null.
- **skuId**: SKU id of the product. It is set non-null when autosuggest_type is `POPULAR_PRODUCTS`.
- **unbxdPrank**: unbxdPrank is the position of selected suggestion the list of items/suggestions received in Autosuggest response.

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

- **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor. This distinct ID is saved to the storage device so that it will persist across sessions.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
- **recommendationType**: Specifies the type of recommendation widget. For different permissible values, refer the table below.

| Widget Type              | Box Type                   |
|--------------------------|----------------------------|
| Recommended For You      | RECOMMENDED_FOR_YOU        |
| Recently Viewed          | RECENTLY__VIEWED           |
| More Like These          | MORE_LIKE__THESE           |
| Viewed also Viewed       | ALSO__VIEWED               |
| Bought also Bought       | ALSO__BOUGHT               |
| Cart Recommendations     | CART__RECOMMEND            |
| HomePage Top Sellers     | TOP__SELLERS               |
| Category Top Sellers     | CATEGORY__TOP__SELLERS     |
| PDP Top Sellers          | PDP__TOP__SELLERS          |
| Brand Top Sellers        | BRAND__TOP__SELLERS        |

- **productIds**: The unique identifier of the products rendered.

### Search Impression

A search impression event is fired when a search results page loads for the first time, and whenever results changes on applying pagination, auto scroll, sort, and filters. For each of these actions, the unique IDs of the products visible on the search page should be sent as payload.

Example:

```swift
let searchImpressionAnalytics = SearchImpressionAnalytics(uid: userId.id, visitType: userId.visitType, requestId: requestId, query: "Shoes", productIds: ["1692741-1758","01692015-285","1692908-480"])
client.track(analyticsDetails: searchImpressionAnalytics, completion: {(response, httpResponse, err) -> Void in
})
```

- **action**: `search_impression`.
- **pids_list**: List of product ids of products visible in the window when the event occurs.
- **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.

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

- **UID**: The SDK will generate a randomized unique identifier – UID to each unique user, who installs your application and it would be used to identify the user as first time visitor or a repeat visitor.
- **visitType**: This information is extracted from a ‘visitor’ cookie setup by SDK. Its value can be either ‘first-time’ or ‘repeat’.
- **withCategories**: unique identifier for the page passed in the category page API as parameter ‘p’ in case of Category Page. For instance, if you have integrated category pages using the API call: `https://search.unbxd.io/api-key/site-key/category?p=categoryName` then categoryQuery will be called as:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["categoryName"])
```

If you have integrated category pages using the API call: `https://search.unbxd.io/api-key/site-key/category?p=category:categoryName` then `categoryQuery` will be called as:

```swift
let categoryQuery = CategoryNamePath(withCategories: ["category:\(categoryName)"])  
```

- **pageType**: It is an enum defined in SDK. It accepts the following values:
  - URL
  - CATEGORY_PATH
  - TAXONOMY_NODE
  - ATTRIBUTE
  - BOOLEAN
- **requestId**: The unbxd request id returned in the search/category page/recommendations API call response.
- **pids_list**: List of product ids of products visible in the window when the event occurs.

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

## Unbxd Commerce Search

Unbxd Site Search is an e-commerce search platform that enhances your on-site search to deliver fast, relevant, and tailored search results to visitors on your website/mobile application. Unbxd Site Search is platform-agnostic, which makes it incredibly versatile and easily implementable.

For more information, see [here](https://unbxd.com/docs).

### Using Search Method

Search methods perform a search with key and a few other parameters. The search key is the mandatory argument and rest is applied for different criteria.

Query method signature:

```swift
init(key: String, rows: Int? = nil, start: Int? = nil, format: ResponseFormat = .JSON, spellCheck: Bool = false, analytics: Bool = true, statsField: String? = nil, variant: Variant? = nil, fields: Array? = nil, facet: Facet? = nil, filter: FilterAbstract? = nil, categoryFilter: CategoryFilterAbstract? = nil, multipleFilter: MultipleFilterAbstract? = nil, fieldsSortOrder: Array? = nil, personalization: Bool? = nil)
```

Search method signature:

```swift
func search(query: SearchQuery, completion: @escaping (_ response: Dictionary<String, Any>?, _ httpResponse: HTTPURLResponse?, _ error: Error?) -> Void) {  
    // Handle response or request
}
```

Keywords marked in bold are different arguments for the search method. ‘query’ of type ‘SearchQuery’ is mandatory argument and rest are optional which are used as needed. SearchQuery consists of searchKey parameter with a few other parameters. Let’s see how these arguments can be composed and passed in search() method invocation.

#### Search Query

SearchQuery consists of a searchKey parameter with other parameters. Invoking Search method with key:

```swift
let query = SearchQuery(key: "Shirt")
client.search(query: query, completion: { (response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Format

The format parameter specifies the format of the response. Possible values are ‘JSON’ or ‘XML’. It is an optional parameter and the default value is ‘JSON’.

```swift
let query = SearchQuery(key: "Shirt", format: .XML)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Start

The start parameter is used to offset the results by a specific number. It indicates offset in the complete result set of the products. It is an optional parameter and the default value is 0.

```swift
let query = SearchQuery(key: "Shirt", start: 2, format: .JSON)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Rows

The rows parameter is used to paginate the results of a query. It indicates the number of products on a single page. It is an optional parameter and the default value is 10, the maximum value is 100.

```swift
let query = SearchQuery(key: "Shirt", rows: 20)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Spellcheck

The spellcheck feature provides spelling suggestions or spell-checks for misspelled search queries.

```swift
let query = SearchQuery(key: "Shirt", spellCheck: true)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Analytics

The analytics parameter enables or disables tracking the query hit for analytics. By default, tracking is enabled.

```swift
let query = SearchQuery(key: "Shirt", analytics: false)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Stats

The stats parameter gives information about the products with the highest and lowest field value.

```swift
let query = SearchQuery(key: "Shirt", statsField: "price")
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Variants

Products in the feed can be available in different sizes, colors, styles, materials, etc. For example, a dress can be available in different sizes, colors and/or styles.

```
Variant 1: Color – Blue, Size: Small, Style – Solid print
Variant 2: Color – Red, Size: Small, Style – Solid print
Variant 3: Color – Blue, Size: Large, Style – Polka-dot
```

Variants parameter enables or disables variants in the API response. It can take two values: “true” or “false”. Default value is “false”.

Examples:

```json
{
    "feed": {
        "catalog": {
            "schema": [{
                "fieldName": "vColor",
                "id": "76678",
                "dataType": "text",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }, {
                "fieldName": "vSize",
                "dataType": "text",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }, {
                "fieldName": "vImages",
                "dataType": "link",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }, {
                "fieldName": "vPrice",
                "dataType": "decimal",
                "multiValue": "true",
                "autoSuggest": "false",
                "isVariant": "true"
            }]
        }
    }
}
```

Example: Search with variants:

Variants parameter enables or disables variants in the API response. It can take two values: “true” or “false”. Default value is “false”.

```swift
let query = SearchQuery(key: "Shirt", variant: Variant(has: true, count: 2))  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If you want to get more than one variants in the API response, you can use variantCount parameter. It can have any numerical value (for example, 1, 2, 3, etc) or “.max” (to get all the variants).

#### Fields

The fields parameter is used to specify the set of fields to be returned as the response, otherwise, all the fields will be returned in the response by default.

For more information, see [here](https://unbxd.com/docs) (Request Parameters section).

Example: Search:

The fields parameter is used to specify the set of fields to be returned. When returning the results, only fields in the list will be included.

```swift
let query = SearchQuery(key: "Shirt", fields: ["title","vPrice"])
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Facets

Facets are filters in the UI that allow visitors to narrow down result set based on product fields. It is usually known as Layered Navigation or Guided Navigation. Facets can be easily configured from the SDK.

Facets can be of three types:

- **Multi-level**: Facets on categories. For a given API response, multi-level facets would represent the top-most categories those products lie under.
- **Text**: Facets on text fields in the feed. For example, color, brand, etc.
- **Range**: Facets on numeric fields in the feed. For example, price, discount, etc.

Example: Search with multi-level Facets:

```swift
let query = SearchQuery(key: "Shirt", facet: .MultiLevel)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

Example: Search with multi-select Facets:

This feature enables or disables the option to select multiple values within a facet or across facets for visitors. For example, for a query “red dress”, facets of gender and size fields are displayed. If the value for facet.mult is selected is set as true and if a visitor selects Women in the Gender Facet, the search results will be refined according to the selection. However, all values in the gender facet will still be sent in the response as if the gender filter isn’t applied (and other filters are applied, if any).

```swift
let query = SearchQuery(key: "Shirt", facet: .MultiSelect)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

Example: Search with the selected facet with field ID and value ID:

```swift
let query = SearchQuery(key: "Shirt", facet: .Selected(IdFilter(field: "76678", value: "5001")))
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

Selected facet with field name and value name:

```swift
let query = SearchQuery(key: "Shirt", facet: .Selected(NameFilter(field: "Brand_uFilter", value: "Vince Camuto")))
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Filtering

A filter is used to restrict the products based on criteria passed. Three types of filters are supported:

- **Text**: It is used to filter products based on fields with string values such as color, gender, brand, etc. It can be defined in the API call in two ways:

  **Using Field Ids**:

  `IdFilter` can be formed with 2 parameters.

  ```swift
  field: The id of the field on which the text filter is applied.
  value: The id of the value on which the results are filtered.
  ```

  Example:

  ```swift
  let query = SearchQuery(key: "Shirt", filter: IdFilter(field: "76678", value: "5001"))
  client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
      //Handle response
  })
  ```

  **Using Field Names**:

  `NameFilter` can be formed with 2 parameters.

  ```swift
  type: The id of the field on which the text filter is applied.
  value: The id of the value on which the results are filtered.
  ```

  ```swift
  let query = SearchQuery(key: "Shirt", filter: NameFilter(field: "vColor_uFilter", value: "Black"))
  client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
      //Handle response
  })
  ```

- **Range**: It is used to filter products based on fields with data types – date, number or decimal. It can be defined in the API in two ways:

  **Using Field Names**:

  Filter Range of type id is built using `IdFilterRange` class and it can be initialized with below parameters.

  ```swift
  field: The id of the field on which the text filter is applied.
  lower: The id of the lower limit of the range.
  upper: The id of the upper limit of the range.
  ```

  Example:

  ```swift
  let query = SearchQuery(key: "Shirt", filter: IdFilterRange(field: "76678", lower: "2034", upper: "8906"))
  client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
      //Handle response
  })
  ```

  **Using Field Name**:

  Filter Range of type name is built using `NameFilterRange` class and it can be initialized with below parameters.

  ```swift
  field: The name of the field on which the text filter is applied.
  lower: The name of the lower limit of the range.
  upper: The name of the upper limit of the range.
  ```

  Example:

  ```swift
  let query = SearchQuery(key: "Shirt", filter: NameFilterRange(field: "vColor", lower: "red", upper: "blue"))
  client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
      //Handle response
  })
  ```

- **Multilevel**: It is used to filter products based on categories.

Each of the three filters can filter on field-name and field-id. Field-id/field-name is an optional parameter. If passed, it eliminates those products that do not match the criteria.

**NOTE**: If IDs are present in the feed, filtering should be done on IDs only.

The multilevel filter is used to filter products based on categories. It can be defined in the API call in two ways:

**Using Field Ids**:

`CategoryIdFilter` is used to filter the results using category path comprised of category IDs.

Example:

```swift
let categoryNameFilter = CategoryNameFilter()  
categoryNameFilter.categories.append("Fashion")  
categoryNameFilter.categories.append("Shirts")
let query = SearchQuery(key: "Shirt", categoryFilter: categoryNameFilter)
client.search(query: query, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

#### Search with Multiple Filters using Field ID/Field Name

Multiple Filters: Multiple facets can be selected, which applies corresponding filters in a single call. There are two types of filter operations:

- AND
- OR

**Search with multiple filters using AND and field ID/field name**:

`MultipleIdFilter` takes two parameters, fieldType Id and fieldValue id.

`MultipleNameFilter` takes two parameters, fieldType name, and fieldValue name.

Multiple filters can be added and `operatorType` is set to ‘AND’.

```swift
// Using field ID
let multipleIdFilter = MultipleIdFilter.init()
multipleIdFilter.operatorType = .AND
multipleIdFilter.filters.append(IdFilter.init(withFieldType: "76678", fieldValue: "5001"))
multipleIdFilter.filters.append(IdFilter.init(withFieldType: "76678", fieldValue: "5021"))
client?.searchWithQuery(query: searchQuery, multipleFilter: multipleIdFilter, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response 
})
```

OR

```swift
// Using field name
let multipleNameFilter = MultipleNameFilter.init()
multipleNameFilter.operatorType = .AND
multipleNameFilter.filters.append(NameFilter.init(withFieldType: "vColor_uFilter", fieldValue: "Black"))
multipleNameFilter.filters.append(NameFilter.init(withFieldType: "vColor_uFilter", fieldValue: "White"))  
client?.searchWithQuery(query: searchQuery, multipleFilter: multipleNameFilter, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response 
})
```

**Search with multiple filters using OR and field ID/field name**:

`MultipleIdFilter` takes two parameters, fieldType Id and fieldValue id.

`MultipleNameFilter` takes two parameters, fieldType name, and fieldValue name.

Multiple filters can be added and `operatorType` is set to ‘OR’.

```swift
// Using field ID
let multipleIdFilter = MultipleIdFilter()  
multipleIdFilter.operatorType = .OR  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5001"))  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5021"))  
let query = SearchQuery(key: "Shirt", multipleFilter: multipleIdFilter)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})    
```

OR

```swift
// Using field name
let multipleNameFilter = MultipleNameFilter()  
multipleNameFilter.operatorType = .OR  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "Black"))  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "White"))  
let query = SearchQuery(key: "Shirt", multipleFilter: multipleIdFilter)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Sorting

The sort parameter is used to rank the products based on specified fields in the specified order. You can sort on a single field or in multiple fields.

**Search with sorting on the single field/multiple fields**:

- **fieldName**: The field on which the sort is applied.
- **sortOrder**: The order in which the sort is applied. This value can be “ASC” (for ascending) or “DSC” (for descending).

```swift
// single field
var fieldsWithOrder = Array()  
fieldsWithOrder.append(FieldSortOrder(field: "price", order: .ASC))  
let query = SearchQuery(key: "Shirt", fieldsSortOrder: fieldsWithOrder)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// multiple fields hence 2 or more FieldSortOrder instances are added
var fieldsWithOrder = Array()  
fieldsWithOrder.append(FieldSortOrder(field: "price", order: .ASC))  
fieldsWithOrder.append(FieldSortOrder(field: "title", order: .DSC))  
let query = SearchQuery(key: "Shirt", fieldsSortOrder: fieldsWithOrder)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Spellcheck

The spellcheck feature provides spelling suggestions or spell-checks for misspelled search queries. In such cases, the context-aware algorithm of Unbxd understands your visitor’s intent and sends a “Did You Mean” response along with search result set for the query, if any.

```swift
let query = SearchQuery(key: "Shirt", spellCheck: true)  
client.search(query: query, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

## Unbxd Autosuggest

The Autosuggest feature provides query suggestions, which helps your visitors to search faster in your site. Unbxd supports autocompletion of search queries and showcasing products relevant to query as they type.

Unbxd Autosuggest comprises of different types of suggestions that are known as doctypes. A standard Unbxd Autosuggest is segmented into five doctypes:

| Features              | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| **In-fields**         | The In-fields doctype suggest groups of relevant products along with their associated field values the query may belong to. These field values can be categories, brands, occasion, etc. For example, a visitor types ‘Sh’, the In-field doctype will have the following suggestions:  - Shirts - In Men (based on gender) - In Nike (based on brand)  - In Blue (based on occasion) |
| **Keyword Suggestions** | These are intelligent suggestions generated by Unbxd based on the query being typed and suggests relevant products based on your product feed accordingly. For example, a visitor types ‘Sh', the keyword suggestions doctype will have the following suggestions:  - Shirts - Shorts - Shoes - Shapewear |
| **Top Queries**      | This doctype displays the frequently searched queries in your e-commerce store populated with the help of Unbxd Analytics, which keeps a track of your store. |
| **Popular Products** | This doctype displays popular products with thumbnail images. Similar to Top Queries doctype, to render Popular products, Unbxd analytics needs to be integrated in your e-commerce store. |
| **Promoted Suggestions** | These are documents that a customer can configure directly from merchandising console. For example, if a customer configures “jogging shoes” and “running shoes” as promoted suggestions, and a shopper searches for “sh”, the intended results are returned. |

### Using Autosuggest Methods

Autosuggest method signature:

```swift
func search(query: SearchQuery, completion: @escaping (_ response: Any?, _ error: Error?) -> Void) {  
    // Handle response    
}
```

The query of type `AutoSuggestQuery` is mandatory and the rest of the arguments are optional. Below are a few samples of invoking `autoSuggest()` method with different arguments.

Query method signature:

```swift
init(withKey: String, format: ResponseFormat = .JSON, inField: DocTypeInField? = nil, keywordSuggestions: DocTypeKeywordSuggestions? = nil, topQueries: DocTypeTopQueries? = nil, promotedSuggestions: DocTypePromotedSuggestions? = nil, popularProducts: DocTypePopularProducts? = nil, variant: Variant? = nil, filter: FilterAbstract? = nil)  
```

Autosuggest method invocation:

`AutoSuggestQuery` can be initialized with ‘Key’ for suggestions are expected.

```swift
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir")  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Examples

**Autosuggest Query**:

```swift
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir")  
client.autoSuggest(query: autoSuggestQuery, completion: {(response, httpResponse, err) -> Void in  
    //Handle response
})
```

**Autosuggest with various doctypes**:

If `resultsCount` is not set, default value 2 will be considered.

**In Fields**: The query being typed by your visitor can belong to multiple product categories based on your product feed. The In-fields doctype in Autosuggest suggests groups of relevant products along with their associated field values the query may belong to. In Field doctype with result count can be configured as shown below:

```swift
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypeInField(resultsCount: 3))  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If `resultsCount` is not set, default value 2 will be considered as results count for inField doctype.

**Keyword Suggestions**:

These are intelligent suggestions generated by Unbxd cloud servers whose algorithm identifies the keywords from the query being typed and suggests relevant products based on your product feed accordingly.

Keyword Suggestions doctype with result count can be configured as shown below:

```swift
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypeKeywordSuggestions(resultsCount: 4))  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If `resultsCount` is not set, default value 2 will be considered as results count for Keyword Suggestions doctype.

**Top Queries**:

As the name suggests, this autosuggest doctype displays the frequently searched queries in your eCommerce store. These top queries are populated with the help of Unbxd Analytics which keeps a track of your store.

Top Queries doctype with result count can be configured as shown below:

```swift
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypeTopQueries(resultsCount: 3))  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If `resultsCount` is not set, default value 2 will be considered as results count for Top Queries doctype.

**Promoted Suggestions**:

Promoted Suggestions are documents that a customer can configure directly from merchandising console. This gives you the flexibility to manually insert keyword suggestions in autosuggest which may not be part of the default relevance results.

Promoted Suggestions doctype with result count can be configured as shown below:

```swift
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypePromotedSuggestions(resultsCount: 5))  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If `resultsCount` is not set, default value 2 will be considered as results count for Promoted Suggestions doctype.

**Popular Products**:

The Popular Products doctype displays popular product in your e-commerce store with thumbnail images.

Popular Products doctype with fields and result count can be configured as shown below:

```swift
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypePopularProducts(resultsCount: 3, fields: ["vColor","price"]))  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If `resultsCount` is not set, default value 3 will be considered as results count for Promoted Suggestions doctype.

#### Autosuggest with Filters

Filters are used in the `AutoSuggest` method to restrict the products based on criteria passed.

Two types of filters are supported in `autoSuggestWithQuery()` method:

- **Text**: It is used to filter products based on fields with string values such as color, gender, brand, etc.
- **Range**: It is used to filter products based on fields with data types – date, number/decimals.

Each of these filters can filter on field-name and field-id. Field-id/field-name is an optional parameter. If passed, it eliminates those products that do not match the criteria.

**NOTE**: If IDs are present in the feed, filtering should be done on IDs only.

**Autosuggest with text filter using field ID/field name**:

“filter-id” is used to filter the results using field-id. Using Field IDs, ‘IdFilter’ can be formed with two parameters:

- **fieldID**: The id of the field on which the text filter is applied.
- **field**: The id of the value on which the results are filtered.

```swift
// Using Field ID
let idFilter = IdFilter(field: "76678", value: "5001")  
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypeKeywordSuggestions(resultsCount: 4), filter: idFilter)  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// Using Field Name
let nameFilter = NameFilter(field: "vColor_uFilter", value: "Black")  
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypeKeywordSuggestions(resultsCount: 4), filter: nameFilter)  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Autosuggest with Range filter using field ID/field name**:

“filter-id” is used to filter the results using field-id. Using Field IDs, ‘IdFilter’ can be formed with two parameters:

- **fieldID**: The id of the field on which the text filter is applied.
- **field**: The id of the value on which the results are filtered.

```swift
// Using Field ID
let idRange = IdFilterRange(field: "76678", lower: "2034", upper: "8906")  
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypeKeywordSuggestions(resultsCount: 4), filter: idRange)  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// Using Field Name
let nameRange = NameFilterRange(field: "vColor", lower: "red", upper: "blue")  
let autoSuggestQuery = AutoSuggestQuery(withKey: "Shir", docType: DocTypeKeywordSuggestions(resultsCount: 4), filter: nameRange)  
client.autoSuggest(query: autoSuggestQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

## Unbxd Browse

The SDK lets you customize your page experience by leveraging various built-in features of Browse. You can also power any type of page, such as Category, Brand, or any other attribute.

### Using Browse Method

Browse methods operate on Category fields query which is configured part of Browse Query.

Query method signature:

```swift
init(categoryQuery: CategoryAbstract, rows: Int? = nil, start: Int? = nil, format: ResponseFormat = .JSON, spellCheck: Bool = false, analytics: Bool = false, statsField: String? = nil, variant: Variant? = nil, fields: Array? = nil, facet: Facet = .None, filter: FilterAbstract? = nil, categoryFilter: CategoryFilterAbstract? = nil, multipleFilter: MultipleFilterAbstract? = nil, fieldsSortOrder: Array? = nil)
```

Browse method signature:

```swift
func browse(query: BrowseQuery, completion: @escaping (_ response: Any?, _ error: Error?) -> Void)
```

#### Browse with Page Name/Page ID

`BrowseQuery` consists of Category path or field details parameter and few other optional parameters.

It is mandatory to pass either page name or page ID. If both are passed together, page name would be ignored and results would be shown as per page ID. The value passed under page ID (or page name) is displayed in the Unbxd Console and analytics reports as-it-is.

```swift
// With Page name
let categoryQuery = CategoryIdPath(withCategories: ["Fashion","Shoes","Sneakers","Athletic shoes"])  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// With Page ID                        
let categoryQuery = CategoryIdPath(withCategories: ["FA","FA0484"])  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// With Field ID    
let categoryQuery = CategoryIdPath(withCategories: ["FA","FA0484"])  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// With Field name
let categoryQuery = CategoryNameFields(field: "vColor", value: "Black")  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Example: Browse with Variants

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, variant: Variant(has: true, count: 2))
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

If you want to get more than one variants in the API response, you can use the `Count` parameter. It can have any numerical value (for example, 1, 2, 3, etc) or “.max” (to get all the variants).

#### Fields

The fields parameter is used to specify the set of fields to be returned as the response, otherwise, all the fields will be returned in the response by default.

**Browse with selected fields**:

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, fields: ["title","vPrice"])
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Facets

Facets are the filters in the UI that allow visitors to narrow down result set based on product fields. It is usually known as Layered Navigation or Guided Navigation. Facets can be easily configured from the **Manage -> Configure Browse -> Configure Facet** section of the Console.

Facets can be of three types:

- **Multi-level**: Facets on categories. For a given API response, multi-level facets would represent the top-most categories those products lie under.
- **Text**: Facets on text fields in the feed. For example, color, brand, etc.
- **Range**: Facets on numeric fields in the feed. For example, price, discount, etc.

**Browse with multi-level facets**:

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, facet: .MultiLevel)
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with multi-select facets**:

This feature enables or disables the option to select multiple values within a facet or across facets for visitors.

For example, for a query “red dress”, facets of gender and size fields are displayed. If the value for `facet.multiselect` is set as true and if a visitor selects Women in the Gender facet, the Browse results will be refined according to the selection. However, all values in the gender facet will still be sent in the response as if the gender filter isn’t applied (and other filters are applied, if any).

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, facet: .MultiSelect)
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with the selected facet with field ID and value ID**:

```swift
// With Field ID, Value ID
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, facet: .Selected(IdFilter(field: "76678", value: "5001")))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// With Field Name, Value Name
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, facet: .Selected(NameFilter(field: "Brand_uFilter", value: "Vince Camuto")))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Filtering

A filter is used to restrict the products based on criteria passed. Three types of filters are supported:

- **Text**: It is used to filter products based on fields with string values such as color, gender, brand, etc.
- **Range**: It is used to filter products based on fields with data types – date, number or decimal.
- **Multilevel**: It is used to filter products based on categories.

Each of the three filters can filter on field-name and field-id. Field-id/field-name is an optional parameter. If passed, it eliminates those products that do not match the criteria.

**NOTE**: If IDs are present in the feed, filtering should be done on IDs only.

**Browse with text filter using field ID/field name**:

“filter-id” is used to filter the results using field-id. Using Field IDs, ‘IdFilter’ can be formed with two parameters:

- **Field**: The id/name of the field on which the text filter is applied.
- **Value**: The id/name of the value on which the results are filtered.

```swift
// Using field ID
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, filter: IdFilter(field: "76678", value: "5001"))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// Using field name
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, filter: NameFilter(field: "vColor_uFilter", value: "Black"))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with Range filter using field ID/field name**:

Range filter is built using `FilterIdRange` class and it can be initialized with parameters below.

- **field**: The id/name of the field on which the text filter is applied.
- **lower**: The id of the lower limit of the range.
- **upper**: The id of the upper limit of the range.

```swift
// Using field ID
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, filter: IdFilter(field: "76678", value: "5001"))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// Using field name
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, filter: NameFilter(field: "vColor_uFilter", value: "Black"))  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with Multi-level filter using field ID/field name**:

`CategoryIdFilter` is used to filter the results using a category path comprised of category IDs.

`CategoryNameFilter` is used to filter the results using a category path comprised of category Names.

```swift
// Using field ID
let categoryIdFilter = CategoryIdFilter()  
categoryIdFilter.categories.append("FA")  
categoryIdFilter.categories.append("A0485")  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, categoryFilter: categoryIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// Using field name
let categoryNameFilter = CategoryNameFilter()  
categoryNameFilter.categories.append("Fashion")  
categoryNameFilter.categories.append("Shirts")  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, categoryFilter: categoryNameFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
}) 
```

**Browse with Multiple filters using field ID/field name**:

Multiple Filters: Multiple facets can be selected which applies corresponding filters in a single call. There are two types of filter operations:

- AND
- OR

**Browse with multiple filters using AND and field ID/field name**:

`MultipleIdFilter` takes two parameters, field Id and Value id.

`MultipleNameFilter` takes two parameters, field name and Value name.

Multiple filters can be added and `operatorType` is set to ‘AND’.

```swift
// Using field ID
let multipleIdFilter = MultipleIdFilter()  
multipleIdFilter.operatorType = .AND  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5001"))  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5021"))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, multipleFilter: multipleIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})    
```

OR

```swift
// Using field name
let multipleNameFilter = MultipleNameFilter()  
multipleNameFilter.operatorType = .AND  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "Black"))  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "White"))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, multipleFilter: multipleIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

**Browse with multiple filters using OR and field ID/field name**:

`MultipleIdFilter` takes two parameters, field Id and Value id.

`MultipleNameFilter` takes two parameters, field name and Value name.

Multiple filters can be added and `operatorType` is set to ‘OR’.

```swift
// Using field ID
let multipleIdFilter = MultipleIdFilter()  
multipleIdFilter.operatorType = .OR  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5001"))  
multipleIdFilter.filters.append(IdFilter(field: "76678", value: "5021"))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, multipleFilter: multipleIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})    
```

OR

```swift
// Using field name
let multipleNameFilter = MultipleNameFilter()  
multipleNameFilter.operatorType = .OR  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "Black"))  
multipleNameFilter.filters.append(IdFilter(field: "vColor_uFilter", value: "White"))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, multipleFilter: multipleIdFilter)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Sorting

The sort parameter is used to rank the products based on specified fields in the specified order. You can sort on a single field or in multiple fields.

For more information, see [here](https://unbxd.com/docs) (Request Parameters section).

**Browse with sorting on the single field/multiple fields**:

- **field**: The field on which the sort is applied.
- **Order**: The order in which the sort is applied. This value can be “ASC” (for ascending) or “DSC” (for descending).

```swift
// single field
var fieldsWithOrder = Array()  
fieldsWithOrder.append(FieldSortOrder(field: "price", order: .ASC))  
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, fieldsSortOrder: fieldsWithOrder)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

OR

```swift
// multiple fields hence 2 or more FieldSortOrder instances are added
var fieldsWithOrder = Array()  
fieldsWithOrder.append(FieldSortOrder(field: "price", order: .ASC))  
fieldsWithOrder.append(FieldSortOrder(field: "title", order: .DSC))
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, fieldsSortOrder: fieldsWithOrder)  
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

#### Spellcheck

The spellcheck feature provides spelling suggestions or spell-check for misspelled Browse queries. In such cases, the context-aware algorithm of Unbxd understands your visitor’s intent and sends a “Did You Mean” response along with Browse result set for the query, if any.

```swift
let browseQuery = BrowseQuery(categoryQuery: categoryQuery, spellCheck: true)
client.browse(query: browseQuery, completion: {(response: Any?, error: Error?) -> Void in  
    //Handle response
})
```

## Unbxd Recommendations

Unbxd Recommendations is a set of tailored widgets that showcase personalized product suggestions to visitors on different pages of your online e-commerce store. The widgets are easy to configure and provides a smart way of exposing your inventory to the visitors. These widgets are powered by the Unbxd analytics engine that constantly tracks and records visitor events on your store such as clicks, cart additions, orders, etc. The captured event information is used to build profiles that help our search engine to fetch relevant products for each widget.

The Unbxd SDK supports the following types of widgets:

- Recommended For You
- Recently Viewed
- More Like This
- Viewed also Viewed
- Bought also Bought
- Cart Recommendations
- Top Sellers
- Homepage Top Sellers
- Category Top Sellers
- PDP Top Sellers
- Brand Top Sellers
- Complete the Look

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

- **Fashion vertical**: [https://github.com/unbxd/FashionApp](https://github.com/unbxd/FashionApp)
- **Home Decor App**: [https://github.com/unbxd/HomeDecorApp](https://github.com/unbxd/HomeDecorApp)

## Feedback

Did this answer your question?

- **Yes!**  
  Nice work, I love it.

- **No…**  
  I have some feedback

## Copyright

Copyright 2020 © Unbxd Inc, All Rights Reserved. [Privacy Policy](https://unbxd.com/privacy-policy)