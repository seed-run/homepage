---
layout: docs
title: Deploying With the Seed CLI
---

In addition to deploying through Git or [your CI]({%link _docs/connect-your-own-ci.md %}), you can trigger a deployment using the [**Seed CLI**]({{ site.cli_npm }}).

The Seed CLI allows you to decide when you want a deployment to be triggered in Seed. You could for example:

- Trigger a deployment to your serverless apps after you run your own CI/CD process.
- Or you can programmatically trigger a deployment anywhere in your workflow.

The Seed CLI allows you to better integrate Seed into your organization's workflow.

Let's look at how the Seed CLI works.

### Installation

The Seed CLI is available as an [npm package]({{ site.cli_npm }}).

You can install it by running:

``` bash
$ npm install -g @seed-run/cli
```

### Options

You simply need to pass in the:

- Org name `--org`
- App name `--app`
- Stage name `--stage`
- Git commit SHA `--commit`
- Force deploy even if there are no changes `--force`
- And a Seed CLI token as an environment variable `SEED_TOKEN`

For example, to deploy a specific commit to the `dev` stage of the `backend-api` app in the `acme` org.

``` bash
$ SEED_TOKEN=$ACME_ORG_TOKEN seed deploy \
  --org acme \
  --app backend-api \
  --stage dev \
  --commit 700b9c2
```

Where the `$ACME_ORG_TOKEN` is the Seed CLI token for the `acme` org.

Note that the commit doesn't need to be associated with any specific branch. You can deploy any commit that's available in Git.

### Seed CLI Token

You can generate a token for your org from your org settings.

![CLI token in the org settings](/assets/docs/deploying-with-the-seed-cli/cli-token-in-the-org-settings.png)

Make sure to secure access to this token as it allows the Seed CLI to trigger deployments to your organization.

You can also optionally remove the token and generate a new one if necessary.

![Remove CLI token in the org settings](/assets/docs/deploying-with-the-seed-cli/remove-cli-token-in-the-org-settings.png)

Note that, you can only create a single token per organization.
