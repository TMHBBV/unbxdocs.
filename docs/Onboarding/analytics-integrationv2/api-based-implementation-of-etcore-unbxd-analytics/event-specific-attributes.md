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

| Attribute Name | Type   | Value to Pass                                                                                                                    |
| :------------- | :----- | :------------------------------------------------------------------------------------------------------------------------------- |
| `action`       | String | `visitor`                                                                                                                        |
| `url`          | String | Website URL where the search is performed                                                                                        |
| `visit_type`   | String | Either `first_time` or `repeat`                                                                                                  |
| `UnbxdKey`     | String | UnbxdSitekey value                                                                                                               |
| `uid`          | String | `unbxd.userId` (Needs to be extracted from the cookie)                                                                           |
| `t`            | String | Timestamp formula: `t : current\_time \\| random number between 0 to 1 and t = new Date().getTime() + ‘\\|’ + Math.random();`    |
| `referrer`     | String | Link from where the page is opened referrer: `referrer: sessionStorage.getItem('urlPrevious') \\|\| document.referrer \\|\| '';` |

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

| Attribute Name | Type   | Value to Pass                                                                           |
| :------------- | :----- | :-------------------------------------------------------------------------------------- |
| `action`       | String | `visitor`                                                                               |
| `url`          | String | Website URL where the search is performed                                               |
| `visit_type`   | String | Either `first_time` or `repeat`                                                         |
| `UnbxdKey`     | String | UnbxdSitekey value                                                                      |
| `uid`          | String | `unbxd.userId` (Needs to be extracted from the cookie)                                  |
| `t`            | String | Timestamp formula: \`t : current\_time \\                                               |
| `referrer`     | String | Link from where the page is opened referrer: \`sessionStorage.getItem('urlPrevious') \\ |