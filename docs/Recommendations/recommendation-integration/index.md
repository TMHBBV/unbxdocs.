---
title: Recommendation Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The Recommendations API lets you interact with the Unbxd platform and implement all recommendation-related functionality with ease. Unbxd Recommendations are a set of widgets, both pre-defined and customizable, designed to showcase personalized product suggestions to shoppers on your web store.

You can use the JSON /XML response format and customize your recommendation experience by leveraging various built-in features of Recommendations. This API can communicate over HTTP and HTTPS. However, we recommend using the HTTPS protocol.

## Recommendations Endpoint

* **Request Method**: GET
* **Endpoint**
  ```
  recommendations.unbxd.io/v2.0/{apikey}/{sitekey}/items
  ```

This API call fetches recommendations for the corresponding page type, for your website.

* **Path Parameters**

| Field Name   | Description                   | Requirement |
| ------------ | ----------------------------- | ----------- |
| `<sitename>` | Unique site key for each site | Required    |
| `<apikey>`   | Unique API key for each site  | Required    |

* **Authentication**\
  Our APIs use an API\_KEY and a SITE\_KEY to authenticate recommendation requests.
  These keys are generated at the time of account creation and can be accessed within Console at **User Management** > **Configure Site** > **Keys**.
* **Request Parameters**\
  The values of the request parameters are defined below:

| Parameter       | Description                                                                                                          | Type                                                                     | Required                                               |
| --------------- | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------ |
| `pageType`      | Define the Page type for which the recommendations have to be requested                                              | String (enumerated)\<br>HOME\<br>CATEGORY\<br>BRAND\<br>PRODUCT\<br>CART | Yes                                                    |
| `widget`        | Defines the position of the widgets on the page. If nothing is specified, recommendations for all widgets are given. | String (enumerated)\<br>Widget 1\<br>Widget 2\<br>Widget 3               | No                                                     |
| `id`            | Unique ID of the product                                                                                             | String                                                                   | Required to be passed only for PRODUCT, CART Page type |
| `uid`           | Unique identifier of a user. It cannot have special character except ‘\_’                                            | String                                                                   | All Page types                                         |
| `catlevel1Name` | The first level of products. Denotes the hierarchy of products in your catalog.                                      | String                                                                   | Required to be passed only for CATEGORY Page type      |
| `catlevel2Name` | The second level of products. Denotes the hierarchy of products in your catalog.                                     | String                                                                   | Required to be passed only for CATEGORY Page type      |
| `catlevel3Name` | The third level of products. Denotes the hierarchy of products in your catalog.                                      | String                                                                   | Required to be passed only for CATEGORY Page type      |
| `catlevel4Name` | The fourth level of products. Denotes the hierarchy of products in your catalog.                                     | String                                                                   | Required to be passed only for CATEGORY Page type      |
| `brand`         | Distinctive name or label of the manufacturer of the product.                                                        | String                                                                   | Required to be passed only for BRAND Page type         |
| `ip`            | IP address for which recommendation is required                                                                      | X.X.X.X                                                                  | All Page types                                         |

* **Response Components** After you input the request body(Path and Query) parameters and run the call successfully, we receive a response with the following parameters:

| Parameter | Description        | Always Present |
| --------- | ------------------ | -------------- |
| widget1   | ExperienceResponse | No             |
| widget2   | ExperienceResponse | No             |
| widget3   | ExperienceResponse | No             |
| error     | ErrorResponse      | No             |

* **Experience Response**

| Parameter       | Description   | Always Present |
| --------------- | ------------- | -------------- |
| count           | Size of list  | Yes            |
| recommendations | List of items | Yes            |

## Component Description

The aforementioned table provided a with the default values of the request parameters. It is a pre-defined table of APIs which you can directly integrate by inputting the \<sitekey> and \<apikey> of your site.&#x20;

Let’s dwell deep and understand the API calls of each page individually.

| Page Type       | Description                                                       | URL                                                                                                                                                                                |
| --------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Home Page       | Recommendations for the home page                                 | `https://recommendations.unbxd.io/v2.0/<apiKey>/<isitename>/items?pageType=HOME&uid=<uid>&ip=<ip>`                                                                                 |
| Category Page   | Recommendations based on category hierarchy                       | `https://recommendations.unbxd.io/v2.0/<apiKey>/<isitename>/items?pageType=CATEGORY&catlevel1Name=cat1&catlevel2Name=cat2&catlevel3Name=cat3&catlevel4Name=cat4&uid=<uid>&ip=<ip>` |
| PDP             | Recommendations for a specific product                            | `https://recommendations.unbxd.io/v2.0/<apiKey>/<isitename>/items?pageType=PRODUCT&id=<pid1>&uid=<uid>&ip=<ip>`                                                                    |
| Cart Page (UID) | Recommendations based on the carted products fetched from the UID | `https://recommendations.unbxd.io/v2.0/<apiKey>/<isitename>/items?pageType=CART&uid=<uid>&ip=<ip>`                                                                                 |
| Cart Page (PID) | Recommendations based on product IDs (PIDs), not UID              | `https://recommendations.unbxd.io/v2.0/<apiKey>/<isitename>/items?pageType=CART&id=<pid1>&id=<pid2>&uid=<uid>&ip=<ip>`                                                             |
| Brand Page      | Recommendations based on the brand                                | `https://recommendations.unbxd.io/v2.0/<apiKey>/<isitename>/items?pageType=BRAND&brand=<brand1>&uid=<uid>&ip=<ip>`                                                                 |