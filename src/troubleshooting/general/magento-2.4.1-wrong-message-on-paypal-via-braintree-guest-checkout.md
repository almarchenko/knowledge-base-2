---
title: Magento 2.4.1 wrong message on Paypal via Braintree guest checkout
labels: .
---

This article describes a known Magento 2.4.1 issue where if guest checkout is disabled, a guest customer trying to place an order with PayPal through Braintree gets a non-informative error message.

## [None](#affected-products-and-versions) Affected products and versions

* Magento Commerce 2.4.0, 2.4.1
* Magento Commerce Cloud 2.4.0, 2.4.1

## [None](#issue) Issue

When guest checkout is disabled from the backend, and the PayPal through Braintree payment option is selected from the minicart or shopping cart, an unspecific error is shown.

Prerequisites:

1. In Magento Admin, under **Stores** > **Configuration** > **Sales** > **Checkout** , set **Allow Guest Checkout** = *No* .
1. Enable PayPal through Braintree as described in [Braintree](https://docs.magento.com/user-guide/payment/braintree.html?) section of Magento User Guide.

Steps to reproduce:

1. Add product to cart as a guest.
1. Select Minicart and click **Pay with PayPal** .
1. Complete the Paypal checkout, and then you will land on the Order Review page.
1. Select shipping method.
1. Click **Place Order** .

Expected result When a customer clicks on the PayPal button on mini-cart or on the Shopping Cart page, the following message should be displayed to the customer:

<pre>To check out, please sign in with your email address.</pre>

<clipboard-copy>
</clipboard-copy>

If you enable direct Paypal without using Braintree, this scenario behaves differently. It doesn't allow the guest user to continue with the payment process. It will show the following message when the guest user clicks on PayPal button in the minicart:

<pre>To check out, please sign in with your email address.</pre>

<clipboard-copy>
</clipboard-copy>

Actual resultThe customer is redirected to the Shopping Cart page and shows the following message:

<pre>The customer email is missing. Enter and try again.</pre>

<clipboard-copy>
</clipboard-copy>

## [None](#workaround) Workaround

The workaround for this issue is the customer can log in at a store instead (Logged-in users do not use guest checkout.) where guest checkout is disabled.This issue is scheduled to be resolved in Magento version 2.4.2, which is scheduled for release in Q1 1. \#\# Related reading

* [Best practice for number of products in cart in Magento](https://support.magento.com/hc/en-us/articles/360048550332)
* DevDocs [Order processing tutorial: Step 1. Add items to the cart](https://devdocs.magento.com/guides/v2.4/rest/tutorials/orders/order-add-items.html) 
* DevDocs [GraphQL checkout tutorial: Step 1. Add products to the cart](https://devdocs.magento.com/guides/v2.4/graphql/tutorials/checkout/checkout-add-product-to-cart.html) 

