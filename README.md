# ESN Packaging

Packaging ESN using FPM and Docker.

## Build

The gitlab-ci.yml file does a curl to the openpaas-build-package repository with right arguments to launch a build using Docker in Docker such as:

```sh
curl -s -X POST
  -F "token=${BUILD_PACKAGE_CI_TOKEN}"
  -F "ref=master"
  -F "variables[PACKAGING_REPO]=https://ci.linagora.com/linagora/lgs/openpaas/esn-linux-packaging.git"
  -F "variables[PACKAGING_BRANCH]=master"
  -F "variables[REPO]=https://ci.linagora.com/linagora/lgs/openpaas/esn.git"
  -F "variables[REPO_BRANCH]=master"
  -F "variables[VERSION]=1.8.0"
  -F "variables[PACKAGE_NAME]=openpaas"
  -F "variables[DOCKERFILE]=debian/jessie/openpaas/Dockerfile"
  https://ci.linagora.com/api/v4/projects/338/trigger/pipeline | jq .
```

Where:

- `PACKAGING_REPO`: The repo to clone to get the build assets. This is the current repository?
- `PACKAGING_BRANCH`: The branch to use in the packaging repo
- `REPO`: The ESN repository to clone and build
- `REPO_BANCH`: The ESN repository branch to use
- `DOCKERFILE`: The Dockerfile to use in the `PACKAGING_REPO` to build ESN package
- `VERSION`: The version of the package to generate
- `PACKAGE_NAME`: The package name

**BUILD_PACKAGE_CI_TOKEN** is defined at the gitlab level and used to reach the API. Check it with your Gitlab manager.
