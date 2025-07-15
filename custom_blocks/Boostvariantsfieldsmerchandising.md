---
name: Boostvariantsfieldsmerchandising
---
# Q. Can we do boosting on variants field?

A. Yes, we can.

First is if a customer wants to boost products using the variant fields: As in, boost the products but the logic will be coming from a variant field. For e.g., if the price is a variant field, and the customer wants all products with price>$50 to be boosted. Then all products (which have any variant with a price>$50) will be boosted.

Second is if a customer wants to boost variants within a product, and the image of the variant becomes the face of the product: In this case, e.g., if a customer applies a boost on color field = red then, all products in the result set which  have a red color variant – that image will become the face for them.