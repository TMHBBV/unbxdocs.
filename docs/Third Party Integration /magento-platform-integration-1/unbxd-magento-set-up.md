---
title: Unbxd-Magento Set Up
deprecated: false
hidden: false
metadata:
  robots: index
---
# General Settings

This section allows you to indicate the product types available in your catalog while excluding specific categories of products while synchronizing.

To upload product types:

On the Unbxd tab, click Catalog

In General Settings, within Available Product Types, select All Available Types to select all available product types within your catalog. Click the drop-down box to select from one of the product types.\
Click Save Config
The Unbxd extension supports seven types of products:

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/b38f78b3d250c615cead7c14cf9971c2177bc5c5d99a3c624db40c726b70f26f-image.png" />

* Simple Product: A simple product is a physical item with a single SKU. When converted to the Unbxd format, a simple product is considered as a Normal Feed.
* Configurable Product: A configurable product is a parent product of multiple simple products. When converted to the Unbxd format, configurable products are considered as variants.
* Grouped Product: A grouped product presents multiple, standalone products as a group. You can offer variations of a single product, or group them for a promotion. The products can be purchased separately or as a group. Like configurable products, when converted to the Unbxd format, grouped products are considered as variants.
* Virtual Product: A Virtual Product or Digital Product can be used for intangible items such as a membership, service, warranty, or subscription. They can be sold individually or included in grouped or bundled products. They are the same as simple products but without the weight field.
* Bundle Product: Bundle product lets the shoppers choose from a variety of options to create their own customized version. The options are a bundle of simple products.
* Downloadable Product: A downloadable product can be anything that you can deliver as a file, such as an eBook, music, video, software application, or update. You can offer an album for sale and sell each song individually. You can also use a downloadable product to deliver an electronic version of your product catalog.
* Gift Card: The three types of gift cards are Virtual, Physical, and Combined. Gift cards can be set to Redeemable or Non-Redeemable. The lifetime of a gift card can be unlimited or set to a number of days. The value of a gift card can be set to a fixed amount or set to an open amount with a minimum and maximum value.

> 📘 Note
>
> If your catalog has a mix of 'Simple products' and 'Configurable products' and you wish to send both Parent products and Variants to Unbxd, select both 'Simple Product' and 'Configurable Product' in the 'Available Products Types' dropdown

Our extension allows you to exclude four exclusive criteria of products:

* Disabled: Indicates products that have been disabled from being listed in the Product Listing Page
* Out Of Stock: Indicates products where the inventory count is 0
* Not Visible Individually: Indicates products that are available only as a bundle
* Without Images: Indicates products where there isn’t an available image

> 📘 NOTE
>
> Select only one value

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/3f9ce54af149d1ce4bcf63d1d03c2b38b19eb2c319edae103fd5f4c3d8953a73-image.png" />

**Maximum Number of Synchronization Attempts**\
The number of synchronization allowed in case of page load errors is specified in this bar. The value can vary between 1 to 5.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/773b7e3cdbd88caf7eede584081822746998bf0102d855aac1e2504dfab5fcd7-image.png" />

## Category Configuration

Following are the configuration options available:

Use Category ID: Category ID will be sent to Unbxd

Retain Disabled Category: Yes | Retain Disabled Category in the category path

