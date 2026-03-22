---
layout: post
title: Field Mapping in Salesforce Revenue Cloud
description: Learn how to map custom fields from Quote Line objects to Order Products in Salesforce Revenue Cloud using the Context Service.
date: 2025-02-04 14:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud]
featured:
video_embed:
---

# Introduction

This tutorial explains how to map custom fields from Quote Line objects to Order Products in Salesforce Revenue Cloud. The example uses an "Installation Date" field, but the process applies to any custom field.

## Prerequisites

- Custom fields must already exist on both Quote Line and Order Product objects
- Access to Salesforce Setup

## Configuration Steps

### Step 1: Navigate to Context Service

1. Go to Salesforce **Setup**
2. Use the Quick Find box to search for **Context Service**
3. Select **Context Definitions**

### Step 2: Edit Active Sales Transaction Context

1. Locate the **Active Sales Transaction Context** definition
2. Click **Edit**

### Step 3: Add Attributes

In the Attributes section of the context editor:

1. Navigate to the **Sales Transaction Item** node
2. Create a new attribute with these specifications:
   - **Name**: Installation Date (or your field name)
   - **Type**: Input and Output
   - **Data Type**: Date (match your field type)
3. Save the attribute
4. Create a matching tag with the same name

### Step 4: Map Quote Data

1. Access the **Map Data** tab within the context definition
2. Select **Quote Entities Mapping**
3. Locate **Sales Transaction Item** in the Unmapped Fields section (left side)
4. Match your field (e.g., "Installation Date") to the corresponding Quote Line Item field (right side)
5. Save the mapping

### Step 5: Map Order Data

1. Navigate to **Order Entities Mapping**
2. Find **Sales Transaction Item** under Unmapped Fields
3. Map your field to the corresponding Order Item field
4. Save changes

### Step 6: Test the Configuration

1. Create a Quote with your custom field populated (e.g., Installation Date)
2. Generate an Order from the Quote
3. Verify the Order Product contains the mapped field value

## Why Context Service Instead of Flows?

A common question: why use Context Service for field mapping instead of a Flow or Apex trigger? The Context Service is the correct architectural approach for Revenue Cloud because:

1. **It's part of the platform's data model**  -  Revenue Cloud's pricing and order pipeline reads from Context Service definitions, not from ad-hoc triggers
2. **It runs at the right time**  -  the mapping happens during order generation, before downstream processes fire
3. **It's declarative and visible**  -  the mapping is auditable through Setup rather than buried in Apex or Flow logic
4. **It scales**  -  the same approach works for any field type and both directions (quote-to-order and order-to-fulfillment)

Using Flows or triggers for this mapping often results in timing issues where the order product is created before the trigger fires, causing data to be missing on first creation.

## Common Use Cases

- **Installation Date**  -  capture when a customer wants service to start, flow it to the order for fulfillment
- **Contract Reference**  -  custom external contract ID that needs to appear on both quote and order
- **Billing Account**  -  custom billing entity field populated on the quote, needs to flow to the order product
- **Promo Code**  -  promotional code applied at quote time that should be recorded on the order product for billing logic

## Troubleshooting

If field values aren't flowing from quote to order, check these in order:

1. Confirm the attribute Type is set to **Input and Output** (not just Input or Output)
2. Verify the tag name exactly matches the attribute name (case-sensitive)
3. Check the Quote Entities Mapping  -  confirm the left-side Sales Transaction Item field is mapped, not just created
4. Ensure you've saved and re-activated the Context Definition after making changes
5. If the field is a custom field, confirm it's been added to both the `SalesTransactionItem` and `OrderItem` objects and deployed to the org

## Summary

Field mapping through the Context Service ensures custom data flows correctly from Quotes to Orders. This process can be repeated for any custom fields you need to sync between these objects. When something doesn't flow as expected, the most common fix is verifying the attribute type and the tag/attribute name match.
