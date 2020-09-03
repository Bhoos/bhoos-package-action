## WorkFlow Steps :

1) build and test scripts are run
2) git config are setup with username Bhoos Action and email action@bhoos.com
3) package version is updated according to branch name i.e minor or patch so this workflow should be only triggered from those branches
4) setup to publish the package using github token provided from env GITHUB_PERSONAL_ACCESS_TOKEN, then  package is published
5) the update is then pushed to the current branch and the master branch
6) tags named nextv(nextVersion) is pushed
7) a draft release is created with above tag


## Example USAGE
```bash
name: Release  Package

on:
  push:
    branches:
      - minor
      - patch
jobs:
  package-release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: '10.x'
      - name: Setup package registry access
        uses: ./ # Uses an action in the root directory
        env:
          GITHUB_PERSONAL_ACCESS_TOKEN: ${{ github.token }}
      - name: check package
        run: |
          cat package.json
          git branch --show-current


```
