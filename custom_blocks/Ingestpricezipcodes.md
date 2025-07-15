---
name: Ingestpricezipcodes
---
# Q. Can we ingest price/availability based on zip codes?

A. Unbxd products support omni-channel use cases where the price and availability of the product varies depending upon the location.

There are two approaches to handle price/availability information depending upon region :

1. Option 1 : Suitable when the number of regions are less than 50 (cases where the price/availability varies by states or country)
   * The price/availability information for each region can be passed as separate fields in the catalog
   * At the time of query time, use the location of the user to filter the price/availability
2. Option 2 : Suitable when the number of regions are more than 50 (cases where price varies with zip-codes)
   * The recommended approach in these cases is to use Unbxd APIs to get the list of product  IDs,  then request price/availability of the products using another function while rendering the UI