# NPM

## Scripts

### `test`

Runs all tests.

There is no distinguish between integration or unit tests. If you need to introduce it then you MUST use
following names for scripts:

* `test:unit` - unit tests
* `test:integration` - integration tests

### `lint`

Runs all linters.

This is not limited to code linters only so linters for markdown, package.json etc are allowed.

### `compile`

Compiles package.

Note this does NOT performs build of package. Most of the time packages are not built but rather compiled only.
Build is performed by CI and therefore build configuration setup is in CI.

### `start`

Starts **compiled** app.

This command does NOT set `NODE_ENV` env variable to `production` or any other value.

### `develop`

Starts app in `watch` mode which means the app should restart automatically on code change.

This command does NOT set `NODE_ENV` env variable to `development` or any other value.

### `prepack`

Special NPM's script. Here it should map to `npm run compile` command most of the time.
