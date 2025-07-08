---
title: Java Library Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
Unbxd Search JS Library helps you build awesome search experiences with Unbxd Search powering the search results page. With a few simple configurations, you can quickly get up and running with our default template to experience the Unbxd Search functionalities.

Version\
The current version is v2.0.0.

## Quick Integration with Unbxd Template

There are two ways in which you can quickly get up and running with our default template to try out our JS Library functionalities:

If you have a console account already, follow the below steps:

Go to the console dashboard  & click the Website Preview button.\
Then click the Download UI Kit button to download the Unbxd Default template package for your catalog.
Unzip the package & open the index.html file in your browser to view the search results landing page for your catalog with the Unbxd default template.

Or,

Download the Unbxd Search Library default template package from here .\
Unzip the package & open the index.html file inside the folder.\
Update the global variables UNBXD\_SITE\_KEY and UNBXD\_API\_KEY present in the \<head> section \<script>  tag of the index.html file with your Site key & API keys.

```
window.UNBXD_SITE_KEY=  < your site key >//yoursitekey
window.UNBXD_API_KEY= < your API key>//yourapikey
```

Update the global variable “UNBXD\_MAPPED\_FIELDS” with the field mapping of your catalog fields.

```
 window.UNBXD_MAPPED_FIELDS = {
   "unxTitle": "title",
  "unxImageUrl": "Image_Link",
   "unxPrice": "Price",
   "unxDescription":" productDescription"
};
```

Finally, open index.html in your browser to view the search results landing page for your catalog with the Unbxd default template.

## Quick Integration to your Site

To integrate the JS Library into your site, follow the following steps:

Include the JS Library. This can be done in two ways:\
a. Adding it as a URL to your HTML file.
First, add the following CSS file into the “ section of your HTML page to get the Unbxd default theme styles.

```
<link rel="stylesheet" href="https://libraries.unbxdapi.com/search-sdk/v2.0.0/vanillaSearch.min.css" /> 
```

Then add the following script file for the library at the end of the body section.

```
<script type="text/javascript" src="https://libraries.unbxdapi.com/search-sdk/v2.0.0/vanillaSearch.min.js">
```