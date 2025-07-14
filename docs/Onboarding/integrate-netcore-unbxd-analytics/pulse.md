---
title: Pulse
deprecated: false
hidden: false
metadata:
  robots: index
---
---
title: What is Pulse?
sidebarTitle: Netcore Unbxd Pulse
---

 Integration method recommended by Netcore Unbxd onboarding experts.

Netcore Unbxd Pulse is a JavaScript snippet added to your website to capture anonymous data on user interactions. This data is sent to our servers, where it fuels Unbxd’s AI models, enhancing your shoppers’ ability to find the products they’re looking for.

Pulse is engineered to function without impacting site performance. It operates efficiently, utilizing event listeners to track shopper activity without interfering with the browser’s event loop.

<Accordion title="Why is Netcore Unbxd Pulse the preferred integration method?">
  - **Simplified Ownership**  
  With other methods, customers bear the responsibility of integrating analytics, often requiring extensive support. Netcore Unbxd Pulse shifts this responsibility to us, requiring you to only include a single line of code on your website.

- **Faster Integration**  
  Traditional integration processes are often delayed by roadblocks during implementation, leading to analytics not being ready even after going live. With Netcore Unbxd Pulse, the integration process is drastically shortened, targeting completion within a couple of days.

- **Enhanced Post-Go-Live Experience**  
  Netcore Unbxd Pulse proactively addresses issues with broken analytics after going live. If analytics fails for specific metrics:
  - An alert banner will appear in the Console.
  - The support team will be notified automatically.
  - The support team will proactively resolve the issue and redeploy the analytics script without your intervention.
</Accordion>

## How to integrate Netcore Unbxd Pulse?


  < title="Review prerequisites">
    
Every event requires mandatory attributes to form its payload. Ensure these values are accessible in the page, DOM, or URL for sending the event. Additionally, specific HTML attributes may need to be added for each document or event type. Refer to the event payload section for detailed information.
  
  < title="Add the integration code">
  Add the following `<script>` tag at the end of your site's HTML body.
    ```html
 <script
    type="text/javascript"
    defer
    charset="utf-8"
    src="https://libraries.unbxdapi.com/sdk-clients/PROD_SITEKEY/ua/ua.js">
  </script>
```

 The use of the `defer` attribute is to load the script in parallel with HTML parsing, ensuring the script executes only after the HTML is fully parsed. This improves the load performance of the page.

  
  < title="Validate payload data retrieval">
    Verify that Netcore Unbxd Pulse can retrieve event payload data from sources such as DOM, URL, or browser windows.
 

## How to check if event payload data is retrieved?

### Search event

The **mandatory** `query` **payload** is captured from the search input box, and the event is triggered when the shopper either presses the Enter key or clicks the search submit button.

In this reference markup, the query value is extracted by targeting the input value from the class selector.

```html Example markup of the universal search bar
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