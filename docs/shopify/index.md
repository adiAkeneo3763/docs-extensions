# UnoPim Shopify Connector

The **UnoPim Shopify Connector** syncs your UnoPim product catalog with one or more Shopify stores. Export categories, simple products, and configurable products (with variants) from UnoPim to Shopify — and import Shopify data back into UnoPim.

## How it works

1. Install the connector and enter your Shopify API credentials in UnoPim.
2. Map UnoPim attributes to Shopify product fields under **Export / Import Mappings**.
3. Create an export or import job under **Data Transfer**.
4. Run the job — products, categories, images, and metafields are synced automatically.

## Key features

- Export categories as Shopify **Collections**.
- Export simple and configurable products (with variants).
- Transfer title, description, price, SKU, barcode, quantity, weight, and images.
- Map UnoPim attributes to Shopify fields with support for **fixed values**.
- Export product images via **Image** or **Gallery** media mapping.
- Map product units — weight, volume, and dimensions.
- Export in **multiple languages** (multi-locale support).
- Create and export **Shopify Metafield Definitions** directly from UnoPim.
- Connect **multiple Shopify stores** from one UnoPim instance.
- Import jobs for products, attributes, categories, family variants, and metafield definitions.
- Source code is open for customization.

## Requirements

| Requirement        | Version / Detail                    |
|--------------------|-------------------------------------|
| UnoPim             | >= 1.0.0                      |
| PHP       | <= 8.3 |
|Laravel    | 12.0 |


## In this guide

- [Installation](./installation.md)
- [Configuration](./configuration.md)
- [Usage](./usage.md)