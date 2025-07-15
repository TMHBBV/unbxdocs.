---
name: AcceptJSONcatalog
---
# Q. We accept JSON, XML, and CSV but is JSON the only format that can be uploaded by the customer through feed API?

A. Yes. We only support JSON via feed API. Also, XML and CSV via SFTP won’t be self serve. Unbxd will anyway need to transform these files to JSON, and then call our feed API internally. Eventually, everything needs to pass via the feed API.