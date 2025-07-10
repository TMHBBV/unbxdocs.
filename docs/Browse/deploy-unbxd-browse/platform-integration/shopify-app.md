---
title: Shopify App
deprecated: false
hidden: false
metadata:
  robots: index
---
# Installation

To install the Shopify app:

1. Navigate to: [https://shopify-dev.unbxd.com/login](https://shopify-dev.unbxd.com/login)
2. Enter your details and click **‘Install’** to download the app.
3. Once downloaded, install the app in your Shopify store.
4. After installation, you will see the **Unbxd App** listed under **Shopify > Apps**.

***

# Configuration

To configure the Shopify app:

1. Log in to the **Unbxd Console**.
2. Copy the **Site Key**, **Secret Key**, and **API Key** from the `Manage > Configure Site` section.
3. Go to **Unbxd Site Search App** under **Shopify > Apps**.
4. Paste the copied keys into the **Setup** section.
5. Submit the form. Upon success, you’ll see:

```
"Keys Updated successfully"
```

***

# Components

The Shopify app consists of four major components:

* **Product**
* **Catalog**
* **Debuggability**
* **Analytics**

***

## Product

In this section, you can easily sync all your Shopify products:

* Navigate to **Products > Shopify Products**.
* View all synced Shopify products in one place.
* Options available:

  * Download products in **Excel** or **CSV** format.
  * Use the **search** feature to find specific products.
  * View 10 products per page (pagination enabled).

***

## Catalog

You can upload and sync your product catalog here — a core function of the Unbxd Dev app.

### Enable Sync

Two types of synchronization available:

* **Manual Synchronization** (default)
* **Auto Synchronization**

> To switch modes, change the selection from the dropdown.

### Full Product Catalog Synchronization

* Manual sync: select `No` from the dropdown.
* Auto sync: select `Yes` from the dropdown.

### Incremental Product Catalog Synchronization

* Use **Incremental Feed Upload** to update/add multiple records (partial catalog updates).
* Updates only the product fields sent in the feed; others remain unchanged.
* To perform incremental sync:

  * Click the **"Synchronization"** button.

### Single Feed Upload

* For adding/updating a single product.
* Steps:

  1. Click **"Synchronization"**.
  2. Select the **Single Feed Upload** label.
  3. Choose the product to upload via the popup.

***

### Debuggability

This section contains the **Feed Upload Status History**, including:

* **File Name**
* **Upload ID**
* **Date**
* **Message**
* **Status** (Success/Failure)
* **Type of Feed Upload**
* **Failure Reason** (if any)
* **Timestamp**
* **Miscellaneous Errors & Exceptions**

> Logs can be downloaded in **CSV** or **Excel** format.

It provides the status for all types of product feed uploads:

* Single Feed Upload
* Incremental Feed Upload
* Full Feed Upload