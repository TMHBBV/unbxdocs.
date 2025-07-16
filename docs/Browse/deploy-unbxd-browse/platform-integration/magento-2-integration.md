---
title: Magento 2 Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Magento 2 is an open-source CMS designed to help eCommerce businesses scale. The Unbxd Extension for Magento 2 offers the following features:

* **Automatic Catalog Sync**: Automatically syncs product updates and deletions with Unbxd servers.
* **Analytics Integration**: Tracks user behavior (clicks, add-to-cart, orders) to power personalized experiences.
* **Product Integration**: Enables Unbxd Site Search, Browse, and Recommendations with customizable UI templates.

***

## Prerequisites

Before using the Unbxd Site Search extension:

* Create an Unbxd account and site in the Unbxd Console.
* Install Magento 2 (version 2.2.x and above) on your server.

***

## Installation

You can install the Unbxd Magento extension in two ways:

### 1. Using Composer

```bash
composer require unbxd/magento2-search
php bin/magento module:enable Unbxd_Search
php bin/magento module:enable Unbxd_ProductFeed
php bin/magento module:enable Unbxd_Analytics
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy
php bin/magento cache:flush
```

### 2. Direct Plugin File Upload

Download the zip files for:

* `UnbxdProductFeed`
* `UnbxdAnalytics`
* `UnbxdSearch`

Extract and copy files to:

```bash
mkdir -p app/code/Unbxd/SearchJs
mkdir app/code/Unbxd/ProductFeed
mkdir app/code/Unbxd/Analytics
```

Run:

```bash
php bin/magento module:enable Unbxd_Search
php bin/magento module:enable Unbxd_ProductFeed
php bin/magento module:enable Unbxd_Analytics
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy
php bin/magento cache:flush
```

***

## Authentication

To authenticate, use:

* Site Key: The unique identifier of a Site. Each site added on your dashboard will have a visible unique alphanumeric key
* API Key: The unique identifier of the API calls made from an account. Unbxd provides only one API Key per account.
* Secret Key: An additional securely generated key used in important request calls such as Product Feed upload. Secret Key is not exposed in the URL. Unbxd provides one Secret Key per account.

You can find these in the Unbxd Console: `Manage > Configure Site > Keys`.

Steps:

1. Go to `Unbxd > Setup`
2. Enter keys in **General Settings**
3. Click **Save Config**

