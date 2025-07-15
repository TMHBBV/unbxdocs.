---
name: Relativepathmerchandising
---
# Q. Can we use a relative path to define the redirect URL or should we always use an absolute path?

A. The redirect feature in Unbxd search API supports both the relative and absolute paths. However, if a relative URL is specified in a redirect rule, then the customers must take care of adding the prefix for the URL before requesting the page pointed by the URL.

Customers can also create some redirect rules with relative URLs and some redirect rules with absolute path, as long as they have logic in place to handle the response of both types.

If it’s Ajax implementation by Unbxd, then we handle the redirects in our JS code after verifying the logic with the customer.