---
name: Redirectquerymerchandising
---
# Q. If we misspell a redirect query, will ‘Did you mean’ work?

A. Redirect will not get triggered for miss-spelled queries (i.e. if the query does not match with the one specified in the rule). Summarizing the behavior in case of fallback

A – Correct query -> Redirect gets triggered. `http://search.unbxd.io/c28b3b5ae91e7b48bf78825e7b63b483/globalindustrial-com702401520254089/search?q=gloves&rows=0&variants=true&analytics=false&facet=false`

Case B – Miss-spelled query -> Redirect is not triggered. DYM received. `http://search.unbxd.io/c28b3b5ae91e7b48bf78825e7b63b483/globalindustrial-com702401520254089/search?q=glovas&rows=0&variants=true&analytics=false&facet=false`

Case C – Miss-spelled query -> Fallback is set as true here so it automatically falls back to DYM which invokes the redirect. `http://search.unbxd.io/c28b3b5ae91e7b48bf78825e7b63b483/globalindustrial-com702401520254089/search?q=glovas&rows=0&variants=true&analytics=false&facet=false&fallback=true`