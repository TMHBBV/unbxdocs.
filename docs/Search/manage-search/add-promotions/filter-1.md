---
title: 'Promotions: Filter'
excerpt: Apply rules to quickly Filter products
deprecated: false
hidden: false
metadata:
  robots: index
---
Filtering products allows you to include or exclude specific products from the search results based on defined conditions. Unlike other merchandising strategies like Boost, Sort, Slot, or Pin, Filter strictly removes products that don’t meet the specified criteria.

***

## Setting up Filter:

1. Click the **Filter** button in the *Set merchandising strategy* section.

2. **Select Attribute**: Choose the [Attribute](/user-guides/merchandising/introduction#attributes) you want to base the condition on from the drop-down menu.\
   *(If an attribute is missing from the dropdown, you need to navigate to the Field Configuration page and add it to the configuration table.)*

3. **Choose Operator**: Define the [Operator](/user-guides/merchandising/introduction#values) by clicking the *=\`* button and selecting the desired one (e.g., equals, contains).

4. **Set Value**: Select the attribute [Value](/user-guides/merchandising/introduction#operators) that the condition will match or exclude.

***

## Adding multiple conditions within a Filter Group:

1. After adding the first condition to a Filter group, click **+ Add Another Attribute** to include more.
2. All conditions within the group must be satisfied for a product to be filtered. Products not meeting all conditions will not be visible.

***

## Adding new Filter groups

1. Use **+ Add new Filter group** to create additional Filter groups.
2. Products that meet conditions of *any* group will be shortlisted.

> **Note:**\
> Groups are connected with an **OR** condition. This means if the products meet all the conditions of at least one group, they will be included.

***

## Deleting existing Filter conditions

If you accessed this page from the listing page, click the **Edit** icon next to Filter in the Strategy Summary section.

1. To delete an entire Filter group, click the **Delete** icon next to the desired group and confirm your action.
2. To remove a specific Filter condition within a group, click the **Delete** icon next to the condition and confirm.

***

## Final steps

1. Once you have configured the rule, click **Apply filter**.
2. You can also view your merchandising strategy summary by clicking the **View summary** button.

> **Note:**\
> Viewing the summary before applying the changes will lead to the configurations being lost. It is **recommended** to click **Apply filter** before viewing the summary.

***

## Publish the rule to your live site

After applying the rule, you can do one of the following:

1. Click the **Save** button to retain the Campaign as a draft.
2. Continue adding more rules.
3. Click the **Publish rule** button to push it live.

<Cards columns={4}>
  <Card title="Filter" href="https://readme.com" icon="fa-home" target="_blank">
    Neque porro quisquam est qui dolorem ipsum quia
  </Card>

  <Card title="Second Card" icon="fa-user">
    *Lorem ipsum dolor sit amet, consectetur adipiscing elit*
  </Card>

  <Card title="Third Card" icon="fa-star">
    > Ut enim ad minim veniam, quis nostrud ullamco
  </Card>

  <Card title="Fourth Card" icon="fa-question">
    **Excepteur sint occaecat cupidatat non proident**
  </Card>
</Cards>