---
title: Magento Platform Integration
excerpt: Integration of Magento 2 to Netcore Unbxd services
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Magento 2 is an open-source CMS that gives eCommerce business owners an opportunity to expand their business operations in the digital eCommerce world. Essentially, Magento is a powerful system that is flexible, scalable, and easy to customize.

It enables the following two functionalities:

* **Automatic Catalog Sync**: Each product change in Magento 2, whether an addition or removal, is sent to the Netcore Unbxd servers based on your chosen schedule. This ensures that our data remains current for all customers.
* **Product Integration**: Unbxd Extension for Magento 2 provides easy integration of Unbxd Site Search with your website, facilitating a fully functional search. This plugin comes equipped with user-friendly UI/UX libraries and templates for instant search interface setup. You also have the option to modify the UI with custom templates. Moreover, the extension facilitates easy integration of Browse and Recommendations, optimizing your online shopping experience.

## Prerequisites

Before you can use the Netcore Unbxd Site Search extension make sure the below is completed:

1. Create an Unbxd account and a site within our Console.
2. Set up Magento 2 on your server.

> 📘 Note
>
> Supported versions are **Magento 2.2.x** and above.

# Installation Methods

You can install the Unbxd extension in two ways: **Composer** or **Direct File Upload**.

### Composer Installation

It allows you to easily integrate external packages (like Unbxd extensions) into your Magento 2 environment without having to manually download and upload files. Follow the steps below

1. Login to SSH Console on your server.
2. Navigate to the Magento root directory.
3. Run the following commands:

```
composer require unbxd/magento2-product-feed

composer require unbxd/magento2-search-js

php bin/magento module:enable Unbxd_ProductFeed

php bin/magento module:enable Unbxd_SearchJs

php bin/magento setup:upgrade

php bin/magento setup:di:compile

php bin/magento setup:static-content:deploy

php bin/magento cache:flush
```

Once this is done, you have successfully downloaded, installed, and enabled the Unbxd Magento extension using Composer.

### Direct Plugin Feed Upload

This is a method of integrating product data with an external service (like Unbxd) directly from your Magento 2 store using plugin files, rather than through a dependency manager. Follow the steps below:

1. Download the [extension](https://drive.google.com/file/d/1N34h2WHsn1Vmm763isSjw6o90ZO32b1F/view?usp=drive_link) from the GitHub repository.

* Unbxd [ProductFeed](https://drive.google.com/file/d/1H_v3hd6KJsKL-s3u0a_9uWKVSMvczcA2/view?usp=drive_link)
* Unbxd [Search](https://drive.google.com/file/d/1N34h2WHsn1Vmm763isSjw6o90ZO32b1F/view?usp=drive_link)

2. Extract and copy files to the Magento root directory.
3. Create missing directories. If the ***app/code/Unbxd*** folder is missing, follow the steps below to create it:

```
mkdir -p app/code/Unbxd/SearchJs
mkdir app/code/Unbxd/ProductFeed  
```

4. Login to the SSH console of your server and run the following commands from Magento 2 root directory to enable the extensions:

```
php bin/magento module:enable Unbxd_SearchJs
php bin/magento module:enable Unbxd_ProductFeed
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy
php bin/magento cache:flush 
```

Once this is done, you have successfully downloaded, installed, and enabled the Unbxd Magento extension using Direct Plugin Feed Upload.

# Authentication

Once the Netcore Unbxd extension is installed, you need to authenticate it using your Unbxd account keys (also known as Authentication Keys).

> 📘 Important
>
> You can find your authentication keys within the Welcome mail you receive when signing up with Netcore Unbxd. Alternatively, you can also find the following keys in the within your Unbxd Console. **Manage** > **Configure Site** > **Keys**
>
> Also, If you have more than one Magento store, select the correct store from the Store View option at the top of the screen to update the Site Key, API Key, and Secret Key.

* **Site Key**: Unique identifier for your Unbxd site.
* **API Key**: Unique identifier for API calls.
* **Secret Key**: Used for secure requests like Product Feed uploads.

In Magento:

1. Navigate to the Netcore Unbxd tab in the admin panel.
2. Under General Settings, enter your Site Key, API Key, and Secret Key copied from Netcore Unbxd console.
3. Click Save Configuration.

<Image align="center" border={true} caption="Setting up Netcore Unbxd Keys in Magento" src="https://files.readme.io/ce1d1405912b8440ec90dbba664a55551c06d8c4afb7b5f599ca892aaf92a15f-Authentication.png" width="80% " />

To know more, Refer the Feed API documentation [here](https://unbxdocs.readme.io/update/docs/feed-preparation-and-upload#/).

> 📘 NOTE
>
> The API key and Secret key must be saved somewhere as they are hidden behind the asterisk value.

# Catalog Synchronization

Unbxd algorithms rely on product-related information from your product catalog. When you send your catalog to Unbxd, we convert it into our format, store it, and index it on our servers. This process is known as the Product Feed.

**Synchronizing Your Catalog Feed**\
By synchronizing your feed, your Unbxd extension will be able to retrieve the catalog information from your Magento database. To know more, refer to the  [documentation](https://unbxdocs.readme.io/update/docs/set-up-analytics#/) for Catalog preparation.

When synchronizing a catalog, you'll see one of the following status updates:

| **Status Code** | **Description**                                                             |
| --------------- | --------------------------------------------------------------------------- |
| **Running**     | The catalog synchronization is in progress and has been submitted to Unbxd. |
| **Indexing**    | The catalog data is currently being indexed.                                |
| **Complete**    | The catalog has been successfully uploaded.                                 |
| **Error**       | There was an issue with the catalog synchronization, and it has failed.     |

These statuses help you track the progress and identify any issues during synchronization.