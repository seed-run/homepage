---
layout: common-errors
title: Trying to populate non string value into a string for variable
image: /assets/social-cards/common-errors.png
description: "Trying to populate non string value into a string for variable ${opt:stage, self:provider.stage}. Please make sure the value of the property is a string."
---

#### Error Message

> Trying to populate non string value into a string for variable ${opt:stage, self:provider.stage}. Please make sure the value of the property is a string.


#### Problem

Certain values in your `serverless.yml` are expected to take on a string type, but non-string values were assigned.

This usually happens when the value is a reference instead of a string, and the reference resolves to a non-string, ie. usually _undefined_ or an object. 

#### Solution

If you are using a referenced value, ensure that the reference can be resolved to a string.

For example, if you running into the error with the following reference: `${file(./config.yml):tableName.${self:opt.stage}}`. Ensure the `config.yml` file exists, has the `tableName` attribute, and that `tableName` in turn has an attributte with the name of the stage you are trying to deploy to.
