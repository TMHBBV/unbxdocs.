---
title: Boost or Bury specific products
deprecated: false
hidden: true
metadata:
  robots: index
---
Boost is a merchandising strategy that lets you control the visibility of products in search results based on specific conditions:

* Boost (Boost Value = 1 to 100): Highlight products by increasing their ranking on the search results page when certain conditions are met.
* Bury (Boost Value = -1 to -100): Lower product visibility by lowering their ranking on the search results page when the set conditions are met.

> 📘 Note
>
> Using Boost disables Sort.

## How to set up use the Boost option?

1. Click the Boost button in the Set merchandising strategy section.
2. Select Attribute: Choose the [Attribute](/user-guides/merchandising/introduction#attributes) you want to base the condition on from the drop-down menu.
3. Choose Operator: Define the [Operator](/user-guides/merchandising/introduction#values) by clicking the *=\`* button and selecting the desired one (e.g., equals, contains).
4. Set Value: Select the attribute [Value](/user-guides/merchandising/introduction#operators) that the condition will match or exclude.

## Adding multiple conditions within a Boost group:

1. After adding your first rule to the Boost group, use + Add another attribute to include additional rules within the same Boost group.
2. All conditions within the group must be met for the Boost Value of the Boost group to apply. If even one condition fails, the Boost Value will not be applied.

> 📘 Note
>
> Each Boost group will have its own Boost Value.

## Configuring the Boost Value:

After configuring all rules, set the Boost Value:

* A positive (Boost Value = 1 to 100) Boost Value moves qualifying products higher in search results.
* A negative (Boost Value = -1 to -100) Boost Value moves qualifying products lower in search results.

> 📘 Note
>
> Boost Value cannot be set to 0.

## Adding new Boost groups

1. Use *+ Add new Boost Group* to create additional Boost groups.
2. The assigned Boost Value will be applied if all the conditions in any Boost groups are met.

> 📘 Note
>
> Groups are connected with an OR condition. This means if the products meet all the conditions of at least one group, they will be included.

## Deleting existing Boost conditions

If you accessed this page from the listing page, click the Edit icon next to Boost in the Strategy Summary section.

1. To delete an entire Boost group, click the Delete icon next to the desired group and confirm your action.
2. To remove a specific Boost condition within a group, click the Delete icon next to the condition and confirm your action.

Once you have configured the rule, click Apply boost.

* You can also view your merchandising strategy summary by clicking the View summary button.

> 📘 Note
>
> Viewing the summary before applying the changes will lead to the configurations being lost. It is *recommended* that you click Apply boost before viewing the summary.

## Publish the rule to your live site

After applying the rule, you can do one of the following:

1. Click the Save button to retain the Campaign as a draft.
2. Continue adding more rules.
3. Click the Publish rule button to push it live.