---
title: UI Terminologies
excerpt: Netcore Unbxd UI terminologies on the console page
deprecated: false
hidden: false
metadata:
  robots: index
---
In an ecommerce catalog, attributes are the characteristics or properties that describe a product. These attributes can be textual or numerical and help effectively organize, filter, and display products.

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        **Parameter**
      </th>

      <th style={{ textAlign: "left" }}>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        **Attributes**
      </td>

      <td style={{ textAlign: "left" }}>
        Characteristics or properties that describe a product (e.g., Color, Price, Brand).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **Values**
      </td>

      <td style={{ textAlign: "left" }}>
        Specific data points associated with an attribute (e.g., Color = Red, Price = 100, Brand = Nike).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **Operators**
      </td>

      <td style={{ textAlign: "left" }}>
        Conditions used to create rules by comparing attributes and their values. This is applicable for [Boost]() and [Filter]().

        * **Equals (=)**:The attribute value must exactly match the specified value. Example: Brand = Nike.
        * **Not Equals (≠)**:The attribute value must not exactly match the specified value. Example: Color ≠ Red.
        * **Contains (⊂)**:The attribute value must include the specified keyword or text. Example: Brand ⊂ "Nike".
        * **Does Not Contain (⊄)**: The attribute value must not contain the specified keyword or text. Example: Color ⊄ "Red".
        * **Greater than or Equal to (>=)**: The attribute value must be greater than or equal to the specified value. Example: "Price >= 100".
        * **Less than or Equal to (\<=)** : The attribute value must be less than or equal to the specified value. Example: "Rating \<= 4".
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **AND**
      </td>

      <td style={{ textAlign: "left" }}>
        All conditions must be true for the rule to apply. Example: Brand = Nike AND Color = Red.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **OR**
      </td>

      <td style={{ textAlign: "left" }}>
        At least one condition must be true for the rule to apply. Example: Brand = Nike OR Brand = Adidas.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **THEN**
      </td>

      <td style={{ textAlign: "left" }}>
        Defines the sequence of rules. The second rule will apply if the first condition is met. Example: Sort by Price Ascending THEN Sort by Rating Descending.
      </td>
    </tr>
  </tbody>
</Table>