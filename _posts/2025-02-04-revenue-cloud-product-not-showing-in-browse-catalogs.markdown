---
layout: post
title: Product Not Showing in Browse Catalogs? Step-by-Step Fix Guide
description: Troubleshoot why your newly created product isn't appearing in the Browse Catalogs screen in Salesforce Revenue Cloud, with a complete checklist to resolve the issue.
date: 2025-02-04 09:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud]
featured:
video_embed:
gate: true
---

# Introduction

You've just created a new product in Salesforce Revenue Cloud. All the details are configured exactly as you want them. You navigate to a quote, click **Browse Catalogs**, select your catalog, find the category where you assigned your product... and it's not there.

This is one of the most common issues administrators encounter when setting up products in Revenue Cloud. The good news is that the fix is usually straightforward once you know what to check.

For general setup guidance, refer to the official [Set Up Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.set_up_revenue_cloud.htm&language=en_US&type=5) documentation.

## The Complete Product Visibility Checklist

Before diving into troubleshooting, let's walk through every setting that affects whether a product appears in Browse Catalogs. For an overview of product catalog concepts, see [Build Your Product Catalog in Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.product_catalog_introduction.htm&language=en_US&type=5).

### 1. Product Record Settings

On the Product record itself, verify:

- **Active** = TRUE
- **Sell only with other products** = FALSE

The "Sell only with other products" field is easy to overlook. When set to TRUE, the product is hidden from direct selection in Browse Catalogs. This setting is designed for products that should only be added as part of a bundle or as an option on another product.

For details on creating and configuring products, see [Create Products and Product Bundles in Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.product_catalog_products.htm&language=en_US&type=5).

### 2. Product Selling Model

Your product must have a **Product Selling Model Option** assigned. This defines how the product is sold (one-time, subscription, evergreen, etc.).

Navigate to the **Related** tab on your product record and confirm a Product Selling Model Option exists and is set as the default.

