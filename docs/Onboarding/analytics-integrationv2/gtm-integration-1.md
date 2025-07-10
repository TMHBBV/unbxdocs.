---
title: GTM Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
Google Tag Manager (GTM) simplifies the process of managing and deploying tags on your website. It acts as a bridge, allowing data from your website to flow seamlessly into other data sources like Google Analytics. GTM is particularly useful when managing multiple tags, as it consolidates all the code in one centralized location, making updates and maintenance easier and more efficient.

# How to implement Analytics integration using GTM?

1. Add the following `<script>` tag at the end of your site's HTML body.

```
<script   
src="https://libraries.unbxdapi.com/sdk-clients/PROD_SITEKEY/ua/ua.js">
</script>
```