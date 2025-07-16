---
title: Feed Actions
deprecated: false
hidden: false
metadata:
  robots: index
---
These are useful when there are frequent product-based changes, like when you want to add a new product, delete an existing product, or update multiple fields within an existing product.

NOTE: We support only one type of feed action (operation) in a single delta upload request. For eg: it can be either of "Add", "Update" or "Delete" for delta uploads. You cannot use multiple operations in the same delta uploads.

## Add

Used when you want to add a new product, reset product fields within your existing feed, or add/update variants to an existing feed file.

NOTE: This is the default feed action when performing a full feed.

You can use the Add block when you want to:

* Add Product: When new products are added to your catalog, you can use this action to add to your existing Feed by uploading the snapshot of only those products. Once uploaded, we will add these products to your existing product feed.
* Add Variants: Variants are different combinations of options for a product with the same SKU.\
  For instance, you can have a tee shirt with two options: size and color. The size option has three values: small, medium, and large. The color option has two values: blue and green. An example of a variant would be a blue tee-shirt in large.

### Adding Products

Use the Add block to add new products to your catalog.

For example, let’s assume you want to add a product ‘Acme Party Shirt’ to your catalog. The JSON to add a new product when the uniqueId does not exist would appear like this:

```
{
    "feed": {
        "catalog": {
            "add": {
                "items": [{
                    "uniqueId": "GDR1234",
                    "title": "Acme Party Shirt"
                }]
            }
        }
    }
}
```

In the code below, the ‘Add’ block allows you to replace a product that has an existing uniqueId:

```
{
    "feed": {
        "catalog": {
            "add": {
                "items": [{
                    "uniqueId": "GDR1234",
                    "title": "Acme Party Shirt",
                    "description": "A cotton shirt that cloths the party animal in you",
                    "color": "Tangerine",
                    "size": "L"
                }]
            }
        }
    }
}
```

<br />

> 📘 NOTE
>
> You can use the 'Add' block to add a new product when the uniqueId is already in the catalog. However, if the catalog already has the uniqueId then it will replace the entire product with the fields within the Add block.

It is common for product feeds to have products with multiple variants.

To add a variant to a product that already has variants and an existing uniqueId:

```
{
    "feed": {
        "catalog": {
            "add": {
                "items": [{
                    "uniqueId": "ffff78ac",
                    "title": "Acme Jumper Suit",
                    "description": "The perfect casual wear for an evening out",
                    "color": "Orange",
                    "variants": [{
                            "var_description": "The jumper suit for the party animal in you",
                            "variantId": "GOR00302",
                            "var_price": 400,
                            "color": "Dark Red"
                        },

                        {
                            "var_description": "The jumper suit when you don't want to blend in",
                            "variantId": "GOR00302",
                            "var_price": 400,
                            "color": "Purple"
                        }
                    ]
                }]
            }
        }
    }
}
```

<br />

As in the code above, the ‘Add’ block allows you to pass a new variant along with all other variants and other product fields.

There are two scenarios when syncing latest changes/additions to variants using the Add action.

**Scenario 1**

When performing a delta upload, you can use the ‘Add’ action to add new variants to existing products as well as updating the rest of the variants.

To do this, ensure that all variants are a part of the ‘Add’ block within the base product.

For example, let’s assume an existing product in your catalog ‘Acme Party Shirt’ has 2 different variants (colors) and you want to add 1 new variant (colors) to the catalog. You can use the ‘Add’ block to add the new variants to the base product along with the 2 existing variants. So as to achieve this, you would be required to perform an ‘Add’ action for all the 3 variants, as shown in the sample JSON below:

```
{
    "feed": {
        "catalog": {
            "add": {
                "items": [{
                        "uniqueId": "GDR1234",
                        "title": "Superman",
                        "variants": [{
                            "variantId": "child-1",
                            "vColor": [{
                                "id": "47587",
                                "value": "Red"
                            },{
                            "variantId": "child-2",
                            "vColor": [{
                                "id": "47587",
                                "value": "Blue"
                               }]
                        },

                       {
                            "variantId": "child-3",
                            "vColor": [{
                                "id": "49867",
                                "value": "Green"
                            }],
                            "vSize": "S",
                            "vPrice": 130
                        }

                    ]
                    },
                 ]
            }
        }
    }
}
```

