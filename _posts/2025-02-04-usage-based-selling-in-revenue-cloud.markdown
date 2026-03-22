---
layout: post
title: Usage-Based Selling in Salesforce Revenue Cloud
description: Step-by-step guide to configuring usage-based products in Salesforce Revenue Cloud, including rate management, usage resources, and tiered pricing.
date: 2025-02-04 17:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud]
featured:
video_embed:
---

# Introduction

This guide explains how to configure usage-based products in Salesforce Revenue Cloud. The example uses an evergreen subscription with included usage and tiered overage fees.

## Step 1: Enable Rate Management

1. Navigate to **Setup** > **Rate Management Settings**
2. Activate the **Rate Management** feature

## Step 2: Configure Rating Procedures

### Pricing Procedure

1. Access **Expression Set Templates**
2. Open **Default Rating Procedure**
3. Save as a new version to create your Pricing Procedure
4. Add Rank for execution order
5. Include all required steps and outputs
6. Activate the procedure

### Discovery Procedure

1. Open **Default Rating Discovery Procedure** template
2. Save as a new version for your custom Discovery Procedure
3. Assign Rank with required outputs
4. Activate the procedure

## Step 3: Set Revenue Settings

1. Go to **Revenue Settings** in Setup
2. Set **Usage Rating procedure** to Default Rating Discovery Procedure
3. Keep the procedure name unchanged for proper functionality

## Step 4: Create Usage-Based Product

1. Open **Product Catalog Management**
2. Create a new Commercial Product
3. Set **Model Type** to Anchor (required for overage charges)
4. Select your Selling Model (e.g., Evergreen Yearly)
5. Set the List Price (this is the base subscription price)
6. Add to a catalog and create a category

## Step 5: Define Units of Measure

1. Add a Type value to the **Unit of Measure** object
2. Create units (e.g., Kilometer as base, Megameter with conversion factor)
3. Group under a class with base and default unit specified

## Step 6: Set Up Usage Resource

1. Create a **Usage Resource** record
2. Specify the Unit of Measure
3. Link to your product
4. Define a **Usage Resource Billing Policy** with:
   - Accumulation method (e.g., Sum)
   - Billing period (e.g., Monthly)

## Step 7: Configure Product Usage Grant

1. Specify the included usage quantity (e.g., 10,000 kilometers annually)
2. Mark overages as chargeable
3. Set validity period (e.g., 12 months)

## Step 8: Create Rate Cards

### Base Rate Card

1. Create a Rate Card with Type = **Base**
2. Create a Rate Card Entry with your base overage rate (e.g., $0.50/km)
3. Set the effective date

### Tiered Rate Card

1. Create a Rate Card with Type = **Tier**
2. Add Rate Card Entries (leave Rate field blank for tiered)
3. Configure Rate Adjustments by Tier:
   - **Tier 1**: Usage range with adjustment amount
   - **Tier 2**: Higher usage range with larger discount
   - **Tier 3**: Highest usage range with maximum discount

## Step 9: Sync Decision Tables

Refresh the following to ensure records are active:
- Rate Adjustment by Tier Entries
- Rate Card Entries
- Price Book Rate Card Entries
- Rate Card Entry Resolutions
- Buy Tier Resolution Entries

## Step 10: Link Rate Cards to Price Books

Create **Price Book Rate Card** records linking both Base and Tiered Rate Cards to your price book.

## Step 11: Test the Setup

1. Add the product to a quote
2. Verify the included usage grant displays correctly
3. Confirm the overage rate and tiered adjustments apply as expected

## Summary

Usage-based products provide flexible, customer-friendly pricing models. Salesforce Revenue Cloud enables precise configuration of included usage, overage rates, and tiered pricing structures.
