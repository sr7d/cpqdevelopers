---
layout: post
title: How to create a product bundle in Salesforce Revenue Cloud
description: Learn the essentials of setting up a product in Salesforce Revenue Cloud. This guide takes you step by step through creating attribute picklists, assigning them to attributes, and organizing them into categories. We'll also cover how to build a product catalog with the necessary categories and product classifications, setting up your product management.
date: 2024-08-29 15:01:35 +0300
author: admin
image: /images/RevenueCloudProductConfig.png
image_caption: 
tags: [revenue-cloud,basics]
featured:
video_embed: 
---
# Part 1: Instructions

## Select the Product Catalog Management App
- **App Launcher** > **Product Catalog Management**

## Create Attribute Picklists with Attribute Picklist Values

### Color Picklist & Values:
1. **App Launcher** > **Product Catalog Management** > **Picklists** > **New**
2. **Name**: Color
3. **Status**: Active
4. **Data Type**: Text
5. **Save**
6. On the new record, select **Related** > **New Attribute Picklist Value**.
7. Create values for White, Blue, Pink, and save.

### Fabric Picklist & Values:
1. **App Launcher** > **Product Catalog Management** > **Picklists** > **New**
2. **Name**: Fabric
3. **Status**: Active
4. **Data Type**: Text
5. **Save**
6. On the new record, select **Related** > **New Attribute Picklist Value**.
7. Create values for Cotton, Polyester, and save.

### Garment Size Picklist & Values:
1. **App Launcher** > **Product Catalog Management** > **Picklists** > **New**
2. **Name**: Garment Size
3. **Status**: Active
4. **Data Type**: Text
5. **Save**
6. On the new record, select **Related** > **New Attribute Picklist Value**.
7. Create values for Small, Medium, and save.

## Create Attributes
1. **App Launcher** > **Product Catalog Management** > **Attributes** > **New**
2. Create attributes for Color, Fabric, Garment Size, Sock Size.
3. Assign the appropriate picklists and save.

## Create Attribute Categories

### Garment Attribute Category:
1. **App Launcher** > **Product Catalog Management** > **Attribute Categories** > **New**
2. **Name**: Garments
3. **Save**
4. Assign attributes: Color, Fabric, Garment Size.

### Sock Attribute Category:
1. **App Launcher** > **Product Catalog Management** > **Attribute Categories** > **New**
2. **Name**: Socks
3. **Save**
4. Assign attributes: Color, Fabric, Sock Size.

## Create a Catalog with Categories
1. **App Launcher** > **Product Catalog Management** > **Catalogs** > **New**
2. **Name**: Salesforce
3. **Save**
4. Create Categories: Bundle, Clothing, Accessories, and assign them to the catalog.

## Create Product Classifications & Assign Attributes

### Garment Product Classification:
1. **App Launcher** > **Product Catalog Management** > **Product Classifications** > **New**
2. **Product Classification Name**: Garment
3. **Save**
4. Assign attributes from the Garments category.

### Sock Product Classification:
1. **App Launcher** > **Product Catalog Management** > **Product Classifications** > **New**
2. **Product Classification Name**: Sock
3. **Save**
4. Assign attributes from the Socks category.

## Test your product:
1. Navigate to an opportunity or create a new one.
2. Create a quote and browse catalogs to view the newly created Salesforce catalog and categories.
