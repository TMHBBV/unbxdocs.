---
title: Query Rules
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

**Query Rule**, as the name suggests, allows a merchandiser to customize the search results page for a particular query. A query rule is automatically applied when a shopper uses the search query on which the rule is defined.

Once you have created a query rule, you must create a **campaign** associated with the query rule. The query rule defines **when** the rule is triggered, and the campaign defines the **constraints** applied to modifying the search results.

***

## Managing Query Rules

Query rules allow you to manually customize the sequence of product listings for a particular query.

For example, to promote specific products during a certain period, brand, franchise, or category, you can create a **promotional campaign** using merchandising options such as:

* Filtering
* Slotting
* Sorting
* Boosting
* Pinning

> **Note:** You can create a query rule for a primary search keyword and additional keywords. To learn more, refer to the *Create* section.

***

# Create a Query Rule

To create a query rule:

1. Within the console, navigate to:\
   `Merchandising > Commerce Search`
2. Click **Query Rule**
3. Click the **Add** icon. The *New Query Rule* window appears.
4. Enter the primary search query in the **Query** text field.
5. Enter similar queries or synonyms in the **Additional Queries** text field.
6. Click **Create**

You’ve successfully added a query rule.

***

# Create a Campaign (Based on Query Rule)

A campaign can be created in **3 steps**:

1. **Enter Campaign Details**
2. **Merchandise**
3. **Set Experience**

> 💡 **Tip:** You can import an existing query rule from another site to create a new campaign.

### Steps

1. Create a query rule.
2. In the *Enter Campaign Details* window:

   * Provide a **name** (required)
   * Specify **start date** (required)
   * Specify **end date** (optional — if not selected, campaign runs perpetually)
   * Set the **time zone** (required)
   * Select **target device/OS** (Desktop, Tablet, Mobile, Android App, iOS App, Windows App)
   * Add campaign **description** (optional)
3. Click **Next** → *Configure Campaign*
4. Choose one:

   * Click **Start Merchandising**
   * Click **Create Landing Page**
   * Click **Add URL**
5. Configure merchandising options: **Boost**, **Slot**, **Sort**, **Pin**, **Filter**
6. Click **Next** → Select **Banner**

   * Enter **Image URL** and **Landing Page URL** or HTML
7. Click **Publish**

***

# Edit a Query Rule

1. Go to `Merchandising > Commerce Search`
2. Click **Query Rule**
3. Select the desired rule and click the **edit** icon
4. In the *Add Similar Search Query* window:

   * Add new search keywords (comma-separated)
   * To delete, click the **X** on the keyword
5. Click **Update**

***

# Delete a Query Rule

### To delete only keywords:

1. Click the query rule
2. Click the **edit** icon
3. Remove keywords from the query rule window

### To delete the entire query rule:

1. Click the **delete** icon

> ⚠️ **Caution:** Deleting a rule is **permanent** and **cannot be undone**.

***

# Campaigns

Campaigns are used when certain products need more visibility. You can:

* Promote catalog items
* Create landing pages
* Redirect to brand/category pages

Campaigns are tied to **query rules** and can be in one of the following **states**:

| State    | Description                      |
| -------- | -------------------------------- |
| Draft    | Campaign not yet published       |
| Upcoming | Scheduled to start in the future |
| Active   | Currently running                |
| Expired  | End date has passed              |
| Stopped  | Manually halted                  |

> **Note:** Restart a stopped campaign by duplicating it.
>
> **Note:** A query rule with no active campaign will not affect search results.

***

## Edit Campaigns

1. Navigate to: `Merchandising > Commerce Search`
2. Click **Query Rule** tab
3. Select the campaign and click **Edit**
4. Update any of the following:

   * Name
   * Start/End Date
   * Timezone
   * Target Device/OS
   * Description
5. Click **Next** → *Configure Campaign*

   * Modify merchandising options
6. Click **Next** → Edit **Banner**
7. Click **Publish**

***

## Preview Campaigns

1. Navigate to: `Merchandising > Commerce Search`
2. Click **Query Rule** tab
3. Select the campaign
4. Click the **Preview** icon
5. View configuration and close

***

## Duplicate Campaigns

1. Navigate to: `Merchandising > Commerce Search`
2. Click **Query Rule** tab
3. Select the campaign
4. Click the **doner icon** → **Duplicate**
5. Rename and edit as needed
6. Click **Next** to edit or publish

***

## Delete Campaigns

1. Navigate to: `Merchandising > Commerce Search`
2. Click **Query Rule** tab
3. Select the campaign
4. Click the **doner icon** → **Delete**
5. Confirm by clicking **Yes, Delete**

> ⚠️ **Caution:**
>
> Deleted campaigns **cannot be recovered**.