---
layout: lander
---

<div class="header">
  <h1>Deploy, Manage, and Monitor Serverless Applications on AWS</h1>
  <h3>Seed manages pipelines, configures environments, and monitors deployments for Serverless Framework projects.</h3>
</div>

<div class="action">
  <div class="background">
    <div></div>
    <div></div>
  </div>
  <div class="controls">
    <p>Add your <b>Serverless Framework project</b> to get started or request a <b>personalized demo</b>.</p>
    <div class="buttons">
      <a class="signup" href="{{ site.console_url }}{{ site.signup }}">
        Sign up for free
      </a>
      <a class="demo" href="{{ site.console_url }}{{ site.request_demo }}">
        Request a demo
      </a>
    </div>
  </div>
</div>

<div class="platforms">
  <div>
    <img title="Node.js" width="31" src="assets/node-logo.png" />
    <i title="Bitbucket" class="fa fa-bitbucket" aria-hidden="true"></i>
    <i title="GitHub" class="fa fa-github" aria-hidden="true"></i>
    <i title="GitLab" class="fa fa-gitlab" aria-hidden="true"></i>
    <img title="Python" width="31" src="assets/python-logo.png" />
  </div>
</div>

<div class="features">

  <hr />

  <div class="feature">
    <div class="header">
      <div class="icon">
        <i class="fa fa-code-fork" aria-hidden="true"></i>
      </div>
      <h2>Continuous Integration</h2>
      <p>Seed is a fully-configured code pipeline for Serverless Framework projects on AWS. Here are a few ways Seed can help you with deployments.</p>
    </div>
    <div class="ci-graphic">
      <div class="stage">
        <i class="fa fa-git-square" aria-hidden="true"></i>
        <p>Commit</p>
      </div>
      <div class="angle"></div>
      <div class="stage">
        <i class="fa fa-cogs" aria-hidden="true"></i>
        <p>Build</p>
      </div>
      <div class="angle"></div>
      <div class="stage">
        <i class="fa fa-check-square-o" aria-hidden="true"></i>
        <p>Test</p>
      </div>
      <div class="angle"></div>
      <div class="stage">
        <i class="fa fa-archive" aria-hidden="true"></i>
        <p>Package</p>
      </div>
      <div class="angle"></div>
      <div class="stage">
        <i class="fa fa-rocket" aria-hidden="true"></i>
        <p>Deploy</p>
      </div>
    </div>
    <div class="points">
      <div class="point">
        <h6>Flexible Git workflow</h6>
        <p>Easily create new Serverless stages from git branches. Each developing branch gets its own independent stage.</p>
        <a href="/docs/adding-a-stage.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Immutable artifacts</h6>
        <p>Each successful commit will generate an immutable artifact that will be used to promote to all downstream stages.</p>
        <a href="/docs/promoting-to-production.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Artifact repository <span>Beta</span></h6>
        <p>Each immutable artifact is stored securely in your AWS S3 bucket. Each artifact can be fetched at anytime and used to deploy to any downstream stage.</p>
        <a>
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Environment variables <span>Beta</span></h6>
        <p>All environment variables are securely stored in your AWS SSM (Systems Manager).</p>
        <a href="/docs/configuring-stage-variables.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Sensitive data</h6>
        <p>Sensitive environments are encrypted with your AWS KMS keys, and stored encrypted in your AWS SSM.</p>
        <a href="/docs/storing-secrets.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Build notifications</h6>
        <p>Get notified when a build starts, succeeds, and fails via the channel you prefer, whether it is Slack, email or custom webhook.</p>
        <a href="/docs/adding-build-notifications.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
    </div>
  </div>

  <hr />

  <div class="feature">
    <div class="header">
      <div class="icon">
        <i class="fa fa-refresh" aria-hidden="true"></i>
      </div>
      <h2>Continuous Delivery</h2>
      <p>Create and configure multiple environments for your team. Environments in Seed are based on the stages in Serverless Framework with all the perks.</p>
    </div>
    <div class="pipeline-table">
      <div class="table">
        <div></div>
        <div>Dev</div>
        <div></div>
        <div>QA</div>
        <div>Staging</div>
        <div></div>
        <div>Prod</div>
        <div>Build 1318</div>
        <div class="info">
          <i class="fa fa-check-circle" aria-hidden="true"></i>
          <span>Mar 14, 2018</span>
        </div>
        <div></div>
        <div class="info promote">Promote</div>
        <div class="info promote">Promote</div>
        <div></div>
        <div class="info promote">Promote</div>
        <div>Build 1317</div>
        <div class="info">
          <i class="fa fa-check-circle" aria-hidden="true"></i>
          <span>Mar 13, 2018</span>
        </div>
        <div></div>
        <div class="info">
          <i class="fa fa-check-circle" aria-hidden="true"></i>
          <span>Mar 13, 2018</span>
        </div>
        <div class="info">
          <i class="fa fa-check-circle" aria-hidden="true"></i>
          <span>Mar 13, 2018</span>
        </div>
        <div></div>
        <div class="info">
          <i class="fa fa-check-circle" aria-hidden="true"></i>
          <span>Mar 13, 2018</span>
        </div>
        <div>Build 1316</div>
        <div class="info">
          <i class="fa fa-check-circle" aria-hidden="true"></i>
          <span>Mar 13, 2018</span>
        </div>
        <div></div>
        <div class="info">
          <i class="fa fa-times-circle" aria-hidden="true"></i>
          <span>Mar 13, 2018</span>
        </div>
        <div class="info">
          <i class="fa fa-minus-circle" aria-hidden="true"></i>
          <span class="hide">Mar 13, 2018</span>
        </div>
        <div></div>
        <div class="info">
          <i class="fa fa-minus-circle" aria-hidden="true"></i>
          <span class="hide">Mar 13, 2018</span>
        </div>
        <div></div>
        <div>
          <img width="28" src="assets/aws-logo.png" />
          Dev account
        </div>
        <div></div>
        <div>
          <img width="28" src="assets/aws-logo.png" />
          Pre-prod account
        </div>
        <div></div>
        <div>
          <img width="28" src="assets/aws-logo.png" />
          Prod account
        </div>
      </div>
    </div>
    <div class="points">
      <div class="point">
        <h6>Pipeline visualization</h6>
        <p>One stop visualization of entire pipeline. Always know which build is running in which stage.</p>
        <a>
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Multi-AWS account</h6>
        <p>Turnkey solution for managing stages across multiple AWS accounts. From deploying one stage per account, to multiple stages sharing the same account.</p>
        <a href="/docs/iam-credentials-per-stage.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Trusted build</h6>
        <p>The same immutable artifact used to promote across all downstream environments.</p>
        <a>
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Manual gating</h6>
        <p>Manually review and approve promotions. Rejected builds are prohibited from being promoted.</p>
        <a href="/docs/promoting-to-production.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Rollback any version</h6>
        <p>Any past immutable artifact can be re-deployed at any time. No re-packaging.</p>
        <a href="/docs/rolling-back.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Bring your own CI <span>Beta</span></h6>
        <p>Seamlessly integrate with your existing CI system. Seed CD will listen to new builds in your artifact repository, and automatically trigger the pipeline.</p>
        <a>
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
    </div>
  </div>

  <hr />

  <div class="feature">
    <div class="header">
      <div class="icon">
        <i class="fa fa-sitemap" aria-hidden="true"></i>
      </div>
      <h2>Mono-Repo Workflow</h2>
      <p>Seed supports mono-repo serverless applications with very little configuration. Simply add your repo and specifiy the services within the repo.</p>
    </div>
    <div class="mono-repo-graphic">
      <div class="root folder">
        <span>
          <i class="fa fa-folder-open" aria-hidden="true"></i><span>/</span>
        </span>
        <div class="content">
          <div class="folder">
            <span>
              <i class="fa fa-folder-open" aria-hidden="true"></i><span>apis/</span>
            </span>
            <div class="content">
              <div class="service">
                <img width="24" src="assets/serverless-folder.png" /><span>users/</span>
              </div>
              <div class="service">
                <img width="24" src="assets/serverless-folder.png" /><span>groups/</span>
              </div>
              <div class="service">
                <img width="24" src="assets/serverless-folder.png" /><span>posts/</span>
              </div>
            </div>
          </div>
          <div class="folder">
            <span>
              <i class="fa fa-folder-open" aria-hidden="true"></i><span>jobs/</span>
            </span>
            <div class="content">
              <div class="service">
                <img width="24" src="assets/serverless-folder.png" /><span>etl/</span>
              </div>
              <div class="service">
                <img width="24" src="assets/serverless-folder.png" /><span>resizer/</span>
              </div>
            </div>
          </div>
          <div class="folder">
            <span>
              <i class="fa fa-folder-open" aria-hidden="true"></i><span>alerts/</span>
            </span>
            <div class="content">
              <div class="service">
                <img width="24" src="assets/serverless-folder.png" /><span>db-trigger/</span>
              </div>
              <div class="service">
                <img width="24" src="assets/serverless-folder.png" /><span>notifier/</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="points">
      <div class="point">
        <h6>Service management</h6>
        <p>Seamlessly add all Serverless services by specifying the path. Seed let's you manage all the services as a whole.</p>
        <a href="">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Service dependencies  <span>Beta</span></h6>
        <p>Coordinate the deployment process between multiple services. Ability to define complex deployment structure with parallel and sequential deployments.</p>
        <a href="">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Git workflow</h6>
        <p>Each commit triggers all services to be deployed at the same time.</p>
        <a href="">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Environment</h6>
        <p>Simple environment context inheritance model. Configure and manage environments across all services.</p>
        <a href="">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Pipelines</h6>
        <p>Ability to configure and manage stage environments across all services. Deploy and rollback across all services as a whole.</p>
        <a href="">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Trusted build</h6>
        <p>Artifacts are generated and securely stored for all services on every commit.</p>
        <a href="">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
    </div>
  </div>

  <hr />

  <div class="feature">
    <div class="header">
      <div class="icon">
        <i class="fa fa-tachometer" aria-hidden="true"></i>
      </div>
      <h2>Manage &amp; Monitor</h2>
      <p>Once your deployments are live, Seed can pull up detailed information on the deployed stack. And give you a live look at what is going on.</p>
    </div>
    <div class="metrics-graphic">
      <div class="graph">
        <svg width="100%" height="100%" version="1.1">
          <defs>
            <linearGradient id="colorRed" x1="0" y1="0" x2="0" y2="1">
              <stop offset="5%" stop-color="#BE2F2B" stop-opacity="0.9"></stop>
              <stop offset="95%" stop-color="#BE2F2B" stop-opacity="0.1"></stop>
            </linearGradient>
          </defs>
          <g>
            <g>
              <path stroke="none" fill="url(#colorRed)" fill-opacity="0.6" width="870" height="135" d="M5,95L56.1764705882353,72.5L107.3529411764706,78.125L158.52941176470588,50L209.7058823529412,21.875L260.88235294117646,5L312.05882352941177,33.125L363.2352941176471,21.875L414.4117647058824,61.25L465.5882352941177,72.5L516.7647058823529,55.625L567.9411764705883,38.75L619.1176470588235,33.125L670.2941176470589,21.875L721.4705882352941,38.75L772.6470588235295,44.375L823.8235294117648,61.25L875,72.5L875,140L823.8235294117648,140L772.6470588235295,140L721.4705882352941,140L670.2941176470589,140L619.1176470588235,140L567.9411764705883,140L516.7647058823529,140L465.5882352941177,140L414.4117647058824,140L363.2352941176471,140L312.05882352941177,140L260.88235294117646,140L209.7058823529412,140L158.52941176470588,140L107.3529411764706,140L56.1764705882353,140L5,140Z"></path>
              <path stroke="#BE2F2B" fill="none" fill-opacity="0.6" width="870" height="135" d="M5,95L56.1764705882353,72.5L107.3529411764706,78.125L158.52941176470588,50L209.7058823529412,21.875L260.88235294117646,5L312.05882352941177,33.125L363.2352941176471,21.875L414.4117647058824,61.25L465.5882352941177,72.5L516.7647058823529,55.625L567.9411764705883,38.75L619.1176470588235,33.125L670.2941176470589,21.875L721.4705882352941,38.75L772.6470588235295,44.375L823.8235294117648,61.25L875,72.5"></path>
            </g>
            <g>
              <circle r="4" stroke="white" fill="#BE2F2B" fill-opacity="1" width="870" height="135" cx="146.5" cy="55.625" stroke-width="2"></circle>
            </g>
          </g>
        </svg>
        <div class="tooltip-wrapper">
          <div class="custom-tooltip">
            <p>Requests: 1413</p>
          </div>
        </div>
      </div>
    </div>
    <div class="points">
      <div class="point">
        <h6>Live logs &amp; metrics</h6>
        <p>Seed collects and displays live metrics from CloudWatch for both Lambdas and API Gateway.</p>
        <a href="/docs/viewing-metrics.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>Resource management</h6>
        <p>Have a overview of all Lambda resources deployed in the project.</p>
        <a href="">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
      <div class="point">
        <h6>API management</h6>
        <p>Turnkey solution for manage API domain and access logs across environments.</p>
        <a href="/docs/configuring-custom-domains.html">
          Learn more
          <i class="fa fa-angle-right" aria-hidden="true"></i>
        </a>
      </div>
    </div>
  </div>

