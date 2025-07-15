---
name: Spellchekmerchandising
---
# Q. When does ‘Did you mean’ get fired?

A. ‘Did you mean’ gets fired when ‘Spellcheck’ is triggered.

For e.g. if the search query is ‘ret dress’ with this API call: `http://search.unbxd.io/8c1bc6cc0fa47076d417690a1e5e1120/test-childrensplace-com702771523873394/search?q=ret%20dress`

Then the result set has 456 products. There is a ‘didyoumean’ suggestion ‘set dress’, as there was a spell-check triggered for token ‘ret’ based on the nearest match found from the catalog.

The process is to first check for exact match results. In case no results are found, then spellcheck is triggered and ‘did you mean’ suggestion is given (if found, also note that ‘didyoumean’ suggestion is not automatically fired). Product results are for alternate.mm=0, in this case for dress. This happens mostly in the case of multi-token queries where one or more words may have been incorrectly spelled.