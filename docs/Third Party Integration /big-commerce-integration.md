---
title: BigCommerce Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Unbxd App for BigCommerce helps you use Unbxd Site Search within your Bigcommerce store. This app allows companies (irrespective of their size) to integrate their websites on the BigCommerce platform with Unbxd’s Site Search solution.

It allows:

* Automatic Catalog Sync: Each product addition or deletion is sent to Unbxd servers every 24 hour automatically, to keep the data at Unbxd servers up-to-date.
* Analytics Integration: The Unbxd Extension for BigCommerce automatically tracks user analytics and behavior that is essential in order to provide accurate and user-specific search results. The extension analyzes every user event and tracks product clicks, products added to cart, and orders. With this information, a user profile is built for every user based on his/her affinity to a certain category, brand, or price.

All you have to do is signup to the Unbxd console,  install the BigCommerce plugin by providing the store hash and configure the BigCommerce store to replace BigCommerce default search experience with Unbxd experience

This section will help you install the Unbxd App, synchronise product catalog, and integrate analytics.

## Prerequisites

The following permissions are required to install the plugin :

* BigCommerce User Role : Store Owner or Store Administrator.
* During the installation process Unbxd app will request for following permissions :
  * View and Modify content, products and theme
  * Generate tokens to access your store’s storefront APIs
  * View basic configuration settings

## Installation

To install the BigCommerce app:

1. Signup to the Unbxd self serve console at [https://console.unbxd.io/signup](https://console.unbxd.io/signup)
2. Create the Site key
3. Choose the “BigCommerce Plugin” from the Platform section
4. Find the store hash for your BigCommerce store
5. Login to your BigCommerce store has store owner
6. Click on Home and scroll down to Advance Settings
7. Click on Advance Settings and scroll down to API Accounts
8. Click on Advance Settings then click on Create API Account and select Create V2/V3 API Token
9. Take a note of store hash present in the API Path i.e. [https://api.bigcommerce.com/stores/(store_hash)/v3/](https://api.bigcommerce.com/stores/\(store_hash)/v3/)
10. Enter the store hash value in the Unbxd console.
11. Accept the terms and conditions by clicking on the confirm button
12. Unbxd automatically starts fetching the catalog from the BigCommerce store

Follow the rest of the instructions on the Unbxd console. Confirm the BigCommerce plugin installation in the store

## Configuration

Once the plugin is installed then we have to do configurations in the BigCommerce store to replace the default BigCommerce search APIs, Autosuggest with Unbxd search APIs and autosuggest.

1. Log in to your BigCommerce store as a store owner
2. Using the sidebar, go to the Storefront and click on my themes
3. Make a copy of the current theme by clicking the Make a copy from the Advanced option
4. Scroll down to the copied theme, click on more option and click on Edit theme files
5. Open the search.html  file present in the templates > pages
6. To render Unbxd search results, we need to replace the default SRP template with Unbxd specific SRP template.To do this

* Remove the content of the partial head \{\{#partial “head”}}
* Replace the content of the partial page \{\{#partial “page”}} with \<div id=”UNX-search-wrapper”>\</div>

7. Save the file and close.
8. Open quick-search.html  file present in templates>components>common

In this we are going to replace the BigCommerce default search query input box with the Unbxd query input box. This will enable you to make search queries to the Unbxd servers rather than to default BigCommerce servers. To do this

1. Hide the default input box by setting CSS style property display as none using style=display:none  &#x20;
   Now just below this input box, add Unbxd input box by adding the this code snipped \<input class="UNX-search-input form-input" autocomplete="off" placeholder="Search">
   Checkout the screenshot below.
2. Save the file and close.
3. Now go back to my themes again and make the copied theme the LIVE theme.
4. As you will make this the LIVE theme, the search experience would be powered by Unbxd AI-based search engine.