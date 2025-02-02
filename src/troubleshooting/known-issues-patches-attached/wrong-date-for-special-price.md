---
title: Wrong date for Special Price
labels: 2.2.2,Magento Commerce,known issues,patch,special price,troubleshooting
---

This article provides a patch for the known Magento Commerce 2.2.2 issue related to the product special price "from" date being incorrect if its value is changed by the admin whose interface locale is different.

## Issue

When you set/change the special price for a product, the current date and time is saved in the database as a value for the `special_from_date` attribute (not visible when editing a product). If you edit the special price and your admin user account is set to different interface locale, a wrong value might be set to `special_from_date` , because of the issues in parsing date format for different locales.

 <span class="wysiwyg-underline">Steps to reproduce</span> :

Prerequisites: the admin user locale is English (United States).

1. Log in to Magento Admin.
1. Go to the admin user account settings.
1. Set Interface Locale to Ukrainian.
1. Click **Save Account** .
1. Go to **Catalog** > **Product** .
1. Select any product.
1. On the product page, click **Advanced Pricing** .
1. Add a special price.
1. Save the product.
1. Repeat steps 7-9.
1. Go to **System** > **Action Logs** .
1. Check the log for product update.

 <span class="wysiwyg-underline">Expected result</span> : Start date for the special price should be the current date.

 <span class="wysiwyg-underline">Actual result</span> : Start date for the special price is for a date a few years in the future, preventing the special price for being active.

## Solution

Applying the patch will prevent the issue from happening again. To correct the data for the products where date was set incorrectly, re-set the special price after applying the patch.

## Patch

The patch is attached to this article. To download it, scroll down to the end of the article and click the file name, or click the following link:

 [Download MDVA-11605\_EE\_2.2.2\_COMPOSER\_v1.patch](assets/MDVA-11605_EE_2.2.2_COMPOSER_v1.patch) 

### Compatible Magento versions:

The patch was created for:

* Magento Commerce 2.2.2

The patch is also compatible (but might not solve the issue) with the following Magento versions and editions:

* Magento Commerce 2.1.0-2.1.18, 2.2.0-2.2.5
* Magento Commerce Cloud 2.1.11-2.1.18, 2.2.0-2.2.5

## How to apply the patch

See [How to apply a composer patch provided by Magento](https://support.magento.com/hc/en-us/articles/360028367731) for instructions.

## Attached Files
