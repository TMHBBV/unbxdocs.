---
title: Configure Site
excerpt: Streamline and secure connection between your site and Unbxd’s features.
deprecated: false
hidden: false
metadata:
  robots: index
---
The **Configure Site** page is your control center for integrating and authenticating your e-Commerce platform with Unbxd's services. It is divided into two key sections: **Keys** and **APIs**,

This section is useful for integration between your store and Unbxd services.

* Authenticating with Unbxd's services using secure keys.
* Accessing preconfigured API endpoints for Search, Feed, and Suggest functionalities.
* Simplifying integration setup with minimal effort.

***

# Keys

This section provides all the access credentials required to connect with various Unbxd services. Each key type serves a different purpose:

* **Site Key**: A unique identifier for your specific site. It is mandatory for every API request sent to Unbxd services and helps route the requests correctly.

* **Secret Key**:\
  A confidential 32-digit hexadecimal key used for backend operations like catalog feed uploads. It is not used in the public-facing APIs.

* **API Key**: Enables search, autosuggest, and analytics API calls. It works with the Site Key to allow requests from your client applications.

* **Platform Key** *(Coming Soon)*: Intended for developers managing multiple eCommerce sites. This key will allow administrative actions like adding or deleting a site through platform-level APIs.

All keys have **Copy** buttons for quick access when configuring integrations or writing scripts.

***

# APIs

This section gives you ready-to-use API endpoints with your site-specific credentials embedded, making it easy to integrate Unbxd features without additional configuration.

* **Commerce Search API**: Used to power the search functionality on your eCommerce site. Includes your site and API keys for instant plug-and-play integration.

* **Catalog Feed API**: A CURL-based endpoint for syncing your product catalog with Unbxd. It supports uploading complete product feeds along with authorization via your secret key.

* **Autosuggest (Autocomplete API)**: Enhances the search experience by showing intelligent product suggestions as the user types. This API ensures faster product discovery and improved UX.

Each API block features **COPY** (and **OPEN**, where applicable) buttons for quick access during development..