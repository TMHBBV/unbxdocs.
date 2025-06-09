---
title: Recommendation Algorithms/ Recipes
deprecated: false
hidden: false
metadata:
  robots: index
---
# Core Algorithms

Core algorithms are a set of Netcore Unbxd defined rules created to generate product recommendations based on business logic, like:

| **Recommendation Name**  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Note                                                                                                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Recommended For You**  | The ‘Recommended For You’ widget analyzes a shopper’s browse or product view history to create tailor-made product recommendations for your shopper. Although this widget can be inserted anywhere across your site, this widget is most effective when displayed on the Homepage or when the search page returns with no results.                                                                                                                                                                                                                                                                                                                                                                                                                                                        | If the shopper is a first-time visitor, you will not see recommendations from this widget.                                                                                                   |
| **Top Sellers**          | The ‘Top Seller’ widget showcases products that are frequently sold in your eCommerce site. Psychologically, this influences a customer’s purchase decision. The algorithm analyzes your site’s overall sales information for a month/fortnight/week/day at a site or category level for recommending top-selling products to your customers. The Top Seller widget display location-based recommendations to visitors. These widgets can be personalized based on visitor location and visitor behavior.                                                                                                                                                                                                                                                                                 | This widget is most effective when placed within the PDP or within the Home page.                                                                                                            |
| **Category Top Sellers** | The ‘Category Top Sellers’ widget displays products frequently sold within the same category of the products that your shopper searches for.\<br>\<br>The algorithm analyzes the sales information for products at the category-level for a month / fortnight / week / day for recommending top-selling products at the category to your shoppers.                                                                                                                                                                                                                                                                                                                                                                                                                                        | This widget is most effective when placed within the PDP, product category page or within the Cart page.                                                                                     |
| **Brand Top Sellers**    | The ‘Brand Top Sellers’ widget displays top selling products of the same brand the shopper searches for. The algorithm analyzes the same information for sales information for products at the brand-level for a month / fortnight / week / day for recommending top-selling products of the same brand to your shoppers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | This widget is most effective when placed within the PDP or the Brand page.                                                                                                                  |
| **Bought Also Bought**   | The ‘Bought Also Bought’ widget displays products that have been frequently bought along with the anchor product. For instance, if a shopper is on the product display page of a running shoe that is frequently bought along with a pair of socks, then this widget will recommend the pair of socks as well. This widget generates products based on a collaborative filtering algorithm for successful orders.\<br>\<br>The products that were ordered the most will be shown first. Once the widget goes live, the recommendations are automatically generated based on batch jobs that run on a daily basis. This widget can help you cross-sell to increase the average cart value. This widget is most effective when placed within the PDP or within the Order Confirmation page. | Useful when shoppers may want to buy a product that complements or adds value to the product they just bought.                                                                               |
| **Viewed Also Viewed**   | Very similar to the logic behind ‘Bought Also Bought’, the ‘Viewed Also Viewed’ widget displays products that have been frequently viewed along with the anchor product. For instance, if a shopper is on the product display page of a running shoe that is frequently viewed along with a pair of socks, then this widget will recommend the pair of socks as well.\<br>\<br>This widget is most effective when placed within the PDP.                                                                                                                                                                                                                                                                                                                                                  | Useful when shoppers are looking for an alternative that is similar to the product they are searching for.                                                                                   |
| **More Like This**       | The ‘More Like This’ widget displays a list of products that are similar to the product in the Product Display Page (PDP).\<br>\<br>This widget is based on ‘text matching’ and ‘category matching’ logic.\<br>\<br>Text matching is where products are recommended when their title text matches the title text of the product being viewed in the PDP. Category matching is when the category of the product being recommended matches the category of the product being viewed in the PDP. This widget lists products where the title text and category match the product in the PDP. This widget is most effective when placed within the PDP.                                                                                                                                        | Useful when shoppers are looking for similar products either from the same category or similar characteristics and is an excellent opportunity to upsell similar products from your catalog. |
| **Recently Viewed**      | The ‘Recently Viewed’ widget analyzes a user’s session data and user cookie to arrive at a list of products that the visitor has viewed in recent sessions. Products are sorted based on the time of the shopper’s visit. This widget is most effective when displayed within the Home Page, Results page when there are 0 results or both. If the shopper is a first-time visitor, then the shopper sees the Top Sellers widget for that session.                                                                                                                                                                                                                                                                                                                                        | This widget will not showcase products you’ve added to cart or purchased.                                                                                                                    |
| **Complete The Look**    | The ‘Complete The Look’ widget uses product images to create visually appealing and on-brand outfits that is personalized for a specific product. This widget provides style inspiration for shoppers and exposes shoppers to products that complement what they wish to buy. This widget is most effective when placed within the Product Display Page (PDP).                                                                                                                                                                                                                                                                                                                                                                                                                            | Useful when you want to personalize a recommendation that can enhance the customer experience.                                                                                               |

## Set up Recs

To set up a Complete the Look rule:

1. Click Manage > Algorithms.
2. On the Manage Algorithms page, click Core.
3. In the Algorithms table, click Configure for Complete the Look. The Configure Complete the Look page appears.\
   Click Create a Look.
4. In the Create a Look page, type in the product name (Product ID or PID) in the Enter Product Name or SKU text field. The PID is the unique ID of the anchor product.

