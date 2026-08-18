# WPML Settings

The WooCommerce WPML addon adds a dedicated **WPML Export Settings** section inside the Attribute Mapping tab of any WooCommerce credential. These settings control how the addon routes export data through WPML's multi-locale pipeline instead of the standard single-locale WooCommerce export.

You must configure these settings before running any WPML export job.

## Step 1 — Open the Credential's Attribute Mapping Tab

Navigate to:

`WooCommerce → Credentials`

Select the credential you want to use for WPML exports, then click the **Attribute Mapping** tab.

Scroll down until you reach the **WPML Export Settings** section.

![Attribute Mapping Tab — WPML Export Settings](assets/mapping/wpml-settings.png)

## Step 2 — Enable WPML Export

The first field in the WPML Export Settings section is **Enable WPML Export**.

| Field | Type | Description |
|---|---|---|
| Enable WPML Export | Toggle (on/off) | When switched **on**, all exports using this credential will go through WPML multi-locale mode. When switched **off**, the connector falls back to the standard single-locale WooCommerce export. |

Toggle the switch to the **on** position to activate WPML mode for this credential.

![Enable WPML Export Toggle](assets/mapping/wpml-enable-toggle.png)

::: warning
Enabling WPML Export requires that the WPML plugin is installed and activated in the connected WordPress site. If WPML is not active, export jobs will fail.
:::

## Step 3 — Select the Default Locale

The second field is **Default Locale**.

| Field | Type | Description |
|---|---|---|
| Default Locale | Dropdown (single select) | The UnoPim locale that WPML treats as the **original** language. The product record for this locale is synced as the base product in WooCommerce. All other locales selected in an export job become WPML translations of that base product. |

Select the locale from the dropdown that matches the primary language of your WooCommerce store.

![Default Locale Dropdown](assets/mapping/wpml-default-locale.png)

::: info
The Default Locale must match one of the languages configured as the default language in the WPML Language Settings inside WordPress. Choosing a locale that is not registered as the WPML default language will cause WPML to reject the product as the base entry.
:::

## Step 4 — Save the Settings

After configuring both fields, click **Save** to store the WPML Export Settings.

These settings apply to all export jobs (categories, attributes, and products) that reference this credential.
