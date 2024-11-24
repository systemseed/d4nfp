# d4nfps
Drupal for non-for-profits based on top of Drupal Recipes

## Installation

If you are installing everything from scratch, we recommend [DDEV](https://ddev.com/) for
running Drupal.

1. Create a new project and configure it:
    ```
    mkdir drupal-charity
    cd drupal-charity
    ddev config --project-type drupal --docroot web --php-version 8.3
    ddev start
    ddev composer create drupal/recommended-project -y
    ddev composer require --dev drush/drush
    ddev composer config minimum-stability rc
    ddev drush site:install minimal --account-name=admin --account-pass=admin -y
    ddev composer require --dev drupal/core-dev
    ddev drush theme:enable claro
    ddev drush config-set system.theme default claro -y
    ddev snapshot --name=d4nfp
    ```

2. Update composer.json to define a recipe path: Add to `installer-paths`:
    ```
    "web/recipes/contrib/{$name}": [
      "type:drupal-recipe"
    ],
    ```
3. Pull this recipe to your file system:
    ```
    ddev composer require systemseed/d4nfp
    ```
4. Install the recipe:
    ```
    ddev drush recipe recipes/contrib/d4nfp
    ```
5. Login and go to the ddev environment to the following path `https://d4nfp.ddev.site/admin/commerce/config/stores` and ensure that `Default Store` was created automatically.
    ```
    ddev drush user:login
    ```
6. Configure `d4nfp` recipe for contributions:
    ```
    rm web/recipes/contrib/d4nfp
    git clone git@github.com:systemseed/d4nfp.git web/recipes/contrib/d4nfp
    ```
