---
name: Trannsmitted_unbxd_user_web_browser
---
# Q. Can we ingest price/availability based on zip codes?

A. Unbxd products support omnichannel use cases where the price and availability of the product vary depending on the location.

There are two approaches to handling price/availability information depending on the region:

**Option 1**: Suitable when the number of regions is less than 50 (cases where the price/availability varies by states or country)

* The price/availability information for each region can be passed as separate fields in the catalog
* At the time of query, use the location of the user to filter the price/availability

**Option 2**: Suitable when the number of regions is more than 50 (cases where price varies with zip-codes)

* The recommended approach in these cases is to use Unbxd APIs to get the list of product  IDs,  then request the price/availability of the products using another function while rendering the UI