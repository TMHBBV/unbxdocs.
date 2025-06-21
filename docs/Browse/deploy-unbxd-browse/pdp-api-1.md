---
title: PDP API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The PDP API powers the product display pages on your e-commerce site by returning all the product information associated with a product ID. The PDP API also fetches information for one or more than one product ID.

You can either view information for a specific product or a product listing with products linked to different product ids. If there are variants of a product, PDP API will include the variants info in the response.

## PDP API Format

To integrate this API, you need to make the following API call to Unbxd servers:

### Fetch product details using a product-id

You can get products details of a product by calling the sample API.

* Method : GET
* End Point:

```
https://search.unbxd.io/sites/site-key/products/
```

* Parameter : `product-id`

### Fetch Product details for more than one product

You can get products details of multiple products by using product ID’s.

* Method : `GET`
* End Point:

```
https://search.unbxd.io/sites/site-key/products?id=<product_id1>,<product_id2>
```

* Parameter : Comma separated list of `product-id`

### Get Siblings for a product

You can use the `rel` feature to find any external relationship for a product. This feature fetches all the related parent products.

* Method : GET
* End Point:

```
https://search.unbxd.io/sites/<sitekey>/products/<id1>?rel.field=<fieldName>
```

* Parameter:

  * `product-id`
  * `rel.fields`: The field on which the related products should be matched. The value of this property would be the fieldName.
  * `rel.{fieldName}.fields`: This returns a list of sibling product details of a, using the filter field passed as the query parameter.
  * `rel.{fieldName}.rows`: Number of related products to be returned. The default value is 1 This would have max value (max value yet to be decided)
  * `rel.{fieldName}.filter`: Filters to be applied for relative products. In the case of nested documents, `parent_unbxd: true` would always be added to exclude variants

**NOTE**: While using the `rel` feature, the `variants` feature will be disabled.