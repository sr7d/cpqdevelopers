---
layout: post
title: How to Create Products in Salesforce Revenue Cloud
description: A straightforward guide to creating products in Salesforce Revenue Cloud, from initial setup through testing on a quote.
date: 2025-02-04 11:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud,basics]
featured:
video_embed:
---

# Introduction

This guide walks through creating and testing products in Salesforce Revenue Cloud, enabling you to add items to quotes.

## Product Creation Steps

### 1. Initiate Product Creation

1. Navigate to **Product Catalog Management**
2. Select **Products**
3. Click **New**

### 2. Configure Product Details

- **Product Name**: Enter a descriptive name
- **SKU**: Assign a unique identifier
- **Status**: Set to Active
- **Assetizable**: Configure based on whether this product should create assets
- **Sell only with other products**: Leave unchecked if this product can be sold individually

### 3. Set Selling Model and Price

1. Define the selling model (one-time purchase or term-based)
2. Add the product to a price book
3. Assign a list price

### 4. Add to Catalog

1. Assign the product to a category within your catalog
2. Navigate to **Setup**
3. Search for **Salesforce Pricing Setup**
4. Click **Sync** to ensure pricing data is accessible for quoting

## Testing the New Product

### 1. Refresh and Browse Catalogs

1. Refresh the quote to ensure all data is current
2. Navigate to **Browse Catalogs**
3. Select the relevant catalog

### 2. Filter and Add the Product

1. Filter by the category where you added your product
2. Locate and add the product to your quote

### 3. Finalize and Save

1. Adjust quantity as needed
2. Apply discounts if applicable
3. Save the quote to verify pricing calculations

## Key Fields Explained

A few product fields that aren't self-explanatory:

**Assetizable**  -  controls whether placing an order for this product creates an Asset record. Set to `true` for subscription products you want to track as active assets (enabling amendments and renewals). Set to `false` for one-time charges or services that don't need lifecycle management.

**Selling Model**  -  determines how Revenue Cloud prices and bills the product:
- *One-time purchase*  -  single charge at order time
- *Term-based*  -  recurring charges over a contract term
- *Usage-based*  -  charges based on consumption (requires additional usage configuration)

**Sync after adding to Price Book**  -  the Sync step in Salesforce Pricing Setup is easy to miss. Revenue Cloud's pricing engine reads from an internal pricing cache, not directly from your price book records. Without syncing, your new product won't appear or price correctly in the configurator.

## Product Catalog Hierarchy

Products exist within a hierarchy: **Product Catalog → Category → Product**. Before creating a product, make sure the category you want to assign it to already exists in the catalog. If the category doesn't exist, you'll need to create it first  -  otherwise the product won't surface in Browse Catalogs.

## Common Issues After Product Creation

**Product appears in Product Catalog Management but not in Browse Catalogs:**
- The product Status may not be set to Active
- You may have skipped the Pricing Sync step
- The product may not be assigned to a category within the catalog
- The catalog may need to be refreshed

For a full troubleshooting checklist see: [Product Not Showing in Browse Catalogs](/revenue-cloud-product-not-showing-in-browse-catalogs/)

## Summary

Creating a product in Revenue Cloud involves four stages: defining the product record, setting the selling model and price, assigning it to a catalog category, and syncing pricing. Skipping the sync step is the most common reason a new product doesn't appear when quoting.
