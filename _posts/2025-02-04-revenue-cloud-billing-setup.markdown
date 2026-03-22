---
layout: post
title: Salesforce Revenue Cloud Billing Setup Guide
description: Complete setup guide for Salesforce Revenue Cloud Billing, including legal entity configuration, billing policies, tax setup, and invoice generation.
date: 2025-02-04 16:00:00 +0300
author: admin
image: /images/ruminations.png
image_caption:
tags: [revenue-cloud]
featured:
video_embed:
---

# Introduction

Salesforce Revenue Cloud Billing (available in Winter '25) streamlines invoice management with support for multiple legal entities and tax engine integration. This guide covers the complete setup process.

## Initial Configuration

### Permissions and Features

1. Assign **Billing Admin** and **Data Pipelines Base User** permission sets
2. Obtain the **Billing User** permission set license
3. Enable **Data Pipelines** in Setup
4. Activate **Billing** in Setup
5. Refresh the page to access the guided setup menu

## Guided Setup Components

### Legal Entity Creation

1. Navigate to the **Legal Entity** section
2. Provide company name and address
3. Save the record

Legal entities are essential for tying operations to billing and invoicing.

### Billing Policy Setup

1. Create a billing policy
2. Set the status to **Draft** initially
3. Leave the default billing treatment empty until treatments are created

### Billing Treatment

1. Create a billing treatment
2. Associate it with a legal entity and billing policy
3. Set status to **Draft** until treatment items are created
4. Define billing treatment items specifying:
   - Percentage to bill
   - Flat amount
   - Full amount

### Billing Settings Configuration

1. Define default values including billing context
2. Establish order entity mappings

## Tax Policy Configuration

1. Create a tax policy associated with your legal entity
2. Create a tax treatment linked to the tax policy
3. Activate the tax policy once both components exist

## Invoice Generation Process

### Payment Terms

1. Search for **Payment Terms** in Salesforce
2. Create a new payment term (e.g., "Net 30")
3. Add term conditions (e.g., 30 days duration)

### Billing Schedules

1. In **Flows**, activate the standard **Order to Billing Schedule** flow
2. This flow triggers billing schedule creation when orders are set to **Active**

### Invoice Creation

1. Set up an invoice scheduler (immediate or recurring)
2. Review invoices under **Invoice Batch Run**
3. Each product receives its own billing schedule
4. Post invoices directly from Salesforce

## Key Features

- Automatic conversion of negative invoice lines to credit memos
- Credit application to invoices
- Multiple legal entity support
- Tax engine integration capability

## Summary

Revenue Cloud Billing provides comprehensive invoicing capabilities. The setup process involves configuring legal entities, billing policies, tax policies, and invoice generation flows to create a complete billing workflow.
