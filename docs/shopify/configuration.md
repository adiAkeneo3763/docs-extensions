# Configuration

Navigate to the **Shopify** section in the UnoPim sidebar to access all configuration options.

## Credentials

Go to **Shopify → Credentials → Create Credentials**.

| Field                   | Description                                          |
|-------------------------|------------------------------------------------------|
| **Shopify URL**         | Your store URL (e.g., `your-store.myshopify.com`)   |
| **Admin API access token** | Token from your Shopify custom app              |
| **API Version**         | Select `API Version`                                     |

After saving, open the credential record to set:

| Field                        | Description                                                                  |
|------------------------------|------------------------------------------------------------------------------|
| **Publishing (Sales Channels)** | Which Shopify sales channels to publish products to                       |
| **Location List**            | Inventory location (must exist in Shopify first)                            |
| **Status**                   | Default product status: active or draft                                     |
| **Locale Mapping**           | All Shopify locales are fetched automatically — map them to UnoPim locales  |

> You can add multiple stores by repeating this step with separate credentials for each.

## Export Mapping

Go to **Shopify → Export Mappings**. Map each Shopify field to a UnoPim attribute.

| Shopify Field                      | Purpose                                  |
|------------------------------------|------------------------------------------|
| `title`                            | Product title                            |
| `descriptionHtml`                  | Product description (HTML supported)     |
| `price`                            | Selling price                            |
| `weight`                           | Shipping weight                          |
| `inventoryQuantity`                | Stock level                              |
| `inventoryTracked`                 | Enable inventory tracking                |
| `inventoryPolicy`                  | Allow/disallow out-of-stock purchases    |
| `vendor`                           | Brand or supplier                        |
| `productType`                      | Product category/type                    |
| `tags`                             | Search and filter keywords               |
| `barcode`                          | Barcode / GTIN                           |
| `compareAtPrice`                   | Original price (for sale display)        |
| `metafields_global_title_tag`      | SEO page title                           |
| `metafields_global_description_tag`| SEO meta description                     |
| `handle`                           | URL-friendly product slug                |
| `taxable`                          | Whether the product is taxable           |
| `cost`                             | Cost of goods (COGS)                     |

### Fixed Value

To apply the same value to a field across all exported products (e.g., quantity = `100`):

1. Clear the UnoPim attribute dropdown for that field.
2. Enter the value in the **Fixed Value** input that appears.

### Media Mapping

Set **Mapping Type** to **Media Mapping**, then choose a media type:

| Media Type | When to use |
|------------|-------------|
| **Image**  | Multiple separate image attributes (e.g., front, back, zoom) |
| **Gallery**| A single gallery-type attribute containing all product images |

### Unit Mapping

Located in **Export Mappings → Shopify Unit Mapping**.

| Unit Type      | Example values           |
|----------------|--------------------------|
| **Weight**     | g, kg, oz, lb            |
| **Volume**     | ml, l, cm³, in³          |
| **Dimension**  | cm, mm, inches           |

> For each unit, you can also create a corresponding Shopify Metafield Definition to store the unit value alongside the measurement.

## Import Mapping

Go to **Shopify → Import Mappings**. The available fields mirror the export mapping fields above.

**Family Mapping** — Under **Other Mapping**, select a product family (e.g., "Accessories") to ensure variants import correctly.

## Metafield Definitions

Go to **Shopify → Metafield Definitions → Add Definition**.

| Field                      | Description                                                         |
|----------------------------|---------------------------------------------------------------------|
| **Used For**               | Shopify entity: Products or Variants                                |
| **UnoPim Attribute**       | The UnoPim attribute linked to this metafield                       |
| **Type**                   | Single line text, Multi-line text, Color, Rating, URL, or JSON      |
| **Definition Name**        | User-friendly label (e.g., "Material")                              |
| **Namespace and Key**      | Unique Shopify identifier in `namespace.key` format (e.g., `custom.color`) |
| **Description**            | Optional internal notes                                             |
| **Min / Max Char Count**   | Enforce input length limits                                         |
| **Pin**                    | Show the metafield in the Shopify admin UI when editing products    |
| **Filtering for Products** | Use as a storefront filter                                          |
| **Smart Collections**      | Use as a rule in Shopify Smart Collections                          |
| **Storefront Access**      | Expose via Shopify Storefront API (required for headless themes)    |

## Tags Settings

Go to **Shopify → Settings**.

| Setting                         | Description                                                          |
|---------------------------------|----------------------------------------------------------------------|
| **Named Tags**                  | Include the attribute name as part of the exported tag               |
| **Pull Attribute Name in Tags** | Export name and value together                                        |
| **Attribute Name Separator**    | Separator between name and value: dash ( `-` ), colon ( `:` ), space |