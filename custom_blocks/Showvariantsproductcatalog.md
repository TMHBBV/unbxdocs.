---
name: Showvariantsproductcatalog
---
# Q. How do we show variants of a product?

A. Variants are properties of a product with different values. Suppose, a product is available in five different colors then that means the product has five different variants.

To integrate variant functionality we have to set variants=true (to enable variants).

Our Search API returns parent products with variants, and never just the variants. Some of the variant properties are:

* By using **variants.count**, we can define how many variants of a product need to be returned.
* We also have a predefined attribute (**relevantDoc**) in our API response that informs the customer if the parent product should be displayed or variant – given we send both back in the response.