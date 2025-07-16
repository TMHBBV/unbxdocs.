---
title: Full Feed API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Allows you to upload the complete version of your schema and catalog files.

> 📘 Tip
>
> We recommend you use the Full Feed Upload API to upload your catalog when you are uploading for the first time.

### Feed API Endpoints

The feed API endpoint for your Unbxd site depends upon the cluster where your site is hosted. Unbxd has the following feed endpoints :

* ANZ region : [https://feed-anz.unbxd.io/](https://feed-anz.unbxd.io/)
* UK region : [https://feed-uk.unbxd.io/](https://feed-uk.unbxd.io/)
* SG region : [https://feed-apac.unbxd.io/](https://feed-apac.unbxd.io/)
* US region : [https://feed.unbxd.io/](https://feed.unbxd.io/)
* US region\* : [https://feed-g-nam.unbxd.io/](https://feed-g-nam.unbxd.io/)

Unbxd has launched a new cluster in US regions. All sites going to the new US cluster must use the new feed endpoint.

You can detect the feed endpoint for your site by navigating to the Manage > Configure Site > API section inside the console.  The Catalog Feed API request in this page contains the feed endpoint for your selected site.

> 📘 Note
>
> In the rest of this document, we have used [https://feed.unbxd.io](https://feed.unbxd.io) as the endpoint. Kindly replace the feed endpoint with the one that is applicable on your store.

## API Structure

```Text API Endpoint
Method : POST

End Point : {feed end point}/api/siteKey/upload/catalog/full

Description : This API will upload your complete feed file as a single JSON file.
```
```Text Parameters
Method : POST

End Point : {feed end point}/api/{siteKey}/upload/catalog/full

Description : This API will upload your complete feed file as a single JSON file.

Request Parameters

1.siteKey: A unique identifier provided when you create an Unbxd account. This key can also be retrieved from the Console. This is a required field.

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
Method : POST

End Point : {feed end point}/api/{siteKey}/upload/catalog/full

Description : This API will upload your complete feed file as a single JSON file.

Response codes to indicate success or failure of an API request.

200 (Ok): Indicates the upload was successful.
401 (Authorization Error): Indicates you may have provided an invalid API key.
400 (Bad Request): Indicates you may have missed a required parameter.
500 (Internal Server Error): Though these are rare, this indicates we may have messed up.
```
```Text Sample Request
Method : POST

End Point : {feed end point}/api/{siteKey}/upload/catalog/full

Description : This API will upload your complete feed file as a single JSON file.

Sample Resquest:

curl -X POST \  
https://feed.unbxd.io/api/{siteKey}/upload/catalog/full \  
    -H 'Authorization:{secretKey}'\
    -F file=@{fileName}.json`
```
```Text Sample Response
{
  "fileName": "{fileName}",
  "uploadId": "{id}",
  "timeStamp": 6581239201,  "status":"ACCEPTED",  "message":"File Queued", "code":200
}
```

### Sample Feed

A typical  feed will contain many other attributes, which will have **display**, **searchable**, **merchandisable**, and **unique attributes**.

1. Here’s how a sample feed file with variants would appear.

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

2. Here’s how a sample feed file without variants would appear.

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

* For URLs, In the address field, type [in](https://feed.unbxd.io/api/%7BsiteKey%7D/catalog/status).
* To check the status of the last 10 uploads, type [in](https://feed.unbxd.io/api/%7BsiteKey%7D/catalog/status?count=10).
* To view the status of your upload using the Upload ID `https://feed.unbxd.io/api/%7BsiteKey%7D/catalog/%7BuploadId%7D/status`

> 📘 NOTE
>
> Once you get the response using the Upload ID, replace (uploadID).

> 📘 Note
>
> To locate your site key, navigate to Manage > Configure Site > Keys > Site Keys within the Console.

### Best Practices

To ensure your feed is uploaded and integrated seamlessly, we recommend the following:

1. When uploading a full feed, use the Add operation in the catalog. Update and Delete operation are not supported in a full feed upload. A full feed will replace the entire catalog hence update and delete operation are not needed.
2. A full feed is recommended when uploading a catalog under 2GB or less than 1 million products. If your catalog is exceeding beyond these limits, then reach out to our support team to get more details on larger catalogs options.