---
title: Configure Site
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

This guide provides the necessary steps to configure Unbxd Search for your site or application. By following this process, you will link your site to the Unbxd platform, set up essential API keys, upload your catalog data, and map fields for optimal search relevance. This guide is intended to help you understand the required configurations and provide best practices for efficient integration of Unbxd Search.

## Prerequisites

Before you start configuring your Unbxd Search, ensure the following steps are completed:

1. **Account Access**: You must have an active Unbxd account. Unbxd Account Manager will provide access to the signup form and related details.
2. **Website URL**: Your website or app's URL must be ready for integration.
3. **Catalog Data**: You need to have your product catalog in a format ready for upload (e.g., CSV, JSON, or so on).
4. **Access to API Keys**: You will need the site key, secret key, and API key to authenticate API calls.

## Set-up Unbxd Panel

### Configure Site

To access the console and set up your site, enter in the details on the signup form shared by your Account Manager. These details will help link your site/app to the **Unbxd** platform.

**Required Fields for Configuration**:

1. **Website URL**: Enter the URL of your site/app for which you want to integrate **Unbxd Search**. This will add a site to the console and link your site to it. You can also add more sites from the console’s interface at any time.
2. **Region**: Select the physical location of Unbxd servers (Singapore or the US) that are closest to your server. This will ensure the best search response times. Choose Singapore if you're located in the Asia-Pacific (APAC) region, otherwise select US.

### Keys

Keys are essential for making API calls to the Unbxd platform from your site. To access your keys through the console navigate to **Manage** > **Configure Site**.

Unbxd Search uses three types of keys to authenticate API calls:

1. **Site Key:** A unique alphanumeric key for each site on the Unbxd platform. It is used in all API calls to identify your site.

<Image align="center" border={true} caption="Site Key" src="https://files.readme.io/f99d29ff8254e0e290d1ab3051f562429b71e5551c6263dd4969d9d388876a29-image.png" width="80% " />

2. **Secret Key**: A unique 32-character hexadecimal key for your account. This key is not exposed in the URL and is used for secure operations, such as catalog uploads.

<Image align="center" border={true} caption="Secret Key" src="https://files.readme.io/498fea6b8d2929f042cf837a4f65f09bda778a6e080c51cf80b691d54682838a-image.png" width="80% " />

3. API Key: A unique hexadecimal API key used to identify your account. Like the site key, it is also used in every API call to authenticate requests.

<Image align="center" border={true} caption="API Key" src="https://files.readme.io/16674d30158860efbf446b3addbd51ee9948f8c6c430fab5014f792cf893fdd4-image.png" width="80% " />

<br />

### APIs

APIs are the building blocks of Unbxd Search. Navigate to **Manage** > **Configure Site** > **APIs**. API calls will be used for different purposes such as **Catalog Upload**, **Search**, and **typeahead features**.

Available APIs include:

1. Commerce Search API: Used to retrieve search results based on user queries.
2. Catalog Feed API: Used to upload and manage catalog data.
3. Typeahead (Autocomplete) API: Used to provide search suggestions as the user types in the search bar.

Copy the relevant API signature from the interface to start making API calls to the Unbxd platform.