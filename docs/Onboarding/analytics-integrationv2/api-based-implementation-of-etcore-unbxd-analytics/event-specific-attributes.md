---
title: Event-specific Attributes
deprecated: false
hidden: false
metadata:
  robots: index
---
Check out our [Events](doc:analytics-integrationv2) overview page to understand the functioning of each event.

# Visitor

## Template API

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

Refer here for our [sample API](https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22url%22%3A%22https%3A//www.demo.unbxd.com.au/c/Sofas%3Fredirectq%3Dsofas%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/search/Sofas%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=visitor\&uid=uid-1707194142543-92694\&t=1709118200869%7C0.3265333503179766)

### Payload details

| Attribute Name | Type   | Value to Pass                                                                                     |                                                                 |                      |
| :------------- | :----- | :------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------- | :------------------- |
| `action`       | String | `visitor`                                                                                         |                                                                 |                      |
| `url`          | String | Website URL where the search is performed                                                         |                                                                 |                      |
| `visit_type`   | String | Either `first_time` or `repeat`                                                                   |                                                                 |                      |
| `UnbxdKey`     | String | UnbxdSitekey value                                                                                |                                                                 |                      |
| `uid`          | String | `unbxd.userId` (Needs to be extracted from the cookie)                                            |                                                                 |                      |
| `t`            | String | Timestamp formula: \`t : current\_time \\                                                         | random number between 0 to 1 and t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`     | String | Link from where the page is opened referrer: \`referrer: sessionStorage.getItem('urlPrevious') \\ | \| document.referrer \\                                         | \| '';\`             |

# Search Hit

## Template API

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

Refer here for our sample [API](https://tracker.unbxdapi.com/v2/1p.jpg?data=\{%22query%22:%22red%20sofa%22,%22url%22:%22https://www.demo.unbxd.com/search/red%20sofa%22,%22referrer%22:%22https://www.demo.unbxd.com/c/Sofas?q=sofas%22,%22visit_type%22:%22repeat%22,%22ver%22:%224.0.28%22,%22_uf%22:3902881952,%22visitId%22:%22visitId-1709112773396-59772%22}\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709112807000|0.10714066830945645)

### Payload details

| Attribute Name | Type   | Value to Pass                                                                            |                                                                 |                      |
| :------------- | :----- | :--------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :------------------- |
| `action`       | String | `search`                                                                                 |                                                                 |                      |
| `url`          | String | Website URL where the search is performed                                                |                                                                 |                      |
| `query`        | String | The search query entered by the shopper                                                  |                                                                 |                      |
| `UnbxdKey`     | String | UnbxdSitekey value                                                                       |                                                                 |                      |
| `uid`          | String | `unbxd.userId` (Needs to be extracted from the cookie)                                   |                                                                 |                      |
| `t`            | String | Timestamp formula: \`t : current\_time \\                                                | random number between 0 to 1 and t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`     | String | Link from where the page is opened: \`referrer: sessionStorage.getItem('urlPrevious') \\ | \| document.referrer \\                                         | \| '';\`             |

# Search Impression

## Template API

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

Refer here for our [sample API](https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Dress%22%2C%22pids_list%22%3A%5B%22RML02384%22%2C%22GER02112%22%2C%22GER02160%22%2C%22WHO03671%22%2C%22KDZ03516%22%2C%22WHO03558%22%2C%22RML02290%22%2C%22GER02158%22%2C%22NAU06605%22%2C%22BEB03937%22%2C%22WHO03672%22%2C%22WHO03670%22%2C%22THA02198%22%2C%22WHO03620%22%2C%22BFA01862%22%2C%22NAU06700%22%2C%22STU04666%22%2C%22STU04612%22%2C%22NCN01301%22%2C%22WHO03659%22%2C%22DKY02759%22%2C%22GER02148%22%2C%22GER02147%22%2C%22ALU10901%22%5D%2C%22url%22%3A%22https%3A//demo.unbxd.com/Search.aspx%3Fk%3DDress%22%2C%22referrer%22%3A%22https%3A//demo.unbxd.com/Search.aspx%3Fk%3Dred%2520dress%22%2C%22requestId%22%3A%220643220e-c900-4825-9f2d-f740025b2b0d%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A1187461382%2C%22visitId%22%3A%22visitId-1662364656433-84380%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=PRODUCT_IMPRESSIONS\&uid=uid-1642414737751-20033\&t=1662366285967%7C0.7498946341398707)

### Payload details

| Attribute Name        | Type   | Value to Pass                                                                                                           |
| :-------------------- | :----- | :---------------------------------------------------------------------------------------------------------------------- |
| `action`              | String | `PRODUCT_IMPRESSIONS`                                                                                                   |
| `pid`                 | String | Unique ID for the product, to be taken from the search API response                                                     |
| `variantId(optional)` | String | Variant ID assigned to the variant of the product. Necessary only if variants are present.                              |
| `url`                 | String | Website URL where the search is performed                                                                               |
| `visit_type`          | String | Either `first_time` or repeat                                                                                           |
| `UnbxdKey`            | String | UnbxdSitekey value                                                                                                      |
| `uid`                 | String | `unbxd.userId` (Needs to be extracted from the cookie)                                                                  |
| `t`                   | String | Timestamp formula: \`t : current\_time \\                                                                               |
| `referrer`            | String | Link from where the page is opened: `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';` |