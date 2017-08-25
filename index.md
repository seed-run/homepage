---
layout: lander
description: Simplest way for teams to build and deploy Serverless apps
---

<div class="header">
  <h1><a href="/">Seed</a></h1>
  <h4>Simplest way for teams to<br /> build and deploy Serverless apps</h4>
  <a class="action" href="{{ site.console_url }}{{ site.beta_signup }}">Sign up for the beta</a>
</div>

<div class="hero">
  <div class="video">
    <div class="bar">
      <span></span>
      <span></span>
      <span></span>
    </div>
    <video
      loop
      muted
      preload
      playsinline
      webkit-playsinline
      poster="assets/hero.png"
      onclick="videoClick(this)"
    >
      <source src="assets/hero.mp4" type="video/mp4">
    </video>
  </div>
</div>

<div class="pitch">
  <h4>Nothing to configure. Nothing to install.</h4>
  <p>Seed is a fully-configured code pipeline for building and deploying Serverless apps on AWS. Simply add your GitHub repository and IAM credentials and your entire team can `git push` to deploy updates to your Serverless app.</p>
  <p>Here is how it works.</p>
</div>

<div class="flow">
  <div class="line"></div>

  <div class="section github">
    <div class="action">
      Push your code to GitHub
    </div>
    <div class="disc">
      <i class="fa fa-github"></i>
    </div>
  </div>

  <div class="divider">
    <div class="logo">SEED</div>
  </div>

  <div class="section tests">
    <div class="action">
      Run your tests
    </div>
    <div class="disc">
      <i class="fa fa-check-circle"></i>
    </div>
  </div>

  <div class="section package">
    <div class="action">
      Package a verified build
    </div>
    <div class="disc">
      <i class="fa fa-cogs"></i>
    </div>
  </div>

  <div class="divider">
    <div>Your AWS</div>
  </div>

  <div class="section dev">
    <div class="action">
      Deploy to staging
    </div>
    <div class="disc">
      <i class="fa fa-paper-plane-o"></i>
    </div>
  </div>

  <div class="section production">
    <div class="action">
      Promote to production
    </div>
    <div class="disc">
      <i class="fa fa-paper-plane"></i>
    </div>
  </div>
</div>

<div class="features-intro">
  <a class="action" href="{{ site.console_url }}{{ site.beta_signup }}">Sign up for the beta</a>
  <p>A few other things you get out of the box.</p>
  <div class="caret">&#9663;</div>
</div>

<div class="features">

  <div class="feature">
    <h2>Unlimited Stages</h2>
    <p>Create a new stage by pointing to a branch in your repository. Each stage automatically gets it’s own endpoint and you can create as many as you like.</p>
    <div class="video">
      <video
        loop
        muted
        preload
        playsinline
        webkit-playsinline
        poster="assets/stages.png"
        onclick="videoClick(this)"
      >
        <source src="assets/stages.mp4" type="video/mp4">
      </video>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2>Encrypted Secrets</h2>
    <p>Secrets can be securely stored via the <a href="{{ site.console_url }}" target="_blank">Seed Console</a> without having to add them to the `serverless.yml`. They are encrypted using your <a href="https://aws.amazon.com/kms/" target="_blank">AWS KMS</a> keys.</p>
    <div class="video">
      <video
        loop
        muted
        preload
        width="640"
        playsinline
        webkit-playsinline
        onclick="videoClick(this)"
        poster="assets/secrets.png"
      >
        <source src="assets/secrets.mp4" type="video/mp4">
      </video>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2>Stage Variables</h2>
    <p>Stage variables are automatically supported and don’t need any configuration. Just reference them by the stage name in your `serverless.yml`.</p>
    <div class="video">
      <video
        loop
        muted
        preload
        width="640"
        playsinline
        webkit-playsinline
        poster="assets/envs.png"
        onclick="videoClick(this)"
      >
        <source src="assets/envs.mp4" type="video/mp4">
      </video>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2>1-Click Rollback</h2>
    <p>Rollback to any of your previously verified production builds through the <a href="{{ site.console_url }}" target="_blank">Seed Console</a> with just one click</p>
    <div class="video">
      <video
        loop
        muted
        preload
        width="640"
        playsinline
        webkit-playsinline
        onclick="videoClick(this)"
        poster="assets/rollback.png"
      >
        <source src="assets/rollback.mp4" type="video/mp4">
      </video>
    </div>
  </div>

</div>

<div class="pricing">
  <h4>Pricing</h4>
  <div class="table">
    <span>Coming soon</span>
  </div>
</div>

<div class="faq">
  <h4>Frequently Asked Questions</h4>
  <ul>
    <li>
      <p>
        Why not just use `serverless deploy`?
      </p>
      <p>
        The deploy command is great when you are working alone but as a part of a team, it does not make sense to grant IAM access to everybody for the production resources. By using Seed’s workflow you can ensure that only verified builds get promoted to production.
      </p>
    </li>


    <li>
      <p>
        What is a verified build?
      </p>
      <p>
        Seed auto-detects and runs any tests your project has. If the tests pass then a build is created for the current stage. It also creates and stores a build for the production stage. This verified build is deployed to production once you decide to promote it.
      </p>
    </li>

    <li>
      <p>
        Where is my Serverless project hosted?
      </p>
      <p>
        The build process is run on our side, while the Serverless project is deployed to your AWS account using your credentials. This ensures that even in the unlikely event of an outage on our side, you’ll still be able to access your API endpoints. We also use your AWS KMS key to encrypt your secrets.
      </p>
    </li>
    <li>
      <p>
        How many concurrent builds can I run?
      </p>
      <p>
        You can create unlimited stages with unlimited concurrent builds using Seed. And you’ll only be charged for the time it takes your builds to run.
      </p>
    </li>
    <li>
      <p>
        Which environments do you support?
      </p>
      <p>
        We currently support <a href="https://serverless.com/framework/" target="_blank">Severless Framework</a> Node.js projects on AWS with GitHub as a source repository. If there are any other environments you’d like us to support, feel free to let us know!
      </p>
    </li>
  </ul>
  <p>Feel free to contact us if you have any questions using the message button or via <a href="mailto:{{ site.email }}">email</a>.</p>
</div>

<div class="closing">
  <p><span class="logo">Seed</span> is created by the trusted folks behind <a target="_blank" href="http://serverless-stack.com">Serverless-Stack.com</a>,<br /> the best resource for building serverless apps on AWS.</p>
  <a class="action" href="{{ site.console_url }}{{ site.beta_signup }}">Sign up for the beta</a>
</div>
