# Eleos Charity

Eleos Charity based on top of Drupal Recipes

## Installation

If you are installing everything from scratch, we recommend [DDEV](https://ddev.com/) for
running Drupal.

1. Create a new project and configure it:
    ```
    mkdir eleos-charity
    cd eleos-charity
    ddev config --project-type drupal --docroot web --php-version 8.3
    ddev start
    ddev composer create drupal/recommended-project -y
    ddev composer require --dev drush/drush
    ddev composer config minimum-stability dev
    ddev drush site:install minimal --account-name=admin --account-pass=admin -y
    ddev composer require --dev drupal/core-dev
    ddev drush theme:enable claro
    ddev drush config-set system.theme default claro -y
    ddev snapshot --name=eleos_charity
    ```

2. Update composer.json to define a recipe path: Add to `installer-paths`:
    ```
    "web/recipes/contrib/{$name}": [
      "type:drupal-recipe"
    ],
    ```
3. Pull this recipe to your file system:
    ```
    ddev composer require systemseed/eleos_charity
    ```
4. Clear the cache:
    ```
    ddev drush cr
    ```
5. Install the recipe:
    To install only the "Commerce Base" recipe:
    ```
    ddev drush recipe recipes/contrib/eleos_charity/eleos_charity_commerce_base
    ```

    To install the full Eleos Charity recipe Suite:
    ```
    ddev drush recipe recipes/contrib/eleos_charity
    ```
6. Login and go to the ddev environment to the following path `https://eleos-charity.ddev.site/admin/commerce/config/stores` and ensure that `Default Store` was created automatically.
    ```
    ddev drush user:login
    ```
7. Configure `eleos-charity` recipe for contributions:
    ```
    rm -r web/recipes/contrib/eleos_charity
    git clone git@github.com:systemseed/eleos_charity.git web/recipes/contrib/eleos_charity
    ```
