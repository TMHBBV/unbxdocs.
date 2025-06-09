---
title: Check Product Count​
excerpt: Allows you to check the number of products you have in your feed.
deprecated: false
hidden: false
metadata:
  robots: index
---
# API Parameters

```Text API Endpoint
Method : GET

End Point : {feed end point}/api/{siteKey}/catalog/size

Description : This API will provide the size of the uploaded feed. 
```
```Text Site Key
1. siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

2. size: Returns the number of products your feed has.
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
```
```Text Sample Response
Response: The response will have the number of products in the feed file.
```

## Best Practices

1. We should specify clearly whether schema and catalog can be part of one document together or separate.
2. We should document if there is a limit on file size, record count for schema and catalog files
3. We should document feed processing failures midway and its affect on indexing.
4. Document the time taken to record the index file.