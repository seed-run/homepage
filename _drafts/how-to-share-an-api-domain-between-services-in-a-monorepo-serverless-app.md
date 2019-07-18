# How to share an API domain between services in a monorepo Serverless app?

As a refresher, a monorepo Serverless app is one where multiple Serverless services are in subdirectories with their own serverless.yml file. Here is a sample repo for the app that we’ll be configuring. The directory structure might look something like this:
```
/
  package.json
  services/
    users-api/
      serverless.yml
    billing-api/
      serverless.yml
    search-api/
      serverless.yml
```

## What we try to achieve is:
- **users-api** service handles api requests with path falling under https://api.domain.com/users/...
- **billing-api** service handles api requests with path falling under https://api.domain.com/billing/...
- **search-api** service handles api requests with path falling under https://api.domain.com/search/...

There are two ways:
1. Each service creates their own API Gateway project and endpoint, and then we map the three endpoints to the **/users**, **/billing**, and **/search** base path respectively.
2. We create a new **root-api** service that creates an API Gateway project and endpoint. And the other services reuses the same API Gateway project.

We will look at each in detail.


## Method 1: Multiple API Gateway Project
- sample repo: https://github.com/seed-run/serverless-example-monorepo-with-multi-apig
- each service looks very similar:
```
service: mono-repo-users-api
  
plugins:
  - serverless-domain-manager

custom:
  customDomain:
    domainName: api.seed-frank-playground.download
    basePath: users

provider:
  name: aws
  runtime: nodejs10.x
  region: us-east-1

functions:
  main:
    handler: handler.main
    events:
      - http:
          path: /
          method: get
          cors: true
```
- follow this article to setup the following - https://seed.run/blog/how-to-set-up-a-custom-domain-name-for-api-gateway-in-your-serverless-app:
  - create a certificate for the domain
  - validate the domain in Route53
  - run `serverless create_domain` in one of the service to configured the custom domain

- after deploying the services, you get 3 endpoints
  - users-api: https://r3f6c4wjl0.execute-api.us-east-1.amazonaws.com/dev/
  - billing-api: https://uufd2irj1e.execute-api.us-east-1.amazonaws.com/dev/
  - search-api: https://poaw3vyekj.execute-api.us-east-1.amazonaws.com/dev/

- each endpoint mapped to the custom domain:
  - users-api: https://api.seed-frank-playground.download/users/
  - billing-api: https://api.seed-frank-playground.download/billing/
  - search-api: https://api.seed-frank-playground.download/search/

- here is what the custom domain setup looks like in API Gateway console

![](https://i.imgur.com/n1cJWRc.png)

- curling both of curls return the same response
```
$ curl https://r3f6c4wjl0.execute-api.us-east-1.amazonaws.com/dev/
Hello users!

$ curl https://api.seed-frank-playground.download/users/
Hello users!
```

## Method 2: Single API Gateway Project
- sample repo: https://github.com/seed-run/serverless-example-monorepo-with-single-apig
- create a **root-api** service that creates an API Gateway endpoint mapped to the custom domain's root path. We also export the API Gateway resource which the other 3 services will use.
```
service: mono-repo-root-api
  
plugins:
  - serverless-domain-manager

custom:
  stage: ${opt:stage, self:provider.stage}
  customDomain:
    domainName: api.seed-frank-playground.download

provider:
  name: aws
  runtime: nodejs10.x
  region: us-east-1

functions:
  main:
    handler: handler.main
    events:
      - http:
          path: /
          method: get
          cors: true
          
resources:
  - Outputs:
      ApiGatewayRestApiId:
        Value:
          Ref: ApiGatewayRestApi
        Export:
          Name: ${self:custom.stage}-ApiGatewayRestApiId
    
      ApiGatewayRestApiRootResourceId:
        Value:
           Fn::GetAtt:
            - ApiGatewayRestApi
            - RootResourceId 
        Export:
          Name: ${self:custom.stage}-ApiGatewayRestApiRootResourceId
```
- each service reference **root-api** service's API Gateway project instead of creating their own project. 
  - Note, we only need to setup custom domain once in the **root-api**, no need to use the **serverless-domain-manager** plugin in these services.
  - Also note the http path for is now '/users' not at the root '/'
```
service: mono-repo-users-api

custom:
  stage: ${opt:stage, self:provider.stage}

provider:
  name: aws
  runtime: nodejs10.x
  region: us-east-1
  apiGateway:
    restApiId:
      'Fn::ImportValue': ${self:custom.stage}-ApiGatewayRestApiId
    restApiRootResourceId:
      'Fn::ImportValue': ${self:custom.stage}-ApiGatewayRestApiRootResourceId

functions:
  main:
    handler: handler.main
    events:
      - http:
          path: /users
          method: get
          cors: true
```
- follow this article to setup the following - https://seed.run/blog/how-to-set-up-a-custom-domain-name-for-api-gateway-in-your-serverless-app:
  - create a certificate for the domain
  - validate the domain in Route53
- go into the **root-api** folder
  - run `serverless create_domain` to configured the custom domain
  - run `serverless deploy`
- run `serverless deploy` to deploy the rest 3 services
- after deploying the services, you will notice only the **root-api** has an endpoint:
  - root-api: https://rpxd6e2wc91.execute-api.us-east-1.amazonaws.com/dev/
  - users-api: https://rpxd6e2wc91.execute-api.us-east-1.amazonaws.com/dev/users/
  - billing-api: https://rpxd6e2wc91.execute-api.us-east-1.amazonaws.com/dev/billing/
  - search-api: https://rpxd6e2wc91.execute-api.us-east-1.amazonaws.com/dev/search/

- **root-api** is also mapped to the custom domain
  - root-api: https://api.seed-frank-playground.download/
  - users-api: https://api.seed-frank-playground.download/users/
  - billing-api: https://api.seed-frank-playground.download/billing/
  - search-api: https://api.seed-frank-playground.download/search/


- curling users- of curls return the same response
```
$ curl https://rpxd6e2wc91.execute-api.us-east-1.amazonaws.com/dev/users/
Hello users!

$ curl https://api.seed-frank-playground.download/users/
Hello users!
```
