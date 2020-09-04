Provides a typical workflow for packages here at bhoos

## WorkFlow Steps:
### Push to minor and patch branch
1. Checkout repo
2. Setup, Test and Build
3. Prepare Patch or Minor release version
4. Commit and push update to respective branch and the latest branch
5. Publish update to github package registry as `next` version
6. Create a Draft Release for publishing to production

### Publish Draft Release 
1. Update package registry tag next to latest version to be used in production


## Example usage

```yml
  on:
    push:
      branches:
        - minor
        - patch
  release:
    types: [published]

  jobs:
    package-release:
      runs-on: ubuntu-latest
      steps:
        - name: Use Bhoos release action
          uses: bhoos/action-release@v1
          env:
            # use PERSONAL_ACCESS_TOKEN as secrets.GITHUB_TOKEN is limited to current repository
            NPM_PKG_GITHUB_TOKEN: ${{ secrets.PERSONAL_ACCESS_TOKEN }}

```
