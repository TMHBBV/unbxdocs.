---
title: What is Pulse?
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📘 Note
>
> Integration method recommended by Netcore Unbxd onboarding experts.

**Netcore Unbxd Pulse** is a JavaScript snippet added to your website to capture anonymous data on user interactions. This data is sent to our servers, where it fuels Unbxd’s AI models, enhancing your shoppers’ ability to find the products they’re looking for.

Pulse is engineered to function without impacting site performance. It operates efficiently, utilizing event listeners to track shopper activity without interfering with the browser’s event loop.

<Accordion title="Why is Netcore Unbxd Pulse the preferred integration method?" icon="fa-info-circle">
  * Simplified Ownership
    With other methods, customers bear the responsibility of integrating analytics, often requiring extensive support. Netcore Unbxd Pulse shifts this responsibility to us, requiring you to only include a single line of code on your website.
  * Faster Integration
    Traditional integration processes are often delayed by roadblocks during implementation, leading to analytics not being ready even after going live. With Netcore Unbxd Pulse, the integration process is drastically shortened, targeting completion within a couple of days.
  * Enhanced Post-Go-Live Experience
    Netcore Unbxd Pulse proactively addresses issues with broken analytics after going live. If analytics fails for specific metrics:
    * An alert banner will appear in the Console.
    * The support team will be notified automatically.
    * The support team will proactively resolve the issue and redeploy the analytics script without your intervention.
</Accordion>

## How to integrate Netcore Unbxd Pulse?

\<Accordion title="1. Review Prerequisities" icon="fa-info-circle">\
Every event requires mandatory attributes to form its payload. Ensure these values are accessible in the page, DOM, or URL for sending the event. Additionally, specific HTML attributes may need to be added for each document or event type. Refer to the event payload section for detailed information.
\</Accordion>

\<Accordion title="2. Add the integration code" icon="fa-info-circle">\
Add the following `\<script>` tag at the end of your site’s HTML body.\`\`\`
\<script
type="text/javascript"
defer
charset="utf-8"
src="[https://libraries.unbxdapi.com/sdk-clients/PROD\_SITEKEY/ua/ua.js](https://libraries.unbxdapi.com/sdk-clients/PROD_SITEKEY/ua/ua.js)">
\</script>

````

The use of the `defer` attribute is to load the script in parallel with HTML parsing, ensuring the script executes only after the HTML is fully parsed. This improves the load performance of the page.

\</Accordion>

\<Accordion title="3.Validation payload data retrieval" icon="fa-info-circle">\
Verify that Netcore Unbxd Pulse can retrieve event payload data from sources such as DOM, URL, or browser windows.
\</Accordion>

## How to check if event payload data is retrieved?

### Search Event

The mandatory `query` payload is captured from the search input box, and the event is triggered when the shopper either presses the Enter key or clicks the search submit button.

In this reference markup, the query value is extracted by targeting the input value from the class selector.

```Text Example Markup of the Universal Search Bar
<form id="searchQueryForm" method="method" action="/action">
  <input
    class="search-inputbox"
    id="searchInput"
    type="text"
    placeholder="find amazing products"
  />
  <button class="search-submit-button" id="searchBtn" type="submit">
    <i class="fas fa-search-icon"></i>
  </button>
</form>
````

### Browse Event

> 📘 Remember
>
> You can skip this event if you’ve not purchased Netcore Unbxd Browse.

The mandatory `page` and `pageType` payloads should be triggered on all category pages.

Activating the `categoryPage` event relies on the configuration of category fields in your feed and the method used to request the category API. To enable this event, make sure the `UnbxdAnalyticsConf` object is properly set on the window with accurate `page` and `page_type` values.

In this reference markup, the `page` and `page_type` values are extracted by targeting the `UnbxdAnalyticsConf` object from the window.

```Text Example Markup of the Category Page
window.UnbxdAnalyticsConf = window.UnbxdAnalyticsConf || {};
window.UnbxdAnalyticsConf["page"] =
  "{{categoryPath used for category api call (value of 'p' parameter)}}";
window.UnbxdAnalyticsConf["page_type"] = "BOOLEAN";
```

### Click Event

The mandatory `pid` payload is captured from the product element of the Products Listing Page, and the click event is triggered when the shopper clicks on the product.

#### Key points:

* The `pid` can be obtained from an HTML attribute or a URL, such as the `img_url` or `href` on the product card.
* If the unique ID for the product has not been added to the product element, refer to the Netcore Unbxd Search API response to pass it.

```Text Example Markup of the Product Listing Page
<div class="search-results-grid" pageType="search">
  <div class="search-result" data-item-id="371823">
    <a href="https://www.example.com/product/productname">
      <img src="https://www.example.com/images/productname.png" />
      <span>Organic Honeycrisp Apple</span>
    </a>
  </div>
  <div class="search-result" data-item-id="371811">
    <a href="https://www.example.com/product/productname">
      <img src="https://www.example.com/images/productname.png" />
      <span>Organic Banana</span>
    </a>
  </div>
</div>
```

