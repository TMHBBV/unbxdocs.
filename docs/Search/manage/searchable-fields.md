---
title: Searchable Fields
deprecated: false
hidden: false
metadata:
  robots: index
---
This section allows you to control which fields from your product catalog are available for search. It also allows you how much weight each field carries in influencing search relevance. To add searchable fields, set the 'Search Weight' to High, Normal, Low. Fields with 'Search Weight' set as Non-Searchable will not be available for search.

# Navigate to the Searchable Fields Section

1. Navigate to **Manage Search** > **Searchable fields** tab. Refer to the given table to know the headers available here.

| Column Name                      | Description                                                                                                                                             |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Field Name**                   | Displays the name of each field in your product catalog.                                                                                                |
| **Product Coverage**             | Indicates the percentage of products in your catalog that contain values for this field.                                                                |
| **Query Coverage**               | Represents how often this field appears in user queries. If it's "Unable to detect," it means query analytics aren't available or data is insufficient. |
| **Search Weight**                | The importance of the field in the search algorithm. Options: `High`, `Normal`, `Low`, `Non-Searchable`.                                                |
| **AI Recommended Search Weight** | Shows the AI-suggested setting for the field based on catalog and query analysis. You can choose to "Apply" this setting.                               |

3. Under the **Search Weight** column, each field has a dropdown.
4. Click the dropdown and select one of the following:

   * **High**: Field is critical for search and strongly influences ranking.
   * **Normal**: Field is relevant but secondary in importance.
   * **Low**: Field has minor influence on search results.
   * **Non-Searchable**: Field is excluded from search relevance.

> ⚠️ Note
>
> Fields marked as **Non-Searchable** will not be included in the search index.

5. Toggle **Show AI Recommendation** (enabled by default) to view suggestions under the **AI Recommended Search Weight** column.
6. Click **Apply** next to a recommendation to adopt the suggested setting for that field.
7. You can also click **Refresh AI Recommendations** if the catalog has been updated recently.

> 📘 Search and Sort Fields
>
> * **Search by Field Name**: Use the search box at the top to filter fields.
> * **Sort Columns**: Click on the column headers (Field Name, Product Coverage, etc.) to sort ascending or descending.

8. Once all changes are made, click the **Save Changes** button. Your updated searchable field weights will be saved and applied to the search index.

> 👍 Best Practices
>
> * Prioritize fields like **title**, **sku**, and **brand** for `High` search weight.
> * Review AI recommendations periodically to keep search relevance optimized.
> * Keep rarely-used or inconsistent fields set to **Non-Searchable** to improve indexing efficiency.