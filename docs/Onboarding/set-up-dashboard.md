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

1. **Platform Plugin**: Use our platform plugins to upload catalog if you are using one of these platforms (SAP Hybris and Magento2). Using platform plugins is the fastest way to integrate Unbxd search.
2. **Feed API**: If the number of products in your catalog are more than 25K then, you can upload the catalog via our Feed APIs. **Feed APIs only support the JSON file format**.

<Image align="center" border={true} caption="Upload a catalog via Feed API" src="https://files.readme.io/314900b1e1d6b1cb0bc8adca9d6178030d16463acbd8425dd434f6f2018c0d34-image.png" />

3. **PIM**: PIM allows you to upload the catalog via SFTP, URL, or directly via your computer. PIM uploads are recommended for catalog with less than 25K products. Unbxd PIM allows you to add transformations for each attribute before uploading the catalog.

> 📘 Good to Know
>
> PIM stands for **Product Information Management**. It is a system or software used by businesses to manage and centralize product information in a single location. The purpose of a PIM system is to ensure consistency, accuracy, and ease of access to product data, which can then be used across various sales channels.