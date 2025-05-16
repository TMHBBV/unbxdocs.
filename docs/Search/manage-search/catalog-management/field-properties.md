---
title: Field Properties
excerpt: >-
  A field configuration is a set of rules that determines which fields are
  available for a catalog.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The Field Configuration feature has been introduced to streamline the management of fields within your catalog. Over time, businesses can accumulate many irrelevant and unused fields that affect the efficiency of search and browse operations, particularly when creating promotions, facets, and banners. These excessive fields increase API costs, consume unnecessary resources, and degrade system performance.

Imagine you are a merchandiser managing an online catalog. You have many fields that are not used for promotions, banners, or facets, but they are still part of the catalog's backend. As a result, you face higher costs due to the unnecessary API calls, and your system is slowed down due to indexing irrelevant fields. With Field Configuration, you can easily manage and streamline which fields are used for specific operations, optimizing your workflow and saving on API costs.

To view the field properties for your products by navigate to **Manage** > **Configure Site** > **Field Properties**.

## Properties of Field Configuration

The Field Configuration feature offers several key properties that allow you to configure your catalog fields with features. Refer below to understand the available fields on the panel.

**Field Names**: This specifies the name of field used in the system. For example, color, brand, price and so on

**Multi-Valued**: It specifies if the field can contain multiple values. It can either be True or False.

**Features**: Merchandisers can assign specific tags to available fields which are of following types

| **Feature Type** | **Description**                                                                                                                                   |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Merchandisable   | This field will only be available in the promotion section in Filter.                                                                             |
| Facetable        | This field will only appear in the Facets and Banners section.                                                                                    |
| Autosuggest      | Only fields marked as Autosuggest will appear in keyword suggestions, in-field suggestions, and search fields under the popular products section. |
| Searchable       | Only fields marked as searchable in the catalog will be used for indexing.                                                                        |
| FieldRule        | Fields marked as FieldRule will be available to create field-based rules in Facets and Banners.                                                   |

## Enable Field properties

Below are the other functionalities on the Segment dashboard.

1. Search
2. Refresh
3. Filter
4. Sync
5. Ability to bulk export/import field configuration
6. Action

### Search a Field property

You can utilise the **Search** option to find relevant information of a specific field configuration using keywords quickly to edit and manage it.

<Image align="center" border={true} caption="Search Field Property" src="https://files.readme.io/c9a8c5ddbbd94b0811e6496c58ca64fbc4d3e3613a5a7b16de23f0333c36179f-Fieldsegment.gif" width="80% " />

### Refresh the feed

If you dont see a field that is newly added to the feed, you can choose to refresh the page. This operation takes 20 seconds approximately.

### Filter Fields

Use the Filter option to narrow your search for specific field names. This makes it easier to find fields when managing large catalogs.\
Following capabilities are available in Filter:

<Table>
  <thead>
    <tr>
      <th>
        **Option**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Select features
      </td>

      <td>
        Filter your available field names based on the Feature type.
      </td>
    </tr>

    <tr>
      <td>
        Field type is multi-valued
      </td>

      <td>
        Filter based on whether a field can store multiple values.

        * All: Show all fields regardless of type.
        * True: Show only multi-valued fields.
        * False: Show only single-valued fields.
      </td>
    </tr>

    <tr>
      <td>
        Field type is dimension mapped
      </td>

      <td>
        Filters based on whether a field is mapped to a product dimension. Refer to Dimension Mapping for details.

        * All: Show all fields.
        * True: Show only fields mapped to dimensions.
        * False: Show only fields not mapped to dimensions.
      </td>
    </tr>

    <tr>
      <td>
        Actions
      </td>

      <td>
        * Reset Filters: Clears all selected filters.
        * Apply Filters: Applies the currently selected filters to the field list.
      </td>
    </tr>
  </tbody>
</Table>

<Image align="center" src="https://files.readme.io/7bf63b1f089a97f2bfa38edf050821a3a5ce92c474e013f5170405eda8ce2057-Filterfieldpro.gif" />

### Sync the field properties

Once you’ve enabled or disabled features, click the Sync button. This ensures that changes are reflected and indexed correctly. Without syncing, the feed won’t be indexed, which may lead to delays in applying the feature changes.

### Ability to bulk export/import Field Configurations

The Bulk Export/Import Field Configurations feature allows users to manage and migrate field configuration settings efficiently across different environments. Bulk export/import enables you to streamline field management tasks. This feature saves time and effort by enabling easy migration of field settings while ensuring consistency and accuracy.

With **Bulk Export/Import**, users can:

* Export field configurations from the platform into a structured format (such as CSV or Excel), allowing for offline review or backup.
* Import field configurations back into the system, making it easier to apply pre-defined configurations across multiple fields without having to manually edit them one by one.

## Action Button

Follow these steps to configure your fields and enable necessary features:

1. Select Fields to Modify: Select one or more fields that need to be enabled for specific features.
2. Bulk Enable Features: Click on the Action button and from the dropdown, click on "**Bulk Enable Features**". A pop-up will appear where you can select the feature (e.g., "Merchandisable", "Facetable", or "Autosuggest"). Click Bulk Enable to activate the features for the selected fields.
3. Bulk Disable Features: If you need to disable a feature for a field, follow the same steps and select Bulk Disable Features from the dropdown menu.

# Troubleshoot & FAQs

<Accordion title="My Feed Attribute is Missing in the Drop-down">
  If you encounter a situation where an attribute is missing from a dropdown (e.g., when configuring rules, facets, or promotions), follow these steps to resolve the issue:
  Refresh Fields:
  Navigate to Manage > Catalog > Field Properties and click on the refresh icon to reload the field properties. Wait for 10 seconds.

  Check for Missing Attribute:
  Search for the attribute in the table. If it's not listed, it means the attribute is not present in the current feed.

  Update the Feed:
  If the attribute is missing, initiate a new feed containing the required attribute. Wait for the indexing cycle to complete.

  Sync the Feed:
  After the feed is indexed, click on the refresh icon again to ensure the attribute is updated.

  Tag the Attribute:
  Once the attribute is available, tag it with the appropriate property for the dropdown context.

  Check the Dropdown:
  Go back to the dropdown, and the missing attribute should now be available.
</Accordion>

<Accordion title=" Importing Fields with Errors">
  If you receive an error during import:
  Check for Format Issues: Ensure the file format is correct (CSV or Excel) and the required columns (e.g., Field Name, Feature Tag, Enabled) are included.

  Feature Tag Mismatch: Verify that the feature tags in the import file match the predefined tags in the system (e.g., Merchandisable, Facetable, Autosuggest).

  Missing Fields: If a field mentioned in the import file does not exist in the catalog, ensure that the field is created first before importing the configuration.
</Accordion>