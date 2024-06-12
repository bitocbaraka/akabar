# akabar
RC versions
You can use specify a rc version to download it from https://nodejs.org/download/rc.

jobs:
  build:
    runs-on: ubuntu-latest
    name: Node sample
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '16.0.0-rc.1'
      - run: npm ci
      - run: npm test
Note: Unlike nightly versions, which support version range specifiers, you must specify the exact version for a release candidate: 16.0.0-rc.1.

Caching packages data
The action follows actions/cache guidelines, and caches global cache on the machine instead of node_modules, so cache can be reused between different Node.js versions.

Caching yarn dependencies: Yarn caching handles both yarn versions: 1 or 2.

steps:
- uses: actions/checkout@v4
- uses: actions/setup-node@v4
  with:
    node-version: '14'
    cache: 'yarn'
- run: yarn install --frozen-lockfile # optional, --immutable
- run: yarn test
Caching pnpm (v6.10+) dependencies:

# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# NOTE: pnpm caching support requires pnpm version >= 6.10.0

steps:
- uses: actions/checkout@v4
- uses: pnpm/action-setup@v2
  with:
    version: 6.32.9
- uses: actions/setup-node@v4
  with:
    node-version: '14'
    cache: 'pnpm'
- run: pnpm install
- run: pnpm test