In the Complete the look here section, type in the PID of the link products in Enter Product Name or SKU text field.\
To add products to Look, click the add icon. To remove, click the minus icon.

5. Click Save the Look. The newly created Look will appear in the Complete the Look table.\
   You’ve successfully created a new Complete the Look rule. To view the anchor and link products, click the drop-down arrow for the corresponding Look.

> 📘 Note
>
> Feature fields are a list of predefined Unbxd attributes and can differ, by business. To map dimensions within your catalog to Unbxd fields, click Show Fields.

## Import a Rule

You can also import an existing Complete the Look rule. To import:

1. Click Manage > Algorithms.
2. On the Manage Algorithms page, click Core.
3. In the Algorithms table, click Configure for Complete the Look. The Configure Complete the Look page appears.
4. Click Upload Config.
5. To add a comma-separated (CSV) config file, drag and drop the file or click Fetch from the device. Click Done.

The Look will appear in the Complete the Look table. You’ve successfully imported a Look.

## Edit

You can edit an existing Complete the Look rule, from the Manage Algorithms page. To edit an existing Complete the Look rule:

1. Click Manage > Algorithms.
2. On the Manage Algorithms page, click Core.
3. In the Algorithms table, click Configure for Complete the Look. The Configure Complete the Look page appears.
4. To edit, click the drop-down arrow of the required rule and click Edit.
5. To edit the PID of the anchor product, change the PID in the Enter Product ID or SKU.
6. To edit the PID of the link products, change the PID in the Enter Product ID or SKU within the Complete the Look section.
7. To add products to the Look, click the add icon. To remove, click the minus icon.
8. Click Save the Look.

You have successfully edited the rule.

## Delete

You can delete an existing Complete the Look rule, from the Manage Algorithms page. To delete an existing Complete the Look rule:

1. Click Manage > Algorithms.
2. On the Manage Algorithms page, click Core.
3. In the Algorithms table, click Configure for Complete the Look. The Configure Complete the Look page appears.
4. To delete the look, click the drop-down arrow of the required look and click Delete.
5. Click OK. You will be redirected to the Configure Complete the Look page.

You have successfully deleted the rule.

## Cross-Sell

The ‘Cross-Sell’ widget focuses on introducing products that may complement another product your shopper is viewing on the site or have already added it to their shopping cart.

This widget is based on recommending categories of products that are related to products that have been added to the cart or have been purchased. As a merchandiser, you’ll need to set Cross-Sell rules.

This widget is most effective when placed within the Product Display Page, the Order Confirmation page, or both. Useful when you want to ‘bundle’ products together.

| **Status**   | **Description**                                                   |
| ------------ | ----------------------------------------------------------------- |
| **Running**  | Indicates the catalog is running and has been submitted to Unbxd. |
| **Indexing** | Indicates the catalog is being indexed.                           |
| **Complete** | Indicates the catalog has successfully uploaded.                  |
| **Error**    | Indicates the catalog synchronization failed.                     |

NOTE: By default, Magento doesn’t synchronize the catalog automatically.

### To set up a Cross-Sell rule:

1. Click Manage > Algorithms.
2. On the Manage Algorithms page, click Core.
3. In the Algorithms table, click Configure for Cross-Sell. The Cross-Sell page appears.
4. Click Create a Cross-Sell.
5. In the Configure Cross-Sell page, in the Choose parent category section, click the drop-down boxes to choose the required product categories. You can choose up to 4 levels of categories.
6. In the Complete the Look here section, click the Choose child category drop down boxes to choose the categories you want to cross-sell.
7. To add products to the Look, click the add icon. To remove, click the minus icon.\
   Click Save Rule.

You’ve successfully configured Cross-Sell. To view the Associated Categories, click the drop-down arrow for the corresponding Cross-Sell rule.

## Import an existing Cross-Sell rule.

1. Click Manage > Algorithms.
2. On the Manage Algorithms page, click Core.
3. In the Algorithms table, click Configure for Cross-Sell. The Configure Cross-Sell page appears.\
   Click Upload Config.
4. To add a comma-separated (CSV) config file, drag and drop the file or click Fetch from the device.
5. Click Done. The Look will appear in the Cross-Sell table.
6. You’ve successfully imported a Cross-Sell rule.

## Edit

You can edit an existing Cross-Sell rule, from the Manage Algorithms page. To edit an existing Cross-Sell rule:

1. Click Manage > Algorithms.
2. On the Manage Algorithms page, click Core.
3. In the Algorithms table, click Configure for Cross-Sell. The Configure Cross-Sell page appears.
4. To edit, click the drop-down arrow of the required rule and click Edit.
5. To edit the anchor category, click the drop-down box, and choose the required product category.
6. To edit the link category, click the drop-down box, and choose the required product category. Click the Save Rule button.

You have successfully edited the rule.

## Delete

You can delete an existing Cross-Sell rule, from the Manage Algorithms page. To delete an existing Cross-Sell rule:

1. Click Manage > Algorithms.
2. On the Manage Algorithms page, click Core.
3. In the Algorithms table, click Configure for Cross-Sell. The Configure Cross-Sell page appears.
4. To delete the rule, click the drop-down arrow of the required rule and click Delete.
5. Click OK. You will be redirected to the Configure Cross-Sell page.

You have successfully deleted the rule.