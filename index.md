---
layout: lander
description: Simplest way for teams to build and deploy Serverless apps
---

<div class="header">
  <h1><a href="/">Seed</a></h1>
  <h4>Simplest way for teams to<br /> build and deploy Serverless apps</h4>
  <a class="action" href="{{ site.console_url }}{{ site.signup }}">Create a Free Account</a>
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
      onloadstart="videoLoadStart(this)"
      oncanplaythrough="videoCanPlayThrough(this)"
    >
      <source src="assets/hero.mp4" type="video/mp4">
      <img src="assets/hero.gif" />
    </video>
    <div class="overlay spinner" onclick="playClick(this)">
      <i class="fa fa-circle-o-notch fa-spin"></i>
    </div>
    <div class="overlay play" onclick="playClick(this)">
      <i class="fa fa-play"></i>
    </div>
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
  <a class="action" href="{{ site.console_url }}{{ site.signup }}">Create a Free Account</a>
  <p>A few other things you get out of the box.</p>
  <div class="caret">&#9663;</div>
</div>

<div class="features">

  <div class="feature">
    <h2 id="unlimited-stages">Unlimited Stages</h2>
    <p>Create a new stage by pointing to a branch in your repository. Each stage automatically gets it’s own endpoint and you can create as many as you like. <a class="more" href="/docs/adding-a-stage.html">Read more on working with stages</a>.</p>
    <div class="video">
      <video
        loop
        muted
        preload
        playsinline
        webkit-playsinline
        poster="assets/stages.png"
        onclick="videoClick(this)"
        onloadstart="videoLoadStart(this)"
        oncanplaythrough="videoCanPlayThrough(this)"
      >
        <source src="assets/stages.mp4" type="video/mp4">
        <img src="assets/stages.gif" />
      </video>
      <div class="overlay spinner" onclick="playClick(this)">
        <i class="fa fa-circle-o-notch fa-spin"></i>
      </div>
      <div class="overlay play" onclick="playClick(this)">
        <i class="fa fa-play"></i>
      </div>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2 id="stage-variables">Stage Variables</h2>
    <p>Stage variables are automatically supported and don’t need any configuration. Just reference them by the stage name in your `serverless.yml`. <a class="more" href="/docs/configuring-stage-variables.html">Learn more about stage variables</a>.</p>
    <div class="video">
      <video
        loop
        muted
        preload
        playsinline
        webkit-playsinline
        poster="assets/envs.png"
        onclick="videoClick(this)"
        onloadstart="videoLoadStart(this)"
        oncanplaythrough="videoCanPlayThrough(this)"
      >
        <source src="assets/envs.mp4" type="video/mp4">
        <img src="assets/envs.gif" />
      </video>
      <div class="overlay spinner" onclick="playClick(this)">
        <i class="fa fa-circle-o-notch fa-spin"></i>
      </div>
      <div class="overlay play" onclick="playClick(this)">
        <i class="fa fa-play"></i>
      </div>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2 id="preview-pull-requests">Preview Pull Requests<span>New</span></h2>
    <p>Pull requests are automatically built in Seed. They get their own unique endpoint and use the variables of the stage they are going to be merged into. <a class="more" href="/docs/working-with-pull-requests.html">More on working with pull requests</a>.</p>
    <div class="video">
      <video
        loop
        muted
        preload
        playsinline
        webkit-playsinline
        poster="assets/pull-request.png"
        onclick="videoClick(this)"
        onloadstart="videoLoadStart(this)"
        oncanplaythrough="videoCanPlayThrough(this)"
      >
        <source src="assets/pull-request.mp4" type="video/mp4">
        <img src="assets/pull-request.gif" />
      </video>
      <div class="overlay spinner" onclick="playClick(this)">
        <i class="fa fa-circle-o-notch fa-spin"></i>
      </div>
      <div class="overlay play" onclick="playClick(this)">
        <i class="fa fa-play"></i>
      </div>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2 id="encrypted-secrets">Encrypted Secrets</h2>
    <p>Secrets can be securely stored via the <a href="{{ site.console_url }}" target="_blank">Seed Console</a> without having to add them to the `serverless.yml`. They are encrypted using your <a href="https://aws.amazon.com/kms/" target="_blank">AWS KMS</a> keys. <a class="more" href="/docs/storing-secrets.html">Learn about how secrets are stored</a>.</p>
    <div class="video">
      <video
        loop
        muted
        preload
        playsinline
        webkit-playsinline
        poster="assets/secrets.png"
        onclick="videoClick(this)"
        onloadstart="videoLoadStart(this)"
        oncanplaythrough="videoCanPlayThrough(this)"
      >
        <source src="assets/secrets.mp4" type="video/mp4">
        <img src="assets/secrets.gif" />
      </video>
      <div class="overlay spinner" onclick="playClick(this)">
        <i class="fa fa-circle-o-notch fa-spin"></i>
      </div>
      <div class="overlay play" onclick="playClick(this)">
        <i class="fa fa-play"></i>
      </div>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2 id="review-changeset">Review Stack Changes<span>New</span></h2>
    <p>Review your infrastructure changes to double-check any irreversible updates that your Serverless project is about to deploy. <a class="more" href="/docs/promoting-to-production.html">Read more on promoting to production</a>.</p>
    <div class="video">
      <video
        loop
        muted
        preload
        playsinline
        webkit-playsinline
        poster="assets/changeset.png"
        onclick="videoClick(this)"
        onloadstart="videoLoadStart(this)"
        oncanplaythrough="videoCanPlayThrough(this)"
      >
        <source src="assets/changeset.mp4" type="video/mp4">
        <img src="assets/changeset.gif" />
      </video>
      <div class="overlay spinner" onclick="playClick(this)">
        <i class="fa fa-circle-o-notch fa-spin"></i>
      </div>
      <div class="overlay play" onclick="playClick(this)">
        <i class="fa fa-play"></i>
      </div>
    </div>
  </div>

  <hr />

  <div class="feature">
    <h2 id="1-click-rollback">1-Click Rollback</h2>
    <p>Rollback to any of your previously verified production builds through the <a href="{{ site.console_url }}" target="_blank">Seed Console</a> with just one click</p>
    <div class="video">
      <video
        loop
        muted
        preload
        playsinline
        webkit-playsinline
        poster="assets/rollback.png"
        onclick="videoClick(this)"
        onloadstart="videoLoadStart(this)"
        oncanplaythrough="videoCanPlayThrough(this)"
      >
        <source src="assets/rollback.mp4" type="video/mp4">
        <img src="assets/rollback.gif" />
      </video>
      <div class="overlay spinner" onclick="playClick(this)">
        <i class="fa fa-circle-o-notch fa-spin"></i>
      </div>
      <div class="overlay play" onclick="playClick(this)">
        <i class="fa fa-play"></i>
      </div>
    </div>
  </div>

