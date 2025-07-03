---
title: UI Terminologies
excerpt: Netcore Unbxd UI terminologies on the console page
deprecated: false
hidden: false
metadata:
  robots: index
---
In an ecommerce catalog, attributes are the characteristics or properties that describe a product. These attributes can be textual or numerical and help effectively organize, filter, and display products.

| **Parameter**            | **Description**                                                                                                                                                                          |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Attributes**           | Characteristics or properties that describe a product (e.g., Color, Price, Brand).                                                                                                       |
| **Values**               | Specific data points associated with an attribute (e.g., Color = Red, Price = 100, Brand = Nike).                                                                                        |
| **Operators**            | Conditions used to create rules by comparing attributes and their values.\<ul>\<li>\*\*Equals (=)\*\*: The attribute value must exactly match the specified value. Example: Brand = Nike |
| **Equals (=)**           | The attribute value must exactly match the specified value. Example: Brand = Nike.                                                                                                       |
| **Not Equals (≠)**       | The attribute value must not exactly match the specified value. Example: Color ≠ Red.                                                                                                    |
| **Contains (⊂)**         | The attribute value must include the specified keyword or text. Example: Brand ⊂ "Nike".                                                                                                 |
| **Does Not Contain (⊄)** | The attribute value must not contain the specified keyword or text. Example: Color ⊄ "Red".                                                                                              |
| **AND**                  | All conditions must be true for the rule to apply. Example: Brand = Nike AND Color = Red.                                                                                                |
| **OR**                   | At least one condition must be true for the rule to apply. Example: Brand = Nike OR Brand = Adidas.                                                                                      |
| **THEN**                 | Defines the sequence of rules. The second rule will apply if the first condition is met. Example: Sort by Price Ascending THEN Sort by Rating Descending.                                |