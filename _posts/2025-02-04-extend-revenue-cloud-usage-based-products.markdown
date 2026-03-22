---
layout: post
title: Extend Salesforce Revenue Cloud for Usage-Based Products
description: Learn how to extend Salesforce Revenue Cloud to support usage-based products using custom configuration flows and Lightning Web Components.
date: 2025-02-04 15:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud]
featured:
video_embed:
---

# Introduction

Salesforce Revenue Cloud doesn't natively support all usage-based product scenarios out of the box. This guide explains how to extend RLM to support usage-based products (like pay-per-mile billing) using the Product Configurator and custom components.

## Implementation Steps

### Step 1: Set Up Your Product

1. Navigate to the **Product** object in Salesforce
2. Create or select your product (e.g., "Pay-per-Mile Service")
3. Enable a custom configurator by assigning it to the product record

### Step 2: Customize the Configuration Flow

1. Clone the default configuration flow to use as a base template
2. Add custom input fields such as:
   - Minimum Usage field (number type for baseline usage levels)
   - Consumption rate fields with lower/upper bounds
3. Define tiered pricing structures under the product configuration

### Step 3: Implement Data Transfer Flow

1. Create a flow triggered on quote line creation
2. Configure the flow to copy consumption rates from product to quote line
3. Use lookup fields linking consumption rates to both products and quote lines

### Step 4: Build Lightning Web Component (Optional)

For more complex scenarios:

1. Create an LWC with a data table component
2. Display and edit consumption rates during configuration
3. Save changes directly within the component

**Important:** Due to the custom footer used in product configuration, ensure that changes are saved directly rather than relying on post-screen flow processes.

### Step 5: Testing

1. Test the full configuration workflow from quote to transaction line editor
2. Verify minimum usage and rate modifications save correctly
3. Test any backend billing system integrations

## Summary

This approach combines point-and-click tools with minimal custom code to achieve flexible usage-based billing models within Revenue Cloud. The key is using custom configuration flows and ensuring data saves correctly during the configuration process.
