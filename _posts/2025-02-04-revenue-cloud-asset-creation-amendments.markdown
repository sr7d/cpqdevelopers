---
layout: post
title: Asset Creation and Amendments in Salesforce Revenue Cloud
description: Learn how to create assets from orders and process amendments in Salesforce Revenue Cloud, including step-by-step instructions for managing customer agreements.
date: 2025-02-04 10:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud]
featured:
video_embed:
---

# Introduction

Managing asset lifecycles is a core function in Salesforce Revenue Cloud. This tutorial covers creating assets from quotes and orders, and processing amendments to existing assets.

## Asset Creation Process

### Step 1: Create an Order from a Quote

1. Start with a prepared quote containing all necessary products
2. Click the **Create Order** button
3. The system automatically inherits all products from the quote, including subscriptions and physical products

### Step 2: Activate the Order

1. Activate the newly created order
2. Upon activation, Salesforce's standard flow automatically creates assets from order products

**Note:** You can also use the provided Apex actions in custom flows to create assets at specific points in your business process.

### Step 3: View Created Assets

1. Navigate to the **Assets** tab under the associated Account
2. View the list of owned assets
3. Details include quantity and monthly recurring revenue (MRR) per asset

## Amendment Process

### Step 1: Initiate an Amendment

1. Select the asset requiring modification
2. Click **Amend** to create an amendment quote
3. The amendment quote reflects desired changes to existing asset terms

### Step 2: Adjust Details

1. Modify quantities or other agreement terms within the amendment quote
2. Specify additional quantities or service changes as needed

### Step 3: Finalize the Amendment

1. Create and activate a new order to apply changes
2. The process mirrors the initial asset creation
3. Asset records update to reflect the current engagement terms

## Review Amended Assets

### Verify Updated Quantities

Confirm the amended asset reflects accumulated changes. For example, if the original asset had 10,000 units and you added 5,000, the total should show 15,000 units.

### Dashboard Review

The asset dashboard displays:
- Quantity trends over time
- Impact on monthly recurring revenue
- Financial analysis of amendments

## Summary

Salesforce Revenue Cloud simplifies asset creation and amendment workflows, making it easier to manage customer agreements and adapt to changing customer needs.
