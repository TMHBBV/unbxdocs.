---
title: Analytics
deprecated: false
hidden: false
metadata:
  robots: index
---
# Introduction To Analytics

The trackers are unique tracking codes that must be configured onto the store properties that yield an interaction. We call this interaction an “event”. UNBXD collects visitor events, such as search queries, product clicks, impressions, products added to cart, orders., etc. These events are tracked for each user/visitor using browser cookies. With this information, a profile is built for every visitor, based on his/her affinity to different categories, brands, or prices. This information is then aggregated and analyzed for multiple purposes:

Providing relevant and personalized results on the listing page\
Enhancing the recommendation algorithms to have a satisfactory product discovery experience.
Generating reports
The visitor profiles are key in fetching help fetch relevant and personalized products as search results. It also helps in generating detailed reports. Integrating analytics is a mandatory step towards achieving conversion goals.

Integration Options\
There are 3 ways for integrating Unbxd analytics on your web pages:

1. GTM/Tealium Integration – This approach is suitable if you are already using any of these tools for managing the tags on the web pages of your site without touching the HTML code. .
2. Browser integration – This approach is suitable if you can add the JS snippets on the web pages. The included JS analytics SDK makes the easiest way to integrate analytics and this is our recommended approach/
3. API Integration –  Refer to our API documentation and we recommend this route only if you have reasons to not go with the above approaches.

## Events required for UNBXD Products

Please find below the list of all the events required to be added based on the scope of the integration ( Search, Browse, Recommendations )

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Search
      </th>

      <th>
        Browse
      </th>

      <th>
        Recommendation
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Visitor
      </td>

      <td>
        Visitor
      </td>

      <td>
        Visitor
      </td>
    </tr>

    <tr>
      <td>
        Search Hit
      </td>

      <td>
        Category Page Hit
      </td>

      <td>
        *
      </td>
    </tr>

    <tr>
      <td>
        Search Impression
      </td>

      <td>
        Category Impression
      </td>

      <td>
        Recommendation Impression
      </td>
    </tr>

    <tr>
      <td>
        Product Click
      </td>

      <td>
        Product Click
      </td>

      <td>
        Product Click
      </td>
    </tr>

    <tr>
      <td>
        Facets
      </td>

      <td>
        Facets
      </td>

      <td>
        *
      </td>
    </tr>

    <tr>
      <td>
        Add To Cart
      </td>

      <td>
        Add To Cart
      </td>

      <td>
        Add To Cart
      </td>
    </tr>

    <tr>
      <td>
        Product View
      </td>

      <td>
        Product View
      </td>

      <td>
        Product View
      </td>
    </tr>

    <tr>
      <td>
        Dwell Time
      </td>

      <td>
        Dwell Time
      </td>

      <td>
        Dwell Time
      </td>
    </tr>

    <tr>
      <td>
        Remove From Cart
      </td>

      <td>
        Remove From Cart
      </td>

      <td>
        Remove From Cart
      </td>
    </tr>

    <tr>
      <td>
        Order
      </td>

      <td>
        Order
      </td>

      <td>
        Order
      </td>
    </tr>
  </tbody>
</Table>