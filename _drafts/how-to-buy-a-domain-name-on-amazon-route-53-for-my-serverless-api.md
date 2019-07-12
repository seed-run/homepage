---
layout: post
title: How to buy a domain name on Amazon Route 53 for my Serverless API?
image: assets/social-cards/custom-domains.png
description: In this post we'll look at how you can purchase your own domain name for your Serverless API using Amazon Route 53.
categories: tips
author: frank
---

When you deploy your Serverless application with API Gateway, AWS auto-generates an URL for you with a default AWS domain. Over the next couple of posts we'll be looking at how to buy and manage custom domains for your Serverless API.

You'll recall that the auto-generated API Gateway endpoints have the following format:

```
https://xxxxxxxxxx.execute-api.REGION.amazonaws.com/STAGE/
```

In this post we'll look at how you can purchase your own domain name hosted on Amazon Route 53. And in the next post we'll look at how to update your Serverless app to use your new custom domain so that your API Gateway endpoints look like this:

```
https://my-serverless-app.com/
```

[Amazon Route 53](https://aws.amazon.com/route53/) is a highly available and scalable cloud Domain Name System (DNS) web service. However, you can use it to buy and manage domains as well.

Let's look at how to do that.

### Purchase a domain using Route 53

You can purchase a domain right from the AWS Console by heading to the Route 53 section in the list of services.

![Select Route 53 in list of AWS services](/assets/blog/how-to-buy-a-domain-name-on-amazon-route-53-for-my-serverless-api/select-route-53-in-list-of-aws-services.png)

Type in your domain in the **Register domain** section and click **Check**.

![Check for domain availability in Route 53](/assets/blog/how-to-buy-a-domain-name-on-amazon-route-53-for-my-serverless-api/check-for-domain-availability-in-route-53.png)

After checking its availability, click **Add to cart**.

![Add new domain to cart in Route 53](/assets/blog/how-to-buy-a-domain-name-on-amazon-route-53-for-my-serverless-api/add-new-domain-to-cart-in-route-53.png)

And hit **Continue** at the bottom of the page.

![Continue add to cart in Route 53](/assets/blog/how-to-buy-a-domain-name-on-amazon-route-53-for-my-serverless-api/continue-add-to-cart-in-route-53.png)

Fill in your contact details and hit **Continue** once again.

![Fill in contact details to purchase Route 53 domain](/assets/blog/how-to-buy-a-domain-name-on-amazon-route-53-for-my-serverless-api/fill-in-contact-details-to-purchase-route-53-domain.png)

Finally, review your details and confirm the purchase by hitting **Complete Purchase**.

![Confirm Route 53 domain purchase](/assets/blog/how-to-buy-a-domain-name-on-amazon-route-53-for-my-serverless-api/confirm-route-53-domain-purchase.png)

And that's it! In the next post, we'll look at how to configure your app to use the new domain.
