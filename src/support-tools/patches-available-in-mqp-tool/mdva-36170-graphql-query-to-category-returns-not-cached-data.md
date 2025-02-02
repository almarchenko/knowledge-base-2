---
title: MDVA-36170: GraphQL query to category returns not cached data
labels: 2.3.1,2.3.2,2.3.2-p2,2.3.3,2.3.3-p1,2.3.4,2.3.4-p2,2.3.5-p1,2.3.5-p2,2.3.6,2.3.6-p1,2.4.0,2.4.0-p1,2.4.1,2.4.1-p1,GraphQL,GraphQL queries,MQP 1.0.20,MQP patches,Magento Commerce,Magento Commerce Cloud,caching,category,data,support tools
---

The MDVA-36170 Magento patch fixes the issue where the result of the GraphQL query is not cached. This patch is available when the [Magento Quality Patch (MQP) tool](https://support.magento.com/hc/en-us/articles/360047139492) 1.0.20 is installed. The patch ID is MDVA-36170. Please note that the issue was fixed in Magento 2.4.2.

## Affected products and versions

 **The patch is created for Magento version:** Magento Commerce Cloud 2.3.6

 **Compatible with Magento versions:** Magento Commerce and Commerce Cloud 2.3.1-2.4.1-p1

>![info]
>
>Note: the patch might become applicable to other versions with new MQP tool releases. To check if the patch is compatible with your Magento version, run `./vendor/bin/magento-patches status` .

## Issue

Fixes the issue where the result of the GraphQL query is not cached.

 <span class="wysiwyg-underline">Steps to reproduce:</span> 

The merchant is using the GET method for GraphQL caching but not getting the cached data.

<pre>https://magento_url/graphql?query={ products(filter: {category_id: {eq: "2"}}, pageSize: 2000, currentPage: 1, sort: {position: ASC}) {
items {
  sku
  id
  name
  description {
    html
  }
  url_key
  specifications
  image {
    label
    gallery_url
  }
  __typename
  quantity_in
  small_image {
    gallery_url
    label
  }
  product_price_range {
    maximum_price {
      final_price {
        value
      }
    }
    minimum_price {
      final_price {
        value
      }
    }
  }
  ... on ConfigurableProduct {
    variants{
      attributes{
        code
        label
        value_index
      }
      product{
        sku
        quantity_in
      }
    }
   }
  }
}
}}</pre>

 <span class="wysiwyg-underline">Actual result:</span> 

The data is not cached.

 <span class="wysiwyg-underline">Expected result:</span> 

The data is cached.

## Apply the patch

For instructions on how to apply an MQP patch, use the following links depending on your Magento product:

* Magento Commerce: DevDocs [Apply patches using Magento Quality Patches Tool](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) .
* Magento Commerce Cloud: DevDocs [Upgrades and Patches > Apply patches](https://devdocs.magento.com/cloud/project/project-patch.html) .

## Related reading

To learn more about Magento Quality Patches, refer to:

* [Magento Quality Patches released: a new tool to self-serve quality patches](https://support.magento.com/hc/en-us/articles/360047139492) .
* [Check if patch is available for your Magento issue using Magento Quality Patches](https://support.magento.com/hc/en-us/articles/360047125252) .

For info about other patches available in MQP tool, refer to the [Patches available in MQP tool](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) section.