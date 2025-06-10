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