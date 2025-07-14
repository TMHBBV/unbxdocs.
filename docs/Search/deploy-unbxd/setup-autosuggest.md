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

| Config Name                    | Data Type       | Description                                                              | Sample Values                                           |
| ------------------------------ | --------------- | ------------------------------------------------------------------------ | ------------------------------------------------------- |
| siteName                       | String          | Site name assigned from Unbxd (unique identifier for each customer/site) | demo-com809841570123270                                 |
| APIKey                         | String          | Unique key assigned from Unbxd                                           | 7689867nbh868u4j3b4u998                                 |
| inputSelector                  | String          | CSS selector of the search input box                                     | #search\_mini\_form input                               |
| searchButtonSelector           | String          | CSS selector of the search submit button/icon                            | #search\_mini\_form button.searchicon                   |
| type                           | String          | Used to indicate whether search or category page                         | search / category                                       |
| searchQueryParam               | String          | Search query parameter name                                              | q                                                       |
| getCategoryId                  | Function        | Evaluates category id or path for category pages                         | function returning categoryPath                         |
| deferInitRender                | Array           | List of components to defer render until initial setup                   |                                                         |
| spellCheck                     | String          | CSS selector for 'did you mean' section                                  | #did\_you\_mean                                         |
| spellCheckTemp                 | String          | Handlebars HTML template for spell check suggestions                     | `<span class='base'>...</span>`                         |
| searchQueryDisplay             | String          | CSS selector for search results message                                  | #search\_result\_display                                |
| searchQueryDisplayTemp         | String          | Handlebars HTML template for search result message                       | `<span class='base'>...</span>`                         |
| searchResultContainer          | String          | CSS selector for product results container                               | #results-container                                      |
| searchResultSetTemp            | String/Function | Template/function for displaying product results                         | `{{#products}}...{{/products}}`                         |
| isAutoScroll                   | Boolean         | Enable autoscroll without pagination                                     | true                                                    |
| heightDiffToTriggerNextPage    | Number          | Trigger next page load before this pixel value from bottom               | 250                                                     |
| isClickNScroll                 | Boolean         | Enable 'load more' behavior                                              | true                                                    |
| clickNScrollElementSelector    | String          | CSS selector for 'load more' button                                      | #load-more-results                                      |
| isPagination                   | Boolean         | Enable traditional pagination                                            | true                                                    |
| setPagination                  | Function        | Custom logic after pagination data load                                  | function with 3 args                                    |
| paginationContainerSelector    | String          | Selector for pagination section                                          | .page-nav-section                                       |
| paginationTemp                 | String          | Template for rendering pagination                                        | `<a href='javascript:;'>Next</a>`                       |
| facetMultiSelect               | Boolean         | Allow multiple facet selections                                          | true                                                    |
| facetContainerSelector         | String          | Selector for facet section                                               | #facets\_container                                      |
| facetCheckBoxSelector          | String          | Selector for all facet checkboxes                                        | #facets\_container .facet\_value input\[type=checkbox]  |
| selectedFacetTemp              | String          | Template for applied filters                                             | `<ol class='unbxd_selected_facets'>...</ol>`            |
| selectedFacetContainerSelector | String          | Selector for selected filters section                                    | #applied-filter-section                                 |
| facetMultilevel                | Boolean         | Enable multilevel facets                                                 | true                                                    |
| facetMultilevelName            | String          | Field name for multilevel facet                                          | CATEGORY                                                |
| clearSelectedFacetsSelector    | String          | Selector for clear all filters link                                      | #clear-all-filters                                      |
| removeSelectedFacetSelector    | String          | Selector for individual filter remove buttons                            | .unbxd-remove-item                                      |
| loaderSelector                 | String          | Selector for loading indicator                                           | #loader-icon                                            |
| onFacetLoad                    | Function        | Callback after facet rendering                                           | function(obj) \{...}                                    |
| onIntialResultLoad             | Function        | Callback after first result set is loaded                                | function(obj) \{...}                                    |
| onPageLoad                     | Function        | Callback after every subsequent result load                              | function(obj) \{...}                                    |
| sanitizeQueryString            | Function        | Sanitize search input                                                    | function(q) \{...}                                      |
| getFacetStats                  | String          | Variable for holding facet stats                                         | facetstats                                              |
| processFacetStats              | Function        | Logic for slider range behavior                                          | function(obj) \{...}                                    |
| setDefaultFilters              | Function        | Apply default filters on data fetch                                      | function() \{...}                                       |
| fields                         | Array           | Product attributes to be fetched                                         | \['title', 'price', 'brand']                            |
| onNoResult                     | Function        | Handler when no search result found                                      | function(obj) \{...}                                    |
| noEncoding                     | Boolean         | Enable encoding of URL params                                            | true                                                    |
| customReset                    | Function        | Custom behavior on reset or sort                                         | function() \{...}                                       |
| bannerSelector                 | String          | Selector for merchandising banners                                       | #up-sell-banner-section                                 |
| bannerTemp                     | String          | Template for banners                                                     | `<a href='{{landingUrl}}'><img src='{{imageUrl}}'></a>` |
| bannerCount                    | Number          | Number of banners to show                                                | 2                                                       |
| sortContainerSelector          | String          | Selector for sort section                                                | #sort-section                                           |
| sortOptions                    | Array           | Sorting options to be shown                                              | \[\{name: 'Popularity'}, \{...}]                        |
| sortContainerType              | String          | Sort interaction type                                                    | click / select                                          |
| sortContainerTemp              | String          | Template for sort UI                                                     | `<select>...</select>`                                  |
| pageSize                       | Number          | Products per page                                                        | 24                                                      |
| pageSizeContainerSelector      | String          | Selector for page size UI                                                | #results-pagesize                                       |
| pageSizeOptions                | Array           | Page size options                                                        | \[\{name: '48 items', value: '48'}, ...]                |
| pageSizeContainerType          | String          | Page size selection method                                               | click / select                                          |
| pageSizeContainerTemp          | String          | Template for page size UI                                                | `<select>...</select>`                                  |
| viewTypeContainerTemp          | String          | Template for view type UI                                                | `<a class='selected'>grid</a>`                          |
| viewTypeContainerSelector      | String          | Selector for view type section                                           | #results-pageview                                       |
| viewTypes                      | Array           | Available views                                                          | \['grid', 'list']                                       |
| variants                       | Boolean         | Enable variant display                                                   | true                                                    |
| variantsCount                  | Number          | Number of variants per product                                           | 3                                                       |
| isSwatches                     | Boolean         | Enable swatch display                                                    | true                                                    |
| swatchesSelector               | String          | Selector for swatch UI                                                   | .swatch-box                                             |
| mappedFields                   | Object          | Mapping of product attributes                                            | \{ imageUrl: 'imageUrl', ... }                          |

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