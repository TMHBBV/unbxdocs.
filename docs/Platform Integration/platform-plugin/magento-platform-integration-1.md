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

1. Extract and copy files to the Magento root directory.
2. Create missing directories: