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

Let us walk through the important configs that need to be passed along with their values for powering the auto suggest component.\
NOTE: You can find a detailed list of all acceptable configs at the end of this doc.

## Authentication

Once installed, you need to authenticate your Unbxd extension using your Unbxd account keys (also known as Authentication Keys).

Whenever a customer signs up with Unbxd, they are issued one or more site keys and api keys depending on their use case. Some common scenarios:

For a customer with one website and two environments (production and staging), 2 site keys (one for each environment) and  1 API key is issued\
For a customer with more than one website (multi website vendor), the site key would be issued for every website + environment combination. So there would be an “n” number (equal to the number of website’s) of API keys generated.
For multiple site keys, check if you have:

more than one environment\
more than one website
different product set for staging and live, or
wish to track search performance and clicks separately for every microsite.
To get your Site Key and API Key in the console, please refer to the steps mentioned in the Help Documentation

Pass the Site Key and API Key that you get from the console in the “siteName” and “APIKey” configs.

| **Field**       | **Value**                                                              |
| --------------- | ---------------------------------------------------------------------- |
| **Data Type**   | String                                                                 |
| **Required**    | True                                                                   |
| **Default**     | N/A                                                                    |
| **Description** | Site name assigned by Unbxd (unique identifier for each customer/site) |

**APIKey**:

| **Field**       | **Value**                        |
| --------------- | -------------------------------- |
| **Data Type**   | String                           |
| **Required**    | True                             |
| **Default**     | N/A                              |
| **Description** | Unique API key assigned by Unbxd |

**Platform:**

| **Field**       | **Value**                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Data Type**   | String                                                                                                             |
| **Required**    | False                                                                                                              |
| **Default**     | `com`                                                                                                              |
| **Description** | Autosuggest supports two platforms: `io` and `com`. Customers are advised to use `io` as it is the latest version. |

At the end of this step, you should have the Site Key & API Key which can be passed into the “siteName” & “APIKey” configs as shown below:

```
   new Unbxd.setSearch({
       siteName: "<Your Site Name>",
       APIKey: "< Your API key>"
     });
```

### Configure the autosuggest options object

In this, you would be introduced to the various options properties which can be leveraged to customize the behavior and look and feel of the autosuggest widget.

**Template Design**\
The autosuggest widget can be styled as either 1 column or 2 column layout, depending on available real estate and business needs, the two columns are referenced as “maincontent” and “sidecontent”.

#### Styling the autosuggest widge

**template**:

| **Parameter**     | **Data Type** | **Required** | **Default**        | **Description**                                                                                                        | **Possible / Sample Values**                         |
| ----------------- | ------------- | ------------ | ------------------ | ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| **column**        | String        | False        | `1column`          | Choose the column layout for the widget. Recommended: `2column` for tablet/desktop and `1column` for mobile.           | `1column`, `2column`                                 |
| **mainWidth**     | Number        | False        | `0`                | Width of the main content column in a two-column layout.                                                               | `200`, `jQuery("#search_input").outerWidth() * 0.52` |
| **sideWidth**     | Number        | False        | `180`              | Width of the side content column in a two-column layout.                                                               | `180`                                                |
| **position**      | String        | False        | `absolute`         | Sets the CSS `position` property for the widget.                                                                       | `absolute`, `fixed`, `relative`, etc.                |
| **sideContentOn** | String        | False        | `right`            | Determines side content position in 2-column layout. Use `left` for searchboxes aligned on the right side of the page. | `left`, `right`                                      |
| **theme**         | String        | False        | `#ff8400`          | Extension point for applying custom styling to the widget.                                                             | `#ff8400`, `10000000`                                |
| **loadingClass**  | String        | False        | `unbxd-as-loading` | Class name for loader element shown while autosuggest is fetching results.                                             | `unbxd-as-loading`                                   |
| **resultClass**   | String        | False        | `unbxd-as-wrapper` | Class name applied to the widget container’s parent div — useful for applying custom styles.                           | `unbxd-as-wrapper`                                   |

At the end of this step, you should have populated all styling options available in the autosuggest widget as shown below,

```
new Unbxd.setSearch({
       siteName: "",
       APIKey: "",
      version: “io”,
   resultsClass: "unbxd-as-wrapper",
      loadingClass: "unbxd-as-loading",
   mainWidth: jQuery("#search_input").outerWidth() * 0.52,
   sideWidth: 524,
   zIndex: 1000000,
   position: "relative",
   sideContentOn: "right",
   template: "2column",
   theme: "#ff8400"
 
     });
```

## Configure the functional behaviour

The following config options can be used to control the functional behaviour of the widget.

