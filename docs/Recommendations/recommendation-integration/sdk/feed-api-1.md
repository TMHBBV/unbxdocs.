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