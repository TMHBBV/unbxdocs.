---
title: Feed API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Feed APIs Overview

You can use our custom APIs to upload your feed.

Three types of feed uploads we support:

1. Full Feed Upload: Use this method to upload your entire product catalog or to overwrite any previous copy of your feed on our servers.
2. Delta Feed Upload: Also known as Incremental Feed Upload, use this to update/add multiple records or to upload a catalog partially.
3. Single Record Upload: Use this method to update/add a single attribute within a product in your existing feed file.

## Full Feed Upload

Allows you to upload the complete version of your schema and catalog files.

> 📘 Tips
>
> We recommend you use the Full Feed Upload API to upload your catalog when you are uploading for the first time.

## API Structure

```Text API Endpoint
Method : POST

 

End Point : {feed end point}/api/{siteKey}/upload/catalog/full

 

Description : This API will upload your complete feed file as a single JSON file.


```
```Text Parameter
Method : POST

 

End Point : {feed end point}/api/{siteKey}/upload/catalog/full

 

Description : This API will upload your complete feed file as a single JSON file.

Request Parameters

siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

 

secretKey: A unique identifier provided when your Unbxd account is created. The secretKey is used to authorize your upload request. This is a private key and will not be exposed to the public. This is a required field.

 

feed end point : The feed end point depends upon the region selected at the time of site creation.

 

US region: http://feed.unbxd.io/

 

ANZ region : http://feed-anz.unbxd.io/

 

UK region : http://feed-uk.unbxd.io/

 

SG region : http://feed-apac.unbxd.io/

 

Response Parameters

fileName: The name of the feed file, in JSON format.

 

uploadID: The unique identifier assigned to your upload session.

 

timeStamp: Indicates the time of the file in YYYY-MM-DD | HH:MM:SS format.
```
```Text Error Codes
Method : POST

 

End Point : {feed end point}/api/{siteKey}/upload/catalog/full

 

Description : This API will upload your complete feed file as a single JSON file.

We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
```
```
Method : POST

 

End Point : {feed end point}/api/{siteKey}/upload/catalog/full

 

Description : This API will upload your complete feed file as a single JSON file.

Sample Resquest: 
curl -X POST \  
https://{feed end point}/api/{siteKey}/upload/catalog/full \  
    -H 'Authorization:{secretKey}'\
      -F file=@{fileName}.json

Sample Response:
{
  "fileName": "{fileName}",
  "uploadId": "{id}",
  "timeStamp": 6581239201
}
```

## Sample Feed

Broadly, the typical feed will contain many other attributes, which will have display, searchable, merchandisable, and unique attributes.

Here’s how a sample feed file with variants would appear.

```
{
    "feed": 
                        {
        "catalog": 
                        {
            "add": 
                         {
                "items": [
                         {
                        "uniqueId": "ss10010",
                        "title": "Short Sleeve Shirt",
                        "description": "Start your summer right with the all new short sleeve shirt."
                    },
                    {
                        "uniqueId": "sj10011",
                        "title": "Stretch Jeans",
                        "description": "Fit perfectly even after wash.",
                        "variants": [
                                    {
                            "variantId": "9890101",
                            "vSize": "s",
                            "vPrice": 90
                        }, 
                        {
                            "variantId": "9890102",
                            "vSize": "xxl",
                            "vPrice": 100,
                            "vImages": "http://example.com/images/2-2.jpg"
                        }
                       ]
                    }
                ]
            }
        }
    }
}
```

Here’s how a sample feed file without variants would appear.

```
{
  "feed": {
    "catalog": {
      "add": {
        "items": [
          {
            "uniqueId": "ss10010",
            "title": "Short Sleeve Shirt",
            "description": "Get the perfect look for the summer."
          },
          {
            "uniqueId": "ss11023",
            "title": "Relaxed Fit Jeans",
            "description": "Jeans for all seasons."
          }
        ]
      }
    }
  }
}
```

### Check Status

After the upload is done, you can check the status of the uploaded feed. There are two ways to do it. Either by URL or via APIs.

