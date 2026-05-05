# Configuration

After installation, open the **Magento 2** section from the UnoPim sidebar to begin configuration.

## Credentials

The connector supports two authentication methods. Choose the one that fits your Magento setup.

### Option A — Token-Based Credentials (Recommended)

**Step 1 — Create an integration in Magento**

1. In your Magento admin, go to **System → Integrations → Add New Integration**.
2. Enter a **Name** and **Password**, then go to the **API** tab.
3. Set resource access to **All** (or select specific resources listed below), then click **Save**.
4. On the Integrations page, find your integration and click **Activate → Allow**.
5. Copy the generated **Access Token**.

Required API resources:

- Catalog, Inventory, Products, Categories
- Stores, Settings, Currency, Attributes, Other Settings

> **Note:** If your Magento version is 2.4.4 or above, run this command in your Magento root before proceeding:
> ```bash
> bin/magento config:set oauth/consumer/enable_integration_as_bearer 1
> ```

**Step 2 — Add credentials in UnoPim**

1. Go to **Magento 2 → Credentials → Create Token-Based Credentials**.
2. Enter your **Magento Shop URL** and **Access Token**.
3. Click **Save**.

---

### Option B — Login-Based Credentials

> **Note:** Login-based credentials will not work if Magento 2FA is enabled. Disable 2FA or use Token-Based instead.

1. Go to **Magento 2 → Credentials → Create Login-Based Credentials**.
2. Enter your **Magento Shop URL**, **Admin Username**, and **Admin Password**.
3. Click **Save**.

### Store Views

If your Magento store uses multiple store views, map each one to the correct UnoPim locale, channel, and currency after saving your credentials. Products will export to Magento using the channel and currency set for each store view.

> **Note:** When exporting attribute families, Magento creates new attribute sets based on an existing one. In your credential settings, select the **base attribute set** you want UnoPim families to be created from (default is "Default").


## Attribute Mapping

Go to **Magento 2 → Export Mappings**. There are four mapping types.

### Standard Attribute Mapping

Map UnoPim attributes to Magento's built-in product fields. The following fields are available by default:

| Magento Field              | Description                             |
|----------------------------|-----------------------------------------|
| `status`                   | Enable/disable product                  |
| `sku`                      | Product SKU                             |
| `name`                     | Product name                            |
| `price`                    | Product price                           |
| `description`              | Full product description                |
| `short_description`        | Short description                       |
| `weight`                   | Product weight                          |
| `product_has_weight`       | Whether product has weight              |
| `tax_class_id`             | Tax class                               |
| `visibility`               | Storefront visibility                   |
| `qty`                      | Stock quantity                          |
| `is_in_stock`              | Stock status                            |
| `url_key`                  | Product URL                             |
| `meta_title`               | SEO page title                          |
| `meta_keyword`             | SEO keywords                            |
| `meta_description`         | SEO meta description                    |
| `cost`                     | Cost of goods                           |
| `special_price`            | Sale price                              |
| `special_from_date`        | Sale start date                         |
| `special_to_date`          | Sale end date                           |
| `news_from_date`           | "New" badge start date                  |
| `news_to_date`             | "New" badge end date                    |
| `country_of_manufacture`   | Country of manufacture                  |
| `product_websites`         | Magento websites to assign product to   |
| `page_layout`              | Product page layout                     |
| `options_container`        | Display product options setting         |
| `custom_design_from`       | Schedule update start                   |
| `custom_design_to`         | Schedule update end                     |
| `custom_design`            | Custom theme                            |
| `custom_layout`            | Custom layout                           |

### Additional Field Mapping (Custom Attributes)

Use this section to map any custom Magento attributes that are not in the standard list above. Enter the Magento attribute code and select the corresponding UnoPim attribute.

This is also where you map variant-specific attributes like **Color** and **Size** for configurable products.

### Image Mapping

| Field | Required | Description |
|---|---|---|
| **Image Attributes** | Required | Select UnoPim image attributes — these become the Magento product gallery images |
| **Alt Text Attribute** | Optional | Select the attribute whose value will be used as the image alt text |
| **Image Role** | Optional | Map images to Magento roles: base, small, thumbnail, or swatch |
| **Hide from Product Page** | Optional | Toggle whether the image is hidden on the product page |

### Video Mapping

| Field | Required | Description |
|---|---|---|
| **Video Attribute** | Required | Map the UnoPim attribute that holds the video URL |
| **Preview Image** | Optional | Map an image to show as the video thumbnail |
| **Title** | Required | Map the attribute used as the video title |
| **Description** | Optional | Map an attribute for the video description |
| **Hide from Product Page** | Optional | Toggle visibility on the product page |

### Category Mapping

Map UnoPim category fields to Magento category fields. If no mapping is set, the connector exports categories with name, URL key, and enabled status only. Add mappings here to export additional category data.