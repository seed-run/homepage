---
layout: common-errors
title: Property AttributeDefinitions is inconsistent with the KeySchema of the table and the secondary indexes.
image: /assets/social-cards/common-errors.png
description: Property AttributeDefinitions is inconsistent with the KeySchema of the table and the secondary indexes.
---

#### Error Message

> Property AttributeDefinitions is inconsistent with the KeySchema of the table and the secondary indexes.


#### Problem

This error comes from the DynamoDB table resources in your `serverless.yml`.

In a DynamoDB table definition, the `AttributeDefinitions` should only contain attributes that are used as KeySchema for the table and its indexes.

For example, the following table definition will result in the above error because the `username` attribute is not being used in the table or index's KeySchema.

``` yml
UsersTable:
  Type: AWS::DynamoDB::Table
  Properties:
    TableName: users
    AttributeDefinitions:
      - AttributeName: id
        AttributeType: S
      - AttributeName: username
        AttributeType: S
      - AttributeName: email
        AttributeType: S
    KeySchema:
      - AttributeName: id
        KeyType: HASH
    GlobalSecondaryIndexes:
      -
        IndexName: "email-index"
        KeySchema:
          - AttributeName: email
            KeyType: HASH
        Projection:
          NonKeyAttributes: []
          ProjectionType: "ALL"
```


#### Solution

Remove attributes that are not a part of the KeySchema. You can still store other attributes (such as `name`, `age`, etc.) in this table. But you only need to list out the attributes that DynamoDB needs to know to build the KeySchema.

``` yml
UsersTable:
  Type: AWS::DynamoDB::Table
  Properties:
    TableName: users
    AttributeDefinitions:
      - AttributeName: id
        AttributeType: S
      - AttributeName: email
        AttributeType: S
    KeySchema:
      - AttributeName: id
        KeyType: HASH
    GlobalSecondaryIndexes:
      -
        IndexName: "email-index"
        KeySchema:
          - AttributeName: email
            KeyType: HASH
        Projection:
          NonKeyAttributes: []
          ProjectionType: "ALL"
```
