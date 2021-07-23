---
layout: docs
title: Deploy Badges
---

[Seed](/) generates deploy badges for each of the stages in your app. A deploy badge is a little image that reflects the deploy status of a given stage.

![Seed deploy badge](https://api.seed.run/jayair/serverless-project/stages/production/build_badge)

You can use these badges in your project's README, so people can get a sense of the current deploy status of the project.

To grab the markdown code snippet for a deploy badge, head over to your app settings.

![Seed deploy badge markdown code snippet in app settings](/assets/docs/deploy-badges/seed-deploy-badge-markdown-code-snippet-in-app-settings.png)

The code snippet will look something like this:

``` md
[![Seed Status](https://api.seed.run/jayair/serverless-project/stages/production/build_badge)](https://console.seed.run/jayair/serverless-project)
```

The first URL here generates the badge as an SVG, while the second URL simply links to the app on Seed. You'll notice that the badge is generated for a specific stage. You can customize this.

### Changing the stage 

By default, the badge points to your _production_ stage. But you can change this by using the name of the stage you'd like to generate the badge for.

Just customize the template below with the appropriate org, app, and stage name.

``` md
[![Seed Status](https://api.seed.run/{org_name}/{app_name}/stages/{stage_name}/build_badge)](https://console.seed.run/{org_name}/{app_name})
```

### Badge Styles

The deploy badge supports two different styles. The default style is the one that's commonly found across GitHub.

| Style | URL |
|-------|-------|-----|
| Default ![Seed default deploy badge](https://api.seed.run/jayair/serverless-project/stages/production/build_badge?style=default) | `https://api.seed.run/{org_name}/{app_name}/stages/{stage_name}/build_badge?style=default`
| Flat ![Seed flat deploy badge](https://api.seed.run/jayair/serverless-project/stages/production/build_badge?style=flat) | `https://api.seed.run/{org_name}/{app_name}/stages/{stage_name}/build_badge?style=flat`

Note that, if a style is not passed in, it'll use the default style.