Fetch from Category Entity Tables: Fetch from Category Entity Tables, instead of using the index tables, (experimental for those customers where category index tables are not consistently updated.

Note: enabling this feature could result in longer processing time v/s category data accuracy fetched from eav (entity attribute value)  tables.

## Product Images Settings

This section walks you through the process of uploading images for your products in the catalog.

<Image align="center" className="border" border={true} src="https://files.readme.io/fc9aa9207cc83642657a4b7a0c29d8ee008d2a7ab47af2ae7561a2b6d5dce21a-image.png" />

To enable Product Image Settings:

On the Unbxd tab, click **Catalog**.\
Within Product Image Settings, select Yes for Enabling it. If you select No, you will have no product images to display.
Click Save Config.
You need to upload a base image after which all the relative images are automatically uploaded.

* **Base Image**: This is a high-resolution JPEG file of your product images.
* **Small Image**: This version of the image is used on pages with multiple products, such as homepage, category and search results layouts. It’s also used for small boxes on product pages, such as up-sells, and cross-sells. A normal size for this image is around 250 pixels high and 250 pixels wide.
* **Thumbnail**: This version of the image is often seen at the bottom of the product page. If you buy this product, you’ll also see this image in the shopping cart. These images can be around 100 pixels high and 100 pixels wide.
* **Swatch Image**: This version of the images is used in more advanced store setups. If your product is available in more colors or options (also called as variants), customers can click on the swatch images to see what each version looks like.

## Indexing Settings

This section walks you through the process of configuration of the type of indexing operation.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/5819ed8fe5aeaa7650370476319cb5093d1d258b125539005e1b88f51cad2d89-image.png" />

To enable indexing:

On the Unbxd tab, click Catalog\
Within Indexing Settings, select Yes for Enable Indexing Queue. If you select No, your product catalog is not indexed automatically. Click **Save Config**

* If Enable Indexing Queue is set to ‘Yes’, then all indexing operations related to the products in the catalog will be added to the Indexing Queue and done asynchronously by a scheduled cron job.
* If Enable Indexing Queue is set to ‘No’, then all indexing operations related to the products in the catalog will be done immediately after the original product information is modified.

## Indexing Optimization

By default full feed will be executed as a multi part upload with a batch size of up-to 10000 products per iteration. This enables us to limit the memory requirement under ( 0.75GB – 1.5 GB ) irrespective of the catalog size.

**Reader Database support**:

For customer who prefer to route the select queries to a dedicated reader database can leverage the following configuration.

> 📘 Note
>
> We recommend you set Enable Indexing Queue to Yes when you are in Production Mode or if you have a product catalog that has more than 2 million products or is larger than 2GB.

## Data Fields Mapping

Data Fields mapping provides the ability to manually map the Unbxd Fields to the defined product attribute.

Unbxd Field can have the values as Availability, Category Path Id, Image URL, Product URL, Title, or UniqueID which can be mapped to the product attribute specified in your catalog.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/20607ab7664f91b52d8077c834917a424d9db82e05551208ed95426acf899589-image.png" />

In the above illustration, we can see the Unbxd field ‘UniqueID’ is mapped to SKU to track the inventory status.

# Catalog Sync

Before you sync your catalog, your Unbxd extension will upload your catalog as a JSON file and sync it to the Unbxd server in three ways:

1. Automatic Synchronization
2. Manual Synchronization
3. Command Line Interface (CLI)

## Automatic Synchronization

Our extension will send every update and deletion on products or categories to our servers to keep all data up-to-date by setting cron jobs.The indexers’ behavior can be changed to prevent these update calls, and only update the data through manual reindexing. For this to work, the cron type should be set to ‘Manually’.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/a9ad341557fc1bfc3d824b6ec45da5aebc4a8e0a89517ccaa983c000e2ecf5b6-image.png" />

<br />

1. To schedule automated synchronization, On the Unbxd tab, click **Catalog**.
2. To schedule automated indexing, within Cron Settings, select **Yes** for Enable Cron
3. In Cron Type dropdown box, select the required type:

* Manually: When this is chosen, you can indicate the frequency of the cron job. When the Cron Type is set to Manually indicate the frequency of indexing within Cron Schedule.
* By Template: When this is chosen, you can indicate Start Time and the Frequency to ‘Daily’, ‘Weekly’, or ‘Monthly’.

4. In the Cron Schedule text field, type in the required frequency. Click the icon for examples.
5. To test the schedule, click the Check button for Check. If Cron Is Running. This lists the status and a log of the last 10 cron jobs.
6. Click Save Config

You have successfully scheduled automated synchronization for your product catalog.

## Manual Synchronization

You can also set to manually index your product catalog using manual synchronization options.

> 📘 NOTE
>
> Before you set up manual indexing, ensure the related cron job is configured.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/3d50451acbc08da4d2ff3cc1fd2246f4a622cebd82a1e582e897f69ba78aa572-image.png" />

<br />

To set up manual synchronization:

On the Unbxd tab, click Catalog, In General Settings, within Indexing Settings, select Yes for Enable Indexing Queue.

* In Manual Synchronization, select Yes for Enable Manual Synchronization.
* To perform a full feed upload, click the Synchronize button for Full Product Catalog Synchronization. To perform a delta upload, click the Synchronize button for Incremental Product Catalog Synchronization. Click Save Config
* You have successfully set up Manual synchronization for your product catalog.

To check the status of the feed upload, click Unbxd > Feed View.

> 📘 Note
>
> To avoid causing unnecessary resource delays and timeout errors, the synchronization operation will be added to the Indexing Queue even when Enable Indexing Queue is set to Number.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/f81cb9f3ab692f0c47ea07c666e79a082fac9277b0bf02cb26f4e3171f17f1c4-image.png" />

By navigating to **Unbxd** > **Catalog** > **Cron Settings** > **Full Feed**, you can automatically upload the full feed.

## Command Line Interface

You can use the Command Line Interface to update your product catalog from within the Magento directory.

**Add the –h key to see the features and configuration of each command.** More about Magento CLI commands [here](https://developer.adobe.com/commerce/docs/).

1. **Full product Catalog Synchronization**

This command allows you to perform a full product catalog synchronization. If the specific store ID is not specified, synchronization will occur for default store ID.

To schedule a full catalog synchronization, run:

```
php bin/magento unbxd:product-feed:full
```

2. **Incremental Product Catalog Synchronization**

This command allows you to perform an incremental product catalog synchronization. If the specific store ID is not specified, synchronization will occur for default store ID.

To schedule an incremental catalog synchronization, run:

```
php bin/magento unbxd:product-feed:incremental
```

3. **CheckFeed Upload Size**

This command allows you to check the total size of the feed being uploaded for a specific store. If the specific store ID is not specified – a default store ID will be used.

To check the file size of the feed, run:

```
php bin/magento unbxd:product-feed:upload-size
```

## Product Feed Generation

Product Feed can be generated in different formats viz .csv, .txt, or XML file formats. You can include all the product type to generate feed: simple, bundle, downloadable, grouped, or configurable.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/8377305ce1400772bbb3fed832046f30e7efb396b1b560e39f62da933274dfb7-image.png" />

You can generate product feed, download it, or delete the existing one.

## Optimize Product Data To Send To Unbxd

Depending on the line of business each of our customers has 100+ product specific information. By default the plugin will send all the product attributes configured in your system. Whereas Unbxd only needs product attributes which satisfies one or more of the following condition.

The attributes contain information which the customer will be searching on (name, description, brand, categories…)\
The attributes are used to create facets on the website (brand, price, color, screenSize …)
The attributes are shown on the product tile in the search results page (ratings, delivery information, images , productUrl ….)
We recommend customers review the list of product attributes and enable it to be sent to Unbxd only ones that meet the criteria listed above.

To disable an attribute being sent in the product feed to Unbxd:

1. Navigate to **Stores** > **Attributes**  > **Product**
2. Select the respective product attribute and navigate to storefront properties
3. Update value for **Include in Product Feed** attribute to “No”
4. Click on **save** attribute

### Customize Product Feed to Send Additional Information

Unbxd Product Feed extension is designed to be extended based on customer specific requirements. Like, there will be instances where you would like to send additional product information which are not managed as product attributes in Magento (ex: vendor specific pricing and availability for a customer running marketplace website, where prices and availability is managed per vendor using some third party magento extension).

To append additional information per product:

1. Create a php class which implements Unbxd\ProductFeed\Model\Indexer\Product\Full\DataSourceProviderInterface
2. Implement the appendData functionfunction appendData($storeId, array $indexData)
3. The second argument $indexData to the function is an associative array with key as product entityId and the value will an array of attributeName -> respective values.
4. Iterate through the array and add custom product information as additional attributes on the product array.

Refer to an implementation sample used to  compute reviewCount & finalRating for every product stored by Magento\_Review extension.

```
<!--?php


namespace Unbxd\ProductRating\Model\Product\DataSourceProvider;


/**
* @author      Jag S <jagadeesh@oceaniasolution.com-->
*/


use Unbxd\ProductFeed\Model\Indexer\Product\Full\DataSourceProviderInterface;
use Unbxd\ProductFeed\Logger\LoggerInterface;
use Magento\Framework\DB\Adapter\AdapterInterface;
use Magento\Catalog\Api\ProductRepositoryInterface;
use Magento\Review\Model\RatingFactory;
use Unbxd\ProductFeed\Helper\Data as HelperData;
use Exception;


class ProductRatingDataProvider implements DataSourceProviderInterface
{
   /**
    * Related data source code
    */
   const DATA_SOURCE_CODE = 'rating_productfeed_extension';




   const REVIEW_COUNT = "reviewCount";


   const RATING_SUM = "ratingSum";


   const FINAL_RATING = "finalRating";
  


    /**
    * @var LoggerInterface
    */
   private $logger;


    /**
    * @var HelperData
    */
   private $helperData;


   protected $productRepository;


 
   /**
    *
    *
    * @var RatingFactory
    */
   protected $ratingFactory;




   /**
    * Constructor.
    */
   public function __construct(ProductRepositoryInterface $productRepository,LoggerInterface $logger, HelperData $helperData, RatingFactory $ratingFactory) {
       $this->productRepository = $productRepository;
       $this->logger = $logger->create("feed");
       $this->helperData = $helperData;
       $this->ratingFactory = $ratingFactory;


   }


   /**
    * {@inheritdoc}
    */
   public function getDataSourceCode()
   {  
       return self::DATA_SOURCE_CODE;
   }


   /**
    * Add custom code here
    *
    * {@inheritdoc}
    */
   public function appendData($storeId, array $indexData)
   {
       /* product ID is the entity id in magento , add your custom logic for your custom attribute */
       foreach (array_keys($indexData) as $productId) {
           try {
               if ($productId != "fields"){
                   /**
                    * Replace the logic within this if condition to that of yours
                    */
                   $entitySummary = $this->ratingFactory->create()->getEntitySummary($productId);
                   if($entitySummary){
                       $data = $entitySummary->getData();
                       if($data && array_key_exists("count",$data)){
                           $reviewCount = $data["count"];
                           $indexData[$productId][self::REVIEW_COUNT] = $reviewCount;
                           $ratingSum = $data["sum"];
                           $indexData[$productId][self::RATING_SUM] = $ratingSum;
                           $ratingAvg = round($ratingSum/(20*$reviewCount));
                           $indexData[$productId][self::FINAL_RATING] = $ratingAvg;
                       }
                   }
               }
           } catch (\Exception $e) {
               $this->logger->error('Error Getting Entity Summary -'.$productId. $e->__toString());
           }
       }
       $this->addIndexedFields($indexData,self::REVIEW_COUNT);
       $this->addIndexedFields($indexData,self::RATING_SUM);
       $this->addIndexedFields($indexData,self::FINAL_RATING);


       /**
        * Replace the second argument with that of the attribute name which was included in line 75
        * addIndexedFields accepts a third optional argument which should one of the following values ('text','longText','decimal','number','link','date','bool','sku','path')
        * */
       return $indexData;
   }


   /**
    * @param $indexData
    * @return
    */
   private function addIndexedFields(array &$indexData,$attrName,$fieldType = "number")
   {
       $alreadyExistFields = array_key_exists('fields', $indexData) ? $indexData['fields'] : [];
       $indexData['fields'] = array_merge($alreadyExistFields, [$attrName => [
           'fieldName' => $attrName,
           'dataType' => $fieldType,
           'multiValued' => false, /*set it to true if the attribute will carry more than one value for the same product */
           'autoSuggest' => false
]]);
   }
}
```

5. Wire the new datasource provider created in the previous step to unbxd feed providers in your di.xml file as shown below:

```
 <type name="Unbxd\ProductFeed\Model\Indexer\Product\Full\DataSourceProvider">
       <arguments>
           <argument name="dataSources" xsi:type="array">
               <item name="rating_productfeed_extension" xsi:type="object">Unbxd\ProductRating\Model\Product\DataSourceProvider\ProductRatingDataProvider</item>
           </argument>
       </arguments>
   </type>
```

## Website Configuration

Using the Unbxd plugin via the Magento platform, you can integrate all the product features like Autosuggest, Search, Browse, and Recommendations in few easy steps.

The config has two properties named **siteName** & **APIKey** which is used by the SDK to identify the Unbxd site for the respective Magento store and environment (dev/stage/prod). You can  take values rof the keys by referencing the  **UnbxdSiteName** &  **UnbxdApiKey** in the Unbxd console. The values are populated from the respective values configured in the setup section of Unbxd.

> 📘 Note
>
> Prior to enabling Unbxd Features (Search/Autosuggest/Browse) ensure that the product feed is submitted and indexed with Unbxd.

## Autosuggest Configuration

After the catalog indexing is done, you can navigate to Unbxd > Website config and in the ‘Autosuggest’ section, enable the field value to ‘Yes’ to enable Autosuggest Feature. Autosuggest delivers suggestions as the shoppers’ type on the search bar of your site.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/6c1cec07851469b1485caae23321f52382456c856e9236b531f933de52f274ca-image.png" />

To know more about the Autosuggest SDK configs and the different possible options, click here.

Enable Custom Template

If you are using a custom template with a different CSS selector for your Search input box, then select ‘Yes’ and populate the block with the field value, so that we can get that input from our JS onto the CSS selector.