</div>

<div class="comparison">
  <h4 id="comparison">How Do We Compare?</h4>
  <div>
    <div>
      <div>Circle/Travis CI</div>
      <div>vs</div>
      <div>Seed</div>
    </div>
    <table>
      <tbody>
        <tr>
          <td>Branch<br /> Endpoints</td>
          <td>Needs configurtation</td>
          <td>Included</td>
        </tr>
        <tr>
          <td>Pull Request<br /> Endpoints</td>
          <td>Needs configurtation<br /> and custom code</td>
          <td>Included</td>
        </tr>
        <tr>
          <td>Review<br /> Change Sets</td>
          <td>Custom code with a<br /> manual approval step</td>
          <td>Included</td>
        </tr>
        <tr>
          <td>Concurrent<br /> Builds</td>
          <td>Pay extra for concurrency</td>
          <td>Included</td>
        </tr>
        <tr>
          <td>Rollbacks</td>
          <td>Git revert and re-build</td>
          <td>Rollback to previous production builds</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<!--
<div class="testimonials">
  <h4 id="testimonials">From Our Customers</h4>
  <div class="list">
    <div class="testimonial">
      <h6>Amazing support</h6>
      <p>&ldquo;I just completed your tutorial on the Serverless stack, and it was fantastic. It was carefully thought out, well-written, and incredibly thorough. You guys rock!&rdquo;</p>
      <div>
        <img width="56" src="assets/spongebob.png" />
        <p>Daniel Chen</p>
        <p>CTO, <a href="https://myshyft.com">Shyft</a></p>
      </div>
    </div>
    <div class="testimonial">
      <h6>Saves a lot of time</h6>
      <p>&ldquo;This is the best and most comprehensive fullstack serverless tutorial available. Take the time to go through every step, you will learn a ton!&rdquo;</p>
      <div>
        <img width="56" src="assets/patrick.png" />
        <p>Patrick Star</p>
        <p>CEO, <a href="https://myshyft.com">Krabby Inc.</a></p>
      </div>
    </div>
    <div class="testimonial">
      <h6>Less things to worry about</h6>
      <p>&ldquo;Rarely do tutorials neatly break things down into bite-sized steps. Even rarer do they clearly explain what each step is for and why it is necessary. The Serverless-Stack is the Holy Grail that does all three.&rdquo;</p>
      <div>
        <img width="56" src="assets/sandy.png" />
        <p>Sandy Cheeks</p>
        <p>CEO, <a href="https://myshyft.com">Chum Bucket</a></p>
      </div>
    </div>
  </div>
</div>
-->

