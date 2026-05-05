
# Export Jobs

Navigate to:  
**Data Transfer → Exports → Create Export Profile**

### Available Export Types
- Magento Category
- Magento Attribute
- Magento Attribute Set
- Magento Product

## Recommended Export Order

1. Magento Attribute  
2. Magento Attribute Set  
3. Magento Product  

> Category export can be run anytime.


## Export: Categories

- Exports UnoPim categories with full hierarchy
- No channel-based filtering

**Steps:**
1. Create export profile
2. Select **Magento Category**
3. Click **Export Now**

## Export: Attributes

- Exports attributes and their options

**Filters:**
- Magento Store URL
- Store View
- Additional Attributes (optional)


## Export: Attribute Sets

- Exports attribute families as Magento attribute sets
- Maintains attribute groups

## Export: Products

- Exports simple and configurable products

**Filters:**

| Filter | Description |
|--------|------------|
| Store URL | Target Magento instance |
| Store Views | Store views to populate |
| Product Types | Simple / Configurable |
| Attribute Families | limited families |
| Product Status | Enabled / Disabled / All |
| With Media | Include images/videos |
| SKU | Export specific product |


# Export Logs

After execution:
- Click **Download Log**
- Use logs to debug missing or failed records

## Import Functionality

Navigate to:  
**Data Transfer → Imports → Create Import Profile**

Imports data from Magento into UnoPim.


## Supported Import Types

# 1. Magento Categories Import

**Purpose**: Import product categories from Magento to UnoPim

**When to Use**:
- Migrating category structure to UnoPim
- Keeping category hierarchy in sync

**What It Imports**:
- Category name and description
- Parent-child hierarchy
- Status (enabled/disabled)
- Auto-generated category codes (`{nameInCamelCase}_{magentoId}`)

**Key Features**:
- Supports multi-level categories
- Automatically creates missing parent categories
- Supports store view-specific data

## 2. Magento Categories Attribute Import

**Purpose**: Import category-specific attributes

**When to Use**:
- When categories have custom attributes in Magento
- Before importing categories with custom fields

**What It Imports**:
- Attribute definitions (name, type, options)
- Select, multiselect, checkbox options
- Attribute properties (required, filterable, etc.)

> Run this BEFORE category import if custom attributes exist

## 3. Magento Store View Mapping

**Purpose**: Map Magento store views to UnoPim channels

**When to Use**:
- Multi-store / multi-language setups
- Initial configuration before other imports

**What It Does**:
- Maps store views → channels
- Configures locale and currency
- Connects Magento structure with UnoPim

**Note**: Manual configuration required after import


## 4. Magento Attribute Sets Import

**Purpose**: Import attribute sets as UnoPim families

**When to Use**:
- When products use different attribute structures
- Before product import

**What It Imports**:
- Attribute set names and codes
- Attribute group structure

**Example**:
Magento sets like `Default`, `Clothing`, `Electronics` become UnoPim families.


## 5. Magento Attribute Groups Import

**Purpose**: Import attribute groups within sets

**When to Use**:
- To maintain attribute organization

**What It Imports**:
- Group names and positions
- Group-to-set relationships


## 6. Magento Attribute Import

**Purpose**: Import product attributes

**When to Use**:
- Before product import
- When Magento has custom attributes

**What It Imports**:
- Attribute codes, labels, and types
- Locale-based labels
- Attribute options
- Scope (global/store)

**Type Mapping Examples**:
- `text` → `text`
- `price` → `price`
- `select` → `select`

> Must run BEFORE product import


## 7. Magento Attribute Mapping Import

**Purpose**: Link attributes to attribute families

**When to Use**:
- After importing attributes and families
- To fix missing mappings

**What It Does**:
- Assigns attributes to families
- Places attributes in "Others" group
- Builds relationships between attribute, group, and family

**Note**: Often handled automatically during product import


## 8. Magento Simple Product Import

**Purpose**: Import simple products

**When to Use**:
- For standalone products without variants

**What It Imports**:
- SKU, name, price, status
- Custom attributes
- Categories
- Images and gallery

**Prerequisites**:
- Attributes imported
- Categories imported
- Attribute families exist


## 9. Magento Configurable Product Import

**Purpose**: Import configurable products (with variants)

**When to Use**:
- Products with variations (size, color, etc.)

**What It Imports**:
- Parent configurable product
- Variant attributes
- Child product associations

**Dependency**:
- Simple products must be imported first


## 10. Magento Product Association Import

**Purpose**: Sync product relationships

**When to Use**:
- After products are imported

**What It Updates**:
- Related products
- Upsell products
- Cross-sell products

> Does NOT create products, only updates relationships


## 11. Magento Store Import

**Purpose**: Import Magento stores as UnoPim channels

**When to Use**:
- Initial setup of channels

**What It Creates**:
- Channels from Magento stores
- Store-to-channel mappings
- Locales and currencies (auto-created if needed)


## Recommended Import Order

For smooth migration, follow this sequence:

1. **Magento Store View Mapping**
2. **Magento Store Import**
3. **Magento Categories Attribute Import**
4. **Magento Categories Import**
5. **Magento Attribute Import**
6. **Magento Attribute Sets Import**
7. **Magento Attribute Groups Import**
8. **Magento Attribute Mapping Import**
9. **Magento Simple Product Import**
10. **Magento Configurable Product Import**
11. **Magento Product Association Import**



## Notes

- Always follow the correct import order to avoid errors
- Logs should be reviewed after each import
- Mapping data is stored for future synchronization
- Supports multi-store and multi-locale setups


