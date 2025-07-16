---
name: Shopifyintegration
---
# Overview

Shopify is one of the most popular e-commerce platforms, allowing businesses to build online stores with ease. It offers a range of features for store setup, sales tracking, product management, and integration with various tools, like payment gateways, marketing platforms, and analytics tools.

# Integrating Unbxd with Shopify:

There are some distinct benefits and challenges in integrating Unbxd with Shopify.

| **Benefits**                  | **Details**                                                                                                                                                 |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Enhanced Search**           | Unbxd can enhance Shopify's basic search functionality, providing more relevant search results, better product filtering, and faster responses.             |
| **Better Recommendations**    | Offers personalized product recommendations, increasing average order value (AOV) and overall sales, which Shopify lacks out of the box.                    |
| **Improved Conversion Rates** | Better search results, personalized recommendations, and a more tailored user experience can help increase conversion rates on Shopify stores.              |
| **Analytics Insights**        | Unbxd's search analytics offer deeper insights into user behavior, which can inform product strategy, marketing, and store optimization efforts on Shopify. |

Challenges:

| **Challenges**             | **Details**                                                                                                                                            |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Integration Complexity** | Implementing Unbxd may require technical setup or custom development, which could be time-consuming and complex.                                       |
| **Cost vs. Benefit**       | Unbxd is a premium solution, and its benefits should be weighed against the cost, especially for smaller businesses or those still testing the market. |
| **Data Privacy**           | Personalized search and recommendations require careful handling of customer data to comply with data protection regulations (e.g., GDPR).             |

Below is the steps to install and configure Shopify app to your Netcore Unbxd console.

1. Navigate to: [https://shopify-dev.unbxd.com/login](https://shopify-dev.unbxd.com/login) , enter your details and click **Install** to download the app.

Install the downloaded app and installation is completed, you can see the Netcore Unbxd App under **Shopify**>**Apps**

2. To configure the Shopify app, Login to Unbxd console, navigate to **Manage** > **Configure Site** section. Copy the **Site Key**,  **Secret Key**, and the **API Key**.
3. In **Shopify** > **Apps** navigate to Unbxd Site Search App in the Shopify and paste all the key details copied from the Netcore Unbxd’s Console in the Setup section.

After submitting the keys, new message will be popped up stating **Keys Updated successfully**.

## Components of Shopify

There are four components that you can access on the Shopify App:

1. Product
2. Catalog
3. Debuggability
4. Analytics

### Product

In this section you can easily sync all your products in the catalog at one place. Navigate to **Products** > **Shopify Products**. You can see all the synced Shopify products in one place. You can either download the products in an Excel format or in CSV format. With, search option you can search for any product from the list.\
*The pagination option is set to 10 products on a page.*

<Image align="center" border={true} caption="Products in Shopify" src="https://files.readme.io/99319bac4232c668e575ab6697519a542c281c3fa0f8ab8ea28f4ae5c1776f8b-image.png" />

### Catalog

You can upload and sync the catalog here. This is an important part of the **Unbxd Dev** app where synchronization will happen.

<Image align="center" border={true} caption="Catalog Sync" src="https://files.readme.io/7b93af75b56a6084f6659d0400c64c2623126691f880e4865f015f6180daa80f-image.png" />

Below capability is offered from Catalog page of Shopify:

| **Feature**                                     | **Description**                                                                                                                                                                                                                                                                                 |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Enable Sync**                                 | Two types of synchronization: Auto Synchronization and Manual Synchronization. By default, Manual Synchronization is enabled. To switch to Auto Synchronization, change the mode from the dropdown.                                                                                             |
| **Full Product Catalog Synchronization**        | To enable Manual Synchronization, select "NO" from the dropdown. To enable Auto Synchronization, select "Yes" from the dropdown.                                                                                                                                                                |
| **Incremental Product Catalog Synchronization** | Use Incremental Feed Upload to update/add multiple records (partial catalog upload). Only the products and product fields in the current JSON feed will be updated, while other products from previous uploads will remain untouched. For Incremental Sync, click the “Synchronization” button. |
| **Single Feed Upload**                          | For updating or adding a single product, use the Single Feed Upload option. Click the “Synchronization” button followed by the “Single Feed Upload” label. A popup will open, allowing you to select the product to add/update.                                                                 |

### Debuggability

The Debuggability section contains the Feed Upload Status History. It captures the following details of the Full/Incremental/Single Feed upload as:

| **Field**                               | **Description**                                                         |
| --------------------------------------- | ----------------------------------------------------------------------- |
| **File Name**                           | The name of the file being uploaded.                                    |
| **Upload ID**                           | The unique identifier assigned to the upload.                           |
| **Date**                                | The date of the upload.                                                 |
| **Message**                             | A message related to the upload (success, error details, etc.).         |
| **Status**                              | The status of the upload, which can be either "Success" or "Failure."   |
| **Type of Feed Upload**                 | The type of feed upload (e.g., full, incremental, single feed).         |
| **If Failed, Reason for Failure**       | The specific reason for the failure, if applicable.                     |
| **Timestamp**                           | The exact timestamp of when the event occurred (upload or failure).     |
| **Miscellaneous Errors and Exceptions** | Any other errors or exceptions that were encountered during the upload. |

You can also download the logs in a CSV or Excel file format. It contains the status of three types of Product Feed upload i.e. Single, Incremental and full feed upload.