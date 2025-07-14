---
title: Shopping Assistant
excerpt: >-
  This guide outlines two methods for integrating the Shopping Assistant for
  Netcore Unbxd console.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The Netcore Unbxd Shopping Assistant, is an AI-driven chatbot integrated into e-commerce websites. It assists customers by understanding their preferences, guiding them in product selection, and offering tailored suggestions based on their interactions with the assistant.

> 📘 Note
>
> 1. Netcore Unbxd's Shopping Assistant is a ***PAID*** feature and is not included by default in the standard Unbxd Panel.
> 2. Merchandisers do not have access to enable this feature, contact **Unbxd Business Team** to enable this feature for your panel.
> 3. Once it's enabled, customers can preview the shopping assistant within their console in the preview section under the tab Shopping Assistant.

### Key Features of a Shopping Assistant:

1. **Personalized Recommendations**: Based on user queries, browsing behavior, and past interactions, the assistant suggests products that the user will likely be interested in.
2. **Real-time Interaction**: It engages users in real-time conversations, offering immediate answers to questions about products, shipping details, availability, and more.
3. **Search Assistance**: It helps users refine their search by applying filters (e.g., size, color, brand) or guiding them through a product catalog.
4. **Product Discovery**: If the user is unsure about what to buy, the assistant offers curated product options, helping users explore a variety of choices.

### Why is a Shopping Assistant Useful?

1. **Improved Customer Experience**:

   By offering immediate assistance, personalized product suggestions, and easy navigation, shopping assistants make the shopping process more intuitive and enjoyable for users. This leads to higher customer satisfaction.
2. **Increased Conversions and Sales**:

   Personalized product recommendations can directly influence purchasing decisions. By presenting the right products at the right time, a shopping assistant can drive higher conversion rates and more sales.
3. **24/7 Availability**:

   Unlike human customer support, a shopping assistant is always available, providing instant responses to users' queries at any time of the day. This is particularly useful for global ecommerce platforms where users might be browsing at different times.
4. **Efficient Handling of Queries**:

   The assistant can handle a large volume of queries simultaneously, reducing the need for human agents. It can answer repetitive questions like product details, availability, price, and shipping, freeing up customer support staff to focus on more complex issues and so on.

## Integration of Shopping Assistant to Netcore Unbxd console.

We support the following two methods for integrating the Shopping Assistant: an API-driven approach for more control and flexibility, and a simpler JavaScript (JS) embedding method.

# API-Driven Implementation

This method allows for greater control and customization of the integration by making API calls from your backend or frontend to interact with the Shopping Assistant.

#### 1. Initialize Conversation

**Purpose**: This API call initiates a new conversation session for a unique user on your website, establishing a context for future interactions.

**Endpoint**:

```
GET /v1/sites/{site_key}/conversation?uid={netcoreid}
```

**Parameters**:

| **Parameter Type**  | **Parameter** | **Description**                                                                                                                                                                                                                                                                | **Required** |
| :------------------ | :------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------- |
| **Path Parameter**  | `site_key`    | Your unique site identifier, as provided by Netcore Unbxd.                                                                                                                                                                                                                     | Yes          |
| **Query Parameter** | `uid`         | A unique identifier for the current user on your website. For consistent behavior across devices, users can unify their experience by adding their `customerid` and `netcoreid`. Otherwise, the `uid` provides behavior similar to their search history on the current device. | Yes          |

**Example Request**:

```
GET /v1/sites/your_site_key/conversation?uid=user123
```

**Successful Response (200 OK)**:

```json
{   
"conversation_id": "1672hsuafdguya-1268tebhbsc-978te3hsqw" 
} 
```

**Response Fields**:

| **Field**            | **Description**                                                                                                               |
| :------------------- | :---------------------------------------------------------------------------------------------------------------------------- |
| **conversation\_id** | A unique identifier for the newly created chat session. This ID will be used for all subsequent messages within this session. |

**Possible Error Codes**:

| **Error Code**                | **Description**                                                                                | **Action**                                                                  |
| :---------------------------- | :--------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------- |
| **400 Bad Request**           | Missing or invalid `uid` or `site_key`. Please ensure these parameters are correctly provided. | Ensure that the `uid` and `site_key` are correctly provided in the request. |
| **401 Unauthorized**          | An issue with access credentials. Verify your API key or authorization method.                 | Check and verify the API key or authorization credentials.                  |
| **500 Internal Server Error** | An unexpected error on the Netcore Unbxd server. Try again later or contact support.           | Retry the request later or contact support for further assistance.          |

#### 2. Send Chat Message

**Purpose**: To send a user's message to the Shopping Assistant and receive AI-generated responses, product recommendations, and relevant filters.

**Endpoint**:

```
POST /v1/sites/{site_key}/conversation/{conversation_id}/chat?uid={uid}
 
```

**Parameters**:

