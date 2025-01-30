---
layout: post
title: Product Configurator in Salesforce Revenue Cloud Advanced
description: Learn how to customize Salesforce RLM's Product Configurator, from modifying flows to assigning them to products, for a tailored and efficient configuration process.
date: 2025-01-24 15:01:35 +0300
author: admin
image: /images/ruminations.png
image_caption: 
tags: [revenue-cloud-advanced,rlm]
featured:
video_embed: 
---
# Introduction

The **Salesforce Revenue Lifecycle Management (RLM) Product Configurator** is a powerful tool designed to simplify and customize the process of configuring products within Salesforce. Whether you're managing simple products or complex bundles, the configurator provides flexibility and efficiency tailored to your organization’s needs.

In this guide, we’ll explore the following key aspects of the Product Configurator:
1. The standard configurator flow.
2. How to clone and customize the flow.
3. Assigning custom flows to products or product classifications.
4. Testing the updated configurations.

Let’s dive in!

## 1. The Standard Product Configurator Flow

The default Product Configurator in Salesforce RLM is accessible within the **Transaction Line Editor**. Here's how it works by default:

- **Accessing the Configurator:**  
  From the Transaction Line Editor, click the configure option on a product. This opens the configurator with:
  - **Product details** on the left.
  - **Attributes** in the center.
  - **Product options** grouped on the right.
  - A **Pricing Summary**, updated automatically if instant pricing is enabled or manually by clicking "Update Pricing."

- **Flow Structure:**  
  The configurator’s default flow operates through a single screen in the **Flow Editor**, designed as a template that cannot be directly modified. However, it can be cloned for customization.

## 2. Creating a Custom Product Configuration Flow

Customizing the configurator involves cloning the default template and tailoring it to your specific needs. Here’s how to create a custom flow:

### Step 1: Clone the Default Flow
- Open the default product configurator in the **Flow Editor**.
- Select **Save As** to create a new flow (e.g., "Demo Custom Flow").
- Save and open the cloned flow for editing.

### Step 2: Modify the Flow
- Use the Flow Editor to add or update components. For example:
  - Add a **Display Text** component with a message such as:  
    *"Please make sure to add Wheels to the car."*
- Customize the layout, add data mappings, or include new components to enhance functionality.

### Step 3: Activate the Custom Flow
- Save the updated flow and activate it.
- Note the flow’s **API Name** for use in the assignment step.

## 3. Assigning the Custom Flow to Products

To apply your custom flow, follow these steps:

### Step 1: Add the Flow to RLM
- Navigate to the **Product Configuration Flow** menu in Salesforce RLM.
- Create a new flow record:
  - Enter the API name of your custom flow.
  - Set the flow as **Active** but leave it as non-default unless you want it applied universally.

### Step 2: Assign the Flow to Specific Products
- Go to the **Product Configuration Flow Assignment** menu.
- Create a new record and:
  - Specify whether to assign the flow to a product classification or an individual product.
  - For example, assign it to the "Model Tree" product.

## 4. Testing the Updated Configuration

After assigning the custom flow:
1. Navigate back to the **Quote** page.
2. Reload the page to ensure the new configuration is applied.
3. Select the product, click **Configure**, and verify the customizations. For instance, the added message, *"Please make sure to add Wheels to the car,"* should now appear.

## Conclusion

The **Salesforce RLM Product Configurator** offers a flexible and customizable way to enhance user experience and streamline product configuration processes. By cloning and customizing the default flow, you can tailor the interface to meet your specific business requirements.

**Key Takeaways:**
- The default flow provides a solid starting point but is designed as a template.
- Cloning the flow allows full customization, including UI and logic updates.
- Assign custom flows to specific products or classifications for a targeted approach.

With these tools at your disposal, you can create a seamless and efficient configuration process that aligns with your organization’s needs. For further assistance or insights, feel free to reach out or explore additional Salesforce RLM resources!