| **Parameter** | **Data Type** | **Required** | **Default** | **Description**                                                                         |
| ------------- | ------------- | ------------ | ----------- | --------------------------------------------------------------------------------------- |
| **minChars**  | Number        | False        | `1`         | The minimum number of characters a user must type before autosuggestions are triggered. |
| **delay**     | Number        | False        | `100`       | Delay (in milliseconds) between user keystrokes and the update of autosuggest results.  |

**Configure the contents of template**\
Unbxd offers 6 different types of suggestion for the searched term,

* Keyword suggestion (Textual match to complete or spell correct the searched term)
* Top queries (Based on the popular searches across customer profiles)
* Popular suggestion (Handpicked suggestion to be boosted)
* In fields (keyword suggestion within an attribute in a product – suggestion within brand, product type)
* Featured fields (Similar to keyword suggestion but limited within a given attribute in a product)
* Popular products

In the following sections , we will discuss how to configure and render each of these suggestions within autosuggest widget.

| **Parameter** | **Data Type**    | **Required** | **Default**                                                           | **Description**                                                            | **Possible Values**                                                                                                                                                              |
| ------------- | ---------------- | ------------ | --------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **mainTpl**   | Array of Strings | False        | `[‘inFields’, ‘keywordSuggestions’, ‘topQueries’, ‘popularProducts’]` | Suggestion types to display in the **main content** area where applicable. | All 6 suggestion types listed in the [introduction section](https://docs.google.com/document/d/1ob1DdJvZ2oEyf8bkNRfJh7EtsLpEjbQirUDqq7HEZfk/edit?tab=t.0#heading=h.mn12pktcy79k) |
| **sideTpl**   | Array of Strings | False        | `[]`                                                                  | Suggestion types to display in the **side content** area when applicable.  | All 6 suggestion types listed in the [introduction section](https://docs.google.com/document/d/1ob1DdJvZ2oEyf8bkNRfJh7EtsLpEjbQirUDqq7HEZfk/edit?tab=t.0#heading=h.mn12pktcy79k) |

At the end of this step the config should be as below,

```
   new Unbxd.setSearch({
       siteName: "",
       APIKey: "",
      version: “io”,
   resultsClass: "unbxd-as-wrapper",
      loadingClass: "unbxd-as-loading",
   mainWidth: jQuery("#search_input").outerWidth() * 0.52,
   sideWidth: 524,
   zIndex: 1000000,
   position: "relative",
   sideContentOn: "right",
   template: "2column",
   theme: "#ff8400",
   mainTpl: ["topQueries","keywordSuggestions","promotedSuggestion","inFields"
       ],
       sideTpl: ["popularProducts"],
     });
```

<br />

## Configure the various suggestions types

In this section you would configure details of each suggestion type which is configured in the mainTpl or SideTpl

**keywordSuggestions**:

**Default**:

```
{
<p><span style="font-weight: 400;">                count: 2,</span></p>
<p><span style="font-weight: 400;">                header: "",</span></p>
<p><span style="font-weight: 400;">                tpl: "{{{safestring highlighted}}}"</span></p>
<p><span style="font-weight: 400;">   },</span></p>
```

<br />

**Description**

* **count:number**: The number of suggestions to be shown
* **header:String**: Header to be displayed
* **tpl:String**: Handlebar template to representing the HTML layout for the suggestion

**Input Value**:

```
{"autosuggest"
<p><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"Lift Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"highlighted"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"Lift <strong>Cha</strong>irs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"type"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"KEYWORD_SUGGESTION"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"_original"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">{</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"doctype"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"KEYWORD_SUGGESTION"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"timeStamp_unbxd"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">1586968522402</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"autosuggest"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"Lift Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"autosuggest_unstemmed"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"Lift Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"source_unbxd_fields"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">[</span></p>
<p><span style="font-weight: 400;">                  </span><span style="font-weight: 400;">"category"</span></p>
<p><span style="font-weight: 400;">               ]</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"frequency_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">2</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"uniqueId"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"IN_FIELD `~|@` Lift Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"clicks_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">4</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"revenues_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"carts_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"suggestion_length_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">11</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"hits_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">7</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"orders_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"_version_"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">1664057123816865800</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"parent_unbxd"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">true</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">}</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"Source"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">""</span></p>
<p><span style="font-weight: 400;">}</span></p>
```

**topQueries:**

Default:

```
{
count: 2,
<p><span style="font-weight: 400;">                header: "",</span></p>
<p><span style="font-weight: 400;">                tpl: "{{{safestring highlighted}}}"</span></p>
},
```

Description:

* **count:number** -> the number of suggestions to be shown
* **header:String** -> Header to be displayed
* **tpl:String** -> Handlebar template to representing the HTML layout for the suggestion

Input value:

```
{"autosuggest"
<p><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"Zinger Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"highlighted"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"Zinger <strong>Cha</strong>irs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"type"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">TOP_SEARCH_QUERIES</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"_original"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">{</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"doctype"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"TOP_SEARCH_QUERIES</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"timeStamp_unbxd"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">1586968522402</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"autosuggest"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">Zinger</span><span style="font-weight: 400;"> Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"autosuggest_unstemmed"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">Zinger</span><span style="font-weight: 400;"> Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"source_unbxd_fields"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">[</span></p>
<p><span style="font-weight: 400;">                  </span><span style="font-weight: 400;">"category"</span></p>
<p><span style="font-weight: 400;">               ]</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"frequency_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">2</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"uniqueId"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"IN_FIELD `~|@` </span><span style="font-weight: 400;">Zinger</span><span style="font-weight: 400;"> Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"clicks_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">4</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"revenues_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"carts_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"suggestion_length_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">11</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"hits_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">7</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"orders_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"_version_"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">1664057123816865800</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"parent_unbxd"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">true</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">}</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"Source"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">""</span></p>
<p><span style="font-weight: 400;">}</span></p>
```

promotedSuggestion:

Default:

```
{
<p><span style="font-weight: 400;">                count: 2,</span></p>
<p><span style="font-weight: 400;">  header: "",</span></p>
<p><span style="font-weight: 400;">                tpl: "{{{safestring highlighted}}}"</span></p>
<p><span style="font-weight: 400;">   },</span></p>
```

Description:

* **count:number** -> the number of suggestions to be shown
* **header:String** -> Header to be displayed
* **tpl:String**-> Handlebar template to representing the HTML layout for the suggestion

INPUT VALUE:

```
{
"autosuggest":"Zinger Chairs"<span style="font-weight: 400;">,</span><p></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"highlighted"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"Zinger <strong>Cha</strong>irs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"type"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">PROMOTED_SUGGESTION</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"_original"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">{</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"doctype"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"PROMOTED_SUGGESTION</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"timeStamp_unbxd"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">1586968522402</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"autosuggest"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">Zinger</span><span style="font-weight: 400;"> Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"autosuggest_unstemmed"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"</span><span style="font-weight: 400;">Zinger</span><span style="font-weight: 400;"> Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"source_unbxd_fields"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">[</span></p>
<p><span style="font-weight: 400;">                  </span><span style="font-weight: 400;">"category"</span></p>
<p><span style="font-weight: 400;">               ]</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"frequency_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">2</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"uniqueId"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">"IN_FIELD `~|@` </span><span style="font-weight: 400;">Zinger</span><span style="font-weight: 400;"> Chairs"</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"clicks_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">4</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"revenues_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"carts_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"suggestion_length_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">11</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"hits_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">7</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"orders_unbxd_double"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">0</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"_version_"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">1664057123816865800</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">               </span><span style="font-weight: 400;">"parent_unbxd"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">true</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">}</span><span style="font-weight: 400;">,</span></p>
<p><span style="font-weight: 400;">            </span><span style="font-weight: 400;">"Source"</span><span style="font-weight: 400;">:</span><span style="font-weight: 400;">""</span></p>
<p><span style="font-weight: 400;">}</span></p>
```

featuredFields:

| **Attribute**    | **Details**                                                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Data Type**    | Array                                                                                                                                                                   |
| **Default**      | `['brand']`                                                                                                                                                             |
| **Description**  | Can be any autosuggest indexed properties in the product. \<br>\*\*Note:\*\* Before using, ensure Unbxd technicians configure the featured field in the backend system. |
| **Sample Value** | `['category']`                                                                                                                                                          |

Featured field property configuration\
For properties listed in the featured field array, a configuration for each of those properties should be added to the autosuggest options. Assume if category is listed as a featured field then

category:

<Table>
  <thead>
    <tr>
      <th>
        **Attribute**
      </th>

      <th>
        **Details**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Data Type**
      </td>

      <td>
        Object
      </td>
    </tr>

    <tr>
      <td>
        **Default**
      </td>

      <td>
        N/A
      </td>
    </tr>

    <tr>
      <td>
        **Description**
      </td>

      <td>
        * \`count: number\` → Number of suggestions to show\<br>- \`header: string\` → Header to display\<br>- \`tpl: string\` → Handlebars template for HTML layout
      </td>
    </tr>

    <tr>
      <td>
        Input Value
      </td>

      <td>
        \{         doctype: "Furniture"

        <br />

        timeStamp\_unbxd: 1587064397473\
        autosuggest: "Furniture"
        autosuggest\_unstemmed: "Furniture"
        source\_unbxd\_fields: \["category"]
        frequency\_unbxd\_double: 100
        uniqueId: "category `~\|@` Furniture"
        *version*: 1664157643371970600
        parent\_unbxd: true
        }
      </td>
    </tr>
  </tbody>
</Table>

```Text Sample Value
{
count: 2,
<p><span style="font-weight: 400;">                header: "",</span></p>
<p><span style="font-weight: 400;">                tpl: "{{{safestring highlighted}}}"</span></p>
<p><span style="font-weight: 400;">   },</span></p>
```