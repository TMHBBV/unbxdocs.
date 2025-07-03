---
title: UI Terminologies
excerpt: Netcore Unbxd UI terminologies on the console page
deprecated: false
hidden: false
metadata:
  robots: index
---
In an ecommerce catalog, attributes are the characteristics or properties that describe a product. These attributes can be textual or numerical and help effectively organize, filter, and display products.

<Table>
  <thead>
    <tr>
      <th>
        **Parameter**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Attributes**
      </td>

      <td>
        Characteristics or properties that describe a product (e.g., Color, Price, Brand).
      </td>
    </tr>

    <tr>
      <td>
        **Values**
      </td>

      <td>
        Specific data points associated with an attribute (e.g., Color = Red, Price = 100, Brand = Nike).
      </td>
    </tr>

    <tr>
      <td>
        **Operators**
      </td>

      <td>
        Conditions used to create rules by comparing attributes and their values.

        <ul><li>**Equals (=)**:The attribute value must exactly match the specified value. Example: Brand = Nike
        </li><li>**Not Equals (≠)**:The attribute value must not exactly match the specified value. Example: Color ≠ Red.
        </li><li>**Contains (⊂)**:The attribute value must include the specified keyword or text. Example: Brand ⊂ "Nike".
        </li><li>**Does Not Contain (⊄)**: The attribute value must not contain the specified keyword or text. Example: Color ⊄ "Red".
        </li><li>**Greater than or Equal to (>=)**: The attribute value must be greater than or equal to the specified value. Example: "Price >= 100".
        </li><li>**Less than or Equal to (=)**: The attribute value must be less than or equal to the specified value. Example: Rating =\< 4.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        **Equals (=)**
      </td>

      <td>
        The attribute value must exactly match the specified value. Example: Brand = Nike.
      </td>
    </tr>

    <tr>
      <td>
        **Not Equals (≠)**
      </td>

      <td>
        The attribute value must not exactly match the specified value. Example: Color ≠ Red.
      </td>
    </tr>

    <tr>
      <td>
        **Contains (⊂)**
      </td>

      <td>
        The attribute value must include the specified keyword or text. Example: Brand ⊂ "Nike".
      </td>
    </tr>

    <tr>
      <td>
        **Does Not Contain (⊄)**
      </td>

      <td>
        The attribute value must not contain the specified keyword or text. Example: Color ⊄ "Red".
      </td>
    </tr>

    <tr>
      <td>
        **AND**
      </td>

      <td>
        All conditions must be true for the rule to apply. Example: Brand = Nike AND Color = Red.
      </td>
    </tr>

    <tr>
      <td>
        **OR**
      </td>

      <td>
        At least one condition must be true for the rule to apply. Example: Brand = Nike OR Brand = Adidas.
      </td>
    </tr>

    <tr>
      <td>
        **THEN**
      </td>

      <td>
        Defines the sequence of rules. The second rule will apply if the first condition is met. Example: Sort by Price Ascending THEN Sort by Rating Descending.
      </td>
    </tr>
  </tbody>
</Table>