---
layout: docs
title: Configuring Custom Domains
---

[Seed](/) can help you configure a custom domain for any of your stages in your project.

Here are a couple of things to ensure before setting it up:

1. [Migrate your domain to Amazon Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/MigratingDNS.html)

   Currently, Seed only supports the configuration of domains managed by Route 53. You can read more about migrating to Route 53 [here](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/MigratingDNS.html).

2. Ensure the IAM Policy has the appropriate permissions

   Seed does all the configuration on your behalf using the IAM Role assigned to it when you created the project. Just ensure to give it the appropriate set of permissions as outlined in the [Customizing your IAM Policy]({% link _docs/customizing-your-iam-policy.md %}) chapter.

To configure a stage with a custom domain, Seed will automatically create the SSL certificate using [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/) and assign the requested path and sub-domain to the API Gateway stage.

> Domains need to be managed by Amazon Route 53 for Seed to configure the custom domain

To configure the custom domain for a stage, head over to the **Settings** for the stage.

![Stage Settings](/assets/docs/configuring-custom-domains/stage-settings.png)

And select **Update Custom Domain**.

![Select update Custom Domain option Screenshot](/assets/docs/configuring-custom-domains/select-update-custom-domain.png)

Here you can pick the **sub-domain**, **domain**, and **base path** for the stage.

![Configure Custom Domain parts Screenshot](/assets/docs/configuring-custom-domains/configure-custom-domain-parts.png)

For example, to configure your stage to `api.example.com/prod`; you can set the **sub-domain** as `api`, pick `example.com` as your domain, and select `prod` as your **base path**.

![Configure Custom Domain parts Screenshot](/assets/docs/configuring-custom-domains/update-custom-domain-parts.png)

And hit **Update**. Updating the custom domain for a stage can take up to 40mins, since the SSL certificate and the API Gateway CloudFront Distribution need to be configured.

> Seed automatically configures the SSL Certificate and the API Gateway project

If you have any questions or are running into some issues configuring your custom domain; feel free to [contact us]({{ site.email }}).

A couple of quick notes on custom domains:

- Seed will let you know if the given base path is in use. In this case you'll need to disable the stage that is using the base path.

- If a stage is configured to the root base path (`/`); you will not be able to configure another stage with any other base path for that domain (or sub-domain). For example, if you have `api.example.com/` configured to a stage (where `/` is the base path). Then you will not be able to configure `api.example.com/prod` for any other stage.

Finally, you can disable the custom domain for a stage.

![Disable Custom Domain Screenshot](/assets/docs/configuring-custom-domains/disable-custom-domain.png)

Just hit the **Disable** button in the **Update Custom Domain** panel.