### Cart Event

#### 1. Quick view/Product details page

The mandatory `pid` and `variantid` (if your catalog contains product variants) payloads are captured from the DOM or from a URL, such as the browser URL, `img_url`, or `href` in the product details section. The event is triggered when the respective CTA button is clicked.

Example browser URL:`https://www.example.com/product/product_107440/107440_green?sale=clearance`

```Text Example Markup of the Product Description Page
<div class="pdp-page" id="quickLook">
  <div
    class="product-details"
    data-item-id="107440"
    data-variant-id="107440_green"
  >
    <div class="hero-img">
      <img
        src="https://www.example.com/images/product_107440/107440_green.png"
      />
    </div>
    <div id="productInfo">
      <h3>Fresh Blackberry Holland 125 gm</h3>
      <input type="number" class="qty-inputbox" />
      <span class="price">$10.99</span>
      <button class="add-to-wishlist" type="button"></button>
      <button class="add-to-cart" type="button"></button>
    </div>
  </div>
</div>
```

<br />

#### 2. Cart dropdown/Cart page

The mandatory `pid` and `variantid` (if your catalog contains product variants) payloads are captured from the DOM or from a URL, such as the browser URL, `img_url`, or `href` in the product details section. The event is triggered when the quantities are modified.

```Text Example Markup of the Cart Page
<div class="cart-list-grid">
  <div class="cart-item" data-item-id="107440">
    <a href="https://www.example.com/product/product_107440">
      <img src="https://www.example.com/images/product_107440.png" />
    </a>
    <div id="productInfo">
      <h3>Fresh Blackberry Holland 125 gm</h3>
      <span class="qty">2</span>
      <span class="price">$10.99</span>
      <div class="qty-wrap">
        <span class="quantity-increase"> + </span>
        <input type="text" class="quantity-value" />
        <span class="quantity-decrease"> - </span>
      </div>
    </div>
  </div>

  <div class="cart-item" data-item-id="245102">
    <a href="https://www.example.com/product/product_245102">
      <img src="https://www.example.com/images/product_245102.png" />
    </a>
    <div id="productInfo">
      <h3>Fresh Orange Navel Box</h3>
      <span class="qty">1</span>
      <span class="price">$20.99</span>
      <div class="qty-wrap">
        <span class="quantity-increase"> + </span>
        <input type="text" class="quantity-value" />
        <span class="quantity-decrease"> - </span>
      </div>
    </div>
  </div>
</div>
```

### Order event

The ownership of the Order event lies with the retailer. Details of successfully ordered products should be stored as a variable on the browser’s window, as demonstrated in the example below. Netcore Unbxd Pulse will retrieve this data from the window object and trigger the order event accordingly.

> 📘 Note
>
> The key names need to be maintained as shown in the example below given the ownership of the event will not be with Netcore Unbxd.

```Text Example JSON of the Order Success Page
window.unbxdOrderData = [
  {
    pid: "107440", // Required - Product ID
    variantId: "107440_01", // Required only if your catalog has variants
    qty: "1",
    price: "29.99",
  },
  {
    pid: "245102", // Required - Product ID
    variantId: "245102_red", // Required only if your catalog has variants
    qty: "2",
    price: "10.99",
  },
];
```

### Autosuggest

Things to note before configuration:

* Only required if you’ve subscribed to the Netcore Unbxd Autosuggest solution.
* Mandatory to add the payload data to the DOM if you’ve not used the Netcore Unbxd Autosuggest SDK.\
  ​

#### KEYWORD\_SUGGESTION

Below are the mandatory HTML attributes and values that need to be placed in the Autosuggest UI section:

| Attribute Name    | Value(should be an exact match) |
| :---------------- | :------------------------------ |
| `data-unxAsType`  | `KEYWORD\_SUGGESTION`           |
| `data-unxAsSugg`  | suggested query                 |
| `data-unxAsPrank` | index number                    |

> 📘 Note
>
> The attribute names can be defined based on your requirements. However, the attribute values must match EXACTLY as provided above.

```Text Example Markup
<ul class="autosuggest-suggestions-wrapper">
  <li
    class="list-item"
    data-unxAsType="KEYWORD_SUGGESTION"
    data-unxAsSugg="Apple"
    data-unxAsPrank="1"
  >
    Apple
  </li>
  <li
    class="list-item"
    data-unxAsType="KEYWORD_SUGGESTION"
    data-unxAsSugg="Banana"
    data-unxAsPrank="2"
  >
    Banana
  </li>
  <li
    class="list-item"
    data-unxAsType="KEYWORD_SUGGESTION"
    data-unxAsSugg="Cherry"
    data-unxAsPrank="3"
  >
    Cherry
  </li>
  <li
    class="list-item"
    data-unxAsType="KEYWORD_SUGGESTION"
    data-unxAsSugg="Date"
    data-unxAsPrank="4"
  >
    Date
  </li>
  <li
    class="list-item"
    data-unxAsType="KEYWORD_SUGGESTION"
    data-unxAsSugg="Elderberry"
    data-unxAsPrank="5"
  >
    Elderberry
  </li>
</ul>
```

