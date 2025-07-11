---
title: SAP Hybris
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Netcore Unbxd Hybris Plugin allows you to use the Unbxd plugin within your SAP Hybris website, integrating all the product discovery features with minimal developer intervention. This section will help you install the Unbxd extension, synchronize the product catalog, and integrate analytics.

| **Feature**                | **Description**                                                                                                                                                              |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Automatic Catalog Sync** | Automatically synchronizes product additions and deletions with Unbxd servers based on a predefined schedule, keeping the data up-to-date.                                   |
| **Analytics Integration**  | Tracks user behavior (product clicks, cart additions, orders) and builds user profiles based on affinity to categories, brands, or prices, enhancing search result accuracy. |

> 📘 Note
>
> The plugin is currently developed on SAP Commerce version 6.6. However, the plugin will support all Commerce versions from 6.0 to 2211 (latest release)

# Installation

Integration of Unbxd plugin within SAP hybris application can be done for Feed and Analytics.

### Feed Integration

To install Unbxd plugin, follow the steps below:

1. Download the SAP Hybris [module](https://drive.google.com/file/d/1TfQuJHrFr2VKMXwQkRxKlLUino4Wboq2/view?usp=drive_link) from GIT directories.
2. Unzip the module & copy `/hybris/bin/custom to /hybris/bin/custom`
3. Open `/bin/config/localextensions.xml` and add the mentioned code:

```
<extensions>
  . . . . .
  <extension name='unbxd' />
  <extension name='unbxdBackoffice' />
  <extension name='unbxdanalytics' />
</extensions>
```

4. After that, `Open /bin/config/local.properties` and add the following keys:

```
unbxd.sitekey.<index name>=<YOUR UNBXD SITE KEY>
unbxd.secretkey.<index name>==<YOUR UNBXD SECRET KEY>
unbxd.apikey.<index name>==<YOUR UNBXD API KEY>
```

To get the index name, navigate to Search Console and **Navigation** > **Facet Search Configuration** > **Properties** > **Index Name Prefix**.

<Image align="center" border={true} caption="Set up Name Prefix" src="https://files.readme.io/f7a1d4db1877a0056efd8b6f871b3b56e0617873f286ee01a3a64dfd81e01798-image.png" width="80% " />

5. Rebuild **Hybris Solution** by running the following command:

```
$ cd /bin/platform<br>$ ant clean all && ant updatesystem
```

### Analytics Integration

For Analytics integration, add the below code

```
unbxd.analytics.sitekey.<base store name>=DevHybris801271569422411
```

Base store name can be found in Backoffice at node Base **Commerce** > **Base Store**. The analytics plugin needs to be installed as an addon on top of the hybris storefront plugin. You need to run the following command:

```
ant addoninstall -Daddonnames="unbxdanalytics" -<br>DaddonStorefront.yacceleratorstorefront="yacceleratorstorefront"
```

> ❗️ Note
>
> NOTE: in the above command, **yacceleratorstorefront** is a storefront plugin that needs to be replaced with the storefront extension name of your installation.

Once you rebuild the solution. You can see that unbxdanalytics related files are copied in your storefront plugin. When we run the above command and rebuild **hybris unbxdAnalytics**,  addon files are copied into the yacceleratorstorefront.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/09f473b41cb9e51512aed5490e0a8e35a39eae2b93f1989b43e120e3401e3720-image.png" />