</div>

<div class="testimonials">
  <h4 id="testimonials">Used by teams of different sizes around the globe</h4>
  <div class="list">
    <div class="testimonial">
      <div class="context">
        <h6>Small Teams</h6>
        <p>Let your CTO or technical lead focus on product and not on DevOps.</p>
        <hr />
      </div>
      <p>&ldquo;Seed has made deploying and managing our Serverless apps super slick. Prior to Seed, we’d looked at using services like Circle to handle our CI/CD, but so much configuration was needed for them to work well with Serverless. Plus the team at Seed are really helpful and responsive, which is vital when you’re working with new technology.&rdquo;</p>
      <div>
        <p>- <span>Lewis Blackwood</span>, CTO @ <a target="_blank" href="https://personably.co">Personably</a></p>
      </div>
    </div>
    <div class="testimonial">
      <div class="context">
        <h6>Agencies</h6>
        <p>Deliver more value by rolling out projects quickly and efficiently.</p>
        <hr />
      </div>
      <p>&ldquo;At Empirical we strive to provide quality solutions in a very short period of time to every project we take on. With Seed we can speed up the development process for new Serverless projects. We are now rolling out and managing multiple projects, and multiple environments pretty efficiently without having to deal with AWS setup.&rdquo;</p>
      <div>
        <p>- <span>Sebastian Pereyro</span>, Founder @ <a target="_blank" href="https://www.goempirical.com">Empirical</a></p>
      </div>
    </div>
    <div class="testimonial">
      <div class="context">
        <h6>Large Teams</h6>
        <p>Help your developers be more productive and reduce your DevOps cost.</p>
        <hr />
      </div>
      <p>&ldquo;Seed has made it possible for us to use Serverless at Shyft. We don’t need to spend time configuring environments and managing our workflows. It also gives us great control over our deployments and it has reduced our DevOps spend significantly.&rdquo;</p>
      <div>
        <p>- <span>Daniel Chen</span>, CTO @ <a target="_blank" href="https://myshyft.com">Shyft</a></p>
      </div>
    </div>
  </div>
