---
name: Displayhigherfacets
---
# Q. How to display a higher number of facets without hurting request latency ?

A. Returning a higher number of facets hurts performance of your search and adds a few extra milliseconds to your response time. In general, it is recommended to show 10-15 most relevant facets on a search results page (SRP) to help shoppers discover and use filters effectively without too much cognitive load on the shoppers. However, if your business demands showing a higher number of facets on the SRP and you don’t want to sacrifice on the performance then we have a solution for you.

\*\*Solution 1: Using Multi-valued field \*\*

**Step 1**: Combine individual facet fields into a single multi-valued fields. Let us assume that you want to create facets on the following fields :

* Availability which has value “Yes” & “No”
* Gender which has value “Male” & “Female”
* Size which has the unique values “S” , “M” , “L” , “XL”
* Add a new multi-valued field in the catalog called Facet\_group\_1 where the key & value pair of the fields are stored.

Sample feed before transformation :

```
\{  
  "add": [
  \{
  "Availability": "Yes",
  "Gender": "Male",
  "Size": "L",
  "UniqueId" : "1"
    },
  \{
  "Availability": "No",
  "Gender": "Female",
  "Size": "S",
  "UniqueId" : "2"
  }
  ]
}
```

Sample feed after transformation:

```
\{  
  "add": [
  \{
  "Availability": "Yes",
  "Gender": "Male",
  "Size": "L",
  "UniqueId" : "1",
  "Facet_group_1" : ["Availability|Yes","Gender|Male", "Size|L"]
    },
  \{
  "Availability": "No",
  "Gender": "Female",
  "Size": "S",
  "UniqueId" : "2",
  "Facet_group_1" : ["Availability|No","Gender|Female", "Size|S"]
  }
  ]
}
```

**Step 2**: Create a facet on the field Facet\_group\_1 instead of creating a facet on individual attributes Availability, Gender, and Size. The facet response for Facet\_group\_1 is going to have the following format :

```
\{  
"facetName": "Facet_group_1",
"filterField": "Facet_group_1",
"values": [
"Availability|Yes", 50,
"Availability|No", 50,
"Gender|Male", 40,
"Gender|Female", 60,
"Size|L", 20,
"Size|S", 30,
"Size|XL", 40,
"Size|M", 10,
],
"displayName": "Facet Group 1",
"position": 1
}
```

**Step 3**: Parse the facet response to get back values for the individual facet on the front end.\
Iterate through the values returned for Facet\_group\_1 to separate the key-value pairs and group the pairs having the same name to generate facets for the original attributes

Availability

1. Yes – 50
2. No – 50

Gender

1. Female – 60
2. Male – 40

Size

1. XL – 40
2. S – 30
3. M – 10
4. L – 20

<br />

> 📘 Note
>
> * The display name for facets has to be decided at the time of the feed change step (i.e. step 1).
> * The position, display name, and sorting of facet values cannot be configured from the console.\
>   This approach is not recommended for Range facets (e.g. facets created on price).

**Solution 2: Using Multi-level facets for grouping facets**

There are occasions where you may have different ways of classifying a product based on the same property.

For example, the Size of a fashion product can be defined in the following ways :

* Size\_1: “Regular” or “Petite” or “Plus”
* Size\_2: “S” or “M” or “L”

In these situations, you can use multilevel facets to help shoppers narrow down to the right product quickly without introducing a lot of facets. You can achieve this by following the following steps.

**Step 1:** Combine the individual facet fields into a single path type field called Size\_group

Feed before transformation

```
\{  
  "add": [
  \{
  "Size_1": "Regular",
  "Size_2": "L",
  "UniqueId" : "1"
    },
  \{
  "Size_1": "Petite",
  "Size_2": "S",
  "UniqueId" : "2"
  }
  ]
}
```

Feed after transformation

```
\{  
  "add": [
  \{
  "Size_1": "Regular",
  "Size_2": "L",
  "UniqueId" : "1",
  "Size_group" : "Regular > L"
    },
  \{
  "Size_1": "Petite",
  "Size_2": "S",
  "UniqueId" : "2",
  "Size_group" : "Petite > S"
  }
  ]
}
```

**Step 2**: Create a facet on the field Size\_group instead of creating a facet on individual attributes Size\_1 and Size\_2. Handle the response of the Size\_group multilevel facet to display the facet. The facet response will look like:

```
"facets": {  
"multilevel": {
"bucket": [
          \{
          "values": [
          "Regular",
          30,
          "Petite",
          50,
          "Plus",
          20
          ],
          "position": 0,
          "filterParam": "Size_group1_fq",
          "level": 1,
          "multiLevelField": "Size_group"
          }
          ],
"breadcrumb": {}
}
}
```

Once the shopper selects the “Regular” option, then they will get an option to select amongst the options in Size\_2.

```
facets": {  
"multilevel": {
"bucket": [
        \{
        "values": ["S",10,"M",10 ,"L",5,"XL",5],
        "position": 0,
        "displayName": "Size_group",
        "filterParam": "Size_group2_fq",
        "level": 2,
        "multiLevelField": "Size_group"
        }
        ],
"breadcrumb": {
"filterField": "Size_group",
"values": [
          \{
          "value": "Regular"
          }
          ],
"level": 1
}
```

> 📘 Note
>
> The shopper will get an option to select only 1 value at each level.