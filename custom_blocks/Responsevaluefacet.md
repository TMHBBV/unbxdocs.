---
name: Responsevaluefacet
---
# Q. I created facets for my site but still can’t see any response value in the API call. Why?

A. The facets creation is a two step process.

1. First step is adding facet to the global facet pool – It can be done in the console by browsing to **Manage** > **Configure site** > **Configure Facet**
2. Second step is enabling the facets from site-rule – This can be done in the console by going to \*\*Merchandising \*\*> \*\*Commerce search \*\*> **Site Rule**. In site rule, click on View Site Rule, then click  Next to reach the facets screen. Enable the facet that you want to display on the site and click on Save. Publish  the site rule to store the changes.

Once the site-rule is published it starts reflecting immediately. However, it may take 10-15 mins to reflect the changes in site-rule due to caching.

> 📘 Note
>
> Facets enabled in site-rule are returned for all request. You can also enable facets based on criteria using field-rules.