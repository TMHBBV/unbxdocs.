---
title: GTM Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
Google Tag Manager (GTM) simplifies the process of managing and deploying tags on your website. It acts as a bridge, allowing data from your website to flow seamlessly into other data sources like Google Analytics. GTM is particularly useful when managing multiple tags, as it consolidates all the code in one centralized location, making updates and maintenance easier and more efficient.

## How to implement Analytics integration using GTM?


  

  Add the following `<script>` tag at the end of your site's HTML body.
    ```html
 <script   
  src="https://libraries.unbxdapi.com/sdk-clients/PROD_SITEKEY/ua/ua.js">
</script>
```

  
 
  Initialize the GTM window object on page load if it is not already present, using the respective `ContainerID` and `HTMLId`.
  ```html
/ Container ID is present in GTM-XXXX format in the GTM Dashboard
   // HTML ID can be found in the URL. Eg:
   // containers/422XXXX/workspaces/20, 20 is the HTML ID
 
   <script type="text/javascript">
       window.google_tag_manager[{{Container ID }}].onHtmlSuccess({{ HTML ID }}); });
   </script>
```
  
  title="Import Unbxd Template on GTM"
    1. <a href="https://d29240o5wkzuh9.cloudfront.net/GTM-5GJ8NTD_workspace2.json">Download the JSON template</a> for Tags, Triggers, and Variables.
    2. After downloading the JSON template, follow the steps in this document to import it into your GTM container.
  

Follow the steps below for each event to set up the `dataLayer`.


## How to track each event?