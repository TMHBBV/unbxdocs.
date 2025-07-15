---
title: Onboarding
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

With every business pushing itself online, expectations of shoppers from an eCommerce site have increased. Owing to the same, Unbxd has been delivering a competent search engine for them.

A comprehensive site-search helps to:

* Maximize conversion rate
* Increase the customer retention rate
* Improve a shopper’s experience
* Quickly map the shoppers’ to their intended products
* Provide effective results with merchandising techniques
* Reduce the zero results
* Looking at the complexities that you face to set up your site search, we at Unbxd have launched a simplified Onboarding process. The Onboarding process streamlines the process of uploading catalog, indexing, setting up relevance, and integrating the search in a mere five steps.

Our Unbxd’s AI identifies the relevant set of synonyms, searchable fields, and facets in accordance with your product catalog upfront. The AI recommendation sorts your entire catalog by deciding which fields should be marked searchable along with their search weights.

Such upfront settings help you save time and efforts to set your relevancy settings. This documentation will guide you through the process of creating and integrating your site with Unbxd.

You can also refer to this video to set up your site search within 5 minutes using Unbxd’s new Onboarding console :

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=waNLszfKqMM" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FwaNLszfKqMM%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DwaNLszfKqMM%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FwaNLszfKqMM%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=waNLszfKqMM" providerUrl="https://www.youtube.com/" providerName="YouTube" />

You can set-up a site search solution using Unbxd with the following steps :

1. Create an Unbxd Account
2. Create an Unbxd Site
3. Upload a Catalog
4. Setup Search
5. Integrate Search

Tips: A fully functional Sandbox will be available for testing after step 4. You can use our UI library to quickly integrate Unbxd search on your website.

## Create an Unbxd Account

Before setting up your site search, create your Unbxd account. Unbxd helps you to create a free trial account by signing into console.unbxd.io/signup.

<Image align="center" border={true} caption="Signup on console" src="https://files.readme.io/4140df84d13a62142e70a01531b4a3ead983d81f6cb6237a2a2cf9aae38ad5b5-image.png" width="80% " />

To create your account, specify your account details viz Name, Work Email, Password, and Data Center.

> 📘 Note:
>
> Once you have signed up with your details, our team is notified about a new user sign-up. Our team activates your account post verification. You can reach out to [sales@unbxd.com](mailto:sales@unbxd.com) for queries related to account activation. Once your account is activated you can login to Unbxd console.

Log in needs your email address and password to let you in to create your site setup.

> 📘 NOTE
>
> If you’re not able to login to your account, it may happen due to three reasons:
>
> * You have not created your account. So, first signup and then log in to your account.
> * You have not activated your account.
> * You have typed incorrect credentials. So, make sure the credentials are correct and in case you forgot your password, click ‘Forgot Password’ and reset it.

## Create an Unbxd Site

After you have created your account and logged into it, the next step is to create an “Unbxd site”. Each “Unbxd site” represents an independent instance for Search / Browse with a catalog. This entire section on the console will ask you to fill in the relevant field values to start off with your eCommerce site.

To create a site following details are required:

* Name of your site: Fill in a relevant name for your site like if your Sitename is Walmart, use walmart\_dev or walmart\_demo. Best practices to name your site is by appending the environment type (Dev, Prod, Stage) along with your site name. The name of the site is used to uniquely identify the site.
* Environment: Select the hosting environment for your eCommerce site. It can be Prod, Dev, or Staging.\
  Vertical: Select the most appropriate business vertical from the dropdown menu. The vertical is used for setting up relevance on the website.
* Platform: Select any eCommerce platform from the dropdown. We will keep you updated about the latest updates on Unbxd about your platform.
* Language: Select the preferred language for your Unbxd site based on the language used in your catalog to describe products.
* Data Center: Choose the data center that is nearest to the shoppers for better response time.

Once you have filled in all the site details, click the enabled “Proceed” button to start the site creation. The process of site creation may take a few minutes.

> 📘 NOTE
>
> At the time of site creation, customers will get an option to select the location of their website.

## Upload a Catalog

After setting up the site, you can start building your site solution by uploading your product catalog. Select a mode for uploading your catalog from the following options :

* Platform Plugin: Use our platform plugins to upload catalog if you are using one of these platforms (SAP Hybris and Magento2). Using platform plugins is the fastest way to integrate Unbxd search.
* Feed API: If the products in your catalog are more than 25K then, you can upload the catalog via our Feed APIs. Feed APIs only support the JSON file format.

<Image align="center" border={true} caption="Configure Site Key and API Key" src="https://files.readme.io/d8e620838954a097f0d1309291ddeece0f492a3c7b110861bbd2a57a07187f3a-image.png" width="80% " />

* PIM: PIM allows you to upload the catalog via SFTP, URL, or directly via your computer. PIM uploads are recommended for catalog with less than 25K products. Unbxd PIM allows you to add transformations for each attribute before uploading the catalog.

> 📘 NOTE
>
> You can also import your catalog via SFTP locations. Though, which catalog will be uploaded first depends on the catalog size.

## Platform Plugin

The most convenient way to upload your feed is via platform plugins. When you choose ‘Platform’ as your chosen option for uploading the catalog, you get redirected to the next page. We currently support plugins for two platforms:

* Magento
* SAP Hyrbis

If you have your eCommerce site on any of them, then select that plugin option.

### Magento2 Platform

With these two steps you can upload your catalog via Magento2 platform plugin :

* Plugin Installation: Install the plugin using Composer or using our links mentioned in Github. The steps are clearly defined on the console.
* Manual Synchronization: If not, then manually sync your catalog using Magento’s site.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/9564a3fa3e07cc1bd78abe753c0759f9838d93c56c25cbf59c2f688d33672ab2-SAP-HYbris.png" />

Once done, click ‘Proceed’. If the feed is successfully uploaded, the status changes to ‘Feed Upload is successful’.

To know more, read the [Magento2 Documentation](https://unbxdocs.readme.io/docs/magento-platform-integration-1#/).

### SAP Hybris Platform

If your site is on SAP Hybris, do the following:

1. First, install the Hybris plugin by downloading the module from Unbxd’s GIT directories. Perform the steps as mentioned on the console.
2. Then synchronize your feed from your Hybris site account.

<Image align="center" border={true} caption="Configure Hybris" src="https://files.readme.io/6710011524621b3fc44cbe06c7bbdda25b97955d788ef0419a85a61c316a893d-Screenshot-2020-07-31-at-6.30.38-PM.png" width="80% " />

To know more, read the [SAP Hybris Documentation]().

Once done, click ‘Proceed’. If the feed is successfully uploaded, the status changes to ‘Feed Upload is successful’.

### PIM

Unbxd PIM manages and centralizes all your product-related content and process for accuracy. While we have an advanced Extract, Transform, Load (ETL) platform in place to help with major catalog issues, we require you to make sure that some guiding principles around the catalog are followed.

Unbxd supports uploading the catalog in the following file formats:

* .csv
* .xls
* .JSON
* .XML

Uploading your feed in any of the aforementioned formats initiates the import process. You can also upload it as a zip file for the supported formats.

List of unsupported settings\
But even after you decide on the file format for upload, check the following settings to avoid Feed Upload Failure or any other discrepancies:

Nested JSON, XML: Nested JSONs are the ones where an object is nested inside other objects. Our system doesn’t support such nested JSON or XML files. Our system understands the linear mapping in the JSON/XML file. To help you understand, let us look at the following example:

What Unbxd  PIM supports: Fields and Values explained in a linear hierarchy.