---
title: Unbxd-Magento Set Up
deprecated: false
hidden: false
metadata:
  robots: index
---
# General Settings

This section allows you to indicate the product types available in your catalog while excluding specific categories of products while synchronizing.

To upload product types:

On the Unbxd tab, click Catalog

In General Settings, within Available Product Types, select All Available Types to select all available product types within your catalog. Click the drop-down box to select from one of the product types.\
Click Save Config
The Unbxd extension supports seven types of products:

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/b38f78b3d250c615cead7c14cf9971c2177bc5c5d99a3c624db40c726b70f26f-image.png" />

* Simple Product: A simple product is a physical item with a single SKU. When converted to the Unbxd format, a simple product is considered as a Normal Feed.
* Configurable Product: A configurable product is a parent product of multiple simple products. When converted to the Unbxd format, configurable products are considered as variants.
* Grouped Product: A grouped product presents multiple, standalone products as a group. You can offer variations of a single product, or group them for a promotion. The products can be purchased separately or as a group. Like configurable products, when converted to the Unbxd format, grouped products are considered as variants.
* Virtual Product: A Virtual Product or Digital Product can be used for intangible items such as a membership, service, warranty, or subscription. They can be sold individually or included in grouped or bundled products. They are the same as simple products but without the weight field.
* Bundle Product: Bundle product lets the shoppers choose from a variety of options to create their own customized version. The options are a bundle of simple products.
* Downloadable Product: A downloadable product can be anything that you can deliver as a file, such as an eBook, music, video, software application, or update. You can offer an album for sale and sell each song individually. You can also use a downloadable product to deliver an electronic version of your product catalog.
* Gift Card: The three types of gift cards are Virtual, Physical, and Combined. Gift cards can be set to Redeemable or Non-Redeemable. The lifetime of a gift card can be unlimited or set to a number of days. The value of a gift card can be set to a fixed amount or set to an open amount with a minimum and maximum value.

> 📘 Note
>
> If your catalog has a mix of 'Simple products' and 'Configurable products' and you wish to send both Parent products and Variants to Unbxd, select both 'Simple Product' and 'Configurable Product' in the 'Available Products Types' dropdown

Our extension allows you to exclude four exclusive criteria of products:

* Disabled: Indicates products that have been disabled from being listed in the Product Listing Page
* Out Of Stock: Indicates products where the inventory count is 0
* Not Visible Individually: Indicates products that are available only as a bundle
* Without Images: Indicates products where there isn’t an available image

> 📘 NOTE
>
> Select only one value

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/3f9ce54af149d1ce4bcf63d1d03c2b38b19eb2c319edae103fd5f4c3d8953a73-image.png" />

**Maximum Number of Synchronization Attempts**\
The number of synchronization allowed in case of page load errors is specified in this bar. The value can vary between 1 to 5.