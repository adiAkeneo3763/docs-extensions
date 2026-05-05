# Installation

There are two parts to the installation: first set up the **Magento 2 plugin**, then install the **UnoPim connector**.

## Part 1 — Magento 2 Plugin (ProductImportQueue)

This plugin must be installed on your Magento store first. It handles incoming product data from UnoPim.

### 1. Copy the plugin files

Extract the plugin ZIP. Move the `app` folder (found inside the `src` folder) into your Magento root directory.

### 2. Enable the module

```bash
php bin/magento module:enable Webkul_ProductImportQueue
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy
```

### 3. Flush cache and reindex

```bash
php bin/magento cache:clean
php bin/magento indexer:reindex
```
## Part 2 — UnoPim Connector

### 1. Place the package

Unzip the connector and merge the `packages` folder into your UnoPim project root.

### 2. Register the service provider

Open `bootstrap/providers.php` and add:

```php
use Webkul\Magento2\Providers\Magento2ServiceProvider;

return [
    // ...existing providers...
    Magento2ServiceProvider::class,
];
```

### 3. Update Composer autoload

In `composer.json`, add under `autoload.psr-4`:

```json
"Webkul\\Magento2\\": "packages/Webkul/Magento2/src"
```

### 4. Run the installer

```bash
composer dump-autoload
php artisan magento-package:install
php artisan optimize:clear
```

### 5. Verify

A **Magento 2 icon** should now appear in the left sidebar of your UnoPim dashboard.


## Optional — Register Test Cases

Only needed if you plan to run the connector's test suite.

**a) Register the test directory** in `composer.json` under `autoload-dev.psr-4`:

```json
"Webkul\\Magento2\\Tests\\": "packages/Webkul/Magento2/tests"
```

**b) Add the test case** to `tests/Pest.php`:

```php
uses(Webkul\Magento2\Tests\Magento2TestCase::class)
    ->in('../packages/Webkul/Magento2/tests');
```

**c) Register the test suite** in `phpunit.xml`:

```xml
<testsuite name="Magento2 Feature Tests">
    <directory suffix="Test.php">./packages/Webkul/Magento2/tests/Feature</directory>
</testsuite>
```

**d) Create a testing environment file:**

```bash
cp .env .env.testing
```

Open `.env.testing` and update `APP_URL` to your UnoPim base URL.

**e) Run the tests:**

```bash
composer dump-autoload
php artisan optimize:clear
./vendor/bin/pest ./packages/Webkul/Magento2/tests/Feature
```