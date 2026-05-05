# Export & Import Jobs

All jobs are managed under **Data Transfer** in the UnoPim sidebar.

## Export Jobs

Go to **Data Transfer → Exports → Create Export Profile**. Three export job types are available.

### Export Categories

Exports UnoPim categories as **Collections** in Shopify.

1. Enter a unique **Code**.
2. Set **Type** to `Shopify Category`.
3. Click **Save**, then **Export Now**.

### Export Products

Exports simple and configurable products (with variants) to Shopify.

1. Enter a unique **Code**.
2. Set **Type** to `Shopify Product`.
3. In the **Filters** panel, select:
   - **Shopify Credentials** — choose the target store
   - **Channel** and **Currency**
   - **SKU** (optional) — to export a single product
4. Click **Save**, then **Export Now**.

Monitor progress in the job tracker. On completion, the status shows **Completed** and a download log is available.

> **Note:** Inventory is added to Shopify on the **first export only**. Re-running the job updates product details but does not overwrite inventory.

### Export Metafield Definitions

Syncs metafield definitions created in UnoPim to Shopify.

1. Enter a unique **Code**.
2. Set **Type** to `Shopify Metafields Definition`.
3. Select **Shopify Credentials**.
4. Click **Save**, then **Export Now**.

## Import Jobs

Go to **Data Transfer → Imports → Create Import**. Five import job types are available.

### Import Products

| Field               | Value                          |
|---------------------|--------------------------------|
| **Type**            | `Shopify Product`              |
| **Credentials**     | Select your Shopify store      |
| **Channel / Locale / Currency** | Select as needed   |

### Import Attributes

| Field           | Value                |
|-----------------|----------------------|
| **Type**        | `Shopify Attribute`  |
| **Credentials** | Select store         |
| **Locale**      | Select locale        |

### Import Categories

| Field           | Value                         |
|-----------------|-------------------------------|
| **Type**        | `Shopify Category Import`     |
| **Credentials** | Select store                  |
| **Locale**      | Select locale                 |

### Import Family Variant Attribute Assignment

| Field             | Value                                              |
|-------------------|----------------------------------------------------|
| **Type**          | `Shopify Family Variant Attribute Assignment Import` |
| **Credentials**   | Select store                                        |
| **Locale**        | Select locale                                       |
| **Attribute Group** | Select group                                      |

### Import Metafield Definitions

| Field           | Value                           |
|-----------------|---------------------------------|
| **Type**        | `Shopify Metafield Definitions` |
| **Credentials** | Select store                    |
| **Locale**      | Select locale                   |

For all import jobs: fill in the fields, click **Save Import**, then run the job.