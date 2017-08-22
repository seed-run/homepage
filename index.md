---
layout: lander
---

<div class="header">
  <h1><a href="/">Seed</a></h1>
  <h4>Zero configuration code<br /> pipeline for Serverless projects</h4>
  <a class="action" href="{{ site.console_url }}">Sign up for the beta</a>
</div>

<div class="hero">
  <div>
    <video
      loop
      muted
      preload
      width="800"
      playsinline
      webkit-playsinline
      poster="assets/hero-screen.png"
    >
      <source src="assets/hero.mp4" type="video/mp4">
    </video>
  </div>
</div>

<div class="pitch">
  <h4>Nothing to configure. Nothing to install.</h4>
  <p>Seed is a fully-configured code pipeline for building Serverless apps on AWS Lambda. Simply drop in your GitHub repo and IAM credentials and `git push` to deploy updates. Seed will run your tests and create verified builds that can be promoted to production with a single click.</p>
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
  <a class="action" href="{{ site.console_url }}">Sign up for the beta</a>
  <p>A few other things you get out of the box.</p>
  <div class="caret">&#9663;</div>
</div>

<div class="features">

  <div class="feature">
    <h2>Unlimited Stages</h2>
    <p>Simply create a new stage by pushing a new branch to master. Stages automatically get their own endpoint.</p>
    <div class="video">
    <video
      loop
      muted
      preload
      width="640"
      playsinline
      webkit-playsinline
      poster="assets/stages-screen.png"
    >
        <source src="assets/stages.mp4" type="video/mp4">
      </video>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2>Stage Variables</h2>
    <p>Stage variables are automatically supported without any configuration. Just reference them by the stage name in your `serverless.yml`.</p>
    <div class="video">
    <video
      loop
      muted
      preload
      width="640"
      playsinline
      webkit-playsinline
      poster="assets/envs-screen.png"
    >
        <source src="assets/envs.mp4" type="video/mp4">
      </video>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2>Encrypted Secrets</h2>
    <p>Secrets are encrypted using your AWS KMS keys and are available as evironment variables in your Lambda functions.</p>
    <div class="video">
    <video
      loop
      muted
      preload
      width="640"
      playsinline
      webkit-playsinline
      poster="assets/secrets-screen.png"
    >
        <source src="assets/secrets.mp4" type="video/mp4">
      </video>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2>1-Click Rollback</h2>
    <p>Rollback to any of your previously verified builds with one click.</p>
    <div class="video">
    <video
      loop
      muted
      preload
      width="640"
      playsinline
      webkit-playsinline
      poster="assets/rollback-screen.png"
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
      <p>How many concurrent builds can I run?</p>
      <p>You can run unlimited concurrent builds using Seed.</p>
    </li>
    <li>
      <p>Where is a Seed project hosted?</p>
      <p>The build process is hosted on our side, while the Serverless project is deployed to your AWS account. We also use your AWS KMS key to encrypt/decrypt your secrets.</p>
    </li>
    <li>
      <p>Which cloud providers does Seed support?</p>
      <p>We currently only support AWS.</p>
    </li>
    <li>
      <p>How does Seed run my tests?</p>
      <p>We use the `npm run test` command to run your tests.</p>
    </li>
    <li>
      <p>Are the build dependencies cached?</p>
      <p>Yes, we cache your build dependecies automatically.</p>
    </li>
  </ul>
</div>

<div class="closing">
  <p><span class="logo">SEED</span> is created by the trusted folks behind <a target="_blank" href="http://serverless-stack.com">Serverless-Stack.com</a>,<br /> the best resource for building serverless apps on AWS.</p>
  <a class="action" href="{{ site.console_url }}">Sign up for the beta</a>
</div>
