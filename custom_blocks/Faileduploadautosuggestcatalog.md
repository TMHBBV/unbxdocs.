---
name: Faileduploadautosuggestcatalog
---
# Q. Can schema upload fail because ‘Autosuggest’ parameter wasn’t specified in the schema file?

A. Yes. The Autosuggest parameter is marked as ‘Required’. It is mandatory to specify the Autosuggest parameter in the schema file for all the fields. These are the mandatory and optional parameters:

* fieldname (required)
* datatype (required)
* multiValue (required)
* Autosuggest (required)
* isVariant (Optional)
* id (Optional)