---
layout: post
title: Custom Product Configuration Flows in Revenue Cloud
description: Learn how to clone and customize the default product configurator flow in Salesforce Revenue Cloud, and assign custom flows to specific products.
date: 2025-02-04 12:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud]
featured:
video_embed:
---

# Introduction

The Product Configurator in Salesforce Revenue Cloud provides flexibility for customizing how products are configured during the quoting process. This guide covers cloning the default configurator and assigning custom flows to products.

## Understanding the Standard Configurator

1. Access the **Transaction Line Editor** and locate your product
2. Click the arrow next to the product and select **Configure**
3. The default configurator displays:
   - Product details and attributes on the left
   - Pricing summary on the right
4. Pricing updates automatically or via the **Update Pricing** button if instant pricing is enabled

## Creating a Custom Flow

### Step 1: Clone the Default Flow

The default product configurator flow serves as a template and cannot be modified directly.

1. Navigate to the **Flow Editor** in Salesforce Setup
2. Locate the default product configurator flow
3. Click **Save As** to create a new flow from the template
4. Name your custom flow (e.g., "Custom Product Configuration Flow")

### Step 2: Modify Your Custom Flow

1. Add components in the Flow Editor:
   - Display text elements
   - Custom messages
   - Data mappings
2. Customize the interface by resizing components
3. Save and activate the flow
4. Note the **Flow API Name** from the flow's details page

## Assigning Your Custom Flow

### Step 1: Register the Flow in RLM

1. Navigate to the **Product Configuration Flow** tab in Revenue Cloud
2. Click **New** to create a new product configuration flow record
3. Enter the Flow API Name
4. Set the flow to **Active**
5. Do not set as default unless you want it applied to all products

### Step 2: Assign to Products

1. Go to the **Product Configuration Flow Assignment** tab
2. Create a new record
3. Select either a specific product or product classification
4. Save the record

## Testing Your Custom Flow

1. Return to the **Transaction Line Editor**
2. Reload the page to ensure the new configuration is applied
3. Select the assigned product and click **Configure**
4. Verify your custom messages and modifications display correctly

## Summary

- The default configurator flow cannot be modified directly; cloning is required
- The Flow API Name is essential for the assignment process
- Custom flows can be assigned to individual products or product classifications for targeted customization
