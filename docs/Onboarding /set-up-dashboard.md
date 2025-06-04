---
title: Set up Dashboard
deprecated: false
hidden: false
metadata:
  robots: index
---
# Create an Unbxd Account

Before setting up your site search you need to create your Unbxd account. Unbxd helps you to create a free trial account by signing into [sign-up console](console.unbxd.io/signup).

<Image align="center" border={true} caption="Sign Up for Netcore Unbxd console" src="https://files.readme.io/8e29af84978421bc0109491dcb18782d0d87a699cab9398cf891c91a8c19fcfa-image.png" />

To create your account, you need to specify the account details as below:

| **Column Name** | **Description**                                                             |
| --------------- | --------------------------------------------------------------------------- |
| **Name**        | The full name of the user or employee.                                      |
| **Work Email**  | The official email address used for work-related communication.             |
| **Password**    | The security password used to access work-related accounts or systems.      |
| **Data Center** | The physical or cloud location where the user’s data is stored and managed. |

> 👍 Important
>
> 1. Once you have signed up with your details, Netcore Unbxd's sales team is notified about a new user sign-up. The team activates your account post verification.
> 2. You can reach out to [sales@unbxd.com](mailto:sales@unbxd.com) for queries related to account activation

Once your account is activated you can login to Unbxd console.

<Image align="center" border={true} caption="Log in to Netcore Unbxd" src="https://files.readme.io/55a2666ca2c985acb4fdb6c3b20e6dc98ba26b096e93dd71eba4863330f39279-image.png" />

> 📘 Good to Check
>
> Before you proceed further, ensure following is done.
>
> 1. Your Netcore Unbxd account is created
> 2. Your account is activated. To ensure this, check your inbox for the activation email and click the activation link to enable your account.
> 3. While log in to the Netcore Unbxd account, ensure that your username and password entered is correct. If you have forgotten your password, click on **Forgot Password** to reset it.

# Create an Unbxd Site

After you have created your account and logged into it, the next step is to create an **Unbxd Site**.

> 📘 Note
>
> Each **Unbxd Site** represents an independent instance for **Search** / **Browse** with a catalog.

<Image align="center" border={true} caption="Create Site" src="https://files.readme.io/dea2c1201cf30ed6c9c70636bc2fcfafb4db0fa0a410e2367655947d31426389-image.png" />

### Set up the field data:

Set up the following details, and click the enabled **Proceed** button to start the site creation.

| **Field**        | **Description**                                                                                                                                                          |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Name of Site** | Fill in a relevant name for your site (e.g., walmart\_dev, walmart\_demo) by appending the environment type (Dev, Prod, Stage). This name uniquely identifies your site. |
| **Environment**  | Select the hosting environment for your eCommerce site (Prod, Dev, or Staging).                                                                                          |
| **Vertical**     | Select the most appropriate business vertical from the dropdown. This helps set up relevance on the website.                                                             |
| **Platform**     | Select an eCommerce platform from the dropdown menu. You’ll receive updates about your platform from Unbxd.                                                              |
| **Language**     | Select the preferred language for your Unbxd site, based on the language used in your catalog to describe products.                                                      |
| **Data Center**  | Choose the data center nearest to the shoppers for improved response time.                                                                                               |

> 📘 Note
>
> * The process of site creation may take a five minutes or more.
> * At the time of site creation, customers will get an option to select the location of their website.

# Upload a Catalog

After setting up the site, you can start building your site solution by uploading your product catalog. Select a mode for uploading your catalog from the following options :

1. **Platform Plugin**: The most convenient way to upload your feed is via platform plugins. When you choose ‘Platform’ as your chosen option for uploading the catalog, you get redirected to the next page. We currently support plugins for two platforms:
   * [SAP Hybris]()
   * [Magento]()
2. **Feed API**: If the number of products in your catalog are more than 25K then, you can upload the catalog via our Feed APIs. **Feed APIs only support the JSON file format**.

<Image align="center" border={true} caption="Upload a catalog via Feed API" src="https://files.readme.io/314900b1e1d6b1cb0bc8adca9d6178030d16463acbd8425dd434f6f2018c0d34-image.png" />

# Setup Search

The final step involves ways to set up your search features incorporated with AI recommendations. We scan through the catalog to calculate the attributes that will be made searchable or considered as facets.

Our AI system also has diversified knowledge of catalogs from different verticals which makes it intelligent to identify the probable relevancy settings. We use this to set the relevancy of your site automatically which reduces the zero-result queries and improves the recall.

> 📘 Note
>
> These settings can be changed from the console later.

## Searchable Fields

Searchable Fields help in identifying the attributes that are searched while searching for a query. Our AI engine identifies the searchable fields upfront from the uploaded catalog. You can validate the recommendations and edit it later accordingly.

* **Searchable field**: When you define a product attribute (like color) as a searchable field, it affects the search results when a shopper searches for a product.
* **Non-Searchable field**: If an attribute is set as ‘Non-Searchable’, then it doesn’t affect the search results, therefore, simplifies the search results by showing only the relevant ones.

For example, if the **color** attribute of the corresponding products is added as a **High Searchable** attribute then shoppers searching for **Blue Shirts** will get the exact results.

The searchable fields are also assigned search weights (High, Normal, Low) based on their priority of affecting search results defined by our AI engine.

