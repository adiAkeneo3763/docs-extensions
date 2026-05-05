# Installation

## Shopify API Credentials

Before installing, you need a Shopify custom app with an **Admin API access token**.

### 1. Create a custom app in Shopify

1. Go to your Shopify admin → **Settings → Apps → Develop apps**.
2. Click **Create an app**, enter a name, and choose a developer.
3. Click **Configure Admin API scopes** and enable **read and write** for:

| Scope                | Permissions                                           |
|----------------------|-------------------------------------------------------|
| Shop locales         | `write_locales`, `read_locales`                       |
| Fulfillment services | `write_fulfillments`, `read_fulfillments`             |
| Inventory            | `write_inventory`, `read_inventory`                   |
| Product listings     | `write_product_listings`, `read_product_listings`     |
| Products             | `write_products`, `read_products`                     |
| Translation          | `write_translations`, `read_translations`             |
| Sales Channel        | `write_channels`, `read_channels`                     |
| Location             | `write_locations`, `read_locations`                   |
| Publications         | `write_Publications`, `read_Publications`             |

4. Click **Save**, then **Install app**.
5. Copy the **Admin API access token** from the **API credentials** tab.

## Connector Installation

### Option A — Composer (recommended)

```bash
composer require unopim/shopify-connector
php artisan shopify-package:install
php artisan optimize:clear
```

### Option B — Manual

1. Unzip the package, rename the folder to `Shopify`, and place it at:

```
packages/Webkul/Shopify
```

2. Register the service provider in `config/app.php`:

```php
Webkul\Shopify\Providers\ShopifyServiceProvider::class,
```

3. Add the autoload path in `composer.json` under `autoload.psr-4`:

```json
"Webkul\\Shopify\\": "packages/Webkul/Shopify/src"
```

4. Run:

```bash
composer dump-autoload
php artisan shopify-package:install
php artisan optimize:clear
```

### Verify

A **Shopify icon** should appear in the UnoPim sidebar after installation.