</div>

<div class="pricing">
  <h4 id="pricing">Pricing</h4>
  <div class="table">
    <div class="free">
      <div class="cost">
        <p class="header">
          Free
        </p>
        <div class="numbers">
          <p>$0</p>
          <p>per month</p>
        </div>
      </div>
      <ul class="features fa-ul">
        <li>
          <i class="fa-li fa fa-check"></i>
          Unlimited users
        </li>
        <li>
          <i class="fa-li fa fa-long-arrow-right"></i>
          15 deploys per month
        </li>
      </ul>
    </div>
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
          <i class="fa-li fa fa-long-arrow-right"></i>
          60 deploys per month
        </li>
        <li>
          <i class="fa-li fa fa-circle-thin"></i>
          Add 60 deploys for $7
        </li>
      </ul>
    </div>
    <div class="standard">
      <div class="cost">
        <p class="header">
          Standard
        </p>
        <div class="numbers">
          <p>$97</p>
          <p>per month</p>
        </div>
      </div>
      <ul class="features fa-ul">
        <li>
          <i class="fa-li fa fa-ellipsis-h"></i>
          Everything in Startup
        </li>
        <li>
          <i class="fa-li fa fa-long-arrow-right"></i>
          1200 deploys per month
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Team management
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Standard email support
        </li>
      </ul>
    </div>
    <div class="premium">
      <div class="cost">
        <p class="header">
          Premium
        </p>
        <div class="numbers">
          <p>$397</p>
          <p>per month</p>
        </div>
      </div>
      <ul class="features fa-ul">
        <li>
          <i class="fa-li fa fa-ellipsis-h"></i>
          Everything in Standard
        </li>
        <li>
          <i class="fa-li fa fa-long-arrow-right"></i>
          6000 deploys per month
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          API access
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Two-factor auth
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Role based access control
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          Multiple downstream environments
        </li>
        <li>
          <i class="fa-li fa fa-plus"></i>
          4 business hour email support
        </li>
      </ul>
    </div>
    <div class="enterprise">
      <div class="cost">
        <p class="header">
          Enterprise
        </p>
        <div class="numbers">
          <p>
            <a href="mailto:{{ site.sales_email }}?subject=Enterprise%20plan">
              Contact us
            </a>
          </p>
          <p>for a custom plan</p>
        </div>
      </div>
      <ul class="features fa-ul">
        <li>
          <i class="fa-li fa fa-ellipsis-h"></i>
          Everything in Premium
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          Audit logs
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          Uptime SLAs
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          Phone support
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          Single sign-on
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          On premise hosting
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          Dedicated customer success manager
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          Concierge onboarding
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          GitHub Enterprise support
        </li>
        <li>
          <i class="fa-li fa fa-check-circle"></i>
          Fine tuned role based acess control
        </li>
      </ul>
    </div>
  </div>
  <div class="contact">
    <p>Have an existing setup? Need help transitioning?</p>
    <p>Our engineers can help with that.</p>
    <div class="controls">
      <a class="action" href="{% link concierge-onboarding.md %}">
        Learn about Concierge Onboarding
      </a>
    </div>
  </div>
  <div class="extra">
    <hr />
    <p>
      There are soft limits on build minutes. <a href="{% link concierge-onboarding.md %}">Concierge Onboarding</a> is included free in the Enterprise plan. <a href="mailto:{{ site.email }}">Contact us</a> if you have any questions or have custom requirements.
    </p>
  </div>
</div>

<div class="closing">
  <p class="about"><span class="logo">Seed</span> is <a href="{% link about.md %}">created by the trusted folks</a> behind <a target="_blank" href="http://serverless-stack.com">Serverless-Stack.com</a>,<br /> the best resource for building serverless apps on AWS.</p>
  <div class="controls">
    <a class="signup" href="{{ site.console_url }}{{ site.signup }}">
      Sign up for free
    </a>
    <a class="demo" href="{{ site.console_url }}{{ site.request_demo }}">
      Request a demo
    </a>
  </div>
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
</div>
