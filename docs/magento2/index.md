# Overview

The UnoPim Magento 2 Connector connects your UnoPim PIM system with one or more Magento 2 (Adobe Commerce) stores.

It supports **two-way data synchronization**:
- Export data from UnoPim → Magento  
- Import data from Magento → UnoPim  

This eliminates manual data entry and keeps both systems in sync.

## How it Works

### Export (UnoPim → Magento)
1. Install the ProductImportQueue plugin on Magento.
2. Install the connector on UnoPim.
3. Add Magento credentials in UnoPim.
4. Configure mappings (attributes, categories, media, etc.).
5. Create and run export jobs.

### Import (Magento → UnoPim)
1. Configure Magento credentials in UnoPim.
2. Go to **Data Transfer → Imports**.
3. Create an import profile.
4. Select import type and run the job.

## Key Features

### General
- Two authentication methods (API token or admin login)
- Multi-store support
- Bi-directional sync (Import + Export)

### Export Features
- Category export with hierarchy
- Attribute & attribute family export
- Simple & configurable product export
- SEO data export (meta title, keywords, description)
- Media export (images & videos)
- Advanced filtering (SKU, status, family, type)
- Custom attribute mapping
- Product re-sync support

### Import Features
- Category import with hierarchy
- Attribute and attribute options import
- Attribute set and group import
- Product import (simple & configurable)
- Product association import (related, upsell, cross-sell)
- Store view and configuration import
- Automatic entity mapping

## Requirements

| Requirement | Detail |
|------------|--------|
| UnoPim | <= 2.0.0 |
| PHP | 8.2+ |
| Magento 2 | 2.3.x to latest |
| Node & Yarn | Required |
| Magento Cron | Must be running |

