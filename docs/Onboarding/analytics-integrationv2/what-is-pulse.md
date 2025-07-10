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

\<Accordion title="1. Review Prerequisities" icon="fa-info-circle">
&#x20; Every event requires mandatory attributes to form its payload. Ensure these values are accessible in the page, DOM, or URL for sending the event. Additionally, specific HTML attributes may need to be added for each document or event type. Refer to the event payload section for detailed information.
\</Accordion>

\<Accordion title="2. Add the integration code" icon="fa-info-circle">
&#x20; Add the following \`\<script>\` tag at the end of your site’s HTML body.
&#x20; \`\`\`
&#x20;    \<script
type="text/javascript"
defer
charset="utf-8"
src="https\://libraries.unbxdapi.com/sdk-clients/PROD\_SITEKEY/ua/ua.js">
&#x20; \</script>
\`\`\`

The use of the `defer` attribute is to load the script in parallel with HTML parsing, ensuring the script executes only after the HTML is fully parsed. This improves the load performance of the page.

\</Accordion>

\<Accordion title="3.Validation payload data retrieval" icon="fa-info-circle">
&#x20; Verify that Netcore Unbxd Pulse can retrieve event payload data from sources such as DOM, URL, or browser windows.
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
```

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