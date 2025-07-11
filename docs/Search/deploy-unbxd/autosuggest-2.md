---
title: Autosuggest
deprecated: false
hidden: false
metadata:
  robots: index
---
Autosuggest documentation\
Having product suggestions appear as shoppers type in a query isn’t just about efficiency but also about enhancing your shopper’s user experience. The true value and impact on the user’s search experience come from how to autocomplete suggestions that can assist and guide users toward better search queries.

The purpose of this document is to provide the necessary steps to be followed to integrate Unbxd autosuggest using Unbxd Autosuggest JS SDK.

| **Library**    | **Version**                  |
| -------------- | ---------------------------- |
| **jQuery**     | 1.11.3 or higher (`1.11.3+`) |
| **Handlebars** | 3.0.3 or higher (`3.0.3+`)   |

If your website is not using the above mentioned libraries then the same can be bundled along with unbxd autosuggest js file. For more details check config options in bundle build procedure.

## Quickstart

Through this integration guide you will learn how to integrate the Unbxd AutoSuggest JS SDK to power the keyword and product suggestions on your website.The final integrated result that we are aiming at with this step by step guide can be seen at this [codesandbox](https://codesandbox.io/p/sandbox/shy-currying-1ppvv?file=%2Findex.html).

> 📘 Note
>
> The Unbxd JS SDK uses Handlebars as the HTML templating engine. Wherever you see config options that expect an HTML string template, it would be in the Handlebars template format.

The first step is to include the Unbxd Autosuggest JS along with its required dependencies. For this add the following CSS & JS files into the “” section of your HTML page

```
<head>
   <link rel="stylesheet" href="./css/styles.css"/>
    <script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"> </script>
     <script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.5.3/handlebars.min.js"> </script>
    <script type="text/javascript" src="//libraries.unbxdapi.com/unbxdAutosuggest_v1.js"> </script>
```

To instantiate the autosuggest and bind it to the search box,

1. Invoke the “unbxdAutoSuggestFunction” function available as a window variable by passing the instance of jQuery & handlebar as arguments.
2. Select the input box element using jquery and invoke “unbxdautocomplete” function (a Unbxd function added to jQuery prototype) passing the suggestion options object.