![](https://files.readme.io/04bf9f7b46facfbf1df11a8242b206d55c0b2d8446dccf5869c414aa3ebb3b51-image.png)

<br />

To authenticate:

On the Unbxd tab, click Setup. In General Settings, type in the values for:

* Site Key
* Secret Key
* API Key

To know, where will you get your Site, Secret, or API keys from, refer to our Search Documentation.\
Click Save Config.
To know more, check the FEED APIs section.

NOTE: All the keys other than the Site Key need to be saved somewhere as they would be hidden behind the asterisk value.

***

## Catalog Synchronization

Unbxd uses product feeds to keep your catalog updated.

### Status Codes:

* `Running`: Feed is processing
* `Indexing`: Feed is being indexed
* `Complete`: Upload successful
* `Error`: Upload failed

### Product Types Supported

* Simple
* Configurable
* Grouped
* Virtual
* Bundle
* Downloadable
* Gift Card

### Exclusion Criteria

* Disabled
* Out of Stock
* Not Visible Individually
* Without Images

***

## Category Configuration

Configuration options:

* Use Category ID
* Retain Disabled Categories
* Fetch from Category Entity Tables

***

## Product Images Settings

Enable this under `Unbxd > Catalog > Product Image Settings`.

Image types:

* Base Image
* Small Image
* Thumbnail
* Swatch Image

***

## Indexing Settings

Enable indexing via:

```text
Unbxd > Catalog > Indexing Settings > Enable Indexing Queue
```

* `Yes`: Uses scheduled cron jobs
* `No`: Triggers immediate indexing

Supports **Indexing Queue View** for monitoring operations.

***

## Indexing Optimization

Feeds are split into batches of 10,000 products to reduce memory usage.

### Reader DB Support

Use dedicated read-only DB for catalog fetches if needed.

***

## Data Fields Mapping

You can manually map Unbxd fields like:

* Availability
* Category Path ID
* Image URL
* Product URL
* Title
* UniqueID

***

## Catalog Sync Options

1. **Automatic** (via cron)
2. **Manual** (via admin UI)
3. **CLI** (command line)

### CLI Commands

```bash
# Full catalog sync
php bin/magento unbxd:product-feed:full

# Incremental sync
php bin/magento unbxd:product-feed:incremental

# Check upload size
php bin/magento unbxd:product-feed:upload-size
```

***

## Website Configuration

Settings are populated from `UnbxdSiteName` and `UnbxdApiKey`.

### Autosuggest

Enable via: `Unbxd > Website Config > Autosuggest > Enable: Yes`

Supports custom input selectors for templates.

### Search

Enable via: `Unbxd > Website Config > Search > Enable: Yes`

### Browse

Enable via: `Unbxd > Website Config > Category > Enable: Yes`

### Analytics

Enable via: `Unbxd > Website Config > Analytics > Enable: Yes`

### Recommendations

1. Navigate to `Unbxd > Website Config > Recommendations`
2. Create widgets and assign to pages

***

## Custom Template Support

Options:

1. **JSON Config** for layout/styling adjustments
2. **Custom Stylesheet** override
3. **Custom Extension**

Modify:

* `templates/search/productresults.phtml`
* `templates/category/productresults.phtml`
* `catalog_category_view.xml`
* `unbxd_search_handle.xml`

***

## Indexing Queue View

Tracks reindex operations with metadata like:

* ID
* Store View
* Created/Started/Finished Timestamps
* Status (Pending, Running, Complete, Error, Hold)
* Action Types (Row, List, Full)

Actions:

* View
* Hold/Unhold
* Delete

***

## Feed View

Tracks all feed uploads (Full/Incremental) and metadata:

* Execution time
* Operation type
* Affected entities
* Additional information

Supports:

* Log view/download
* Filters
* Default View
* Column Selection

***

## Upgrade

### Manual

If installed in `app/code/Unbxd`:

```bash
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy
php bin/magento cache:flush
```

### Composer

If installed via Composer:

```bash
composer update unbxd/*
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy
php bin/magento cache:flush
```

***

## Uninstall

### Manual

1. Disable modules:

```bash
php bin/magento module:disable Unbxd_Search
php bin/magento module:disable Unbxd_Analytics
php bin/magento module:disable Unbxd_ProductFeed
```

2. Remove files:

```bash
rm -rf app/code/Unbxd
rm -rf var/log/unbxd
```

3. Drop tables and remove config:

```sql
SET FOREIGN_KEY_CHECKS=0;
DROP TABLE IF EXISTS unbxdproductfeedindexingqueue;
DROP TABLE IF EXISTS unbxdproductfeedfeedview;
SET FOREIGN_KEY_CHECKS=1;

DELETE FROM core_config_data WHERE path LIKE '%unbxd%';
DELETE FROM setup_module WHERE module LIKE 'Unbxd_%';
```

4. Run:

```bash
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy
php bin/magento cache:flush
```

### Composer

1. Disable and uninstall:

```bash
php bin/magento module:disable Unbxd_Search
php bin/magento module:disable Unbxd_Analytics
php bin/magento module:disable Unbxd_ProductFeed

php bin/magento module:uninstall -r Unbxd_Search
php bin/magento module:uninstall -r Unbxd_Analytics
php bin/magento module:uninstall -r Unbxd_ProductFeed
```

2. Clean up:

```bash
composer remove unbxd/*
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy
php bin/magento cache:flush
```

***

Let me know if you’d like this in a downloadable `.md` file or want sections modularized for easier documentation integration.