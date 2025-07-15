---
name: Deprecatenewschemacatalog
---
# Q. Can we delete a deprecated field from the Schema file?

A. No, currently there is no mechanism to delete a field from the schema. However, presence of deprecated fields in the schema doesn’t affect the search results anyway.

Deletion of a field from the schema can lead to corruption of the search & category index resulting in downtimes. Unbxd team can delete the deprecated fields from the schema from the backend if it’s extremely necessary. However, these requests can take some time.