<br />

**Scenario 2**

When performing a delta upload, you can use the ‘Add’ action to add a new product with variants.

For instance,

```
{
    "feed": {
        "catalog": {
            "add": {
                "items": [{
                    "uniqueId": "GDR1234",
                    "title": "Superman",
                    "variants": [{
                        "variantId": "child-1",
                        "vColor": [{
                            "id": "47587",
                            "value": "Red"
                        }]
                    }]
                }]
            }
        }
    }
}
```

## Delete

Used when you want to delete products from your existing feed file.

To delete, mention the uniqueID of the product you want to delete.

```
{
    "feed": {
        "catalog": {
            "delete": {
                "items": [{
                    "uniqueId": "GDR1234"
                }]
            }
        }
    }
}
```

## Update

Used when you want to update the values of an existing field in your existing Product Feed synced with Unbxd.

You cannot update the field names or add/delete fields.

To update, upload the snapshot of the uniqueIDs of only those products along with the fields whose values need to be changed.

Generally, this action is used for updating the quantity or availability of a product.

Scenario 1

When performing a delta upload, you can use the ‘Update’ action to update only a few variants of a product, you can update the changes in the update block of that variant.

For example, let’s consider you have a Product ‘Acme Party Shirt’ with three variants \[variantId1, variantId11, variantId12] and another Product ‘Lucus Casual Shirts’ with the three variants \[variantId2, variantId21, variantId22]. If you want to update only variantId1, variantId11 & variantId2, you can include only these three variants when the variantIds are unique as in the JSON below.

```
{
   "feed": {
     "catalog": {
       "update": {
         "items": [{
             "uniqueId": "uniqueId1",
             "variants": [{
                 "variantId": "variantId1",
                 "inventoryCount": 10
               },
               {
                 "variantId": "variantId11",
                 "inventoryCount": 15
               }
             ]
           },
           {
             "uniqueId": "unqiueId2",
             "variants": [{
               "variantId": "variantId2",
               "inventoryCount": 12
             }]
           }
         ]
       }
     }
   }
 }
```

<br />

NOTE: You don’t have to include the uniqueId when the variantId is unique.

Similarly, when the variantId is not unique, the uniqueId needs to be included. Your JSON will appear like this:

```
{
    "feed": {
        "catalog": {
            "update": {
                "items": [{
                        “uniqueId” : “uniqueId1”
                        "variants": [{
                                "variantId": "variantId1",
                                "inventoryCount": 10
                            },
                            {
                                "variantId": "variantId11",
                                "inventoryCount": 15
                            }
                        ]
                    },
                   {
                     “uniqueId” : “unqiueId2”,
                      “Variants” : [{

                                "variantId: "variantId2",
                                "inventoryCount" : 12
                        }]
                  }
                ]
            }
        }
    }
}
```

<br />

**Scenario 2**

You can use the Update block if you want to update the price, add a new field, an attribute, edit the quantity, or update a variant.

Let’s assume your feed in this scenario looks like this:

```
{
"uniqueId": "GDR1234",
"title": "Superman",
"price": 100,
"quantity": 40
}
```

If you want to update the price to $50:

```
{
    "feed": {
        "catalog": {
            "update": {
                "items": [{
                        "uniqueId": "GDR1234",
                        "price": 50
                    }
                ]
            }
        }
    }
}
```

To add a new field to an existing feed:

```
{
    "feed": {
        "catalog": {
            "update": {
                "items": [{
                        "uniqueId": "GDR1234",
                        "size": "S",
                        "price": 50
                    }

                ]
            }
        }
    }
}
```

<br />

> 📘 NOTE
>
> Ensure the field already exists within the Schema.

To add an attribute sleeve-length, and set the value to “full”:

```
{
    "feed": {
        "catalog": {
            "update": {
                "items": [{
                    "uniqueId": "GDR1234",
                    "variants": [{
                        "variantId": "5678",
                        "sleeveLength": "Full"
                    }]
                }]
            }
        }
    }
}
```

To update the quantity to 100:

```
{
    "feed": {
        "catalog": {
            "update": {
                "items": [{
                        "uniqueId": "GDR1234",
                        "quantity": 100
                    }
                ]
            }
        }
    }
}
```