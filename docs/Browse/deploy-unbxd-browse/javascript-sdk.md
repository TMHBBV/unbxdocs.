---
title: Javascript SDK
deprecated: false
hidden: false
metadata:
  robots: index
---
Unbxd Search JS SDK helps you integrate Unbxd search and its functionalities.

With SDK documentation, you can optimise your layout of search results by integrating custom search Javascript (JS).

You will generate a search page template and make corresponding changes to the JS-SDK configuration to render the appropriate HTML responses. The search text box event needs to be replaced with the Unbxd event.

## Libraries

| **Library** | **Version**      |
| ----------- | ---------------- |
| jQuery      | 1.11.3 or higher |
| Handlebars  | 3.0.3 or higher  |

If your website is not using the above mentioned libraries then the same can be bundled along with unbxd search js file. For more details, check config options in bundle build procedure.

## Quickstart

Here, we will learn how to integrate the Unbxd Search JS SDK to optimize and power the search results display page on your site.The final integrated result that we are aiming at with this quickstart can be seen at this [codesandbox](https://codesandbox.io/p/sandbox/unbxdsdkv1-demo-q6hql).

The first step is to include the Unbxd Search JS along with its required dependencies.

For this add the following CSS & JS files into the “\<Head>” section of your HTML page.

```
<head>

    <link rel="stylesheet" href="http://demo-unbxd.unbxdapi.com/static/demo-unbxd/stylesheets/search.css” />

   <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/1.11.3/jquery.min.js”></script>

   <script type="text/javascript"

src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/3.0.3/handlebars.min.js”></script>

    <script type="text/javascript" src="https://libraries.unbxdapi.com/unbxdSearch_v2.js”></script>

</head>
```

Next, we instantiate the “setSearch” method available on the “Unbxd” window variable with the relevant configs. “setSearch” function accepts the search config object as an argument.

```
 <script type="text/javascript”>
     new Unbxd.setSearch({
       siteName: “<your site key>",
       APIKey: “<your API key>",
       type: "search",
       inputSelector: "#search_input"
     });
   </script>
```

Let us walk through the important configs that need to be passed along with their values for powering the search results page.

> 📘 NOTE
>
> You can find a detailed list of all acceptable configs list .

## Authentication

Once installed, yo need to authenticate your Unbxd extension using your Unbxd account keys (also known as Authentication Keys).

Whenever a customer signs up with Unbxd, they are issued one or more site keys and api keys depending on their use case. Some common scenarios:

For a customer with one website and two environments (production and staging), 2 site keys (one for each environment) and  1 API key is issued\
For a customer with more than one website (multi website vendor), the site key would be issued for every website + environment combination. So there would be an “n” number (equal to the number of website’s) of API keys generated.
For multiple site keys, check if you have:

* more than one environment
* more than one website
* different product set for staging and live, or
* wish to track search performance and clicks separately for every microsite.

To get your Site Key and API Key in the console, please refer to the steps mentioned in the Help Documentation.

Pass the Site Key and API Key that you get from the console in the “siteName” and “APIKey” configs.

siteName:

| **Property**    | **Details**                                                            |
| --------------- | ---------------------------------------------------------------------- |
| **Data type**   | `string`                                                               |
| **Required**    | `true`                                                                 |
| **Default**     | NA                                                                     |
| **Description** | Site name assigned by Unbxd (unique identifier for each customer/site) |

APIKey:

| **Property**    | **Details**                      |
| --------------- | -------------------------------- |
| **Data type**   | `string`                         |
| **Required**    | `true`                           |
| **Default**     | NA                               |
| **Description** | Unique API key assigned by unbxd |

At the end of this step, you should have the Site Key & API Key which can be passed into the “siteName” & “APIKey” configs as shown below:

```
   new Unbxd.setSearch({
       siteName: "<your site key>",
       APIKey: "<your API key>"
     });
```

## Types of Pages to render

This section allows you to indicate the product types available in your catalog while excluding specific categories of products while synchronizing.

The Unbxd extension supports seven types of products:

With Unbxd, you can configure the following product settings:

* Search:  used to power search results pages
* Browse: powers category listing pages
* Recommendations: powers personalized recommendations for the shoppers

Pass a config parameter called “type” to indicate whether you want to render the search results page (type=”search”) or the category listing page (type=”category”)

type:

<Table>
  <thead>
    <tr>
      <th>
        **Property**
      </th>

      <th>
        **Details**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Data type**
      </td>

      <td>
        `string`
      </td>
    </tr>

    <tr>
      <td>
        **Required**
      </td>

      <td>
        `true`
      </td>
    </tr>

    <tr>
      <td>
        **Default**
      </td>

      <td>
        `search`
      </td>
    </tr>

    <tr>
      <td>
        **Description**
      </td>

      <td>
        Used to indicate if the page is a search page or a category page.
      </td>
    </tr>

    <tr>
      <td>

      </td>

      <td>
        **Possible values:**
      </td>
    </tr>

    <tr>
      <td>

      </td>

      <td>
        * `search`: The search term in the URL is used by the library.
      </td>
    </tr>

    <tr>
      <td>

      </td>

      <td>
        * `category`: The `getCategoryID` function will be invoked to identify the category based on the given URL.
      </td>
    </tr>

    <tr>
      <td>
        **Dependency**
      </td>

      <td>
        * If `type = "search"`, then `searchQueryParam` attribute must be provided.
      </td>
    </tr>

    <tr>
      <td>

      </td>

      <td>
        * If `type = "category"`, then `getCategoryID` attribute must be provided.
      </td>
    </tr>
  </tbody>
</Table>

At the end of this step, you should choose a “type” of the page that you want to render and pass it in the config as shown below:

```
 new Unbxd.setSearch({
       siteName: “<your site key>",
       APIKey: “< your API key >",
    type: "search"
     });
```

## Configuring the Page

Before we delve into the next set of configs, let’s first understand the most common sections present in a search results page or category landing page.A search results page or a category landing page is made up of the following set of sections:

* Products list section
* View type could be grid or list view
* Sort by widget
* Pagination widget with no. of products per page control
* Pagination could be infinite scroll or page number based
* Facets section
* Spell check / search results message section
* Merchandising banners section

Here is a graphical representation of the various sections on a search results page:

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/4763fa1372ab1307f7baefafc5fa88a4211fa746e6d6b867cf1ed82e797e7794-JSSDK-main-768x861.png" />

In the following sections , we will discuss how to configure and render each of these sections with the Unbxd Search JS SDK.

### Search input box & search button selector

The following two parameters are used by the SDK to bind keyboard and mouse events to the  search input field and search button on your website.

inputSelector:

| **Property**    | **Details**                          |
| --------------- | ------------------------------------ |
| **Data type**   | `string`                             |
| **Required**    | `false`                              |
| **Default**     | `#search_query`                      |
| **Description** | CSS selector of the search input box |

searchButtonSelector:

| **Property**    | **Details**                                                     |
| --------------- | --------------------------------------------------------------- |
| **Data type**   | `string`                                                        |
| **Required**    | `false`                                                         |
| **Default**     | `#search_button`                                                |
| **Description** | Search query parameter name which contains the searched keyword |

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/5e92f341bf4cb42ca31faa7a47869df72490807a17f6a3cd586f5f458cee7379-search-input-box.png" />

At the end of this step, you should have configured the “inputSelector” &  “searchButtonSelector” as shown below:

```
new Unbxd.setSearch({
       siteName: “<your site Key>",
       APIKey: “<your API Key>",
       type: "search",
       inputSelector: "#searchBox",
       searchButtonSelector: "#searchButton"
});Search product results container
```

To render the products that resulted from the search API for the search term, you need to configure the CSS selector of the search results container. For this you can use the “searchResultContainer” config.

| **Property**     | **Details**                                                 |
| ---------------- | ----------------------------------------------------------- |
| **Data type**    | `string`                                                    |
| **Required**     | `true`                                                      |
| **Default**      | `NA`                                                        |
| **Description**  | CSS selector of the product results wrapper in your webpage |
| **Sample Value** | `#unbxd_product_results_container`                          |

In addition to the “searchResultContainer”, you can also configure the handlebars template to be used for each of the product cards using the “searchResultSetTemp” config.

**searchResultSetTemp:**

<Table>
  <thead>
    <tr>
      <th>
        **Property**
      </th>

      <th>
        **Details**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Data type**
      </td>

      <td>
        `array` / `function`
      </td>
    </tr>

    <tr>
      <td>
        **Required**
      </td>

      <td>
        `true`
      </td>
    </tr>

    <tr>
      <td>
        **Default**
      </td>

      <td>
        –
      </td>
    </tr>

    <tr>
      <td>
        **Description**
      </td>

      <td>
        When configured as an **array**, a HTML scheme to display the product for each view type must be configured. Or a **JavaScript function**, where the data will be passed as an input argument and the function should handle the dynamic binding of the HTML section.
      </td>
    </tr>

    <tr>
      <td>
        Input Value
      </td>

      <td>
        Properties in the input object,

        <br />

        numberOfProducts:number ->  Total Count of products matching the search term or browse location

        <br />

        Start:number ->  starting position of the result in the array (this would change while paginating through pages)

        <br />

        Products:array -> Product result data

        <br />

        &#x20;&#x20;
        \*input data -> \{numberOfProducts: 5361

        <br />

        start: 0

        <br />

        products: \[

        <br />

        \{

        <br />

        productUrl: “/shop/prod/mens-spring-step-casual-shoes/423424.htm”

        <br />

        was\_price\_min: 69.95

        <br />

        title: “Mens Spring Step  Casual Shoes”

        <br />

        was\_price\_max: 69.95

        <br />

        uniqueId: “ZTZ47C”

        <br />

        price\_max: 69.95

        <br />

        brand: \[“Spring Step”]

        <br />

        price\_min: 69.95

        <br />

        more\_colors\_available: “true”

        <br />

        imageUrl: \[“/images/store/product/images/563794479patrick.jpg”]

        <br />

        variantTotal: 5

        <br />

        score: 0.4200723

        <br />

        relevantDocument: “parent”

        <br />

        variantCount: 5

        <br />

        unbxdprank: 1

        <br />

        }]

        <br />

        unbxdparam\_requestId: null

        <br />

        }

        <br />

        Sample Value

        <br />
      </td>
    </tr>

    <tr>
      <td>
        Sample Value
      </td>

      <td>
        \[ grid: \[\{\{#products}}

        \<div class=”unbxd\_product\_tile”>

        &#x20;   \<a href=”\{\{productUrl}}” class=”image-hover unbxd-product-image” title=”\{\{title}}” data-url=”\{\{productUrl}}”

        &#x20;       unbxdparam\_title=”\{\{ItemName}}” unbxdattr=”product” unbxdparam\_sku=”\{\{uniqueId}}”

        &#x20;       unbxdparam\_prank=”\{\{unbxdprank}}”>

        &#x20;       \<img alt=”\{\{title}}” src=”\{\{imageurl}}”>

        &#x20; &#x20;

        &#x20;   \<div class=”prod\_price assortment\_price”>

        &#x20;       \<div class=”clearfix subpend-1 price-display featured-pricing money” itemtype=”http\://schema.org/Offer”

        &#x20;           itemscope=”” itemprop=”offers”>

        &#x20;           \<span class=”bold”>Price: \</span>

        &#x20;    \<span class=”bold m-large” itemprop=”price”>\<span

        &#x20;                   class=”dollar”>$\</span>\{\{price\_min}}

        &#x20;               – $\{\{price\_max}}\</span>

        &#x20;       \</div>

        &#x20;   \</div>

        &#x20;   \<div class=”suppend-1 prod\_title”>

        &#x20;       \{\{title}}

        &#x20;   \</div>

        &#x20;   \<div class=”subpend-1 product-ratings”>\<img class=”sli\_ratings\_scaled ae-img”

        &#x20;           src/store/content/bazaarVoice/images/\{\{no\_of\_stars}}.gif”

        &#x20;           alt=”\{\{no\_of\_stars}} star rating”>

        &#x20;       (\{\{getReviewCount}}

        &#x20;       review)\</div>

        &#x20;   \<p class=”sli\_grid\_excerpt”>\{\{description}}\</p>

        &#x20;    \</a>

        \</div>

        \{\{/products}}].join(‘’),

        List: \[\{\{#products}}

        \<div class=”unbxd\_product\_list\_tile”>

        &#x20;   \<div class=”unbxd\_col1″>

        &#x20;       \<a href=”\{\{#getRelativePath productUrl}}\{\{/getRelativePath}}”>\<img

        &#x20;               src=”\{\{#getRelativePath imageUrl}}\{\{/getRelativePath}}” alt=”\{\{ItemName}}” title=”\{\{ItemName}}”

        &#x20;               unbxdparam\_title=”\{\{ItemName}}” unbxdattr=”product” unbxdparam\_sku=”\{\{uniqueId}}”

        &#x20;               unbxdparam\_prank=”\{\{unbxdprank}}”>\</a>\</div>

        &#x20;   \<div class=”unbxd\_col2″>

        &#x20;       \<h2 class=”unbxd\_product\_title”>\<a href=”\{\{#getRelativePath productUrl}}\{\{/getRelativePath}}”

        &#x20;               title=”\{\{ItemName}}” unbxdparam\_title=”\{\{ItemName}}” unbxdattr=”product” unbxdparam\_sku=”\{\{uniqueId}}”

        &#x20;               unbxdparam\_prank=”\{\{unbxdprank}}”>\{\{ItemName}}\</a>\</h2>

        &#x20;       \{\{#if ShortDescription}}\<div class=”unbxd\_product\_description”>\{\{#trim ShortDescription maxchar=400 }}

        &#x20;           \{\{/trim}}\<span>…\<a href=”\{\{#getRelativePath productUrl}}\{\{/getRelativePath}}”>More\</a>\</span>\</div>\{\{/if}}

        &#x20;       \<div class=”unbxd\_product\_price”>

        &#x20;           \{\{#ifValidPrice OriginalPrice CurrentPrice}}

        &#x20;           \{\{#isSalePriceOffered OriginalPrice CurrentPrice}}\<div>Was: \<span

        &#x20;                   class=”was\_price”>$\{\{#priceFormatter OriginalPrice}}\{\{/priceFormatter}}\</span>\</div>

        &#x20;           \<div class=”promo\_price”>Price: $\{\{#priceFormatter CurrentPrice}}\{\{/priceFormatter}}\</div>\{\{else}}

        &#x20;           \<div class=”sell\_price”>Price: $\{\{#priceFormatter CurrentPrice}}\{\{/priceFormatter}}\</div>

        &#x20;           \{\{/isSalePriceOffered}}

        &#x20;           \{\{/ifValidPrice}}

        &#x20;           \<div class=”unbxd-add-to-cart”>

        &#x20;               \{\{#ifValidPrice OriginalPrice CurrentPrice}}

        &#x20;               \<form action=”/shop.axd/AddToCartBP”>

        &#x20;                   \<input type=”hidden” name=”edp\_no” value=”\{\{ProductId}}” />\<input type=”hidden” name=”qty”

        &#x20;                       value=”1″ />

        &#x20;                   \<input type=”image” class=”addToCart”

        &#x20;                       src=”\{\{#getRelativePath “https\://www\.firststreetonline.com/images/buttons/addToCart.png”}}\{\{/getRelativePath}}”

        &#x20;                       value=”Submit” alt=”\{\{ItemName}}” unbxd\_variant\_count=”\{\{variantCount}}”

        &#x20;                       unbxd\_product=”\{\{ProductId}}” />

        &#x20;               \</form>

        &#x20;               \{\{else}}

        &#x20;               \<a href=”\{\{#getRelativePath productUrl}}\{\{/getRelativePath}}” unbxdparam\_title=”\{\{ItemName}}”

        &#x20;                   unbxdattr=”product” unbxdparam\_sku=”\{\{uniqueId}}” unbxdparam\_prank=”\{\{unbxdprank}}”

        &#x20;                   class=”unbxd-clickable-text”>\<span>Click for More Info\</span>\</a>

        &#x20;               \{\{/ifValidPrice}}


        &#x20;           \</div>

        &#x20;       \</div>

        &#x20;   \</div>

        &#x20;   \<div class=”clear”>\</div>

        \</div>

        \{\{/products}}

        ].join(‘’)

        ]
      </td>
    </tr>
  </tbody>
</Table>

<br />

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/382294a60d95377bf22ff108fcabd8e8d0fb849013602f83c5350c689f40c2b6-search-div.png" />

## Sort Options

Sorting allows you to rearrange the search results based on certain fields in a particular order.

To render the Sort By feature, you need to configure the CSS selector of the Sort By container in your webpage. For this you can use the “sortContainerSelector” config.

sortContainerSelector: