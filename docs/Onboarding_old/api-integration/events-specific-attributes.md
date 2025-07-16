---
title: Events Specific Attributes
deprecated: false
hidden: false
metadata:
  robots: index
---
Check out our <a href="/integrations/overview#what-are-the-events-we-track">Events overview page</a> to understand the functioning of each event.

## Visitor

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"url":"{{url-of-the-website}}",
"referrer":"{{reference-link}}",
"visit_type":"{{first-or-repeat}}",
"visitId":"{{visitId}}"}
&UnbxdKey={{unbxd_sitekey}}
&action=”visitor”
&uid=”uid-1642414737751-2003”
&t=”1662364656435|0.29442892143527755”
```

Refer here for our <a href="https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22url%22%3A%22https%3A//www.demo.unbxd.com.au/c/Sofas%3Fredirectq%3Dsofas%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/search/Sofas%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D&UnbxdKey=demo-unbxd700181503576558&action=visitor&uid=uid-1707194142543-92694&t=1709118200869%7C0.3265333503179766">sample API</a>

Payload details:

| **Attribute Name** | **Type** | **Value to Pass**                                                                                                              |
| ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`           | `string` | `visitor`                                                                                                                      |
| `url`              | `string` | Website URL where the search is performed                                                                                      |
| `visit_type`       | `string` | Either `first_time` or `repeat`                                                                                                |
| `UnbxdKey`         | `string` | UnbxdSitekey value                                                                                                             |
| `uid`              | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`         | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |

## Search Hit

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data=%7B%22url%22%3A%22https%3A//www.demo.unbxd.com.au/c/Sofas%3F
redirectq%3Dsofas%22%2C%22
referrer%22%3A%22https%3A//www.demo.unbxd.com.au/search/Sofas%22%2C%22
visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_
uf%22%3A3902881952%2C%22
visitId%22%3A%22visitId-1709116400821-5910%22%7D
&UnbxdKey=demo-unbxd700181503576558
&action=visitor
&uid=uid-1707194142543-92694
&t=1709118200869%7C0.3265333503179766
```

Refer here for our <a href="https://tracker.unbxdapi.com/v2/1p.jpg?data={%22query%22:%22red%20sofa%22,%22url%22:%22https://www.demo.unbxd.com/search/red%20sofa%22,%22referrer%22:%22https://www.demo.unbxd.com/c/Sofas?q=sofas%22,%22visit_type%22:%22repeat%22,%22ver%22:%224.0.28%22,%22_uf%22:3902881952,%22visitId%22:%22visitId-1709112773396-59772%22}&UnbxdKey=demo-unbxd700181503576558&action=search&uid=uid-1707194142543-92694&t=1709112807000|0.10714066830945645">sample API</a>

Payload details:

| **Attribute Name** | **Type** | **Value to Pass**                                                                                                              |
| ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`           | `string` | `search`                                                                                                                       |
| `query`            | `string` | The search query entered by the shopper                                                                                        |
| `url`              | `string` | Website URL where the search is performed                                                                                      |
| `UnbxdKey`         | `string` | UnbxdSitekey value                                                                                                             |
| `uid`              | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`         | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |

## Search Impression

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{search-query}}",
"pids_list":"{{list-of-products-uniqueId}}",
"url":"{{url-of-the-website}}",
"referrer":"{{referrer}}",
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=PRODUCT_IMPRESSIONS
&uid={{uid}}
&t=1662366285967|0.7498946341398707
```

Refer here for our <a href="https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Dress%22%2C%22pids_list%22%3A%5B%22RML02384%22%2C%22GER02112%22%2C%22GER02160%22%2C%22WHO03671%22%2C%22KDZ03516%22%2C%22WHO03558%22%2C%22RML02290%22%2C%22GER02158%22%2C%22NAU06605%22%2C%22BEB03937%22%2C%22WHO03672%22%2C%22WHO03670%22%2C%22THA02198%22%2C%22WHO03620%22%2C%22BFA01862%22%2C%22NAU06700%22%2C%22STU04666%22%2C%22STU04612%22%2C%22NCN01301%22%2C%22WHO03659%22%2C%22DKY02759%22%2C%22GER02148%22%2C%22GER02147%22%2C%22ALU10901%22%5D%2C%22url%22%3A%22https%3A//demo.unbxd.com/Search.aspx%3Fk%3DDress%22%2C%22referrer%22%3A%22https%3A//demo.unbxd.com/Search.aspx%3Fk%3Dred%2520dress%22%2C%22requestId%22%3A%220643220e-c900-4825-9f2d-f740025b2b0d%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A1187461382%2C%22visitId%22%3A%22visitId-1662364656433-84380%22%7D&UnbxdKey=demo-unbxd700181503576558&action=PRODUCT_IMPRESSIONS&uid=uid-1642414737751-20033&t=1662366285967%7C0.7498946341398707">sample API</a>

Payload details:

| **Attribute Name**     | **Type** | **Value to Pass**                                                                                                              |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`               | `string` | `PRODUCT_IMPRESSIONS`                                                                                                          |
| `pid`                  | `string` | Unique ID for the product, to be taken from the search API response                                                            |
| `variantId` (optional) | `string` | Variant ID assigned to the variant of the product. Necessary only if variants are present.                                     |
| `url`                  | `string` | Website URL where the search is performed                                                                                      |
| `visit_type`           | `string` | Either `first_time` or `repeat`                                                                                                |
| `UnbxdKey`             | `string` | UnbxdSitekey value                                                                                                             |
| `uid`                  | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                    | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`             | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |

## Browse Impression

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"page":"categoryPathId:\"117>119\"",
"page_type":'{{category-page-type}}',
"pids_list":"{{list-of-products-uniqueId}}",
"url":"{{url-of-the-website}}",
"referrer":"{{referrer}}",
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=PRODUCT_IMPRESSIONS
&uid={{uid}}
&t=1662366068017|0.9865798147898728
```

Refer here for our <a href="https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22page%22%3A%22categoryPathId%3A%5C%22117%3E119%5C%22%22%2C%22page_type%22%3A%22BOOLEAN%22%2C%22pids_list%22%3A%5B%2240866%22%2C%2242301%22%2C%2242814%22%2C%2242803%22%2C%2242246%22%2C%2242295%22%5D%2C%22url%22%3A%22https%3A//demo.unbxd.com/clothing/women-dresses/cat%3Fdepth%3D2%26label%3DClothing-Dresses%22%2C%22referrer%22%3A%22https%3A//demo.unbxd.com/%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A1187461382%2C%22requestId%22%3A%220643220e-c900-4825-9f2d-f740025b2b0d%22%2C%22visitId%22%3A%22visitId-1662366042689-8947%22%7D&UnbxdKey=demo-unbxd700181503576558&action=PRODUCT_IMPRESSIONS&uid=uid-1641990940843-5809&t=1662366068017%7C0.9865798147898728">sample API</a>

Payload details:

| **Attribute Name**     | **Type** | **Value to Pass**                                                                                                              |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`               | `string` | `PRODUCT_IMPRESSIONS`                                                                                                          |
| `pid`                  | `string` | Unique ID for the product, to be taken from the search API response                                                            |
| `qty`                  | `string` | The number of units added to the cart (as a string). For example, `“2”` for 2 units.                                           |
| `variantId` (optional) | `string` | Variant ID assigned to the variant of the product. Necessary only if variants are present.                                     |
| `url`                  | `string` | Website URL where the search is performed                                                                                      |
| `visit_type`           | `string` | Either `first_time` or `repeat`                                                                                                |
| `UnbxdKey`             | `string` | UnbxdSitekey value                                                                                                             |
| `uid`                  | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                    | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`             | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |

## Product Click

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"pid":"{{uniqueId-of-the-product}}",
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=click&uid={uid}}
&t=1662365583875|0.7442797542869459
```

Refer here for our <a href="https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22pid%22:%22BNC_KEASBOOOLI%22,%22url%22:%22https://www.demo.unbxd.com.au/search/red%20sofa%22,%22referrer%22:%22https://www.demo.unbxd.com.au/c/Sofas?q=sofas%22,%22visit_type%22:%22repeat%22,%22ver%22:%224.0.28%22,%22_uf%22:3902881952,%22visitId%22:%22visitId-1709112773396-59772%22%7D&UnbxdKey=demo-unbxd700181503576558&action=click&uid=uid-1707194142543-92694&t=1709112862073%7C0.42677918156526107">sample API</a>

Payload details:

| **Attribute Name** | **Type** | **Value to Pass**                                                                                                              |
| ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`           | `string` | `click`                                                                                                                        |
| `pid`              | `string` | Unique ID for the product, to be taken from the search API response                                                            |
| `url`              | `string` | Website URL where the search is performed                                                                                      |
| `visit_type`       | `string` | Either `first_time` or `repeat`                                                                                                |
| `UnbxdKey`         | `string` | UnbxdSitekey value                                                                                                             |
| `uid`              | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`         | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |

## Search Facets

Template API: Selection and Deselection of facets

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{search-query}}",
"facets":{"facet-name1":{ "prank": "1","selected":
[{"prank": "2", "val": "facet_value1"},
  {"prank": "3","val": "facet_value2"}]}, 
  "facet-name2":{ "prank": "2","deselected":
  [{"prank": "4", "val": "facet_value1"},
  {"prank": "7","val": "facet_value2"}]}},
  "url":"{{url-of-the-website}}",
  "referrer":"{{referrer}}",
  "requestId":"{{unx-request-id}}",
  "visit_type":"{{first_or_repeat}}",
  "visitId":"{{visit-id}}"}
  &UnbxdKey={{unbxd-sitekey}}
  &action=facets&uid={{uid}}5
  &t=1662365253141|0.6835012308821242

```