For detailed information on selling models, refer to:
- [Manage Product Selling Model in Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.product_catalog_product_selling_model.htm&language=en_US&type=5)
- [Create a Product Selling Model](https://help.salesforce.com/s/articleView?id=sf.product_catalog_create_a_product_selling_model.htm&language=en_US&type=5)
- [Assign a Product Selling Model to a Product](https://help.salesforce.com/s/articleView?id=sf.product_catalog_assign_a_product_selling_model_to_a_product.htm&language=en_US&type=5)

### 3. Pricebook Entry

The product must have an entry in the pricebook that's selected for your quote or order. Without a pricebook entry with a valid price, the product won't appear as available for selection.

For guidance on pricebook configuration, see:
- [Add a Price Book Entry](https://help.salesforce.com/s/articleView?id=ind.pricing_add_price_book_entry.htm&language=en_US&type=5)
- [Design Your Pricing Model in Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.pricing_salesforce_pricing.htm&language=en_US&type=5)

### 4. Catalog Category Assignment

This is where things can get confusing. Even if your product is active and priced correctly, it won't appear in Browse Catalogs unless it's assigned to a category within the catalog you're browsing.

On the Product record, check the **Related** tab and verify the product is assigned to a category. Then confirm that category belongs to the catalog you're selecting in Browse Catalogs.

For example, if you assigned your product to a "Wheels" category within a "Tesla 2024" catalog, you need to:
1. Select "Tesla 2024" as the catalog in Browse Catalogs
2. Navigate to or filter by the "Wheels" category

For detailed instructions on catalog and category setup, refer to:
- [Catalogs](https://help.salesforce.com/s/articleView?id=ind.product_catalog_catalogs.htm&language=en_US&type=5)
- [Assign Products to Catalog Categories in Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.product_catalog_assign_products_to_catalog_cat_and_subcategories.htm&language=en_US&type=5)

## The Missing Step: Sync Pricing Data

Here's the part that trips up most administrators. You can have everything configured correctly (active product, selling model assigned, pricebook entry created, catalog category assigned) and the product still won't appear.

**The solution: You need to sync the pricing data.**

After creating a product and adding it to a pricebook, Salesforce Revenue Cloud requires a sync to make the pricing information available for quoting. This is documented in [Sync Pricing Data in Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.pricing_sync_pricing_data.htm&language=en_US&type=5).

### How to Sync Pricing Data

1. Go to **Setup**
2. In the Quick Find box, search for **Pricing**
3. Select **Salesforce Pricing Setup**
4. Scroll down to the **Sync Pricing Data** section
5. Click **Sync**
6. Confirm the sync when prompted

The sync process runs in the background and may take several minutes to complete depending on the size of your product catalog. There's no progress indicator, so just give it time.

For additional pricing setup information, see [Salesforce Pricing Basic Setup](https://help.salesforce.com/s/articleView?id=ind.pricing_set_up_salesforce_pricing.htm&language=en_US&type=5).

### After the Sync Completes

1. Return to your quote
2. **Refresh the page** (this is important because the quote won't automatically detect new pricing data)
3. Click **Browse Catalogs**
4. Select your catalog
5. Navigate to the category where you assigned your product

Your product should now appear and be available for selection. You can add it to your quote and modify quantity, apply discounts, or configure it as needed.

For more on discovering and adding products, see [Discover and Configure Products](https://help.salesforce.com/s/articleView?id=ind.qocal_discover_and_configure_products.htm&language=en_US&type=5).

## For New Spring '25 Environments

If you're working in a newly provisioned Spring '25 environment and products still aren't appearing, ensure you've completed all the setup steps outlined in the [Get Started with Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.revenue_lifecycle_management_get_started.htm&language=en_US&type=5) guide. New environments may require additional configuration before the product catalog functions correctly.

Also review the [Revenue Cloud Release Notes](https://help.salesforce.com/s/articleView?id=release-notes.rn_revenue.htm&language=en_US&release=252&type=5) for any recent changes that may affect your setup.

## Rebuild the Product Index

For older or pre-configured organizations experiencing persistent issues, rebuilding the product index can help:

1. Navigate to **Setup**
2. Search for **Product Discovery Settings**
3. Enable **Use Indexed Data for Product Listing and Search**

This forces Salesforce to rebuild the index used for product search and filtering in Browse Catalogs.

## Quick Reference Checklist

Before reaching out for support, verify all of the following:

| Setting | Location | Required Value | Documentation |
|---------|----------|----------------|---------------|
| Active | Product record | TRUE | [Create Products](https://help.salesforce.com/s/articleView?id=ind.product_catalog_products.htm&language=en_US&type=5) |
| Sell only with other products | Product record | FALSE | [Create Products](https://help.salesforce.com/s/articleView?id=ind.product_catalog_products.htm&language=en_US&type=5) |
| Product Selling Model Option | Product > Related tab | Assigned and set as default | [Product Selling Model](https://help.salesforce.com/s/articleView?id=ind.product_catalog_product_selling_model.htm&language=en_US&type=5) |
| Pricebook Entry | Pricebook | Entry exists with valid price | [Add Price Book Entry](https://help.salesforce.com/s/articleView?id=ind.pricing_add_price_book_entry.htm&language=en_US&type=5) |
| Catalog Category | Product > Related tab | Assigned to category in target catalog | [Assign Products to Categories](https://help.salesforce.com/s/articleView?id=ind.product_catalog_assign_products_to_catalog_cat_and_subcategories.htm&language=en_US&type=5) |
| Pricing Sync | Setup > Salesforce Pricing Setup | Sync completed | [Sync Pricing Data](https://help.salesforce.com/s/articleView?id=ind.pricing_sync_pricing_data.htm&language=en_US&type=5) |

## Additional Resources

- [Learn About Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.revenue_lifecycle_management.htm&language=en_US&type=5)
- [Explore the Revenue Cloud Data Model](https://help.salesforce.com/s/articleView?id=ind.data_model_overview.htm&language=en_US&type=5)
- [Product Catalog Management Set Up](https://help.salesforce.com/s/articleView?id=ind.product_catalog_set_up_product_catalog_management.htm&language=en_US&type=5)
- [Configure Product Attributes in Revenue Cloud](https://help.salesforce.com/s/articleView?id=ind.product_catalog_configure_product_attributes.htm&language=en_US&type=5)

## Summary

When a product doesn't appear in Browse Catalogs, the issue is almost always one of these settings, most commonly a missing pricing sync. After creating or modifying products, always remember to sync pricing data and refresh your quote page before testing.
