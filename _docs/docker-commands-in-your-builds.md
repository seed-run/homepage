---
layout: docs
title: Docker Commands in Your Builds
---

You can run Docker commands as a part of your build process by adding them to your [build spec]({% link _docs/adding-a-build-spec.md %}). However, Docker is not enabled by default.

### Enable Docker

To enable Docker:

- You'll need to be on one of our [paid plans]({% link pricing.html %}).
- Your builds need to be using one of our [General Purpose build images]({% link _docs/seed-build-images.md %}#build-images).

[Contact us](mailto:{{ site.email }}) and let us know which service needs to have it enabled.

### Running LocalStack on Seed

Once you've got Docker enabled, you can run tests using [LocalStack](https://github.com/localstack/localstack) on Seed by adding something like the following in your `seed.yml`.

``` yml
before_compile:
  - >
    docker run -d --rm
    -p 4567-4608:4567-4608
    -e DOCKER_HOST=unix:///var/run/docker.sock
    -v /tmp/localstack:/tmp/localstack
    -v /var/run/docker.sock:/var/run/docker.sock
    localstack/localstack
```

Read more about [the build spec options here]({ link _docs/adding-a-build-spec.md %}).
