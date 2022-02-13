# Database

* All columns/fields names MUST follow [general naming convention](./general.md)
* Collections/tables names MUST be in plural form

## Postgres

* All column names MUST be in `snake_case` format
* All date columns with default value MUST use `CURRENT_TIMESTAMP(3)`
* All date columns MUST have date precisions of 3 digits after comma

## FAQ

** Why date columns must have precision of 3 digits **

For cursor pagination that paginates over a date field `Date` instance is being used and `Date` in JavaScript have
precision to milliseconds only therefore precision higher than 3 will make pagination not working properly.
