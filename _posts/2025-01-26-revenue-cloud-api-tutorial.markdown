---
layout: post
title: Revenue Cloud API Tutorial - A Developer's Guide
description: A quick guide for developers working with Salesforce Revenue Cloud APIs. Learn authentication, key endpoints, code examples, and best practices for integrating with Revenue Cloud programmatically.
date: 2025-01-26 15:01:35 +0300
author: admin
image: /images/revCloudAPI.png
image_caption:
tags: [revenue-cloud,api,code]
featured:
video_embed:
---
# Revenue Cloud API Tutorial

Revenue Cloud is API-first—everything in the UI is accessible programmatically. This guide covers authentication, key APIs, and practical examples. All verified against [official documentation](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/rlm_get_started.htm).

**Postman Collections**: There's a [Subscription Management collection](https://www.postman.com/salesforce-developers/salesforce-developers/collection/b32utmu/salesforce-platform-apis) in the Salesforce Platform APIs ([setup guide](https://developer.salesforce.com/docs/revenue/subscription-management/guide/postmanSetup.html)). A comprehensive RLM collection hasn't been published yet. Legacy CPQ has a [separate collection](https://www.postman.com/salesforce-developers/workspace/salesforce-developers/folder/12721794-18c19817-3a82-4403-92bc-d96276452c77).

## Quick Reference

**API Versions** (minimum requirements):

| API | Min Version | Docs |
|-----|-------------|------|
| Pricing | 60.0 | [Link](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/pricing_business_apis.htm) |
| Transaction Management | 60.0 | [Link](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/qoc_business_apis.htm) |
| Product Catalog | 61.0 | [Link](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/product_catalog_management_business_api.htm) |
| Product Configurator | 61.0 | [Link](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/product_configurator_business_api_overview.htm) |

**Endpoint Pattern**: `/services/data/v65.0/connect/{service}/...`
- Pricing: `/connect/pricing/...`
- Quotes/Orders: `/connect/qoc/...`
- Catalog: `/connect/pcm/...`

## Authentication

Use OAuth 2.0 Bearer Token. [Full documentation](https://help.salesforce.com/s/articleView?language=en_US&id=sf.remoteaccess_oauth_web_server_flow.htm&type=5).

**Get an access token** (Username-Password flow for dev/testing):

```bash
curl -X POST https://login.salesforce.com/services/oauth2/token \
  -d "grant_type=password" \
  -d "client_id=YOUR_CONSUMER_KEY" \
  -d "client_secret=YOUR_CONSUMER_SECRET" \
  -d "username=YOUR_USERNAME" \
  -d "password=YOUR_PASSWORD_AND_SECURITY_TOKEN"
```

**Use the token** in all API calls:
```
Authorization: Bearer {access_token}
```

| Flow | Best For |
|------|----------|
| Username-Password | Dev/testing only |
| JWT Bearer | Production server-to-server |
| Named Credentials | Apex callouts (recommended) |

## Key APIs

### Transaction Management (Quotes & Orders)

Create quotes/orders with integrated pricing. [Docs](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/qoc_business_apis.htm)

**Create a quote**:
```bash
curl -X POST https://yourinstance.salesforce.com/services/data/v65.0/connect/qoc/sales-transactions \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "transactionType": "Quote",
    "accountId": "001XXXXXXXXXXXX",
    "pricebookId": "01sXXXXXXXXXXXX",
    "lineItems": [{"productId": "01tXXXXXXXXXXXX", "quantity": 1}]
  }'
```

**Key endpoints**:
- [Place Sales Transaction](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/connect_resources_place_sales_transaction.htm) - Create quote/order
- [Create Order From Quote](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/actions_obj_create_order_from_quote.htm) - Convert quote
- [Initiate Amendment](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/actions_obj_amend_assets.htm) / [Renewal](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/actions_obj_renew_assets.htm) - Asset lifecycle

### Pricing Business APIs

Calculate prices, manage pricing recipes. [Docs](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/pricing_business_apis.htm)

- [Price Context](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/connect_resources_price_context.htm) - Create pricing context
- [Pricing Request](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/connect_resources_headless.htm) - Calculate prices
- [Pricing Input](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/connect_requests_core_pricing_input.htm) - Request format

### Product Configurator APIs

Headless configuration with rules and instant pricing. [Docs](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/product_configurator_business_api_overview.htm)

Capabilities: load/save instances, add/update/delete nodes, rule enforcement (Validate, Exclude, Require, Auto-Add), instant pricing, custom UI support.

### Product Catalog APIs

Serve catalog definitions. [Docs](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/product_catalog_management_business_api.htm) | [Data Model](https://developer.salesforce.com/docs/platform/data-models/guide/product-catalog-mgmt.html)

### ConnectApi (Apex)

Native Apex access to these APIs—no auth handling needed. [Docs](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/billing_connect_api_namespace.htm)

## Rate Limits

Standard Salesforce limits apply. [Full reference](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm)

| Limit | Value |
|-------|-------|
| Daily requests (Enterprise) | 100K + 1K per license |
| Concurrent requests | 25 (5 for dev orgs) |
| Bulk API batches/day | 15,000 |

Check usage: `GET /services/data/v65.0/limits`

## Apex Example

```apex
public class RevenueCloudAPI {
    public static HttpResponse callAPI(String endpoint, String body) {
        HttpRequest req = new HttpRequest();
        req.setEndpoint(URL.getOrgDomainUrl().toExternalForm() + endpoint);
        req.setMethod('POST');
        req.setHeader('Authorization', 'Bearer ' + UserInfo.getSessionId());
        req.setHeader('Content-Type', 'application/json');
        req.setBody(body);
        return new Http().send(req);
    }
}
```

For production, use Named Credentials instead of `UserInfo.getSessionId()`.

## Troubleshooting

| Error | Solution |
|-------|----------|
| `401 Unauthorized` | Token expired—get new one |
| `400 Bad Request` | Check payload structure |
| `403 Forbidden` | Check permission sets |
| `404 Not Found` | Verify API version and IDs |

**Debug checklist**:
1. Test auth: `GET /services/data/v65.0/`
2. Verify API version is 60.0+
3. Check user has Revenue Cloud permissions
4. Use [Workbench](https://workbench.developerforce.com/) to test interactively

## Resources
- [Revenue Cloud Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.revenue_lifecycle_management_dev_guide.meta/revenue_lifecycle_management_dev_guide/rlm_get_started.htm)
- [Developer Guide PDF](https://resources.docs.salesforce.com/latest/latest/en-us/sfdc/pdf/revenue_lifecycle_management_dev_guide.pdf)