Template API: Clear All facets

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{search-query}}",
"facets":{"unxFacetsReset":true},
"url":"{{url-of-the-website}}",
"referrer":"{{referrer}}",
"requestId":"{{unx-request-id}}",
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=facets&uid={{uid}}5
&t=1662365253141|0.6835012308821242
```

Payload details:

| **Attribute Name**     | **Type** | **Value to Pass**                                                                                                              |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`               | `string` | `facets`                                                                                                                       |
| `pid`                  | `string` | Unique ID for the product, to be taken from the search API response                                                            |
| `qty`                  | `string` | The number of units added to the cart (as a string). For example, `“2”` for 2 units.                                           |
| `variantId` (optional) | `string` | Variant ID assigned to the variant of the product. Necessary only if variants are present.                                     |
| `url`                  | `string` | Website URL where the search is performed                                                                                      |
| `visit_type`           | `string` | Either `first_time` or `repeat`                                                                                                |
| `UnbxdKey`             | `string` | UnbxdSitekey value                                                                                                             |
| `uid`                  | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                    | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`             | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |

## Browse Facets

Template API: Selection and Deselection of facets

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"page":"categoryPathId:\"117>119\"",
"page_type":"{{category-page-type}}",
"facets":{"facet-name1":{ "prank": "1","selected":[{"prank": "2", "val": "facet_value1"},
{"prank": "3","val": "facet_value2"}]}, 
"facet-name2":{ "prank": "2","deselected":
[{"prank": "4", "val": "facet_value1"},{"prank": "7","val": "facet_value2"}]} },
"url":"{{url-of-the-website}}",
"referrer":"{{referrer}}",
"requestId":"{{unx-request-id}}",
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=facets&uid={{uid}}5
&t=1662365253141|0.6835012308821242

```

Template API: Clear All facets

```
http://tracker.unbxdapi.com/v2/1p.jpg
?data={"page":"categoryPathId:\"117>119\"","page_type":"{{category-page-type}}",
"facets":{"unxFacetsReset": true },
"url":"{{url-of-the-website}}",
"referrer":"",
"requestId":"{{unx-request-id}}",
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=facets&uid={{uid}}5
&t=1662365253141|0.6835012308821242
```

Payload details:

| **Attribute Name**     | **Type** | **Value to Pass**                                                                                                              |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`               | `string` | `facets`                                                                                                                       |
| `pid`                  | `string` | Unique ID for the product, to be taken from the search API response                                                            |
| `qty`                  | `string` | The number of units added to the cart (as a string). For example, `“2”` for 2 units.                                           |
| `variantId` (optional) | `string` | Variant ID assigned to the variant of the product. Necessary only if variants are present.                                     |
| `url`                  | `string` | Website URL where the search is performed                                                                                      |
| `visit_type`           | `string` | Either `first_time` or `repeat`                                                                                                |
| `UnbxdKey`             | `string` | UnbxdSitekey value                                                                                                             |
| `uid`                  | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                    | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`             | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |

## Add to Cart

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"pid":"{{uniqueid-of-the-product}}",
"qty":”{{no-of-units}}",
"variantId":"{{variantId-of-the-variant}}",
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first-or-repeat}}"
&UnbxdKey=”{{unbxd-sitekey}}"
&action=cart&uid={{uid}}&t={{time-spent}}

