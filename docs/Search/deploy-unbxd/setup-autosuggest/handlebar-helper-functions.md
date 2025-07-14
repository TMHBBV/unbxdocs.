---
title: Handlebar Helper Functions
deprecated: false
hidden: false
metadata:
  robots: index
---
# unbxdIf

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        FUNCTION
      </th>

      <th style={{ textAlign: "left" }}>
        DESCRIPTION
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        Purpose
      </td>

      <td style={{ textAlign: "left" }}>
        You can use the unbxdIf function if you need to render a block when two arguments are the same.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Arguments
      </td>

      <td style={{ textAlign: "left" }}>
        unbxdIf accepts two arguments and evaluates to true incase of physical equality of the arguments
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Usage
      </td>

      <td style={{ textAlign: "left" }}>
        The following example Renders “price” text when the value of facet\_name property is equal to “v\_PriceRange\_uFilter”, else it would render the value of facet\_name.

        \{\{#unbxdIf ../facet\_name “v\_PriceRange\_uFilter”}} Price\{\{else}}\{\{../facet\_name}}\{\{/unbxdIf}}
      </td>
    </tr>
  </tbody>
</Table>

# prepareFacetValue

| FUNCTION  | DESCRIPTION                                                                                                                                      |
| :-------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| Purpose   | The prepareFacetValue function returns three non breaking spaces if the argument value is empty.                                                 |
| Arguments | prepareFacetValue accepts one argument and returns three non breaking spaces if the argument value is empty, else would return the value itself. |
| Usage     | \{\{#prepareFacetValue value}}\{\{/prepareFacetValue}}                                                                                           |

<br />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

&#x20;

<br />

prepareFacetValue

<br />

Purpose

<br />

The prepareFacetValue function returns three non breaking spaces if the argument value is empty.

<br />

Arguments

<br />

prepareFacetValue accepts one argument and returns three non breaking spaces if the argument value is empty, else would return the value itself.

<br />

Usage

<br />

\{\{#prepareFacetValue value}}\{\{/prepareFacetValue}}