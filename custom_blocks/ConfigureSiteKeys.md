---
name: ConfigureSiteKeys
---
# Keys

This section provides all the access credentials required to connect with various Unbxd services. Each key type serves a different purpose:

* **Site Key**: A unique identifier for your specific site. It is mandatory for every API request sent to Unbxd services and helps route the requests correctly.

* **Secret Key**:\
  A confidential 32-digit hexadecimal key used for backend operations like catalog feed uploads. It is not used in the public-facing APIs.

* **API Key**: Enables search, autosuggest, and analytics API calls. It works with the Site Key to allow requests from your client applications.

* **Platform Key** *(Coming Soon)*: Intended for developers managing multiple eCommerce sites. This key will allow administrative actions like adding or deleting a site through platform-level APIs.

All keys have **Copy** buttons for quick access when configuring integrations or writing scripts.