```

Refer here for our <a href="https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22pid%22:%22BNC_KEASBOOOLI%22,%22qty%22:%221%22,%22variantId%22:%22KEASBD3STOOOLINBLK%22,%22requestId%22:%22%22,%22url%22:%22https://www.demo.unbxd.com.au/Categories/Bedroom-&-Mattresses/Beds/Sofa-Beds-&-Futons/Kenza-3-Seater-Sofa-Bed/p/KEASBD3STOOOLINBLK%22,%22referrer%22:%22https://www.demo.unbxd.com.au/search/red%20sofa%22,%22visit_type%22:%22repeat%22,%22ver%22:%224.0.28%22,%22_uf%22:3902881952,%22visitId%22:%22visitId-1709112773396-59772%22%7D&UnbxdKey=demo-unbxd700181503576558&action=cart&uid=uid-1707194142543-92694&t=1709113051278%7C0.4969283259317627">sample API</a>

Payload details:

| **Attribute Name**     | **Type** | **Value to Pass**                                                                                                              |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`               | `string` | `cart`                                                                                                                         |
| `pid`                  | `string` | Unique ID for the product, to be taken from the search API response                                                            |
| `qty`                  | `string` | The number of units added to the cart (as a string). For example, `"2"` for 2 units.                                           |
| `variantId` (optional) | `string` | Variant ID assigned to the variant of the product. Necessary only if variants are present.                                     |
| `url`                  | `string` | Website URL where the search is performed                                                                                      |
| `visit_type`           | `string` | Either `"first_time"` or `"repeat"`                                                                                            |
| `UnbxdKey`             | `string` | UnbxdSitekey value                                                                                                             |
| `uid`                  | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                    | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`             | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |

## Order

Template API for single product:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"pid":"{{uniqueId-of-the-product}}",
"qty":"{{quantity-selected}}",
"price":"{{unit-price-for-product}}",
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=order
&uid={{uid}}1658904085468-92302
&t=1662367087116|0.07798836811209986

```

Template API for multiple product:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"products":[{"pid":"{{uniqueId-of-the-product}}",
"qty":"{{quantity-selected}}",
"price":"{{unit-price-for-product}}"}, {"pid":"{{uniqueId-of-the-product}}",
"qty":"{{quantity-selected}}",
"price":"{{unit-price-for-product}}"}],
"url":"{{url-of-the-website}}",
"referrer":"{{reference-link}}",
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=order
&uid={{uid}}1658904085468-92302
&t=1662367087116|0.07798836811209986
```

Refer here for our <a href="https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22products%22%3A%5B%7B%22pid%22%3A%229500%22%2C%22qty%22%3A%221%22%2C%22price%22%3A%22153%22%2C%22variantId%22%3A%22V96576%22%7D%2C%7B%22pid%22%3A%229501%22%2C%22qty%22%3A%222%22%2C%22price%22%3A%22143%22%2C%22variantId%22%3A%22V980560%22%7D%2C%7B%22pid%22%3A%229502%22%2C%22qty%22%3A%225%22%2C%22price%22%3A%22133%22%2C%22variantId%22%3A%22V980033%22%7D%5D%2C%22url%22%3A%22http%3A%2F%2Flocalhost%3A8080%2F%22%2C%22referrer%22%3A%22%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A4213677804%2C%22visitId%22%3A%22visitId-1679387024735-20128%22%7D&UnbxdKey=demo-unbxd700181503576558&action=order&uid=uid-1653404599885-19305&t=1679387036973%7C0.7978658173524473">sample API</a>

Payload details:

| **Attribute Name**     | **Type** | **Value to Pass**                                                                                                              |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `action`               | `string` | `order`                                                                                                                        |
| `pid`                  | `string` | Unique ID for the product, to be taken from the search API response                                                            |
| `qty`                  | `string` | The number of units added to the cart (as a string). For example, `"2"` for 2 units.                                           |
| `variantId` (optional) | `string` | Variant ID assigned to the variant of the product. Necessary only if variants are present.                                     |
| `price`                | `string` | Unit price of the product and its variant (if variant is selected).                                                            |
| `url`                  | `string` | Website URL where the search is performed                                                                                      |
| `visit_type`           | `string` | Either `"first_time"` or `"repeat"`                                                                                            |
| `UnbxdKey`             | `string` | UnbxdSitekey value                                                                                                             |
| `uid`                  | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                         |
| `t`                    | `string` | Timestamp formula: `t : current_time \\| random number between 0 to 1` and `t = new Date().getTime() + ‘\\|’ + Math.random();` |
| `referrer`             | `string` | Link from where the page is opened `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';`         |