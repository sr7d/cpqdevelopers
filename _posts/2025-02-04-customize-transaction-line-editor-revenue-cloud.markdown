---
layout: post
title: Customize the Transaction Line Editor in Revenue Cloud
description: Step-by-step instructions for customizing the columns and fields displayed in the Transaction Line Editor for quotes and orders.
date: 2025-02-04 13:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud]
featured:
video_embed:
---

# Introduction

The Transaction Line Editor is a key component in Salesforce Revenue Cloud that enables users to view and edit line items on quotes and orders. This guide covers how to customize the displayed columns to match your business requirements.

## Step-by-Step Instructions

### 1. Access the Page Editor

1. Navigate to an existing quote or order record in Salesforce
2. Click the **gear icon** in the top right corner
3. Select **Edit Page** from the dropdown menu to open Lightning App Builder

### 2. Locate the Transaction Line Editor Component

1. Find the Transaction Line Editor component in the page layout
2. Click on it to open the properties pane on the right side

### 3. Modify the Displayed Columns

1. Click the **Select** button below the Display Columns section
2. Find desired fields in the available fields list
3. Use the arrow buttons to move fields into the selected fields area
4. Use the up/down arrows to arrange fields in your preferred order
5. Click **OK** when satisfied with the configuration

### 4. Preview and Save Changes

1. Review the editor preview to verify the new column configuration
2. Click **Save** at the top right to apply changes
3. Activate the layout if needed for relevant profiles or apps

### 5. Verify the Changes

Return to your quote or order page to confirm that:
- New columns appear in the specified order
- Fields are editable as configured

## Common Fields to Add

The Transaction Line Editor supports both standard and custom fields. Commonly added columns include:

- **Start Date / End Date**  -  for subscription line items
- **Quantity**  -  often shown but not editable by default on orders
- **Unit Price** / **Net Price**  -  for inline price visibility during quoting
- **Discount**  -  if reps need to apply line-level discounts during quoting
- **Product Description**  -  helpful for reps who need product context while configuring
- **Custom fields**  -  any field on the `SalesTransactionItem` or `OrderItem` object you've added for your business

## Profile and App-Level Activation

After saving your customized layout in Lightning App Builder, you need to activate it. Activation options:

- **Activate for all users**  -  applies the new layout org-wide
- **Activate for specific profiles**  -  useful when different roles need different column sets (e.g., sales reps vs. order management)
- **Activate for specific apps**  -  target the layout to the Revenue Cloud Sales app while leaving other apps unchanged

If your changes aren't showing up for certain users, check that the layout is activated for their profile and app context. This is the most common reason customizations don't appear.

## Limitations to Know

- The Transaction Line Editor is a standard Lightning Web Component. Deep customization beyond column selection (custom cell renderers, conditional formatting, etc.) requires custom LWC development.
- Some fields from related objects (like Product2 fields) may not be directly selectable  -  you'll need formula fields on the SalesTransactionItem object to surface them.
- Changes to column configuration don't affect the underlying data model; they only change what's visible in the UI.

## Summary

Customizing the Transaction Line Editor allows teams to tailor the interface to match specific business requirements for managing line items on quotes and orders. The key steps  -  accessing Lightning App Builder, selecting the component, adjusting display columns, and activating for the right profiles  -  take under 15 minutes once you know where to look.
