# Config

* Use `@pallad/config` whenever possible. It is battle tested tool that gives great flexibility for bringing new
  datasources for configuration.
* Use `config` directory within each service to contain configuration files like `*.env`, `*.json`
* For `development.*` file you MUST have `development.*.dist` file to contain example configuration data
* Configuration for other environments files like `production` or `test` are allowed to exist in `config` directory but
  only non-secrets data could be stored.
    * That means no secrets are allowed to be stored in non-development configuration files
* Secrets for non-development environments MUST be stored in storages designed for storing secres like AWS SSM or some
  kind of encrypted storages
* Secrets for development MAY be stored outside configuration files
