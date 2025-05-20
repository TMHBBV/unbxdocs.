---
title: Attributes
excerpt: >-
  View, manage, and create attributes that define the characteristics of your
  user.
deprecated: false
hidden: false
metadata:
  robots: index
---
Segment attributes define shopper groups based on specific criteria, enabling targeted personalization. These attributes enable precise targeting, improving search relevance, recommendations, and merchandising strategies.\
Attributes include:

**Location**: Segment shoppers by region for localized recommendations.

**Device**: Identify shopping behavior across mobile, desktop, or tablet.

**Visit Type**: Distinguish between first-time and returning visitors to tailor experiences.

**Custom Attributes**: Use business-specific criteria to create unique shopper segments.

## Types of Segment Attributes in Unbxd

Segment attributes classify shoppers based on different criteria for personalization.

1. **Default Attributes**: Built-in attributes such as location, device, and visit type that help segment shoppers based on standard data points.

Default attributes are predefined segmentation criteria available in the Unbxd platform. These attributes help categorize shoppers based on common factors without additional configuration. It simplify segmentation, allowing for quick personalization without custom setup.

<br />

| **Attribute**  | **Description**                                                               | **Use Case**                                                                                                                 |
| -------------- | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Location**   | Groups shoppers based on geographic location for tailored recommendations.    | A shopper from New York sees winter clothing recommendations, while a shopper from California sees summer apparels.          |
| **Device**     | Targets users based on the device they use for personalized user experiences. | Mobile users receive a streamlined experience, while desktop users see a more detailed layout.                               |
| **Visit Type** | Differentiates between new and returning users for customized content.        | First-time visitors see trending products, while returning shoppers see personalized recommendations based on past activity. |

2. **Custom Attributes**: User-defined attributes passed through the search API to create segments based on specific business needs.

Custom attributes are user-defined criteria used to segment shoppers based on specific business needs. These attributes are passed through the search API and help create more tailored shopping experiences.\
You can add up to five custom attributes in addition to the default ones per segment.

| **Attribute**           | **Description**                                                                  | **Description**                                                                                   |
| ----------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **Loyalty Tier**        | Segments shoppers based on their loyalty status for tailored offers.             | Segment shoppers as "Gold," "Silver," or "Bronze" members to offer exclusive discounts.           |
| **Purchase Frequency**  | Groups shoppers by how often they make purchases for targeted incentives.        | Identify frequent buyers to provide personalized promotions or early access to sales.             |
| **Product Preferences** | Classifies shoppers by brand or category interests to enhance product targeting. | Categorize shoppers based on interest in specific brands or categories to refine recommendations. |

## Segment Selection

Priority order is critical in order to resolve the conflict between the different segments.\
The priority order of selecting a segment in one or more matching attributes is available between two segments.

* Unbxd Default: Location
* Unbxd Default: Device Type
* Unbxd Default: Visit Type

### Use Case

For example,

Segment A: Segment is created for Spain which is location bases with the name **Spain\_users**.

Segment B : Another segment is created new shoppers with the name **New\_shoppers**.

**Question**: If a new shopper comes from Spain, both segments will be applicable. Which segment should be chosen by Unbxd?

**Solution**: Unbxd will resolve the issue based on the priority of the segmentable attributes configured by the user.\
Unbxd Default Location is ranked above Unbxd Default visit type, so in the above use case, **Spain\_users** segmentation will be applied.