<div class="pricing">
  <h4 id="pricing">Pricing</h4>
  <div class="free-callout">
    <p>Get started for free</p>
    <ul class="features fa-ul">
      <li>
        <i class="fa-li fa fa-check"></i>
        15 deployments
      </li>
      <li>
        <i class="fa-li fa fa-check"></i>
        Unlimited users
      </li>
      <li>
        <i class="fa-li fa fa-check"></i>
        Unlimited projects
      </li>
      <li>
        <i class="fa-li fa fa-check"></i>
        Unlimited concurrent builds
      </li>
    </ul>
    <a class="action" href="{{ site.console_url }}{{ site.signup }}">Create a Free Account</a>
  </div>
  <div class="table">
    <div class="startup">
      <div class="cost">
        <p class="header">
          Startup
        </p>
        <div class="numbers">
          <p>$7</p>
          <p>per month</p>
        </div>
      </div>
      <ul class="features fa-ul">
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited users
        </li>
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited projects
        </li>
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited concurrent builds
        </li>
        <li>
          <i class="fa-li fa fa-long-arrow-right"></i>
          60 deployments
        </li>
        <li>
          <i class="fa-li fa fa-circle-thin"></i>
          Pay as you go
        </li>
      </ul>
    </div>
    <div class="standard">
      <div class="cost">
        <p class="header">
          Standard
        </p>
        <div class="numbers">
          <p>$47</p>
          <p>per month</p>
        </div>
      </div>
      <ul class="features fa-ul">
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited users
        </li>
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited projects
        </li>
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited concurrent builds
        </li>
        <li>
          <i class="fa-li fa fa-long-arrow-right"></i>
          600 deployments
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Email support
        </li>
      </ul>
    </div>
    <div class="premium">
      <div class="cost">
        <p class="header">
          Premium
        </p>
        <div class="numbers">
          <p>$197</p>
          <p>per month</p>
        </div>
      </div>
      <ul class="features fa-ul">
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited users
        </li>
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited projects
        </li>
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited concurrent builds
        </li>
        <li>
          <i class="fa-li fa fa-long-arrow-right"></i>
          3000 deployments
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Priority email support
        </li>
      </ul>
    </div>
    <div class="pro">
      <div class="cost">
        <p class="header">
          Pro
        </p>
        <div class="numbers">
          <p>$997</p>
          <p>per month</p>
        </div>
      </div>
      <ul class="features fa-ul">
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited users
        </li>
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited projects
        </li>
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited concurrent builds
        </li>
        <li>
          <i class="fa-li fa fa-long-arrow-right"></i>
          18000 deployments
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Priority email support
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Video call support
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Required two-factor auth<br /><span>Coming soon</span>
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Multi-level user roles<br /><span>Coming soon</span>
        </li>
      </ul>
    </div>
  </div>
  <div class="extra">
    <p>
      There are soft limits on build storage and total build minutes. <a href="mailto:{{ site.email }}">Contact us</a> if you have any questions or have custom requirements.
    </p>
    <p>
      All deployments are listed per month.
    </p>
  </div>
</div>

<div class="faq">
  <h4 id="faq">Frequently Asked Questions</h4>
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
        Can I configure upstream and downstream stages?
      </p>
      <p>
        Currently the "production" stage is the only downstream stage with all other stages promoting directly to it via the <a href="{{ site.console_url }}" target="_blank">Seed Console</a>.
      </p>
    </li>

    <li>
      <p>
        Is it only for Serverless APIs?
      </p>
      <p>
        Your Serverless project does not need to be an API but we are focusing primarily on APIs.
      </p>
    </li>

    <li>
      <p>
        Which environments do you support?
      </p>
      <p>
        We support <a href="https://serverless.com/framework/" target="_blank">Severless Framework</a> Node.js and Python projects on AWS with GitHub as a source repository. Let us know if there are any other environments you’d like us to support.
      </p>
    </li>
  </ul>
  <p>Feel free to contact us if you have any questions using the message button or via <a href="mailto:{{ site.email }}">email</a>.</p>
</div>

<div class="closing">
  <p class="about"><span class="logo">Seed</span> is created by the trusted folks behind <a target="_blank" href="http://serverless-stack.com">Serverless-Stack.com</a>,<br /> the best resource for building serverless apps on AWS.</p>
  <a class="action" href="{{ site.console_url }}{{ site.signup }}">Create a Free Account</a>
  <div class="divider">
    <div>
      <hr />
      <span>&amp;</span>
    </div>
  </div>
  <p class="updates">Stay up to date with product updates from Seed</p>
  <a class="button" href="{{ site.newsletter_signup_form }}" target="_blank">
    Subscribe to our newsletter
  </a>
  <br />
  <a class="button" href="{{ site.twitter }}" target="_blank">
    Follow us on Twitter
  </a>
  <div class="platforms">
    <div>
      <img title="Node.js" width="31" src="assets/node-logo.png" />
      <i title="GitHub" class="fa fa-github" aria-hidden="true"></i>
      <img title="Python" width="31" src="assets/python-logo.png" />
      <p>Supported Platforms</p>
    </div>
    <div>
      <i title="Bitbucket" class="fa fa-bitbucket" aria-hidden="true"></i>
      <i title="GitLab" class="fa fa-gitlab" aria-hidden="true"></i>
      <p>Coming Soon</p>
    </div>
  </div>
</div>