For URLs, In the address field, type in [http://feed.unbxd.io/api//catalog/delta/status](http://feed.unbxd.io/api//catalog/delta/status)\
To check the status of the last 10 uploads, type in
[http://feed.unbxd.io/api//catalog/status?count=10](http://feed.unbxd.io/api//catalog/status?count=10)
To view the status of your upload using the Upload ID.

```Text API Endpoint
Method : GET

 

End Point : {feed end point}/api/{siteKey}/catalog/{upload}/status

 

Description : This API will let you know the status of uploaded feed. 

NOTE: Once you get the response using the Upload ID, replace (uploadID).

NOTE: To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console.
```
```Text Parameter
siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

 

uploadID: The unique identifier assigned to your upload session.

 

Status: Indicates the upload situation or progress of your feed file.Status can be:

Indexing
Indexed
Failed
NOTE: Once you get the response using the Upload ID, replace {uploadID}.

NOTE: To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console
```
```Text Error Codes
We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
NOTE: Once you get the response using the Upload ID, replace {uploadID}.

NOTE: To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console.
```
```Text Sample Request
curl -X POST \  
https://feed.unbxd.io/api/{siteKey}/upload/catalog/full/status \  
    -H 'Authorization:{secretKey}'\
    -F file=@{fileName}.json`
```
```Text Sample Response
{
  "Indexed"
}
```

<br />

NOTE: Once you get the response using the Upload ID, replace (uploadID).

NOTE: To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console

## Best Practices

To ensure your feed is uploaded and integrated seamlessly, we recommend the following:

When uploading a full feed, only the Add block is necessary since a full feed will replace the entire current catalog.\
A full feed is recommended when uploading a catalog under 2GB or less than 1 million products. If your catalog is over 2GB or more than 1 million products, we recommend you to split your catalog into smaller chunks and upload these smaller files as multiple delta uploads.

## Delta Feed Upload

A delta (also known as Incremental) feed upload is when you perform a partial feed upload. Changes are updated to the existing product feed file.

```Text API Endpoint
Method : POST

 

End Point : {feed end point}/api/{siteKey}/upload/catalog/delta

 

Description : This API helps to upload some of the updated fields of the catalog.
```
```Text Parameter
Request Parameter
siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

 

secretKey: A unique identifier provided when your Unbxd account is created. The secretKey is used to authorize your upload request. This is a private key and will not be exposed to the public. This is a required field.

 

feed end point : The feed end point depends upon the region selected at the time of site creation.

 

US region: http://feed.unbxd.io/

 

ANZ region : http://feed-anz.unbxd.io/

 

UK region : http://feed-uk.unbxd.io/

 

SG region : http://feed-apac.unbxd.io/

 
 
Response Parameters
fileName: The name of the feed file, in JSON format.

 

uploadID: The unique identifier assigned to your upload session.

 

variantID: The unique ID of variants within the feed file. When there are variants present, the API will have the variantID of the variants.
```
```Text Error Codes
We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
```
```Text Sample Request
curl -X POST \  
 https://{feed end point}/api/{siteKey}/upload/catalog/delta \
  -H 'Authorization:{secretKey}' \
  -F file=@{fileName}.json
```
```Text Sample Response
{
  "fileName": "{fileName}",
  "uploadId": "{id}",
  "timeStamp": 6581239201
}
```

## Sample Feed

This is how a delta feed upload will appear if you want to update the variants and when the variantId is unique:

```
{
  "feed": {
    "catalog": {
      "update": {
        "items": [
          {
            "variants": [
              {
                "variantId": "00889705456424",
                "v_qty": "0",
                "vSize": "s",
                "vColor": Red
              }
            ]
          }
        ]
      }
    }
  }
}
```

If you want to update other fields of a product that has a unique ID:

```
{
  "feed": {
    "catalog": {
      "update": {
        "uniqueId":”12345”,
        "color":"blue",
        "size":”10”
      }
    }
  }
}
```

If you want to update other fields of a product that has a unique ID:

```

{
  "feed": {
    "catalog": {
      "update": {
        "uniqueId":”12345”,
        "color":"blue",
        "size":”10”
      }
    }
  }
}
```

```Text API Endpoint
Method : GET

 

End Point : {feed end point}/api/{siteKey}/catalog/delta/status

 

Description : This API will provide the status of the delta feed upload. 

NOTE: Once you get the response using the Upload ID, replace {uploadID}.

NOTE: To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console.
```
```Text Parameter
siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

 

uploadID: The unique identifier assigned to your upload session.

 

Status: Indicates the upload situation or progress of your feed file.Status can be:

Indexing
Indexed
Failed
timeStamp: Indicates the time of the file in YYYY-MM-DD | HH:MM:SS format.

 

message: Indicates if the upload succeeded or failed. This field will also indicate the error code.

NOTE: Once you get the response using the Upload ID, replace {uploadID}.

NOTE: To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console.
```
```Text Error Codes
We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed u
```
```Text Sample Request
curl -X POST \  
 https://feed.unbxd.io/api/{siteKey}/upload/catalog/delta/status \
  -H 'Authorization:{secretKey}' \
  -F file=@{fileName}.json
```
```Text Sample Response
{
  "Indexed"
}
```

<br />

> 📘 NOTE
>
> Once you get the response using the Upload ID, replace (uploadID).
>
> To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console.

## Best Practices

To ensure your feed is uploaded and integrated seamlessly, we recommend the following:

We recommend a gap of atleast 15 minutes between consecutive delta uploads.\
Don’t use a delta feed API to upload a full feed.

## Feed Actions

These are useful when there are frequent product-based changes, like when you want to add a new product, delete an existing product, or update multiple fields within an existing product.

### Add

Used when you want to add a new product, reset product fields within your existing feed, or add/update variants to an existing feed file.

> 📘 NOTE
>
> This is the default feed action when performing a full feed.

You can use the Add block when you want to:

**Add Product**: When new products are added to your catalog, you can use this action to add to your existing Feed by uploading the snapshot of only those products. Once uploaded, we will add these products to your existing product feed.\
**Add Variants**: Variants are different combinations of options for a product with the same SKU.
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

* In the code below, the ‘Add’ block allows you to replace a product that has an existing uniqueId:

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

Scenario 1

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

**Delete**\
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

<br />

**Update**\
Used when you want to update the values of an existing field in your existing Product Feed synced with Unbxd.

You cannot update the field names or add/delete fields.

To update, upload the snapshot of the uniqueIDs of only those products along with the fields whose values need to be changed.

Generally, this action is used for updating the quantity or availability of a product.

**Scenario 1**

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

> 📘 NOTE
>
> You don’t have to include the uniqueId when the variantId is unique.

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

<br />

## Single Record Upload

When you want to add/update just a single attribute within an existing feed file.

Recommended when you want to upload only parts of an existing product within your feed. Using single record upload instead of delta upload to update single attributes can save you time.

```Text API Endpoint
Method : POST

 

End Point : {feed end point}/api/{siteKey}/upload/feed?operation={operationType}

 

Description : This API helps to update one field from the feed.
```
```Text Parameter
Request Parameters

 

siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

 

secretKey: A unique identifier provided when your Unbxd account is created. The secretKey is used to authorize your upload request. This is a private key and will not be exposed to the public. This is a required field.

 

feed end point : The feed end point depends upon the region selected at the time of site creation.

 

US region: http://feed.unbxd.io/

 

ANZ region : http://feed-anz.unbxd.io/

 

UK region : http://feed-uk.unbxd.io/

 

SG region : http://feed-apac.unbxd.io/

 

 

Response Parameters

fileName: The name of the feed file, in JSON format.

 

variantID: The unique ID of variants within the feed file. When there are variants present, the API will have the variantID of the variants.

 

uploadID: The unique identifier assigned to your upload session.

 

Status: Indicates the upload situation or progress of your feed file.Status can be:

Indexing
Indexed
Failed
timeStamp: Indicates the time of the file in YYYY-MM-DD | HH:MM:SS format.

 

message: Indicates if the upload succeeded or failed. This field will also indicate the error code.


```
```Text Error Codes
We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.

```
```Text Sample Request
curl -X POST 'https://{feed end point}/api/{siteKey}/upload/feed?operation={operationType}'  
  -H 'Authorization:{secretKey}'
  -d '{
  "uniqueId": "parent-id-1",
  "title": "batman",
  "variants": 
[
    {
      "variantId": "child-1",
      "vColor": "black",
      "vSize": "m",
      "vPrice": 19,
      "vImages": "http://example.com/images/1-1.jpg"
    },
    {
      "variantId": "child-2",
      "vColor": "blue",
      "vSize": "xl",
      "vPrice": 10,
      "vImages": "http://example.com/images/1-2.jpg"
    }
  ]
}
```
```Text Sample Response
{
    "fileName": "{fileName}",
    "uploadId": "{id}",
    "status": "INDEXED",
    "timeStamp": 1497016711231
    "message":"success
  }
```

## Sample Single Feed Upload

```
curl -X POST 'https://feed.unbxd.io/api/{siteKey}/upload/feed?operation={operationType}'  
  -H 'Authorization:{secretKey}'
  -d '{
  "uniqueId": "parent-id-1",
  "title": "batman",
  "variants": [
    {
      "variantId": "child-1",
      "vColor": "black",
      "vSize": "m",
      "vPrice": 19,
      "vImages": "http://example.com/images/1-1.jpg"
    },
    {
      "variantId": "child-2",
      "vColor": "blue",
      "vSize": "xl",
      "vPrice": 10,
      "vImages": "http://example.com/images/1-2.jpg"
    }
  ]
}
```

## Check Status

After the upload is done, you can check the status of the uploaded feed. There are two ways to do it. Either by URL or via APIs.

To check the status of your upload within your browser:\
In the address field, type in ‘[http://feed.unbxd.io/api//catalog/status’](http://feed.unbxd.io/api//catalog/status’)
To check the status of the last 10 uploads:
Type in ‘[http://feed.unbxd.io/api//catalog/status?count=10’](http://feed.unbxd.io/api//catalog/status?count=10’)
To view the status of your upload using the Upload ID:

```Text API Endpoint
Method : GET

 