#### TOP\_SEARCH\_QUERIES

Below are the mandatory HTML attributes and values that need to be placed in the Autosuggest UI section:

| Attribute Name    | Value(should be an exact match) |
| :---------------- | :------------------------------ |
| `data-unxAsType`  | `TOP_SEARCH_QUERIES`            |
| `data-unxAsSugg`  | suggested query                 |
| `data-unxAsPrank` | index number                    |

> 📘 Note
>
> The attribute names can be defined based on your requirements. However, the attribute values must match EXACTLY as provided above.

```Text Example Markup
<ul class="autosuggest-suggestions-wrapper">
  <li
    class="list-item"
    data-unxAsType="TOP_SEARCH_QUERIES"
    data-unxAsSugg="Tops"
    data-unxAsPrank="1"
  >
    Tops
  </li>
  <li
    class="list-item"
    data-unxAsType="TOP_SEARCH_QUERIES"
    data-unxAsSugg="Dress"
    data-unxAsPrank="2"
  >
    Dress
  </li>
  <li
    class="list-item"
    data-unxAsType="TOP_SEARCH_QUERIES"
    data-unxAsSugg="Shirt"
    data-unxAsPrank="3"
  >
    Shirt
  </li>
  <li
    class="list-item"
    data-unxAsType="TOP_SEARCH_QUERIES"
    data-unxAsSugg="Shoes"
    data-unxAsPrank="4"
  >
    Shoes
  </li>
  <li
    class="list-item"
    data-unxAsType="TOP_SEARCH_QUERIES"
    data-unxAsSugg="Wallets"
    data-unxAsPrank="5"
  >
    Wallets
  </li>
</ul>
```

#### PROMOTED\_SUGGESTION

Below are the mandatory HTML attributes and values that need to be placed in the Autosuggest UI section:

| Attribute Name    | Value(should be an exact match) |
| :---------------- | :------------------------------ |
| `data-unxAsType`  | `PROMOTED_SUGGESTION`           |
| `data-unxAsSugg`  | suggested query                 |
| `data-unxAsPrank` | index number                    |

> 📘 Note
>
> The attribute names can be defined based on your requirements. However, the attribute values must match EXACTLY as provided above.

```Text Example Markup 
<ul class="autosuggest-suggestions-wrapper">
  <li
    class="list-item"
    data-unxAsType="PROMOTED_SUGGESTION"
    data-unxAsSugg="Toys"
    data-unxAsPrank="1"
  >
    Toys
  </li>
  <li
    class="list-item"
    data-unxAsType="PROMOTED_SUGGESTION"
    data-unxAsSugg="Puma Shoes"
    data-unxAsPrank="2"
  >
    Puma Shoes
  </li>
  <li
    class="list-item"
    data-unxAsType="PROMOTED_SUGGESTION"
    data-unxAsSugg="Tissot Watch"
    data-unxAsPrank="3"
  >
    Tissot Watch
  </li>
  <li
    class="list-item"
    data-unxAsType="PROMOTED_SUGGESTION"
    data-unxAsSugg="Christmas Gift"
    data-unxAsPrank="4"
  >
    Christmas Gift
  </li>
</ul>
```

#### TRENDING\_QUERIES

Below are the mandatory HTML attributes and values that need to be placed in the Autosuggest UI section:

| Attribute Name    | Value(should be an exact match) |
| :---------------- | :------------------------------ |
| `data-unxAsType`  | `TRENDING_QUERIES`              |
| `data-unxAsSugg`  | suggested query                 |
| `data-unxAsPrank` | index number                    |

> 📘 Note
>
> The attribute names can be defined based on your requirements. However, the attribute values must match EXACTLY as provided above.

```Text Example Markup
<ul class="autosuggest-suggestions-wrapper">
  <li
    class="list-item"
    data-unxAsType="TRENDING_QUERIES"
    data-unxAsSugg="Toys"
    data-unxAsPrank="1"
  >
    Toys
  </li>
  <li
    class="list-item"
    data-unxAsType="TRENDING_QUERIES"
    data-unxAsSugg="Puma Shoes"
    data-unxAsPrank="2"
  >
    Puma Shoes
  </li>
  <li
    class="list-item"
    data-unxAsType="TRENDING_QUERIES"
    data-unxAsSugg="Tissot Watch"
    data-unxAsPrank="3"
  >
    Tissot Watch
  </li>
  <li
    class="list-item"
    data-unxAsType="TRENDING_QUERIES"
    data-unxAsSugg="Christmas Gift"
    data-unxAsPrank="4"
  >
    Christmas Gift
  </li>
</ul>
```

####