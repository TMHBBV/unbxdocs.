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

| **Attribute**    | **Details**                                                                                                                                                         |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Data Type**    | Array                                                                                                                                                               |
| **Default**      | `['brand']`                                                                                                                                                         |
| **Description**  | Can be any autosuggest indexed properties in the product. \<br>**Note:** Before using, ensure Unbxd technicians configure the featured field in the backend system. |
| **Sample Value** | `['category']`                                                                                                                                                      |

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
        * `count: number` → Number of suggestions to show\<br>- `header: string` → Header to display\<br>- `tpl: string` → Handlebars template for HTML layout
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

**inFields**:

Default:

```
{
 count: 0
<p><span style="font-weight: 400;">  , fields: {</span></p>
<p><span style="font-weight: 400;">                    'brand': 3,</span></p>
<p><span style="font-weight: 400;">                    'category': 3,</span></p>
<p><span style="font-weight: 400;">                    'color': 3</span></p>
<p><span style="font-weight: 400;">                }</span></p>
<p><span style="font-weight: 400;">                , header: ""</span></p>
<p><span style="font-weight: 400;">                , tpl: "{{{safestring highlighted}}}"</span></p>
<p><span style="font-weight: 400;">            }</span></p>
```

Description:

* count:number -> the number of suggestions to be shown
* header:String -> Header to be displayed
* tpl:String -> Handlebar template to representing the HTML layout for the suggestion
* fields:object -> The various properties which should be used for in field suggestion (for someone searching for shoes infield suggestion would be
  * In brand : Nike, Addidas, Puma
  * In Color: Red, Green and Blue
  * In Category: Casuals , Formals or sports

**Input type**

\{doctype: "IN\_FIELD"\
brand\_in: \["Wilora Select", "Wilora Classic", "Wilora Premier"]
0: "Wilora Select"
1: "Wilora Classic"
2: "Wilora Premier"
material\_in: \["Engineered Wood", "Solid Birch with Veneered HDF Panel",…]
0: "Engineered Wood"
1: "Solid Birch with Veneered HDF Panel"
2: "Solid Birch with Veneered MDF Center Panel"
3: "High-Density Fiberboard (HDF)"
4: "Solid Birch"
timeStamp\_unbxd: 1587089849424
autosuggest: "Wall Cabinets"
autosuggest\_unstemmed: "Wall Cabinets"
source\_unbxd\_fields: \["catlevel3Name"]
frequency\_unbxd\_double: 2018
uniqueId: "IN\_FIELD `~|@` Wall Cabinets"
finish\_in: \["Vertical Wood-Grain", "Scratch Resistant High Gloss White "PET" Laminate", "Textured Melamine",…]
unbxdFeedId: "stage-vevano809641569412780\_-1433400925"
clicks\_unbxd\_double: 0
revenues\_unbxd\_double: 0
carts\_unbxd\_double: 0
suggestion\_length\_unbxd\_double: 13
hits\_unbxd\_double: 7
orders\_unbxd\_double: 0
*version*: 1664184331017388000
parent\_unbxd: true
}

Samle Value

```
{               count: 2,
             header: "",               tpl: "{{{safestring highlighted}}}"   },
```

**popularProducts**:\
Properties applicable when using the default template

| **Property** | **Data Type** | **Required** | **Default** | **Description**                                                                  |
| ------------ | ------------- | ------------ | ----------- | -------------------------------------------------------------------------------- |
| **showCart** | boolean       | false        | `true`      | When set to `true`, the **Add to Cart** button is shown for each popular product |
| **cartType** | string        | false        | `inline`    | Defines how the cart is displayed                                                |
|              |               |              |             | **Possible values:** `inline` or `separate`                                      |

**popularProducts**:

Data type: object

Required: false

Default:

```
           { count: 4<p></p>
<p><span style="font-weight: 400;">                , fields: ['*']</span></p>
<p><span style="font-weight: 400;">                , price: true</span></p>
<p><span style="font-weight: 400;">                , priceFunctionOrKey: "price"</span></p>
<p><span style="font-weight: 400;">                , image: true</span></p>
<p><span style="font-weight: 400;">                , imageUrlOrFunction: "imageUrl"</span></p>
<p><span style="font-weight: 400;">                , currency: "Rs."</span></p>
<p><span style="font-weight: 400;">                , displayHeader: true // used to note if popular products header needs to be shown, Can't base it on the value of header attribute as it get's constructed realtime by filtered products.</span></p>
<p><span style="font-weight: 400;">                , header: ""</span></p>
<p><span style="font-weight: 400;">                , loadmore: false // used in conjuction with filteredProductEvent value equal to click</span></p>
<p><span style="font-weight: 400;">                , view: 'list'</span></p>
<p><span style="font-weight: 400;">                , tpl: ['{{#if ../showCarts}}'</span></p>
<p><span style="font-weight: 400;">                    , '{{#unbxdIf ../../cartType "inline"}}'//"inline" || "separate"</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-inlinecart">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-image-container">'</div>
<p><span style="font-weight: 400;">                    , '{{#if image}}'</span></p>
<p><span style="font-weight: 400;">                    , '<img src="{{image}}">'</span></p>
<p><span style="font-weight: 400;">                    , '{{/if}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-name">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div style="table-layout: fixed; width: 100%; display: table;">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div style="display: table-row;">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div style="display: table-cell; text-overflow: ellipsis; overflow: hidden; white-space: nowrap;">'</div>
<p><span style="font-weight: 400;">                    , '{{{safestring highlighted}}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{#if price}}'</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-price">'</div>
<p><span style="font-weight: 400;">                    , '{{currency}}{{price}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{/if}}'</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-quantity">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-quantity-container">'</div>
<p><span style="font-weight: 400;">                    , 'Qty'</span></p>
<p><span style="font-weight: 400;">                    , '<input class="unbxd-popular-product-qty-input" type="text" value="1">'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-cart-action">'</div>
<p><span style="font-weight: 400;">                    , '<button class="unbxd-as-popular-product-cart-button">Add to cart</button>'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{else}}'</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-info">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-image-container">'</div>
<p><span style="font-weight: 400;">                    , '{{#if image}}'</span></p>
<p><span style="font-weight: 400;">                    , '<img src="{{image}}">'</span></p>
<p><span style="font-weight: 400;">                    , '{{/if}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div>'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-name">'</div>
<p><span style="font-weight: 400;">                    , '{{{safestring highlighted}}}'</span></p>
<p><span style="font-weight: 400;">                    //,'{{{processAutosuggestTitle _original.brandName highlighted}}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<br>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-cart">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-cart-action">'</div>
<p><span style="font-weight: 400;">                    , '<button class="unbxd-as-popular-product-cart-button">Add to cart</button>'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-quantity">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-quantity-container">'</div>
<p><span style="font-weight: 400;">                    , 'Qty'</span></p>
<p><span style="font-weight: 400;">                    , '<input class="unbxd-popular-product-qty-input" type="text" value="1">'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{#if price}}'</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-price">'</div>
<p><span style="font-weight: 400;">                    , '{{currency}}{{price}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{/if}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{/unbxdIf}}'</span></p>
<p><span style="font-weight: 400;">                    , '{{else}}'</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-info">'</div>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-image-container">'</div>
<p><span style="font-weight: 400;">                    , '{{#if image}}'</span></p>
<p><span style="font-weight: 400;">                    , '<img src="{{image}}">'</span></p>
<p><span style="font-weight: 400;">                    , '{{/if}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-name">'</div>
<p><span style="font-weight: 400;">                    , '{{{safestring highlighted}}}'</span></p>
<p><span style="font-weight: 400;">                    //,'{{{processAutosuggestTitle _original.brandName highlighted}}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{#if price}}'</span></p>
<p><span style="font-weight: 400;">                    , '</span></p>
<div class="unbxd-as-popular-product-price">'</div>
<p><span style="font-weight: 400;">                    , '{{currency}}{{price}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{/if}}'</span></p>
<p><span style="font-weight: 400;">                    , ''</span></p>
<p><span style="font-weight: 400;">                    , '{{/if}}'].join('')</span></p>
<p><span style="font-weight: 400;">            }</span></p>
```

**Description**

**count** : number-> the number of products to be shown

**fields**: array -> The attributes on the products to be fetched

**price**: boolean -> true if product price to be shown in the suggest widget

\*\*priceFunctionOrKey:\*\*String (or) Function -> attribute which contains the price value for the product

**image**:boolean -> true if product image to be shown in the suggest widget

**imageUrlOrFunction**:String (or) Function -> attribute which contains the url to the image for the product

**currency**:String -> Denote the currency symbol

**header**:String -> Title for popular products section

**view**:String -> can be list (or) grid

**tpl**:String -> Handlebar template to representing the HTML layout for the suggestion

```
{
            "autosuggest":"Zinger Chair",
            "highlighted":"Zinger Chair",
            "type":"POPULAR_PRODUCTS",
            "pid":"08300",
            "_original":{
               "ShortDescription":"Nimble and quick, yet stable thru the turns, the Zinger's patented design is fun and intuitive to drive. Plus, it's not prone to tipping mobility scooters. With no handlebar or joystick in the way, only a Zinger Chair lets you pull right into a table or desk. The Zinger folds to 10 flat instantly to fit into nearly any car trunk, saving you the hassle and expense of a car mounted scooter lift - and at 42 pounds, it can be carried up steps like a suitcase or travel on airplanes. ",
               "imageUrl":[
                  "https://www.abc.com/content/ZingerChair_hero_08300_md_200.jpg"
               ],
               "productUrl":"https://www.abc.com/Zinger/Zinger+Chair.axd",
               "CurrentPrice":2499,
               "OriginalPrice":2799,
               "uniqueId":"08300",
               "ItemName":"Zinger Chair",
               "ProductId":"14408",
               "doctype":"POPULAR_PRODUCTS",
               "autosuggest":"Zinger Chair",
               "variantTotal":1,
               "score":2078.7332,
               "relevantDocument":"parent",
               "variantCount":1,
               "variants":[
                  {
                     "vId":"08300_08300",
                     "ShortDescription":"Nimble and quick, yet stable thru the turns, the Zinger's patented design is fun and intuitive to drive. Plus, it's not prone to tipping mobility scooters. With no handlebar or joystick in the way, only a Zinger Chair lets you pull right into a table or desk. The Zinger folds to 10 flat instantly to fit into nearly any car trunk, saving you the hassle and expense of a car mounted scooter lift - and at 42 pounds, it can be carried up steps like a suitcase or travel on airplanes. ",
  "imageUrl":[                        "https://www.abc.com/content/ZingerChair_hero_08300_md_200.jpg"                    ],                      "productUrl":"https://www.abc.com/Zinger/Zinger+Chair.axd",                     "CurrentPrice":2499,                     "OriginalPrice":2799,                   "ItemName":"Zinger Chair",                   "ProductId":"14408",                  "doctype":"POPULAR_PRODUCTS",                    "autosuggest":"Zinger Chair",                     "score":0.53983456                  }               ]           },            "price":2499,             "currency":"$",             "image":[               "https://www.abc.com/content/ZingerChair_hero_08300_md_200.jpg"
```

<br />

Properties applicable when using the default template.

showCart:

Data type: object

Default:

```
 count: 4

                , fields: ['*']

                , price: true

                , priceFunctionOrKey: "price"

                , image: true

                , imageUrlOrFunction: "imageUrl"

                , currency: "Rs."

                , displayHeader: true // used to note if popular products header needs to be shown, Can't base it on the value of header attribute as it get's constructed realtime by filtered products.

                , header: ""

                , loadmore: false // used in conjuction with filteredProductEvent value equal to click

                , view: 'list'

                , tpl: ['{{#if ../showCarts}}'

                    , '{{#unbxdIf ../../cartType "inline"}}'//"inline" || "separate"

                    , '

'
                    , '

'
                    , '{{#if image}}'

                    , ''

                    , '{{/if}}'

                    , ''

                    , '

'
                    , '

'
                    , '

'
                    , '

'
                    , '{{{safestring highlighted}}}'

                    , ''

                    , ''

                    , ''

                    , ''

                    , '{{#if price}}'

                    , '

'
                    , '{{currency}}{{price}}'

                    , ''

                    , '{{/if}}'

                    , '

'
                    , '

'
                    , 'Qty'

                    , '
1
'

                    , ''

                    , ''

                    , '

'
                    , 'Add to cart'

                    , ''

                    , ''

                    , '{{else}}'

                    , '

'
                    , '

'
                    , '{{#if image}}'

                    , ''

                    , '{{/if}}'

                    , ''

                    , '

'
                    , '

'
                    , '{{{safestring highlighted}}}'

                    //,'{{{processAutosuggestTitle _original.brandName highlighted}}}'

                    , ''


                    , '

'
                    , '

'
                    , 'Add to cart'

                    , ''

                    , '

'
                    , '

'
                    , 'Qty'

                    , '
1
'

                    , ''

                    , ''

                    , '{{#if price}}'

                    , '

'
                    , '{{currency}}{{price}}'

                    , ''

                    , '{{/if}}'

                    , ''

                    , ''

                    , ''

                    , '{{/unbxdIf}}'

                    , '{{else}}'

                    , '

'
                    , '

'
                    , '{{#if image}}'

                    , ''

                    , '{{/if}}'

                    , ''

                    , '

'
                    , '{{{safestring highlighted}}}'

                    //,'{{{processAutosuggestTitle _original.brandName highlighted}}}'

                    , ''

                    , '{{#if price}}'

                    , '

'
                    , '{{currency}}{{price}}'

                    , ''

                    , '{{/if}}'

                    , ''

                    , '{{/if}}'].join('')

            }
```

**Description**

**Count** : number-> the number of products to be shown

**fields**: array -> The attributes on the products to be fetched

**price**: boolean -> true if product price to be shown in the suggest widget

**priceFunctionOrKey**:String (or) Function -> attribute which contains the price value for the product

**image**:boolean -> true if product image to be shown in the suggest widget

**imageUrlOrFunction**:String (or) Function -> attribute which contains the url to the image for the product

**currency**:String -> Denote the currency symbol

**header**:String -> Title for popular products section

**view**:String -> can be list (or) grid

**tpl**:String -> Handlebar template to representing the HTML layout for the suggestion

**Input Value**:

```
{
            "autosuggest":"Zinger Chair",
            "highlighted":"Zinger Chair",
            "type":"POPULAR_PRODUCTS",
            "pid":"08300",
            "_original":{
               "ShortDescription":"Nimble and quick, yet stable thru the turns, the Zinger's patented design is fun and intuitive to drive. Plus, it's not prone to tipping mobility scooters. With no handlebar or joystick in the way, only a Zinger Chair lets you pull right into a table or desk. The Zinger folds to 10 flat instantly to fit into nearly any car trunk, saving you the hassle and expense of a car mounted scooter lift - and at 42 pounds, it can be carried up steps like a suitcase or travel on airplanes. ",
               "imageUrl":[
                  "https://www.abc.com/content/ZingerChair_hero_08300_md_200.jpg"
               ],
               "productUrl":"https://www.abc.com/Zinger/Zinger+Chair.axd",
               "CurrentPrice":2499,
               "OriginalPrice":2799,
               "uniqueId":"08300",
               "ItemName":"Zinger Chair",
               "ProductId":"14408",
               "doctype":"POPULAR_PRODUCTS",
               "autosuggest":"Zinger Chair",
               "variantTotal":1,
               "score":2078.7332,
               "relevantDocument":"parent",
               "variantCount":1,
               "variants":[
                  {
                     "vId":"08300_08300",
                     "ShortDescription":"Nimble and quick, yet stable thru the turns, the Zinger's patented design is fun and intuitive to drive. Plus, it's not prone to tipping mobility scooters. With no handlebar or joystick in the way, only a Zinger Chair lets you pull right into a table or desk. The Zinger folds to 10 flat instantly to fit into nearly any car trunk, saving you the hassle and expense of a car mounted scooter lift - and at 42 pounds, it can be carried up steps like a suitcase or travel on airplanes. ",
                     "imageUrl":[
                        "https://www.abc.com/content/ZingerChair_hero_08300_md_200.jpg"
                     ],
                     "productUrl":"https://www.abc.com/Zinger/Zinger+Chair.axd",
                     "CurrentPrice":2499,
                     "OriginalPrice":2799,
                     "ItemName":"Zinger Chair",
                     "ProductId":"14408",
                     "doctype":"POPULAR_PRODUCTS",
                     "autosuggest":"Zinger Chair",
                     "score":0.53983456

```

onCartClick:

| **Property**      | **Data Type** | **Required** | **Default**    | **Description**                                                        |
| ----------------- | ------------- | ------------ | -------------- | ---------------------------------------------------------------------- |
| **(onCartClick)** | function      | false        | Empty function | Can be used as an `onClick` hook to trigger the **Add to Cart** action |

On completion of the above steps, the config should be as shown below,

```
new Unbxd.setSearch({
       siteName: "{your site key}",
       APIKey: "{your API key}",
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
   mainTpl: ["topQueries", "keywordSuggestions"],
   sideTpl: ["popularProducts"],
featuredFields: [],
       showCarts: false,
       cartType: "separate",
featuredFields: [],
       inFields: {
         count: 0,
         fields: {
           brand: 3,
           category: 3,
           color: 3
         },
         header: "",
         tpl: "{{{safestring highlighted}}}"
       },
       topQueries: {
         count: 6,
         hidden: false,
         header: "",
         tpl: "{{{safestring highlighted}}}"
       },
       keywordSuggestions: {
         count: 6,
         header: "",
         tpl: "{{{safestring highlighted}}}"
       },
       popularProducts: {
         count: 6,
         fields: [
           "title",
           "uniqueId",
           "imageUrl",
           "productUrl",
           "price",
           "autosuggest",
           "doctype"
         ],
         price: true,
         image: true,
         imageUrlOrFunction: "imageUrl",
         priceFunctionOrKey: "price",
         autosuggestName: "ItemName",
         currency: "$",
         header: "Most Popular Products",
         tpl: [
           '
', '
', '
', '', "
", '
{{{safestring highlighted}}}
', "
"
         ].join("")
       }
     });
```

### Other Properties

| **Property**    | **Data Type**     | **Required** | **Default** | **Description**                                                                                                                                                   |
| --------------- | ----------------- | ------------ | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **noResultTpl** | string / function | false        | N/A         | A Handlebars template string representing the HTML layout to show when **no suggestions** are available. Can also be a **function** that returns such a template. |

<br />

| **Property**   | **Data Type** | **Required** | **Default** | **Description**                                                                        |
| -------------- | ------------- | ------------ | ----------- | -------------------------------------------------------------------------------------- |
| **hbsHelpers** | Function      | false        | N/A         | Used to bind custom **Handlebars helper functions** that can be used within templates. |

SampleValue:

```
function () {

Handlebars.registerHelper("toUpper", function (context, options) {

    return context.toUpperCase();

});

}
```

<br />

| **Property** | **Data Type** | **Required** | **Default** | **Description**                                                                                              |
| ------------ | ------------- | ------------ | ----------- | ------------------------------------------------------------------------------------------------------------ |
| **filtered** | Boolean       | false        | `false`     | When set to `true`, the **popular products section** is refreshed based on the **hover of each suggestion**. |

**Callback functions**\
This section documents the different callback functions exposed by the SDK that you can hook into to listen to respond to various events.

| **Property**      | **Data Type** | **Required** | **Default** | **Description**                                                                                                                                            |
| ----------------- | ------------- | ------------ | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **onSimpleEnter** | Function      | Optional     | N/A         | Callback function invoked when the **Enter** key is pressed in the search input box. Used to **validate and submit** the search if the input is not empty. |

Sample Value:

```
function() {

          this.lastKeyEvent.preventDefault();

          if (this.input.value.trim().length > 0) {

            this.input.form.submit();

          }

        }
```

<br />

| **Property**     | **Data Type** | **Required** | **Default** | **Description**                                                                                               |
| ---------------- | ------------- | ------------ | ----------- | ------------------------------------------------------------------------------------------------------------- |
| **onItemSelect** | Function      | Optional     | N/A         | Callback function invoked when a **suggestion** or **popular product** is selected from the search interface. |

Sample Value:

```
function(data, original) {

          if (

            data.type === "POPULAR_PRODUCTS" ||

            data.type === "POPULAR_PRODUCTS_FILTERED"

          ) {

            window.location =

              window.location.origin + getRelativeUrl(original.productUrl);

          } else if (data.type == "IN_FIELD") {

            window.location =

              window.location.origin + "/?q=" + encodeURIComponent(data.value);

          } else if (data.type == "brand") {

            window.location =

              window.location.origin +

              "/?q=" +

              encodeURIComponent(original.autosuggest_unstemmed); // + '&dispatch=products.advsearch&cid=0&subcats=Y', '_blank';

          } else {

            window.location =

              window.location.origin + "/?q=" + encodeURIComponent(data.value);

          }

        }

      }
```

## Sample Options Object

Including the script object as shown below, would render the autosuggest widget as exhibited on this website

<br />

<Table>
  <thead>
    <tr>
      <th>
        Config Name
      </th>

      <th>
        Data Type
      </th>

      <th>
        Description
      </th>

      <th>
        Sample Values
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        siteName
      </td>

      <td>
        String
      </td>

      <td>
        Site name assigned from Unbxd (unique identifier for each customer/site)
      </td>

      <td>
        demo-com809841570123270
      </td>
    </tr>

    <tr>
      <td>
        APIKey
      </td>

      <td>
        String
      </td>

      <td>
        Unique key assigned from Unbxd
      </td>

      <td>
        7689867nbh868u4j3b4u998
      </td>
    </tr>

    <tr>
      <td>
        inputSelector
      </td>

      <td>
        String
      </td>

      <td>
        CSS selector of the search input box
      </td>

      <td>
        \#search\_mini\_form input
      </td>
    </tr>

    <tr>
      <td>
        searchButtonSelector
      </td>

      <td>
        String
      </td>

      <td>
        CSS selector of the search submit button/icon
      </td>

      <td>
        \#search\_mini\_form button.searchicon
      </td>
    </tr>

    <tr>
      <td>
        type
      </td>

      <td>
        String
      </td>

      <td>
        Used to indicate whether search or category page
      </td>

      <td>
        search / category
      </td>
    </tr>

    <tr>
      <td>
        searchQueryParam
      </td>

      <td>
        String
      </td>

      <td>
        Search query parameter name
      </td>

      <td>
        q
      </td>
    </tr>

    <tr>
      <td>
        getCategoryId
      </td>

      <td>
        Function
      </td>

      <td>
        Evaluates category id or path for category pages
      </td>

      <td>
        function returning categoryPath
      </td>
    </tr>

    <tr>
      <td>
        deferInitRender
      </td>

      <td>
        Array
      </td>

      <td>
        List of components to defer render until initial setup
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        spellCheck
      </td>

      <td>
        String
      </td>

      <td>
        CSS selector for 'did you mean' section
      </td>

      <td>
        \#did\_you\_mean
      </td>
    </tr>

    <tr>
      <td>
        spellCheckTemp
      </td>

      <td>
        String
      </td>

      <td>
        Handlebars HTML template for spell check suggestions
      </td>

      <td>
        `<span class='base'>...</span>`
      </td>
    </tr>

    <tr>
      <td>
        searchQueryDisplay
      </td>

      <td>
        String
      </td>

      <td>
        CSS selector for search results message
      </td>

      <td>
        \#search\_result\_display
      </td>
    </tr>

    <tr>
      <td>
        searchQueryDisplayTemp
      </td>

      <td>
        String
      </td>

      <td>
        Handlebars HTML template for search result message
      </td>

      <td>
        `<span class='base'>...</span>`
      </td>
    </tr>

    <tr>
      <td>
        searchResultContainer
      </td>

      <td>
        String
      </td>

      <td>
        CSS selector for product results container
      </td>

      <td>
        \#results-container
      </td>
    </tr>

    <tr>
      <td>
        searchResultSetTemp
      </td>

      <td>
        String/Function
      </td>

      <td>
        Template/function for displaying product results
      </td>

      <td>
        `{{#products}}...{{/products}}`
      </td>
    </tr>

    <tr>
      <td>
        isAutoScroll
      </td>

      <td>
        Boolean
      </td>

      <td>
        Enable autoscroll without pagination
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        heightDiffToTriggerNextPage
      </td>

      <td>
        Number
      </td>

      <td>
        Trigger next page load before this pixel value from bottom
      </td>

      <td>
        250
      </td>
    </tr>

    <tr>
      <td>
        isClickNScroll
      </td>

      <td>
        Boolean
      </td>

      <td>
        Enable 'load more' behavior
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        clickNScrollElementSelector
      </td>

      <td>
        String
      </td>

      <td>
        CSS selector for 'load more' button
      </td>

      <td>
        \#load-more-results
      </td>
    </tr>

    <tr>
      <td>
        isPagination
      </td>

      <td>
        Boolean
      </td>

      <td>
        Enable traditional pagination
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        setPagination
      </td>

      <td>
        Function
      </td>

      <td>
        Custom logic after pagination data load
      </td>

      <td>
        function with 3 args
      </td>
    </tr>

    <tr>
      <td>
        paginationContainerSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for pagination section
      </td>

      <td>
        .page-nav-section
      </td>
    </tr>

    <tr>
      <td>
        paginationTemp
      </td>

      <td>
        String
      </td>

      <td>
        Template for rendering pagination
      </td>

      <td>
        `<a href='javascript:;'>Next</a>`
      </td>
    </tr>

    <tr>
      <td>
        facetMultiSelect
      </td>

      <td>
        Boolean
      </td>

      <td>
        Allow multiple facet selections
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        facetContainerSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for facet section
      </td>

      <td>
        \#facets\_container
      </td>
    </tr>

    <tr>
      <td>
        facetCheckBoxSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for all facet checkboxes
      </td>

      <td>
        \#facets\_container .facet\_value input\[type=checkbox]
      </td>
    </tr>

    <tr>
      <td>
        selectedFacetTemp
      </td>

      <td>
        String
      </td>

      <td>
        Template for applied filters
      </td>

      <td>
        `<ol class='unbxd_selected_facets'>...</ol>`
      </td>
    </tr>

    <tr>
      <td>
        selectedFacetContainerSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for selected filters section
      </td>

      <td>
        \#applied-filter-section
      </td>
    </tr>

    <tr>
      <td>
        facetMultilevel
      </td>

      <td>
        Boolean
      </td>

      <td>
        Enable multilevel facets
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        facetMultilevelName
      </td>

      <td>
        String
      </td>

      <td>
        Field name for multilevel facet
      </td>

      <td>
        CATEGORY
      </td>
    </tr>

    <tr>
      <td>
        clearSelectedFacetsSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for clear all filters link
      </td>

      <td>
        \#clear-all-filters
      </td>
    </tr>

    <tr>
      <td>
        removeSelectedFacetSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for individual filter remove buttons
      </td>

      <td>
        .unbxd-remove-item
      </td>
    </tr>

    <tr>
      <td>
        loaderSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for loading indicator
      </td>

      <td>
        \#loader-icon
      </td>
    </tr>

    <tr>
      <td>
        onFacetLoad
      </td>

      <td>
        Function
      </td>

      <td>
        Callback after facet rendering
      </td>

      <td>
        function(obj) \{...}
      </td>
    </tr>

    <tr>
      <td>
        onIntialResultLoad
      </td>

      <td>
        Function
      </td>

      <td>
        Callback after first result set is loaded
      </td>

      <td>
        function(obj) \{...}
      </td>
    </tr>

    <tr>
      <td>
        onPageLoad
      </td>

      <td>
        Function
      </td>

      <td>
        Callback after every subsequent result load
      </td>

      <td>
        function(obj) \{...}
      </td>
    </tr>

    <tr>
      <td>
        sanitizeQueryString
      </td>

      <td>
        Function
      </td>

      <td>
        Sanitize search input
      </td>

      <td>
        function(q) \{...}
      </td>
    </tr>

    <tr>
      <td>
        getFacetStats
      </td>

      <td>
        String
      </td>

      <td>
        Variable for holding facet stats
      </td>

      <td>
        facetstats
      </td>
    </tr>

    <tr>
      <td>
        processFacetStats
      </td>

      <td>
        Function
      </td>

      <td>
        Logic for slider range behavior
      </td>

      <td>
        function(obj) \{...}
      </td>
    </tr>

    <tr>
      <td>
        setDefaultFilters
      </td>

      <td>
        Function
      </td>

      <td>
        Apply default filters on data fetch
      </td>

      <td>
        function() \{...}
      </td>
    </tr>

    <tr>
      <td>
        fields
      </td>

      <td>
        Array
      </td>

      <td>
        Product attributes to be fetched
      </td>

      <td>
        \['title', 'price', 'brand']
      </td>
    </tr>

    <tr>
      <td>
        onNoResult
      </td>

      <td>
        Function
      </td>

      <td>
        Handler when no search result found
      </td>

      <td>
        function(obj) \{...}
      </td>
    </tr>

    <tr>
      <td>
        noEncoding
      </td>

      <td>
        Boolean
      </td>

      <td>
        Enable encoding of URL params
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        customReset
      </td>

      <td>
        Function
      </td>

      <td>
        Custom behavior on reset or sort
      </td>

      <td>
        function() \{...}
      </td>
    </tr>

    <tr>
      <td>
        bannerSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for merchandising banners
      </td>

      <td>
        \#up-sell-banner-section
      </td>
    </tr>

    <tr>
      <td>
        bannerTemp
      </td>

      <td>
        String
      </td>

      <td>
        Template for banners
      </td>

      <td>
        `<a href='{{landingUrl}}'><img src='{{imageUrl}}'></a>`
      </td>
    </tr>

    <tr>
      <td>
        bannerCount
      </td>

      <td>
        Number
      </td>

      <td>
        Number of banners to show
      </td>

      <td>
        2
      </td>
    </tr>

    <tr>
      <td>
        sortContainerSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for sort section
      </td>

      <td>
        \#sort-section
      </td>
    </tr>

    <tr>
      <td>
        sortOptions
      </td>

      <td>
        Array
      </td>

      <td>
        Sorting options to be shown
      </td>

      <td>
        \[\{name: 'Popularity'}, \{...}]
      </td>
    </tr>

    <tr>
      <td>
        sortContainerType
      </td>

      <td>
        String
      </td>

      <td>
        Sort interaction type
      </td>

      <td>
        click / select
      </td>
    </tr>

    <tr>
      <td>
        sortContainerTemp
      </td>

      <td>
        String
      </td>

      <td>
        Template for sort UI
      </td>

      <td>
        `<select>...</select>`
      </td>
    </tr>

    <tr>
      <td>
        pageSize
      </td>

      <td>
        Number
      </td>

      <td>
        Products per page
      </td>

      <td>
        24
      </td>
    </tr>

    <tr>
      <td>
        pageSizeContainerSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for page size UI
      </td>

      <td>
        \#results-pagesize
      </td>
    </tr>

    <tr>
      <td>
        pageSizeOptions
      </td>

      <td>
        Array
      </td>

      <td>
        Page size options
      </td>

      <td>
        \[\{name: '48 items', value: '48'}, ...]
      </td>
    </tr>

    <tr>
      <td>
        pageSizeContainerType
      </td>

      <td>
        String
      </td>

      <td>
        Page size selection method
      </td>

      <td>
        click / select
      </td>
    </tr>

    <tr>
      <td>
        pageSizeContainerTemp
      </td>

      <td>
        String
      </td>

      <td>
        Template for page size UI
      </td>

      <td>
        `<select>...</select>`
      </td>
    </tr>

    <tr>
      <td>
        viewTypeContainerTemp
      </td>

      <td>
        String
      </td>

      <td>
        Template for view type UI
      </td>

      <td>
        `<a class='selected'>grid</a>`
      </td>
    </tr>

    <tr>
      <td>
        viewTypeContainerSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for view type section
      </td>

      <td>
        \#results-pageview
      </td>
    </tr>

    <tr>
      <td>
        viewTypes
      </td>

      <td>
        Array
      </td>

      <td>
        Available views
      </td>

      <td>
        If the customer only have grid view then \[‘grid’]

        <br />

        \*If the customer only have list view then \[‘list’]

        <br />

        \*If customer has both views then \[“list”,”grid”]
      </td>
    </tr>

    <tr>
      <td>
        variants
      </td>

      <td>
        Boolean
      </td>

      <td>
        Enable variant display
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        variantsCount
      </td>

      <td>
        Number
      </td>

      <td>
        Number of variants per product
      </td>

      <td>
        3
      </td>
    </tr>

    <tr>
      <td>
        isSwatches
      </td>

      <td>
        Boolean
      </td>

      <td>
        Enable swatch display
      </td>

      <td>
        true
      </td>
    </tr>

    <tr>
      <td>
        swatchesSelector
      </td>

      <td>
        String
      </td>

      <td>
        Selector for swatch UI
      </td>

      <td>
        .swatch-box
      </td>
    </tr>

    <tr>
      <td>
        mappedFields
      </td>

      <td>
        Object
      </td>

      <td>
        Mapping of product attributes
      </td>

      <td>
        \{ imageUrl: 'imageUrl', ... }
      </td>
    </tr>
  </tbody>
</Table>

mappedFields: object: Pass the field names for the important product attributes that you want to render

```
{

“imageUrl”: “imageUrl”,

“productUrl”: “productUrl”,

“title”: “title”,

“description”: “description”,

“price”: “price”,

“categoryPath”: “categoryPath”,

“variantFields”: {

“imageUrl”: “v_imageUrl”,

“productUrl”: “v_productUrl”,

“title”: “v_title”,

“price”: “v_price”,

“groupBy”: “variant_color”,

“swatchFields”: {

“swatch_background_image”: “variant_overhead_swatch”,

“swatch_background_color”: “variant_color”,

“swatch_click_image”: “variant_image_array”

}

}

}
```