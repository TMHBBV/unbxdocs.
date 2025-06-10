---
title: 'PDP API '
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📘 NOTE
>
> PDP API is not added by default. It has an additional cost to integrate PDP APIs. For any additional queries, reach out to our support team.

The PDP API powers the product display pages on your e-commerce site by returning all the product information associated with a product ID and fetching information for one or more product IDs.

You can either view information for a specific product or a product listing with products linked to different product IDs. If there are variants of a product, PDP API will include the variants info in the response.

<br />

## PDP API Format

To integrate this API, you need to make the following API call to Unbxd servers.

## Authorization

To authorize your calls, add the API key as a header before making the API call.

Authorization: “API\_KEY”

> 📘 NOTE
>
> The authorization for PDP API is different than the search one.

***

### Fetch Product Details Using a Product ID​

You can get products details of a product by calling the sample API.

* Method: **GET**
* End Point: `https://search.unbxd.io/sites/site-key/<API key>/products/`
* Parameter: `product-id`

***

### Fetch Product Details for More Than One Product

You can get the product details of multiple products by using product IDs.

* Method : **GET**
* End Point: `https://search.unbxd.io/sites/site-key/products?id=<product_id1>,<product_id2>`
* Parameter: Comma-separated list of `product-id`

***

### Get Siblings for a Product

You can use the rel feature to find any external relationship for a product. This feature fetches all the related parent products.

* Method: **GET**
* End Point: `https://search.unbxd.io/sites/<sitekey>/products/<id1>?rel.field=<fieldName>`
* Parameter:
  * `product-id`
  * `rel.field={fieldName}`

This returns a list of sibling products' details of a, using the filter field passed as the query parameter.

> 📘 NOTE
>
> While using the rel feature, the variants feature will be disabled.