---
layout: build-errors
title: The AWS Access Key Id needs a subscription for the service
image: /assets/social-cards/common-errors.png
description: The AWS Access Key Id needs a subscription for the service
---

#### Error Message

> The AWS Access Key Id needs a subscription for the service


#### Problem

This could happen if the registration process for your AWS account was not completed. Or if you have not signed up for the service you are trying to use. For example, some AWS services like Amazon SES (Simple Email Service), require an explicit sign up step even if you have a verified AWS account. 


#### Solution

To start with, ensure that you have completed the account registrations and verification process for creating an AWS account. Make sure you have provided your payment information. You will not be charged as long as the service has a free tier and your usage is within the limit.

If your account is already verified, double check if you are using any AWS services that require an explicit sign up. In the case of Amazon SES, head over to the SES console and follow the instructions to complete the sign up process.
