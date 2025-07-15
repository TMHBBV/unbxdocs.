---
name: Newschemmacatalog
---
# Q. What happens when a new schema file is sent with some new fields?

A. Schema file uploads are handled on the Unbxd end in the following manner :

* If the new schema file has fields that already existed in the schema, but values corresponding to them are modified, then the schema is updated with the modified values of the field
* If the new schema file has new fields, then the new fields are added to the previously existing schema