---
layout: post
title: Salesforce Revenue Cloud - Free Trial & Setup Guide (RLM)
description: This Salesforce Revenue Cloud setup guide walks you through starting a free trial and configuring essential features like product catalogs, pricing models, and discounting structures. Follow these steps to explore Revenue Cloud’s powerful capabilities in managing revenue lifecycles and customer pricing.
date: 2024-10-31 15:01:35 +0300
author: admin
image: /images/revCloudTrial.png
image_caption: 
tags: [revenue-cloud]
featured:
video_embed: 
---
# Salesforce Revenue Cloud Trial Setup Guide

Are you seeking a comprehensive guide on how to create a developer org, sign up for a free trial, or set up a Trailhead environment to explore **Salesforce Revenue Cloud**? You’ve come to the right place! This detailed guide will walk you through the necessary steps to explore with the features of **Revenue Cloud** (RLM) from Salesforce.

## Setup Steps

### Step 0: Sign Up for a Free Trial

To begin, we will sign up for a free trial of Salesforce Communications Cloud. Currently, this is the only way to access the new features of Revenue Cloud. We will then enable the essential features to use Revenue Cloud within this Org.

<div style="margin-top: 20px; margin-bottom: 20px;">
  <label for="trial-email" style="font-weight: bold;">Email:</label>
  <input type="email" id="trial-email" name="trial-email" placeholder="your.email@company.com" style="width: 100%; padding: 10px; margin-top: 5px;">
  <span id="email-error" style="color: red; display: none; margin-top: 5px; font-size: 14px;">Please enter a valid business email address.</span>
</div>

<a href="#" class="button button--primary" onclick="handleTrialSubmit(event)">
    Start Free Trial
</a>

<!-- Hidden Web-to-Lead Form -->
<form id="web-to-lead-form" action="https://webto.salesforce.com/servlet/servlet.WebToLead?encoding=UTF-8&orgId=00Da500001Nhn69" method="POST" target="hidden_iframe" style="display:none;">
  <input type="hidden" name="oid" value="00Da500001Nhn69">
  <input type="hidden" name="retURL" value="http://">
  <input type="hidden" name="lead_source" value="cpqdevelopers.com/free-revenue-cloud-trial">
  <input type="hidden" id="lead-email" name="email" value="">
</form>
<iframe name="hidden_iframe" style="display:none;"></iframe>

After signing up, check your email for a message from Salesforce. Follow the instructions to complete the new login process (including setting your password). Once logged in, copy the Base URL from your new trial org and paste it in the field below. This will allow us to provide direct links to the setup pages, saving you time navigating through the settings.

<div style="margin-top: 20px; margin-bottom: 40px;">
  <label for="base-url" style="font-weight: bold;">Enter Your Org Base URL:</label>
  <input type="text" id="base-url" name="base-url" placeholder="https://your-instance.salesforce.com" style="width: 100%; padding: 10px; margin-top: 5px;" onblur="updateUrls()" required>
</div>

### Step 1: Contract Lifecycle Management

![Setting Contract Lifecycle Management](/images/settingsCLM.png)
<div class="dynamicLinkDiv" id="clm-url-container"><a id="clm-url" target="_blank">Setup / Contract Lifecycle Management / General Settings</a></div>

1. Enable **Salesforce Contracts**  
2. Enable **Customer Community Plus for Salesforce Contracts**  
3. Enable **Context Service for Salesforce Contracts**

### Step 2: Pricing Waterfall

![Setting Price Waterfall](/images/settingPriceWaterfall.png)
<div class="dynamicLinkDiv" id="waterfall-url-container"><a id="waterfall-url" target="_blank">Setup / Salesforce Pricing / Salesforce Pricing Setup</a></div>

1. Enable **Turn On Price Waterfall**  
2. Enable **Turn On Price Waterfall Persistence**

### Step 3: Document Generation

![Setting Document Generation](/images/settingsDocGen.png)
<div class="dynamicLinkDiv" id="docgen-url-container"><a id="docgen-url" target="_blank">Setup / Document Generation / General Settings</a></div>

