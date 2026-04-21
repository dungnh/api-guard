# Contributing

## Local smoke test

Run this smoke test before opening a PR to verify the package installs and works in a fresh Laravel app.

### Laravel 13

```bash
rm -rf /tmp/api-guard-smoke-l13
composer create-project laravel/laravel /tmp/api-guard-smoke-l13 "^13.0" --no-interaction --prefer-dist
composer config repositories.apiguard path "/Users/DzungNguyen/www/api-guard" --working-dir=/tmp/api-guard-smoke-l13
composer require coliving/api-guard:@dev --no-interaction --with-all-dependencies --working-dir=/tmp/api-guard-smoke-l13
php -r "file_exists('/tmp/api-guard-smoke-l13/database/database.sqlite') || touch('/tmp/api-guard-smoke-l13/database/database.sqlite');"
php /tmp/api-guard-smoke-l13/artisan key:generate --ansi
php /tmp/api-guard-smoke-l13/artisan vendor:publish --provider="Chrisbjr\\ApiGuard\\Providers\\ApiGuardServiceProvider" --tag=config --force
php /tmp/api-guard-smoke-l13/artisan vendor:publish --provider="Chrisbjr\\ApiGuard\\Providers\\ApiGuardServiceProvider" --tag=migrations --force
php /tmp/api-guard-smoke-l13/artisan migrate --force
php /tmp/api-guard-smoke-l13/artisan api-key:generate
```

Expected result:
- `vendor:publish` copies `config/apiguard.php` and migrations successfully.
- `migrate` creates the `api_keys` table migration successfully.
- `api-key:generate` prints `An API key was created with the following key: ...`.

### Laravel 12 (optional)

```bash
rm -rf /tmp/api-guard-smoke-l12
composer create-project laravel/laravel /tmp/api-guard-smoke-l12 "^12.0" --no-interaction --prefer-dist
composer config repositories.apiguard path "/Users/DzungNguyen/www/api-guard" --working-dir=/tmp/api-guard-smoke-l12
composer require coliving/api-guard:@dev --no-interaction --with-all-dependencies --working-dir=/tmp/api-guard-smoke-l12
php /tmp/api-guard-smoke-l12/artisan api-key:generate
```
