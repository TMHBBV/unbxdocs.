---
title: Unbxd Browse UI Dashboard
deprecated: false
hidden: false
metadata:
  robots: index
---
# User Management

### **Profile**

#### Profile Settings: General Information

Manage your personal and organizational details. Keep your account information up-to-date to ensure smooth communication and accurate configuration.

* **Name**: Your full name as registered.
* **Email**: Primary email ID associated with your account.
* **Organization**: Your company or business name.
* **Website**: Website associated with your organization.
* **Time zone**: Time zone used for scheduling and analytics accuracy.

#### Change Password

Update your account security credentials.

* **Enter current password**: Your existing password.
* **New Password**: Enter a strong, secure new password.
* **Confirm New Password**: Re-enter to confirm the new password.

***

### **Team Management**

Control and configure user access, roles, and permissions for your organization.

#### Members

A centralized list of all users in your team.

* **Role**: Assign predefined roles such as Admin, Merchandiser, Analyst, or Developer.
* **Created at**: Date when the user was added.
* **Last Login at**: Timestamp of the user’s most recent login.
* **Status**: User registration state—Registered or Pending.

***

### **Add User**

#### Add New User

Quickly onboard a new team member.

* **Email ID**: Email of the new user (e.g., [name@unbxd.com](mailto:name@unbxd.com)).
* **Site**: Assign the user to a specific site.
* **Role**: Define the user’s access level.

***

## My Sites

Track and manage site allocations within your account.

* **Number of Sites Allotted**: Total number of sites available under your plan.
* **Number of Sites Added**: Sites currently added to your account.
* **Remaining**: Sites still available to add.
* **Min Campaign Duration**: Minimum duration required for a campaign on any site.
* **Add More Sites**: Increase your site capacity based on need.

***

### **Account Sites Table**

View and manage detailed information about added sites.

* **SiteKey**: Unique key identifier for each site.
* **Environment**: Specifies whether the site is in QA, Dev, Prod, or Staging.
* **Added On**: Date the site was added to your account.
* **Campaign Min-Duration**: The least duration required for a campaign to run.
* **Actions**: Options to edit or delete sites.

***

### **Add a Site**

Onboard a new site with key configurations.

* **Name your site**: Provide a recognizable name.
* **Environment**: Choose between QA, Dev, Prod, or Staging.
* **Business Vertical**: Select your domain (e.g., healthcare, electronics).
* **Language**: Define the language your store operates in.
* **Data Center**: Choose the closest data center (UK, US, SG, AU) for optimal performance.

***

## SSO (Single Sign-On)

Enable and manage Single Sign-On for secure, streamlined access to the dashboard using centralized credentials.

***

## Browse

### **Facets**

Customize and control product filtering options on your storefront.

#### Configure Global Facets

Enable facets to display on your website for users to refine product results.

* **Enabled/Disabled**: Determines visibility of the facet on the storefront.

#### Add New Facet

Create a new filtering option.

* **Select attribute**: Choose a catalog field to base the facet on.
* **Display Name**: Set how the facet should appear to users.
* **Sort Order**: Define how values in the facet should be sorted: by Product Count, Alphabetical (A-Z), Custom Sort, or Personalized.
* **Facet Length**: Set the maximum number of values shown under the facet.
* **Enable facet on your website**: Toggle visibility for the facet.
* **Ranking**: Determines display priority of the facet in the UI.

#### Field Name and Type

* **Field Name**: The attribute from your catalog that drives the facet.
* **Facet Type**: Defined by the attribute’s data type:

  * **Text** for textual fields.
  * **Range** for numeric fields.
  * **Path** for multi-level navigation.

#### Status

Facets marked as "Enabled" will be included in the API response and visible on-site.

***

### **Dimension Mapping**

Link UNBXD dimensions to your feed attributes to improve relevance scoring and search quality.

***

## Catalog

### **Configure Field Properties**

Manage the behavior and visibility of catalog fields across different modules.

#### Field Attributes

* **Multi-valued**: Supports multiple values per field.
* **Merchandisable**: Enables the field for use in merchandising promotions.
* **Facetable**: Allows the field to be used for filtering (facets, banners).
* **Searchable**: Field is used in product indexing and search results.
* **Autosuggest**: Field will power suggestions in search UI (keywords, in-field).
* **FieldRule**: Enables field for rule-based merchandising like facet or banner rules.

#### Actions

* **Bulk enable features**: Turn on properties for multiple fields in one action.
* **Bulk disable features**: Turn off properties in bulk for simplification.