1. Enable **Salesforce Contracts Connector for Word (Microsoft 365)**  
2. Enable **Document Templates Export**  
3. Enable **Design Document Templates in Salesforce**

### Step 4: Dynamic Revenue Orchestrator

![Setting Dynamic Revenue Orchestrator](/images/settingsRevOrch.png)
<div class="dynamicLinkDiv" id="revenue-orch-url-container"><a id="revenue-orch-url" target="_blank">Setup / Dynamic Revenue Orchestrator / Dynamic Revenue Orchestrator Settings</a></div>

1. Enable **Dynamic Revenue Orchestrator**

### Step 5: Service Process Definition Settings

![Setting Service Process Definition Settings](/images/settingsServiceProcess.png)
<div class="dynamicLinkDiv" id="service-process-url-container"><a id="service-process-url" target="_blank">Setup / Process Automation / Service Process Definition Settings</a></div>

1. Enable **New Service Process Definition Sync**

## Congratulations!

Your trial org is now ready to go! Keep in mind that it will expire after 30 days, and you will need to repeat this process for a new org. If you found this article helpful, please share it with others who may benefit from it!

<script>
  function isBusinessEmail(email) {
    // List of common personal email domains to block
    const personalDomains = [
      'gmail.com', 'yahoo.com', 'hotmail.com', 'outlook.com', 'aol.com',
      'icloud.com', 'mail.com', 'protonmail.com', 'zoho.com', 'yandex.com',
      'gmx.com', 'live.com', 'msn.com', 'me.com', 'inbox.com',
      'yahoo.co.uk', 'hotmail.co.uk', 'gmail.co.uk', 'outlook.co.uk'
    ];

    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(email)) {
      return false;
    }

    const domain = email.split('@')[1].toLowerCase();
    return !personalDomains.includes(domain);
  }

  function handleTrialSubmit(event) {
    event.preventDefault();

    const emailInput = document.getElementById('trial-email');
    const emailError = document.getElementById('email-error');
    const email = emailInput.value.trim();

    if (!email || !isBusinessEmail(email)) {
      emailError.style.display = 'block';
      emailInput.style.borderColor = 'red';
      return false;
    }

    // Hide error if previously shown
    emailError.style.display = 'none';
    emailInput.style.borderColor = '';
    
    // Set the email in the hidden form
    document.getElementById('lead-email').value = email;

    // Submit the Web-to-Lead form
    document.getElementById('web-to-lead-form').submit();

    // Open the trial signup page in a new tab
    window.open('https://www.salesforce.com/form/signup/comms-cloud-learning-trial/', '_blank');

    return false;
  }

  function updateUrls() {
    const baseUrl = document.getElementById("base-url").value.trim();
    console.log('baseURL: ',baseUrl);
    if (baseUrl) {
      document.getElementById("clm-url").href = `${baseUrl}/lightning/setup/ClmGeneralSettings/home`;
      document.getElementById("clm-url").style.color = 'blue';
      document.getElementById("clm-url").style.textDecoration = 'underline';

      document.getElementById("waterfall-url").href = `${baseUrl}/lightning/setup/CorePricingSetup/home`;
      document.getElementById("waterfall-url").style.color = 'blue';
      document.getElementById("waterfall-url").style.textDecoration = 'underline';

      document.getElementById("docgen-url").href = `${baseUrl}/lightning/setup/GeneralSettings/home`;
      document.getElementById("docgen-url").style.color = 'blue';
      document.getElementById("docgen-url").style.textDecoration = 'underline';

      document.getElementById("revenue-orch-url").href = `${baseUrl}/lightning/setup/DynamicFulfillmentOrchestratorSetupNode/home`;
      document.getElementById("revenue-orch-url").style.color = 'blue';
      document.getElementById("revenue-orch-url").style.textDecoration = 'underline';

      document.getElementById("service-process-url").href = `${baseUrl}/lightning/setup/ServiceProcessPrefSettings/home`;
      document.getElementById("service-process-url").style.color = 'blue';
      document.getElementById("service-process-url").style.textDecoration = 'underline';
    } 
  }
</script>

<style>
  .dynamicLinkDiv{
    margin-bottom: 20px;
  }
</style>
