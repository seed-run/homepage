---
layout: docs
title: Integrating with JFrog
---

To use [JFrog Artifactory](https://jfrog.com/artifactory/) with the npm registry you just need to add the following to your [build spec]({% link _docs/adding-a-build-spec.md %}) (`seed.yml`): 

``` yml
before_compile:
  - echo "registry=https://<ARTIFACTORY_SERVER_DOMAIN>/artifactory/api/npm/npm-repo/" >> ~/.npmrc
  - echo "_auth=<AUTH_CODE>" >> ~/.npmrc
  - echo "email=<YOUR_ACCOUNT_EMAIL>" >> ~/.npmrc
  - echo "always-auth=true" >> ~/.npmrc
```

Where, to get the `AUTH_CODE` you need to run the following:

``` bash
$ curl -u<USERNAME>:<CREDENTIAL> https://<ARTIFACTORY_SERVER_DOMAIN>/artifactory/api/npm/npm-repo/auth
```

Here the `CREDENTIAL` can either be your password or your API key.

Also, `YOUR_ACCOUNT_EMAIL` is the admin email for your JFrog account. And `ARTIFACTORY_SERVER_DOMAIN` is the custom domain you've configured for Artifactory.
