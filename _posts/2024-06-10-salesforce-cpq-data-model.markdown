---
layout: post
title: Salesforce CPQ Data Model - Primary Objects
description: This interactive diagram shows the core data model for Salesforce CPQ. Understanding these object relationships is essential for building custom solutions, writing integrations, and troubleshooting complex configurations.
date: 2024-06-10 10:00:00 +0300
author: admin
image: /images/cpqDataModel.png
hide_image: true
image_caption:
tags: [legacy-cpq, data-model]
featured:
video_embed:
permalink: /salesforce-cpq-data-model/
---
<style>
.drawsql-embed {
  position: relative;
  width: 100%;
  padding-bottom: 56.25%;
  height: 0;
  overflow: hidden;
  border-radius: 15px;
}
.drawsql-embed iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 0;
  border-radius: 15px;
}
</style>

<div class="drawsql-embed">
<iframe allowtransparency="true" allowfullscreen="true" scrolling="no" title="Embedded DrawSQL IFrame" src="https://drawsql.app/teams/no-team-163/diagrams/cpq-data-model/embed"></iframe>
</div>
<br>
## Key Objects

- **Quote (SBQQ__Quote__c)** — The main container for pricing and product selections
- **Quote Line (SBQQ__QuoteLine__c)** — Individual line items on a quote
- **Product (Product2)** — Standard Salesforce product object, extended by CPQ
- **Price Book Entry** — Links products to price books with list prices
- **Quote Line Group (SBQQ__QuoteLineGroup__c)** — Groups related quote lines together