End Point : /api/{siteKey}/catalog/{upload}/status

 

Description : This API helps to give the status of the uploaded records.

NOTE: Once you get the response using the Upload ID, replace {uploadID}.
```
```Text Parameter
uploadID: The unique identifier assigned to your upload session.

 

Status: Indicates the upload situation or progress of your feed file.Status can be:

Indexing
Indexed
Failed
timeStamp: Indicates the time of the file in YYYY-MM-DD | HH:MM:SS format.

 

message: Indicates if the upload succeeded or failed. This field will also indicate the error code.

NOTE: Once you get the response using the Upload ID, replace {uploadID}.
```
```Text Error Codes
We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
NOTE: Once you get the response using the Upload ID, replace (uploadID).
```

## Best Practices

To ensure your feed is uploaded and integrated seamlessly, remember:

To update feed that has variants, use the Add block at the product’s parent-level.

## Check Product Count​

Allows you to check the number of products you have in your feed.

```Text API Endpoint
Method : GET

 

End Point : {feed end point}/api/{siteKey}/catalog/size

 

Description : This API will provide the size of the uploaded feed. 


```
```Text Parameter
siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

 

size: Returns the number of products your feed has.


```
```Text Error Codes
We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.

```
```Text Sample Request
curl -X GET  https://feed.unbxd.io/api/{siteKey}/catalog/size 


Response

The response will have the number of products in the feed file.
```

## Best Practices

We should specify clearly whether schema and catalog can be part of one document together or separate.\
We should document if there is a limit on file size, record count for schema and catalog files
We should document feed processing failures midway and its affect on indexing.
Document the time taken to record the index file.