---
title: Delta Feed Upload
deprecated: false
hidden: false
metadata:
  robots: index
---
A delta (also known as Incremental) feed upload is when you perform a partial feed upload. Changes are updated to the existing product catalog.

> 📘 Note
>
> We support only one type of operation in a single delta upload request. For eg: it can be either of "Add", "Update" or "Delete" for delta uploads. You cannot use multiple operations in the same delta uploads.

## API Structure

```Text API Endpoint
Method : POST

End Point : {feed end point}/api/{siteKey}/upload/catalog/delta

Description : This API helps to upload some of the updated fields of the catalog.
```
```Text Parameters
Request Parameter
1. siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

2. secretKey: A unique identifier provided when your Unbxd account is created. The secretKey is used to authorize your upload request. This is a private key and will not be exposed to the public. This is a required field.

3. feed end point : The feed end point depends upon the region selected at the time of site creation.

Response Parameters

1. fileName: The name of the feed file, in JSON format.

2. uploadID: The unique identifier assigned to your upload session.

3. Status: Indicates the upload situation or progress of your feed file.Status can be:
- Accepted
- Indexing
- Indexed
- Failed

4. timeStamp: Indicates the time of the file in YYYY-MM-DD | HH:MM:SS format.

5. message: Indicates if the upload succeeded or failed. This field will also indicate the error code.

6. code: 200 if feed upload request is ACCEPTED. The code for a feed upload request may be updated if the feed upload request fails during indexing.
```
```Text Error Codes
We use conventional HTTP response codes to indicate success or failure of an API request.

201 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
```
```Text Sample Request
Sample Resquest

curl -X POST \  
 https://feed.unbxd.io/api/{siteKey}/upload/catalog/delta \
  -H 'Authorization:{secretKey}' \
  -F file=@{fileName}.json
```
```Text Sample Response
Sample Response

{
  "fileName": "{fileName}",
  "uploadId": "{id}",
  "timeStamp": 6581239201,  
  "status":"ACCEPTED",  
  "message":"File Queued",  
  "code":200
}
```

### Sample Feed

1. This is how a delta feed upload will appear if you want to update the variants and when the variantId is unique:

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
                "vColor": "Red"
              }
            ]
          }
        ]
      }
    }
  }
}
```

2. If you want to update other fields of a product that has a unique ID:

```
{
  "feed": {
    "catalog": {
      "update": {       
        "items":[{
        "uniqueId":”12345”,
        "color":"blue",
        "size":”10”
      }]
    }
  }
}
```

After the upload is done, you can check the status of the uploaded feed. There are two ways to do it. Either by URL or via APIs.

* In the address field, type in `https://feed.unbxd.io/api/{siteKey}/catalog/delta/status`
* To check the status of the last 10 uploads, type in `https://feed.unbxd.io/api/{siteKey}/catalog/delta/status?count=10`
* To view the status of your upload using the Upload ID:`https://feed.unbxd.io/api/{siteKey}/catalog/delta/{uploadId}/status`

> 📘 NOTE
>
> Once you get the response using the Upload ID, replace (uploadID).

> 📘 Note
>
> To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console.

### Best Practices

To ensure your feed is uploaded and integrated seamlessly, we recommend the following:

1. We recommend a gap of at-least 15 minutes between consecutive delta uploads.
2. Don’t use a delta feed API to upload a full feed.

> 📘 NOTE
>
> Delta feed upload requests received by our systems are processed immediately. However, the changes may require upto 10 mins to reflect in the API response in some cases.