| **Weightage**      | **Description**                                                                           |
| ------------------ | ----------------------------------------------------------------------------------------- |
| **Non-Searchable** | Attributes that shouldn’t affect the search results should be tagged as ‘Non-Searchable’. |
| **High**           | When an attribute is marked as a top priority to affect the search results.               |
| **Medium**         | When an attribute is marked as a second-top priority to affect the search results.        |
| **Low**            | When an attribute is marked as the lowest priority of all to affect the search results.   |

Our AI recommendations calculate the searchable fields and their weights based on the following parameters:

> 📘 Good to know
>
> Descriptive fields with generic information (i.e. information that does not change with each SKU) should not be included in-spite of high query coverage.

**Product Coverage**: Product coverage tells you how many products in the catalog will be affected if this field is made searchable.\
**Query Coverage**: Query coverage is an indicator of how frequently customers are using the information in this attribute while searching for products.
**AI recommendations**: The recommended search weight for the fields decided by the AI based on quantitative (query coverage, product coverage) and qualitative factors

## Facets

Facets are created on site-level to narrow down search results for the shoppers for their intended query. If shoppers type a query **Books**. Facets like **Genre**, **Author**, **Format** get reflected on the Product Display Page(PDP). When shoppers select facets, they further reduce the number of products on the results page. Refer [here](https://unbxdocs.readme.io/update/docs/facets-1#/) to understand capabilities offered by Facets.

## Content Relevance

To improve how Netcore Unbxd understands shoppers' search queries, it suggests **Synonyms**, **Phrases**, **Concepts**, and **Stopwords** related to the queries. This helps prevent ‘Zero Results’ from appearing when shoppers search for products. Follow the steps below to add Content Releance offered by Netcore Unbxd.

1. **Upload Your Own Thesaurus/Dictionary**: You can quickly enhance Unbxd's search understanding by uploading your own thesaurus or dictionary. This helps Unbxd better match queries with your catalog.
2. **Preview Unbxd Suggested Dictionaries**: You can see the dictionaries that Unbxd automatically suggests based on your catalog.
3. **Add Your Own Dictionaries**: You can also add your own dictionaries to complement the ones generated by Unbxd. This allows for more tailored results that better reflect your specific product catalog.

Refer [here](https://unbxdocs.readme.io/update/docs/content#/) to know more.

4. Once configurations are completed, click **Start Indexing** to push the settings and get access to a Sandbox.

> 📘 Note
>
> Once the indexing is done, you will have your site search engine all up and ready!
>
> Access Netcore Unbxd Search Console for further other features or tracking Insight

## Autosuggest

Netcore Unbxd's Autosuggest feature provides query suggestions as shoppers type in the search bar, helping quickly to find what they are looking for. By offering relevant suggestions, it allows shoppers to make faster decisions.

You can configure the type of suggestions to show and adjust where they appear on the page. To enable Autosuggest, simply choose a template for displaying the suggestions on your site, and then proceed to set up the type of suggestions you want to show. Refer [here](https://unbxdocs.readme.io/update/docs/merchandising-autosuggest#/) to know more about Autosuggest.

# Preview & Integrate Search

After you have set up your site search, the next step is to **preview** and then **integrate** the search. The Preview screen lets you see all the features and changes that you have integrated before publishing them. For this, Netcore Unbxd allows you to select a template from a pool of templates (designed for Product Listing Pages) with various features to display your products. Selecting a template saves you time and refrains you from customization pain.

## Set up a Template

A template displays a demo of the Product Listing Page (PLP) with various properties customizable according to your site’s requirements. Follow the steps below to select a template:

1. Click **Live Preview** after setting up the search. You can see a demo Product Listing Page (PLP) has been already set up with a default Unbxd template. On the console, click **Website Preview** on the console dashboard to access the preview page.

Even though a default template is chosen, we have a pool of other templates for you to select from based on your requirements.

2. To see more templates, click **See available templates**.

A list of available templates opens up, out of which a few are marked as Recommended and displayed on the top. Recommended templates are the ones that Unbxd selectively curates for your business vertical and catalog.

3. Click Template Info to view the key features of the template. Once you have selected the template of your choice, click the template to apply it.
4. Dimensional Mapping: Each template needs different attribute mapping to let the features function correctly. In case, you haven’t mapped any essential attribute required for the template, a pop-up will ask you to map the unmapped attributes. Once done, click Save changes. Refer [here](https://unbxdocs.readme.io/update/docs/dimension-mapping#/) to understand in details.

**Benefits of having templates:** You can test Unbxd Search using a template that is similar to your website/vertical. Integrate Unbxd search and its functionalities by simply downloading and integrating the Template UI Kit.

<Image align="center" border={true} caption="Search Integration" src="https://files.readme.io/21f21341dabe143625a09042d06bbbf0bee92067e9628f7082a20b6c170c4f8d-image.png" />

> 📘 Good to Know
>
> We also support the grouping of variants on swatches or size attributes in the templates. To group the variants on swatches, map the field containing the swatch image URL or color hex code in your catalog to the Unbxd  Swatch field.Whenever you preview your site after the template selection, your site will automatically open up in the applied template.

# Integrate a Template

The final step in the process of Onboarding is to integrate Unbxd Search to display search results for shopper’s queries. Unbxd offers RESTful APIs & SDKs for different platforms to allows easy integration of our Search features.

## Using SDKs

Use Unbxd SDK to integrate Unbxd Site Search by following just two steps.

1. Click the Download UI kit.
2. Unzip the package and open the index.html file in your browser to view the search results landing page for your catalog with the Unbxd default template.

To know more about the Search SDK configs and the different possible options, read the SDK documentation here.