| **Parameter Type**  | **Parameter**     | **Description**                                                                                                   | **Required** |
| :------------------ | :---------------- | :---------------------------------------------------------------------------------------------------------------- | :----------- |
| **Path Parameter**  | `site_key`        | Your unique site identifier, as provided by Netcore Unbxd.                                                        | Yes          |
| **Path Parameter**  | `conversation_id` | The unique identifier for the ongoing conversation session, obtained from the "Initialize Conversation" endpoint. | Yes          |
| **Query Parameter** | `uid`             | The unique identifier for the current user on your website.                                                       | Yes          |

**Request Body**:

```json
{
  "message": "Show me some options for tshirts",
  "filters": [
    {
      "field": "size",
      "options": ["XS"]
    }
  ],
  "metadata": [
    {
      "name": "clicks",
      "value": ["uniqueId of product"]
    },
    {
      "name": "carts",
      "value": ["uniqueId of product"]
    }
  ]
} 
```

**Request Fields**:

| **Field**    | **Type** | **Description**                                                                                                                                                                                                                                                                                            | **Required** |
| :----------- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------- |
| **message**  | string   | The user's current chat message or query.                                                                                                                                                                                                                                                                  | Yes          |
| **filters**  | array    | A list of filters to apply to the product search. Each filter object includes:<br /><br />1. **field (string):** The field name to filter by (e.g., "brand", "color", "price").  <br />2. **options (array)**: An array of values to filter for the specified field (e.g., \["Nike"], \["Red"], \[10, 50]) | No(optional) |
| **metadata** | array    | Metadata that provides context about the user's interactions. Each metadata object includes:<br /><br />**name (string)**: The type of metadata (e.g., "clicks", "carts", "views").  **value (array)**: An array of product identifiers related to the metadata.                                           | No(optional) |

**Successful Response (200 OK)**:

```json
{
  "message": "Okay, here are some t-shirts in size XS that you might like:",
  "products": [
    {
      "productId": "tshirt123",
      "title": "Classic Cotton Tee",
      "imageUrl": "https://example.com/images/tshirt123.jpg",
      "productUrl": "https://example.com/products/tshirt123",
      "price": 25.99
    },
    {
      "productId": "tshirt456",
      "title": "Premium Soft T-Shirt",
      "imageUrl": "https://example.com/images/tshirt456.jpg",
      "productUrl": "https://example.com/products/tshirt456",
      "price": 39.50
    }
    // ... more products
  ],
  "filters": [
    {
      "field": "color",
      "options": ["Black", "White", "Blue", "Green"]
    },
    {
      "field": "brand",
      "options": ["YourBrand", "AnotherBrand"]
    }
    // ... more filters
  ]
}
```

**Response Fields**:

| **Field**    | **Type** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                            | **Required** |
| :----------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------- |
| **message**  | string   | The AI-generated reply to the user's query.                                                                                                                                                                                                                                                                                                                                                                                                | Yes          |
| **products** | array    | A list of recommended products, each containing:  <br /><br />1. **productId (string)**: Unique identifier of the product.  <br />2. **title (string)**: Title of the product. <br />3. **imageUrl (string)**: URL of the product image. <br />4. **productUrl (string)**: URL of the product details page. <br />5. **price (number)**: Price of the product and potentially other product-specific fields custom configured for the site | Yes          |
| **filters**  | array    | An array of additional filters that the user can apply to further refine the results.                                                                                                                                                                                                                                                                                                                                                      | No(Optional) |

> 📘 Note
>
> The actual fields returned can vary based on your site's configuration and the data available in your product feed. The product objects are not limited to just the fields listed above.

**Possible Error Codes**:

| **Status Code**               | **Description**                                                                      | **Action**                                                             |
| :---------------------------- | :----------------------------------------------------------------------------------- | :--------------------------------------------------------------------- |
| **200 OK**                    | The chat message was processed successfully, and results are returned.               | No action needed.                                                      |
| **400 Bad Request**           | Missing or malformed input data in the request body or query parameters.             | Ensure the request body and query parameters are properly formatted.   |
| **401 Unauthorized**          | An issue with access credentials. Verify your API key or authorization method.       | Check and verify your API key or authorization credentials.            |
| **404 Not Found**             | Invalid `conversation_id` or the session was not found.                              | Verify that the `conversation_id` is correct and the session is valid. |
| **500 Internal Server Error** | An unexpected error on the Netcore Unbxd server. Try again later or contact support. | Retry the request later or contact support for further assistance.     |

# **JS Script Embedding Implementation**

This method offers a faster and simpler way to integrate the Shopping Assistant by embedding a JavaScript script and a CSS file into your website.

To implement using the JS script, include the following in your website's **\<head>** or **\<body>**:

**HTML:**

```filename
<link rel="stylesheet" href="https://libraries.unbxdapi.com/unbxd-shopping-assistant.css">

<script src="https://libraries.unbxdapi.com/unbxd-shopping-assistant.js"></script>
```