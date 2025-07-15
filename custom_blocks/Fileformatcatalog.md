---
name: Fileformatcatalog
---
# Q. What are the file formats you can upload your catalog in?

A. Unbxd supports catalog in CSV, JSON, and XML formats.

The schema should be uploaded separately in **JSON format** before uploading the catalog in CSV or XML format. The uploads in CSV and XML via SFTP are converted to JSON format by Unbxd and then uploaded via the feed API.