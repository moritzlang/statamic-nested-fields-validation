# Statamic Conditional Field Validation Bug Example

## Requirements

-   Laravel Valet ([Mac](https://laravel.com/docs/8.x/valet) or [Linux](https://cpriego.github.io/valet-linux/))

## Setup

1. `composer install` in the root of the project
2. `cp .env.example .env && php artisan key:generate`
3. Make a new user `php please make:user`
4. `cd public`
5. `valet link statamic-nested-fields-validation`
6. Open `http://statamic-nested-fields-validation.test`

## Bug description

Conditionally hidden required fields (using the [Validating Nested Fields](https://statamic.dev/validation#validating-nestable-fields) syntax with `sometimes` and `required`) always throw a validation error after reordering using the **collapsed** state in a `replicator_field`.

[Video showcasing the issue](https://imgur.com/a/suE4Zyp)

## How to reproduce

1. Open the "Home" page `http://statamic-nested-fields-validation.test/cp/collections/pages/entries/home`
2. Click "Collapse All" on the "Replicator Field"
3. Reorder the "Validation Set"
4. Save the page
5. A validation error for the field `bar` is thrown

### Error Response:

```json
{
    "message": "The given data was invalid.",
    "errors": {
        "replicator_field.0.bar": ["This field is required."]
    }
}
```
